# Forums

Endpoints related to the forums.


## Category view

**Request**

`ajax.php?action=forum&type=main`


**Response**

```json

```


## Forum view

**Request**

`ajax.php?action=forum&type=viewforum`

`&forumid=` — id of the forum to display (required)

`&page=` — the page to display (default: `1`)


**Response**

```json

```


## Thread view 

**Request**

`ajax.php?action=forum&type=viewthread`

`&threadid=` — id of the thread to display (required)

`&postid=` — response will be the page including the post with this id

`&page=` — page to display (default: `1`)

`&updatelastread=` — set to `1` to not update the last read id (default: `0`)


**Response**

```json

```


## Subscriptions

**Request**

`ajax.php?action=subscriptions`

`&showunread=` — `1` to show only unread, `0` for all subscriptions (default: `1`)


**Response**

```json

```


## Raw BBcode

Fetch a post's unrendered content.


**Request**

`ajax.php?action=raw_bbcode`

`&postid=` — post id to display (required)


**Response**

```json

```
