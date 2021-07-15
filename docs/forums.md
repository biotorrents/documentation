# Forums

Endpoints related to the forums.

## Category view

**Request**

`ajax.php?action=forum`

**Response**

```json
{
    "status": "success",
    "response": {
        "categories": [
            {
                "categoryID": 5,
                "categoryName": "Community",
                "forums": [
                    {
                        "forumId": 4,
                        "forumName": "General",
                        "forumDescription": "",
                        "numTopics": 5,
                        "numPosts": 9,
                        "lastPostId": 39,
                        "lastAuthorId": 2,
                        "lastPostAuthorName": "me",
                        "lastTopicId": 30,
                        "lastTime": "2020-05-27 17:53:57",
                        "specificRules": [],
                        "lastTopic": "Unplugging: Tune in, turn on, drop out",
                        "read": false,
                        "locked": false,
                        "sticky": false
                    },
                    {
                        "forumId": 13,
                        "forumName": "Book Club",
                        # etc.
                    },
                    # etc.
                ]
            },
            {
                "categoryID": 10,
                "categoryName": "Help",
                "forums": [
                    {
                        "forumId": 9,
                        "forumName": "BitTorrent",
                        # etc.
                    },
                    # etc.
                ]
            },
            # etc.
        ]
    }
}
```

## Forum view

**Request**

`ajax.php?action=forum&type=viewforum`

`&forumid=` — id of the forum to display (required)

`&page=` — the page to display (default: `1`)

**Response**

```json
{
    "status": "success",
    "response": {
        "forumName": "Bioinformatics",
        "specificRules": [],
        "currentPage": 1,
        "pages": 1,
        "threads": [
            {
                "topicId": 27,
                "title": "Tidy Data: Developing in-house quality standards for original datasets",
                "authorId": 2,
                "authorName": "me",
                "locked": false,
                "sticky": false,
                "postCount": 1,
                "lastID": 36,
                "lastTime": "2020-05-08 17:57:40",
                "lastAuthorId": 2,
                "lastAuthorName": "me",
                "lastReadPage": 1,
                "lastReadPostId": 36,
                "read": true
            },
            {
                "topicId": 26,
                "title": "Microscopy image processing tools",
                # etc.
            },
            # etc.
        ]
    }
}
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
{
    "status": "success",
    "response": {
        "forumId": 10,
        "forumName": "Website",
        "threadId": 2,
        "threadTitle": "Report broken site features",
        "subscribed": false,
        "locked": false,
        "sticky": false,
        "currentPage": 1,
        "pages": 1,
        "poll": null,
        "posts": [
            {
                "postId": 2,
                "addedTime": "2019-12-10 06:47:19",
                "bbBody": "BBcode",
                "body": "HTML",
                "editedUserId": 1,
                "editedTime": "2020-01-18 05:24:59",
                "editedUsername": "ohm",
                "author": {
                    "authorId": 1,
                    "authorName": "ohm",
                    "paranoia": [
                        "downloaded",
                        "uploaded",
                        "ratio",
                        "lastseen",
                        "requiredratio",
                        "invitedcount",
                        "artistsadded",
                        "notifications",
                        "torrentcomments+",
                        "collages+",
                        "collagecontribs+",
                        "uploads+",
                        "uniquegroups+",
                        "perfectflacs+",
                        "seeding+",
                        "leeching+",
                        "snatched+",
                        "requestsfilled_list",
                        "requestsfilled_count",
                        "requestsfilled_bounty",
                        "requestsvoted_list",
                        "requestsvoted_count",
                        "requestsvoted_bounty",
                        "hide_donor_heart"
                    ],
                    "artist": false,
                    "donor": true,
                    "warned": false,
                    "avatar": "",
                    "enabled": true,
                    "userTitle": null
                }
            },
            {
                "postId": 5,
                "addedTime": "2019-12-10 21:59:18",
                # etc.
            },
            # etc.
        ]
    }
}
```

## Subscriptions

**Request**

`ajax.php?action=subscriptions`

`&showunread=` — `1` to show only unread, `0` for all subscriptions (default: `1`)

**Response**

```json
{
    "status": "success",
    "response": {
        "threads": [
            {
                "forumId": 1,
                "forumName": "Announcements",
                "threadId": 36,
                "threadTitle": "The first hundred gigabytes",
                "postId": 51,
                "lastPostId": 51,
                "locked": false,
                "new": false
            },
            {
                "forumId": 5,
                "forumName": "Bioinformatics",
                "threadId": 27,
                "threadTitle": "Tidy Data: Developing in-house quality standards for original datasets",
                # etc.
            },
            # etc.
        ]
    }
}
```

## Raw BBcode

Fetch a post's unrendered content.

**Request**

`ajax.php?action=raw_bbcode`

`&postid=` — post id to display (required)

**Response**

```json
{
  "status": "success",
  "response": {
    "body": "[img]https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1348970636l/12420783.jpg[/img]<br />\r\n<br />\r\nThe human species&#39; enjoyment of food is universal, though different cultures prefer wildly different flavors. Shepherd establishes a new companion field to molecular gastronomy called neurogastronomy. His book explains how the brain constructs and interprets multidimensional flavor profiles as the volatile compounds of food pass through the sense of retronasal smell. The science is accessible and still does justice to the complexity of the olfactory&ndash;neurological interactions described. This book will change the way you eat.<br />\r\n<br />\r\n[url=https://libgen.is/book/index.php?md5=6E9CE452E815418B1F134D5718751000]Library Genesis[/url] / [url=https://www.worldcat.org/title/neurogastronomy-how-the-brain-creates-flavor-and-why-it-matters/oclc/967255519&amp;referer=brief_results]WorldCat[/url]"
  }
}
```
