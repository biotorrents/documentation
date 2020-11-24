# Users

Endpoints related to user accounts.


## User

If you're viewing your own account, `personal->passkey` will be shown.


**Request**

`ajax.php?action=user`

`&id=` — id of the user to display (required)


**Response**

```json

```


## User search 

**Request**

`ajax.php?action=usersearch`

`&search=` — the search term (required)

`&page=` — page to display (default: `1`)


**Response**

```json

```


## Community stats 

**Request**

`ajax.php?action=community_stats`

`&userid=` — id of the user to display (required)


**Response**

```json

```


## Recents (torrents)

This endpoint circumvents the "upload anonymously" feature.


**Request**

`ajax.php?action=user_recents`

`&userid=` id of user (required)

`&limit=` how many recent torrents to fetch


**Response**

```json

```


## History (community)

**Request**

`ajax.php?action=userhistory&type=posts`

`&userid=` id of user (required)


**Response**

```json

```


# Your account

Endpoints that only fetch info about your own account.

## Inbox

**Request**

`ajax.php?action=inbox`

`&page=` — page number to display (default: `1`)

`&search=` — filter messages by search string

`&searchtype=` — one of: subject, message, user

`&sort=` — if set to `unread` then unread messages come first

`&type=` — one of: inbox or sentbox (default: `inbox`)


**Response**

```

```


## Conversation 

**Request**

`ajax.php?action=inbox&type=viewconv`

`&id=` — id of the message to display (required)


**Response**

```json

```

## Bookmarks

Fetch bookmarked torrents or artists.


### Torrents

**Request**

`ajax.php?action=bookmarks`

`&type=` — one of torrents, artists (default: `torrents`)


**Response**

```json

```

### Artists

```json

```


## Notifications

**Request**

`ajax.php?action=notifications`

`&page=` — page number to display (default: `1`)


**Response**

```json
todo
```


### Get user notifications

**Request**

`ajax.php?action=get_user_notifications`


**Response**

```json
todo
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
