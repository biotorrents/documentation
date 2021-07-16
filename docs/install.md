# Install

Thanks for your interest in BioTorrents.de's development!
Gazelle is notoriously difficult to install.
[original announcement protocol](https://github.com/biotorrents/announcement),
is an attempt at an evergreen install guide.

# Debian system profile

```shell
$ uname -a
Linux ohm 5.10.0-6-amd64 #1 SMP Debian 5.10.28-1 (2021-04-09) x86_64 GNU/Linux

$ nginx -v
nginx version: nginx/1.18.0

$ mysql -V
mysql  Ver 15.1 Distrib 10.5.10-MariaDB, for debian-linux-gnu (x86_64) using  EditLine wrapper

$ php -v
PHP 7.4.21 (cli) (built: Jul  2 2021 03:59:48) ( NTS )

$ memcached -h
memcached 1.6.9

$ indexer
Sphinx 2.2.11-id64-release (95ae9a6)
```

# Server setup

This section is done as root.
If you're in a user shell, preface commands with `sudo`.

## Upgrading to Debian Sid

Install the most recent
[Debian netinst image](https://www.debian.org/CD/netinst/)
and modify `/etc/apt/sources.list`:

```
deb http://deb.debian.org/debian unstable main contrib non-free
deb-src http://deb.debian.org/debian unstable main contrib non-free
```

Optionally, create `/etc/apt/apt.conf` with this content:

```
APT::Install-Recommends "1";
APT::Install-Suggests "0";
```

Then upgrade the system:

```shell
# apt update
# apt dist-upgrade
# reboot
```

Further server setup, including DNS, email, etc., are beyond this guide's scope.
For more info about SSH, Unbound, NSD, OpenSMTPd, Dovecot, Unix users, etc.,
[please see the original launch announcement](https://github.com/biotorrents/announcement).

## Nginx and Certbot

Install Nginx and Certbot with `apt install nginx certbot python3-certbot-nginx`.

The basic Gazelle Nginx config should look similar to this.
You'll likely have to change the file paths based on your setup.
Also, PHP-FPM may need larger buffers to serve without 502 errors:

```nginx
server {
        listen 443 ssl http2;
        root /var/www/html/dev.biotorrents.de;

        client_max_body_size 4M;
        server_name dev.biotorrents.de;

        add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload";

        ssl_certificate /etc/letsencrypt/live/biotorrents.de-0001/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/biotorrents.de-0001/privkey.pem; # managed by Certbot

        access_log off;
        error_log  /var/log/nginx/dev.biotorrents.de-error.log;

        location / {
                index index.php;
        }

        # https://www.nginx.com/resources/wiki/start/topics/examples/phpfcgi/
        location ~ [^/]\.php(/|$) {
                fastcgi_split_path_info ^(.+?\.php)(/.*)$;
                if (!-f $document_root$fastcgi_script_name) {
                        return 404;
                }

                # Mitigate https://httpoxy.org/ vulnerabilities
                fastcgi_param HTTP_PROXY "";

                fastcgi_pass  unix:/var/run/php/php7.4-fpm.sock;
                fastcgi_index index.php;

                # include the fastcgi_param setting
                include /etc/nginx/params/fastcgi_params;

                # https://stackoverflow.com/a/23845727
                fastcgi_buffers 16 16k;
                fastcgi_buffer_size 32k;
        }

        # https://nginx.org/en/docs/http/ngx_http_access_module.html
        location ^~ /.git/ {
                deny all;
        }

        location ^~ /classes/config.php {
                deny all;
        }
}
```

The Nginx config for the Ocelot tracker should look like this.
Nginx acts as a TLS reverse proxy so Ocelot isn't directly exposed.
Note the `Host` header (so tracker connections don't show up as localhost):

```nginx
server {
        listen 443 ssl http2;
        server_name tr0.biotorrents.de track.biotorrents.de;

        add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload";

        ssl_certificate /etc/letsencrypt/live/biotorrents.de-0001/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/biotorrents.de-0001/privkey.pem; # managed by Certbot

        access_log off;
        error_log  /var/log/nginx/tr0.biotorrents.de-error.log;

        # https://nginx.org/en/docs/http/ngx_http_proxy_module.html
        location / {
                proxy_pass http://127.0.0.1:34000;
                proxy_set_header Host $remote_addr:$proxy_port;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Real-IP $remote_addr;
        }
}
```

Finally, set up TLS certificates with `certbot --nginx`.
Add this entry to the root crontab to renew the certs daily:

```
20 1 * * * certbot renew >/dev/null 2>&1 && systemctl restart nginx >/dev/null 2>&1
```

Please see the
[Certbot docs](https://certbot.eff.org/docs/using.html)
and
[OWASP Secure Headers Project](https://owasp.org/www-project-secure-headers/)
for more info.

## MariaDB

Install MariaDB with `apt install mariadb-server`
and initialize it with `mysql_secure_installation`.

BioTorrents.de uses TLS connections to a dedicated database server.
Unix sockets are preferred for the database running on localhost.
The config should look similar to this, paying attention to `sql-mode`:

```
[client-server]
# Port or socket location where to connect
port = 3306
#socket = /var/run/mysqld/mysqld.sock

# Import all .cnf files from configuration directory
#!includedir /etc/mysql/conf.d/
#!includedir /etc/mysql/mariadb.conf.d/

[mariadb]
# https://mariadb.com/kb/en/secure-connections-overview/
tls-version = TLSv1.3
#require-secure-transport = on

# https://mariadb.com/kb/en/securing-connections-for-client-and-server/
ssl-cert=/etc/mysql/ssl/server-cert.pem
ssl-key=/etc/mysql/ssl/server-key.pem
ssl-ca=/etc/mysql/ssl/ca.pem

# https://mariadb.com/kb/en/configuring-mariadb-for-remote-client-access/
skip-networking = 0
bind-address = 10.0.0.3

# https://johnemb.blogspot.com/2014/09/adding-or-removing-individual-sql-modes.html
sql-mode = "STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
```

If you'd like to use TLS crypto in your database connections,
[please see the MariaDB docs](https://mariadb.com/kb/en/securing-connections-for-client-and-server/).
They contain the necessary info to generate self-signed certs.

Finally, load the Gazelle database schema in an SQL shell.
I generate secure passphrases with `pwgen -s | encrypt`:

```mysql
CREATE DATABASE gazelle_development;
USE gazelle_development;
SOURCE /var/www/html/dev.biotorrents.de/gazelle.sql;
CREATE USER 'gazelle_development'@'localhost' IDENTIFIED BY '';
GRANT ALL PRIVILEGES ON `gazelle_development`.* TO 'gazelle_development'@'localhost';
```

## PHP

Install PHP and the necessary extensions.
The basic PHP package:
`apt install php php-dev php-fpm`.

The PHP extensions.
There are two PHP memcached extensions.
The correct one is just `php-memcache` without the "d."
Your distro may require other extensions:
`php-apcu php-mbstring php-memcache php-mysql`.

BioTorrents.de also supports the
[Seqhash algorithm](https://blog.libredna.org/post/seqhash/)
and requires Blake3 for this feature.
Optionally, please install
[php-blake3](https://github.com/cypherbits/php-blake3).

Gazelle isn't picky about its PHP config needs,
except that `short_open_tag = On` is still required.
I strongly recommend crafting a
[secure PHP config](https://cheatsheetseries.owasp.org/cheatsheets/PHP_Configuration_Cheat_Sheet.html).

## memcached

Install memcached with `apt install memcached`.

BioTorrents.de supports separate production and development instances.
If you with to run two instances, it's necessary to run memcached twice.
Otherwise the sites will experience significant cross-contamination.
The `/etc/memcached.conf` content:

```
-d
-m 5120
-s /var/run/memcached/memcached.sock
-a 0777
-t16
-C
-u memcache
```

A helper script to quickly bring up a second memcached as root:

```shell
#!/bin/sh
memcached -d -m 5120 -s /var/run/memcached/memcached-dev.sock -a 0777 -t16 -C -u memcache
```

## Sphinx

Install Sphinx with `apt install sphinxsearch`.

The `/etc/sphinxsearch/sphinx.conf` content is too large to reasonably inline.
Please find a copy at
[biotorrents/documentation](https://github.com/biotorrents/documentation/blob/master/docs/dl/sphinx.conf).
The only other Sphinx-related configs are root crontab entries:

```crontab
@reboot /usr/bin/searchd`.
* * * * * indexer -c /etc/sphinxsearch/sphinx.conf --rotate delta requests_delta >/dev/null 2>&1
7 * * * * indexer -c /etc/sphinxsearch/sphinx.conf --rotate torrents >/dev/null 2>&1
7 0,12 * * * indexer -c /etc/sphinxsearch/sphinx.conf --rotate --all >/dev/null 2>&1
```

## Email

Email setup is beyond this guide's scope.
Please see
[Gilles's OpenSMTPd and Dovecot guide](https://poolp.org/posts/2019-09-14/setting-up-a-mail-server-with-opensmtpd-dovecot-and-rspamd/).

# Application setup

This section should use a separate Unix user for each component.
Gazelle, Ocelot, IRC, and sitebot should each have their own home folder and shell.
Otherwise the applications would be an insecure jumble and hard to maintain.

## Gazelle

Please use the
[biotorrents/gazelle development branch](https://github.com/biotorrents/gazelle/tree/development)
to grab the current working copy:

```shell
git clone --branch development https://github.com/biotorrents/gazelle.git
git push origin development
```

First create the necessary files and folders.
Note that locations are arbitrary and may be one of:
home folder, subfolder of `/var/www`, etc.

```shell
# nginx(8) log location
mkdir -m 700 -p /var/www/log/{production,development}
touch /var/www/log/{production,development/{peerupdate.log,schedule.log}
chown -R biotorrents:biotorrents /var/www/log

# files outside the web root
mkdir -m 700 -p /var/www/pictures /var/www/torrents /var/www/torrents-dev
chown -R www-data:www-data /var/www/pictures /var/www/torrents /var/www/torrents-dev
```

The Gazelle app user also needs this crontab.
Expect to have backups in place by this stage,
and note that server backups are beyond this guide's scope:

```crontab
0,15,30,45 * * * * curl -s "https://dev.biotorrents.de/schedule.php?key=00000000000000000000000000000000" >> /var/www/log/development/schedule.log 2>&1
2-59/5 * * * * php /var/www/html/dev.biotorrents.de/peerupdate.php "00000000000000000000000000000000" >> /var/www/log/development/peerupdate.log
```

A useful script for resetting file permissions:

```shell
#!/bin/sh
find . -type f -print0 | xargs -0 chmod 0644
find . -type d -print0 | xargs -0 chmod 0755
```

### Application config

[`classes/config.php`](https://github.com/biotorrents/gazelle/blob/development/classes/config.template.php)
warrants its own section.
When setting up Gazelle for the first time, set these options:

- `'DEBUG_MODE' = false`
- `'OPEN_REGISTRATION' = true`
- `'FEATURE_SET_ENC_KEY_PUBLIC' = true`

Note the separate production and development values and the possibility of duplicate definitions.
BioTorrents.de uses a singleton class with extended recursive ArrayObject support invoked by
[`$ENV = ENV::go()`](https://github.com/biotorrents/gazelle/blob/development/classes/env.class.php).

There are some other values to set up.
Please pay attention to these values for proper functionality:

- `SITE_DOMAIN` and `IMAGE_DOMAIN`
- `WEB_ROOT` and `SERVER_ROOT`
- `TORRENT_STORE` and `STATIC_SERVER`
- The "App keys" and "Database" sections
- The "Tracker" and "Tracker URLs" sections
- `MEMCACHED_SERVERS`

### Composer

Assuming that `php.ini` is correctly set up,
you may need these modified setup instructions from the
[official Composer docs](https://getcomposer.org/download/):

```shell
mkdir -p /var/www/bin
php -d allow_url_fopen=1 -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
# Hash checking, running the install script, and unlinking
# See the official Composer docs for details
mv composer.phar /var/www/bin/composer
```

Then add `/var/www/bin` to the Gazelle user's `$PATH` and run:
`composer update`.

### SCSS and fonts

Install SassC with `apt install sassc`.

[Download the font pack](https://docs.biotorrents.de/dl/fonts.tgz)
and extract it with:
`tar zxvf fonts.tgz -C /var/www/html/dev.biotorrents.de/static/styles/assets/fonts`.

Then install SassC with `apt install sassc`.
This should be a for loop, to compile the CSS:

```shell
#!/bin/sh
styles="/var/www/html/dev.biotorrents.de/static/styles"
sassc "$styles/beluga/beluga.scss" > "$styles/beluga.css"
sassc "$styles/bookish/bookish.scss" > "$styles/bookish.css"
sassc "$styles/development/development.scss" > "$styles/development.css"
sassc "$styles/genaviv/genaviv.scss" > "$styles/genaviv.css"
sassc "$styles/global/global.scss" > "$styles/global.css"
sassc "$styles/matcha/matcha.scss" > "$styles/matcha.css"
sassc "$styles/oppai/oppai.scss" > "$styles/oppai.css"
sassc "$styles/postmod/postmod.scss" > "$styles/postmod.css"
sassc "$styles/public/public.scss" > "$styles/public.css"
```

## Ocelot

BioTorrents.de uses What.CD's Ocelot with the
[10th anniversary mixtape patches](https://twitter.com/whatcd/status/923942203080273921)
and developing TLS support.
The patched version is available at
[biotorrents/ocelot](/biotorrents/ocelot).

First installed the dependencies like below.
The specific dependencies may differ on your system.

```shell
apt install \
	automake \
	g++ \
	gcc \
	libboost-dev \
	libboost-iostreams-dev \
	libboost-system-dev \
	libev-dev \
	libmysql++-dev \
	libtcmalloc-minimal4 \
	make
```

The compilation ritual is likewise fraught with pitfalls.
I found `autoreconf` with manual library locations to work best:

```shell
autoreconf
./configure \
	--with-boost-libdir=/usr/lib/x86_64-linux-gnu \
	--with-ev-lib=/usr/lib/x86_64-linux-gnu \
	--with-mysql-lib=/usr/lib/x86_64-linux-gnu \
	--with-mysqlpp-lib=/usr/lib/x86_64-linux-gnu
make
make install
```

Copy and edit `ocelot/ocelot.conf.dist` to the Ocelot user's home folder.
The daemon runs on `localhost:34000` and Nginx TLS reverse proxies it to `localhost:443`.
The Ocelot daemon runs in a tmux window under as a user process.

## IRC and kana (sitebot)

Docs pending the completion of sitebot API integration.

## Inside the Gazelle Toolbox

At this point it should be possible to register for the site.
The first account is the sysop so please act quickly here.
Disable `DEBUG_MODE` and `FEATURE_SET_ENC_KEY_PUBLIC` as soon as you register!
Then do `apt install qrencode` for 2FA support and enable it with a GPG key on the sysop account.

Configure a client whitelist on the Toolbox page by the
[BitTorrent spec's peer ID list](https://wiki.theory.org/index.php/BitTorrentSpecification#peer_id).
Please find a list of quality client peer IDs below.
LibTorrent 0.1x.y also covers rTorrent/ruTorrent and other clients that use
[rakshasa's library](https://github.com/rakshasa/libtorrent):

| Client Name       | Peer ID |
| :---------------- | :-----: |
| Deluge 1.x.y      | `-DE1`  |
| Deluge 2.x.y      | `-DE2`  |
| KTorrent 3.x.y    | `-KT3`  |
| KTorrent 4.x.y    | `-KT4`  |
| KTorrent 5.x.y    | `-KT5`  |
| LibTorrent 0.x.y  | `-lt0`  |
| qBittorrent 2.x.y | `-qB2`  |
| qBittorrent 3.x.y | `-qB3`  |
| qBittorrent 4.x.y | `-qB4`  |
| Transmission 2.xy | `-TR2`  |
| Transmission 3.xy | `-TR3`  |

For more BitTorrent info see
[Calomel's rTorrent hacking guide](https://calomel.org/rtorrent_mods.html).

## Building these docs

[biotorrents/documentation](https://github.com/biotorrents/documentation)
has the Mkdocs source code.
Install MkDocs with `apt install mkdocs`.
Then do `mkdocs build`.
