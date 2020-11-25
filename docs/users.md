# Users

Endpoints related to user accounts.


## User

If you're viewing your own account, `personal->passkey` will be shown.


**Request**

`ajax.php?action=user`

`&id=` — id of the user to display (required)


**Response**

```json
{
    "status": "success",
    "response": {
        "username": "eva",
        "avatar": "https://ptpimg.me/1x1h48.png",
        "isFriend": false,
        "profileText": "",
        "stats": {
            "joinedDate": "2020-03-08 14:27:59",
            "lastAccess": "2020-11-24 15:25:17",
            "uploaded": 2192870833,
            "downloaded": 1244283888,
            "ratio": 1.76235,
            "requiredRatio": 0
        },
        "ranks": {
            "uploaded": 0,
            "downloaded": 2,
            "uploads": 0,
            "requests": 0,
            "bounty": 0,
            "posts": 2,
            "artists": 0,
            "overall": 0
        },
        "personal": {
            "class": "Donor",
            "paranoia": 0,
            "paranoiaText": "Off",
            "donor": false,
            "warned": false,
            "enabled": true,
            "passkey": ""
        },
        "community": {
            "posts": 4,
            "torrentComments": 0,
            "artistComments": 0,
            "collageComments": 0,
            "requestComments": 0,
            "collagesStarted": 1,
            "collagesContrib": 1,
            "requestsFilled": 0,
            "bountyEarned": 0,
            "requestsVoted": 0,
            "bountySpent": 0,
            "uploaded": 0,
            "groups": 0,
            "seeding": 0,
            "leeching": 0,
            "snatched": 7,
            "invited": 0,
            "artistsAdded": 0
        }
    }
}
```


## User search 

**Request**

`ajax.php?action=usersearch`

`&search=` — the search term (required)

`&page=` — page to display (default: `1`)


**Response**

```json
{
    "status": "success",
    "response": {
        "currentPage": 1,
        "pages": 1,
        "results": [
            {
                "userId": 42,
                "username": "hedomedo",
                "donor": false,
                "warned": false,
                "enabled": true,
                "class": "User",
                "avatar": ""
            },
            {
                "userId": 2,
                "username": "me",
                # etc.
            },
            {
                "userId": 16,
                "username": "Medicus",
                # etc.
            },
            # etc.
        ]
    }
}
```


## Community stats 

**Request**

`ajax.php?action=community_stats`

`&userid=` — id of the user to display (required)


**Response**

```json
{
    "status": "success",
    "response": {
        "leeching": 0,
        "seeding": "60",
        "snatched": "3",
        "usnatched": false,
        "downloaded": false,
        "udownloaded": false,
        "seedingperc": 100
    }
}
```


## Recents (torrents)

This endpoint circumvents the "upload anonymously" feature.
Various features of the response will likely change in the future.


**Request**

`ajax.php?action=user_recents`

`&userid=` — id of user (required)

`&limit=` — how many recent torrents to fetch


**Response**

```json
{
    "status": "success",
    "response": {
        "snatches": [
            {
                "ID": 41,
                "Name": "Enzymatic synthesis of psilocybin",
                "WikiImage": "https://mycocosm.jgi.doe.gov/public/Psiser1/P+serbica+2.png",
                "artists": [
                    [
                        {
                            "id": 58,
                            "name": "Dirk Hoffmeister"
                        },
                        {
                            "id": 57,
                            "name": "Felix Blei"
                        },
                        {
                            "id": 56,
                            "name": "Janis Fricke"
                        }
                    ]
                ]
            },
            {
                "ID": 23,
                "Name": "uBiome kombucha data",
                "WikiImage": "https://kombucha-genomics.github.io/photos/pexels-photo-130947.jpeg",
                # etc.
            },
            # etc.
        ],
        "uploads": [
            {
                "ID": 40,
                "Name": "COVID-19 Genomics UK Consortium: 2020-04-24",
                "WikiImage": "https://www.cogconsortium.uk/wp-content/uploads/2020/04/Screenshot-2020-04-27-at-15.40.51-1536x756.png",
                # etc.
            },
            {
                "ID": 16,
                "Name": "Infinite Discovery Machine v3",
                "WikiImage": "https://binomicalabs.org/wp-content/uploads/2017/04/The-Infinite-Discovery-Machine-Binomica-Labs.jpg",
                # etc.
            },
            # etc.
        ]
    }
}
```


## History (community)

**Request**

`ajax.php?action=userhistory&type=posts`

`&userid=` — id of user (required)


**Response**

```json
{
    "status": "success",
    "response": {
        "currentPage": 1,
        "pages": 2,
        "threads": [
            {
                "postId": 52,
                "topicId": 2,
                "threadTitle": "Report broken site features",
                "lastPostId": 52,
                "lastRead": 0,
                "locked": true,
                "sticky": false,
                "addedTime": "2020-11-19 03:17:36",
                "body": "HTML",
                "bbbody": "BBcode",
                "editedUserId": 1,
                "editedTime": "2020-11-19 16:22:48",
                "editedUsername": "ohm"
            },
            {
                "postId": 49,
                "topicId": 36,
                # etc.
            },
            {
                "postId": 48,
                "topicId": 35,
                # etc.
            },
            # etc.
        ]
    }
}
```


# Your account

Endpoints that only fetch info about your own account.


## Inbox

The current example isn't from the [BioTorrents.de](https://biotorrents.de) database.


**Request**

`ajax.php?action=inbox`

`&page=` — page number to display (default: `1`)

`&search=` — filter messages by search string

`&searchtype=` — one of: subject, message, user

`&sort=` — if set to `unread` then unread messages come first

`&type=` — one of: inbox or sentbox (default: `inbox`)


**Response**

```json
{
    "status": "success",
    "response": {
        "currentPage": 1,
        "pages": 3,
        "messages": [
            {
                "convId": 3421929,
                "subject": "1 of your torrents has been deleted for inactivity",
                "unread": false,
                "sticky": false,
                "forwardedId": 0,
                "forwardedName": "",
                "senderId": 0,
                "username": "",
                "donor": false,
                "warned": false,
                "enabled": true,
                "date": "2012-06-12 00:54:01"
            },
            # etc.
        ]
    }
}
```


## Conversation 

The current example isn't from the [BioTorrents.de](https://biotorrents.de) database.


**Request**

`ajax.php?action=inbox&type=viewconv`

`&id=` — id of the message to display (required)


**Response**

```json
{
    "status": "success",
    "response": {
        "convId": 3421929,
        "subject": "1 of your torrents has been deleted for inactivity",
        "sticky": false,
        "messages": [
            {
                "messageId": 4507261,
                "senderId": 0,
                "senderName": "System",
                "sentDate": "2012-06-12 00:54:01",
                "bbBody": "BBcode",
                "body": "HTML"
            },
            # etc.
        ]
    }
}
```

## Bookmarks

Fetch bookmarked torrents or artists.


### Torrents

**Request**

`ajax.php?action=bookmarks`

`&type=` — one of torrents, artists (default: `torrents`)


**Response**

```json
{
    "status": "success",
    "response": {
        "bookmarks": [
            {
                "id": 33,
                "name": "CoronaWhy: Collaborative sharing of datasets by members of the CoronaWhy group",
                "year": 2020,
                "accession": "",
                "tagList": "machine_learning data_science epidemiology germany natural_language",
                "vanityHouse": false,
                "picture": "https://i.imgur.com/kt0MsEg.jpg",
                "torrents": [
                    {
                        "id": 41,
                        "groupId": 33,
                        "platform": "Literature",
                        "fileCount": 1,
                        "freeTorrent": false,
                        "size": 13703876874,
                        "leechers": 0,
                        "seeders": 4,
                        "snatched": 2,
                        "time": "2020-04-18 22:54:03",
                        "hasFile": 41
                    }
                ]
            },
            {
                "id": 48,
                "name": "Applied Proteogenomics OrganizationaL Learning and Outcomes (APOLLO) Image Data",
                # etc.
            },
            # etc.
        ]
    }
}
```

### Artists

```json
{
    "status": "success",
    "response": {
        "artists": [
            {
                "artistId": 136,
                "artistName": "Marco Cantoni"
            },
            {
                "artistId": 124,
                "artistName": "Bruce Vendt"
            },
            # etc.
        ]
    }
}
```


## Notifications

**Request**

`ajax.php?action=notifications`

`&page=` — page number to display (default: `1`)


**Response**

```json

```


### Get user notifications

**Request**

`ajax.php?action=get_user_notifications`


**Response**

```json

```


### Clear user notification

**Request**

`ajax.php?action=clear_user_notification`

`&type=` — one of the below NotificationsManager class constants:

- Inbox
- News
- Blog
- StaffPM
- Torrents
- Quotes
- Subscriptions
- Collages
- Global


**Response**

```json

```


## Password validate

Is your current password acceptable?


**Request**

`ajax.php?action=password_validate`


**Response**

```json
{
    "status": "success",
    "response": {
        "pwValidate": "true"
    }
}
```
