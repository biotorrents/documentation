# Meta

Endpoints related to BioTorrents.de itself.


## Index

Fetch basic site info from the homepage,
e.g., your ratio and any unread notices.


**Request**

`ajax.php?action=index`


**Response**

```json
{
    "status": "success",
    "response": {
        "username": "me",
        "id": 2,
        "authkey": "00000000000000000000000000000000",
        "passkey": "00000000000000000000000000000000",
        "notifications": {
            "messages": 0,
            "notifications": 0,
            "newAnnouncement": false,
            "newBlog": false,
            "newSubscriptions": false
        },
        "userstats": {
            "uploaded": 15918336971,
            "downloaded": 2341094384,
            "ratio": 6.79,
            "requiredratio": 0,
            "class": "Member"
        }
    }
}
```


## Stats

Fetch the homepage sidebar info.


**Request**

`ajax.php?action=stats`


**Response**

```json
{
    "status": "success",
    "response": {
        "maxUsers": 0,
        "enabledUsers": 82,
        "usersActiveThisDay": 5,
        "usersActiveThisWeek": 10,
        "usersActiveThisMonth": 19,
        "torrentCount": 60,
        "groupCount": 12,
        "artistCount": 151,
        "requestCount": 3,
        "filledRequestCount": 0,
        "seederCount": 225,
        "leecherCount": 0
    }
}
```


## Load average

Requires moderator permissions to access without error.

**Request**

`ajax.php?action=loadavg`


**Response**

```json
{
    "status": "success",
    "response": {
        "loadAverage": [
            0.11,
            0.06,
            0.02
        ]
    }
}
```


**Error**

`Invalid authorization key. Go back, refresh, and try again.`


## Announcements 

Fetch the recent news and blogs.


**Request**

`ajax.php?action=announcements`


**Response**

```json
{
    "status": "success",
    "response": {
        "announcements": [
            {
                "newsId": 16,
                "title": "A quick update",
                "bbBody": "BBcode",
                "body": "HTML",
                "newsTime": "2020-11-12 06:43:38"
            },
            {
                "newsId": 14,
                "title": "Summer solstice sitewide freeleech",
                # etc.
            },
            # etc.
        ],
        "blogPosts": [
            {
                "blogId": 3,
                "author": "ohm",
                "title": "The first hundred gigabytes",
                "bbBody": "BBcode",
                "body": "HTML",
                "blogTime": "2020-11-16 16:28:20",
                "threadId": 36
            },
            {
                "blogId": 2,
                "author": "ohm",
                "title": "New category organization and the rationale",
                # etc.
            },
            # etc.
        ]
    }
}
```


## Wiki

Note that either `id` or `name` is required.

**Request**

`ajax.php?action=wiki`

`&id=` — page id to display (required)

`&name=` — page alias to display


**Response**

```json
{
    "status": "success",
    "response": {
        "title": "User Classes",
        "bbBody": "BBcode",
        "body": "HTML",
        "aliases": "userclasses",
        "authorID": 1,
        "authorName": "ohm",
        "date": "2020-11-13 18:46:06",
        "revision": 10
    }
}
```
