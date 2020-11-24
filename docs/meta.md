# Meta

Endpoints related to BioTorrents.de itself.


## Index

Fetch basic site info from the homepage,
e.g., if there's a new announcement.


**Request**

`ajax.php?action=index`


**Response**

```json

```


## Stats

Fetch the homepage sidebar info.


**Request**

`ajax.php?action=stats`


**Response**

```json

```


## Announcements 

**Request**

`ajax.php?action=announcements`


**Response**

```json

```


## Load average 

**Request**

`ajax.php?action=loadavg`


**Response**

```json

```


## Wiki

Note that either `id` or `name` is required.

**Request**

`ajax.php?action=wiki`

`&id=` — page id to display (required)

`&name=` — page alias to display


**Response**

```json

```
