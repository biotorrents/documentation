# Torrents

Endpoints related to torrents.


## Torrent

**Request**

`ajax.php?action=torrent`

`&id=` — torrent's id (required)

`&hash=` — torrent's hash (must be uppercase)


**Response**

```json

```


## Torrent group

**Request**

`ajax.php?action=torrentgroup`

`&id=` — torrent's group id (required)

`&hash=` — hash of a torrent in the torrent group (must be uppercase)


**Response**

```json

```


## Browse (search)

Note that BioTorrents.de still uses Oppaitime metadata under the hood.
The advanced search options are certain to change in the future.


**Request**

`ajax.php?action=browse`

`&page=` — page to display (default: `1`)

`&searchstr=` — string to search for

`taglist`, `tags_type`, `order_by`, `order_way`, `filter_cat`, `freetorrent`, `vanityhouse`, `scene`, `haslog`, `releasetype`, `media`, `format`, `encoding`, `artistname`, `filelist`, `groupname`, `recordlabel`, `cataloguenumber`, `year`, `remastertitle`, `remasteryear`, `remasterrecordlabel`, `remastercataloguenumber` — as in advanced search


**Response**

```json

```

## Comments 

**Request**

`ajax.php?action=tcomments`

`&id=` — torrent's id (required)


**Response**

```json

```


## Collage

**Request**

`ajax.php?action=collage`

`&id=` — collage's id (required)


**Response**

```json

```


## Artist 

Under construction.
Currently not returning torrents.
Please see the below reponse.


**Request**

`ajax.php?action=artist`

`&id=` — artist's id (required)

`&artistname=` — artist's name

`&artistreleases=` — if set, only include groups where the artist is the main artist


**Response**

```json

```


## Top 10

Fetch the Top 10 torrents, tags, or users.


### Torrents

**Request**

`ajax.php?action=top10`

`&limit=` — one of 10, 100, 250 (default: `10`)

`&type=` — one of: torrents, tags, users (default: `torrents`)


**Response**

```json

```


### Tags

```json

```


### Users

```json

```
