# Requests

Endpoints related to torrent requests.


## Request

**Request**

`ajax.php?action=request`

`&id=` — request id (required)

`&page=` — page of the comments to display (default: last page)


**Response**

```json

```


## Search

If no arguments are specified then the most recent requests are shown.


**Request**

`ajax.php?action=requests`

`&page=` — page to display (default: `1`)

`&search=` — search term

`&show_filled=` — include filled requests in results `true` or `false` (default: `false`)

`&tag=` — tags to search by (comma separated)

`&tags_type=` — `0` for any, `1` for match all

`filter_cat[]`, `releases[]`, `bitrates[]`, `formats[]`, `media[]` — as used on requests.php


**Response**

```json

```
