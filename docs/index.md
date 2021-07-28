The JSON API provides an easily parseable interface to [BioTorrents.de](https://biotorrents.de).
Please use the navigation menu to find lists of endpoints, their arguments, and example responses.

# Introduction

All request URLs are in the form

`api.php?action=<action>`

All the JSON returned is in the form

```json
{
  "status": "success",
  "response": {
    # data
  },
  "info": {
    "source": "BioTorrents.de",
    "version": 1
  }
}
```

If the request is invalid, or a problem occurs, the `status` will be `failure`.
In this case the value of `response` is `undefined`.

## Bearer token auth

First, generate a token in your profile security settings and keep it safe.
It's functionally a password, and like a password, it can't be recovered later.
Then POST an RFC 6750–compliant bearer token along with each GET request:

```sh
curl biotorrents.de/api.php?action=index \
  -H "Accept: application/json" \
  -H "Authorization: Bearer {token}"
```

## Cookie auth

Please send a POST request to `https://biotorrents.de/login.php` with `username` and `password`,
or acquire a cookie from a browser session using the developer tools.
Then store the cookie and use it to access the rest of the API.

# Libraries

These are the current public projects listed on the
[What.CD Gazelle wiki](https://github.com/WhatCD/Gazelle/wiki/JSON-API-Documentation).
Questions about the API can be answered in `#development` on
[Slack](https://join.slack.com/t/biotorrents/shared_invite/enQtODY2Mzg5NzI2OTk5LWQ0NmRlYzZmYTYwMzc3MjJlMzc4ZGJkNzQ1OWE4NDAxYTc3ZTdjY2NkOGRjNDA5MDAxZTA1Y2Y3M2MzMzIwZGY).

Please get it touch if you'd like me to list your project below.

| Language   | GitHub                                                                      |
| :--------- | :-------------------------------------------------------------------------- |
| C#         | [frankston/WhatAPI](https://github.com/frankston/WhatAPI)                   |
| Go         | [kdvh/whatapi](https://github.com/kdvh/whatapi)                             |
| JavaScript | [deoxxa/whatcd](https://github.com/deoxxa/whatcd)                           |
| Java       | [Gwindow/WhatAPI](https://github.com/Gwindow/WhatAPI)                       |
| PHP        | [Jleagle/gazelle-api-client](https://github.com/Jleagle/gazelle-api-client) |
| Python     | [isaaczafuta/whatapi](https://github.com/isaaczafuta/whatapi)               |
| Ruby       | [chasemgray/RubyGazelle](https://github.com/chasemgray/RubyGazelle)         |

# Caveats

**Abusing or using this API for malicious purposes is a bannable offense and will not be taken lightly.**

## Rate limit

The API is rate-limited to one request every 6 seconds.
This limit doesn't apply to users in the Donor class.
[Please consider donating](https://www.patreon.com/biotorrents)
to support this scientific resource's development.

## Under construction

Some endpoints aren't working correctly right now:

- `artist`
- `preview`

[Oppaitime Gazelle](https://git.oppaiti.me/Oppaitime/Gazelle)
also contains other undocumented endpoints:

- `get_friends`
- `news_ajax`
- `send_recommendation`

# Not implemented

## Similar artists

**Request**

`api.php?action=similar_artists`

`&id=` — id of artist (required)

`&limit=` — maximum number of results to return (fewer might be returned)

**Response**

```json

```

## Better

Fetch better.php (suggested torrent improvements).

**Request**

`api.php?action=better`

**Response**

```json

```

## Torrent info

**Request**

`api.php?action=torrent_info`

**Response**

```json

```

## Check private

**Request**

`api.php?action=checkprivate`

**Response**

```json

```

## Vote favorite

**Request**

`api.php?action=votefavorite`

**Response**

```json

```
