# Torrents

Endpoints related to torrents.


## Torrent

**Request**

`ajax.php?action=torrent`

`&id=` — torrent's id (required)

`&hash=` — torrent's hash (must be uppercase)


**Response**

```json
{
    "status": "success",
    "response": {
        "group": {
            "description": "HTML",
            "picture": "https://i.imgur.com/sF40cxi.png",
            "id": 1,
            "name": "Alcohol dehydrogenase ADH1",
            "organism": "Saccharomyces cerevisiae",
            "strain": "S288C",
            "authors": [
                {
                    "id": 2,
                    "name": "David Schild"
                },
                {
                    "id": 1,
                    "name": "Robert K. Mortimer"
                }
            ],
            "year": 1985,
            "accession": "YOL086C",
            "categoryId": 1,
            "categoryName": "Sequences",
            "time": "2019-12-10 01:48:07",
            "isBookmarked": false,
            "tags": [
                "coding",
                "fungi",
                "one.shot",
                "organic.chemistry",
                "protocol.available"
            ]
        },
        "torrent": {
            "id": 1,
            "infoHash": "6A5413B9A0C5EF5B68BED6ABBB8112CBE3870647",
            "platform": "Sanger",
            "format": "FASTA",
            "license": "Public Domain",
            "scope": "Contig",
            "annotated": false,
            "archive": "None",
            "fileCount": 4,
            "size": 5754,
            "seeders": 5,
            "leechers": 0,
            "snatched": 3,
            "freeTorrent": false,
            "reported": false,
            "time": "2019-12-10 01:48:08",
            "description": "HTML",
            "fileList": "S288C_YOL086C_ADH1_coding.fsa{{{1095}}}|||S288C_YOL086C_ADH1_flanking.fsa{{{3157}}}|||S288C_YOL086C_ADH1_genomic.fsa{{{1117}}}|||S288C_YOL086C_ADH1_protein.fsa{{{385}}}",
            "filePath": "ADH1 - YOL086C",
            "userId": 0,
            "username": "Anonymous"
        }
    }
}
```


## Torrent group

**Request**

`ajax.php?action=torrentgroup`

`&id=` — torrent's group id (required)

`&hash=` — hash of a torrent in the torrent group (must be uppercase)


**Response**

```json
{
    "status": "success",
    "response": {
        "group": {
            "description": "HTML",
            "picture": "https://i.imgur.com/SVFU8bC.jpg",
            "id": 37,
            "name": "RSNA Pneumonia Detection Challenge",
            "organism": "",
            "strain": "",
            "authors": [
                {
                    "id": 93,
                    "name": "Radiological Society of North America"
                }
            ],
            "year": 2020,
            "accession": "",
            "categoryId": 8,
            "categoryName": "Images",
            "time": "2020-04-23 05:48:14",
            "isBookmarked": true,
            "tags": [
                "data.science",
                "epidemiology",
                "grayscale",
                "humans",
                "machine.learning",
                "nurse.practitioner",
                "public.health"
            ]
        },
        "torrents": [
            {
                "id": 46,
                "infoHash": "76E026CAA529CED7ECEE99A74E2C060DDEC01F22",
                "platform": "X-Rays",
                "format": "DICOM",
                "license": "Unspecified",
                "scope": "Whole Genome",
                "annotated": true,
                "archive": "ZIP",
                "fileCount": 4,
                "size": 3934053123,
                "seeders": 4,
                "leechers": 0,
                "snatched": 3,
                "freeTorrent": false,
                "reported": false,
                "time": "2020-04-23 05:44:51",
                "description": "Mirror of http://academictorrents.com/details/a0d80e1bb03ef8357d71e058ef9471b4468cd18e",
                "fileList": "stage_2_detailed_class_info.csv{{{1647396}}}|||stage_2_test_images.dcm.zip{{{395756780}}}|||stage_2_train_images.dcm.zip{{{3535158913}}}|||stage_2_train_labels.csv{{{1490034}}}",
                "filePath": "RSNA Pneumonia Detection Challenge - DICOM",
                "userId": 0,
                "username": "Anonymous"
            },
            {
                "id": 47,
                "infoHash": "EFAB8510ED24FC5953AD00993FB62FDDE0013D1D",
                # etc.
            },
            # etc.
        ]
    }
}
```


## Browse (search)

Note that BioTorrents.de still uses Oppaitime metadata under the hood.
These docs are adapted from What.CD, an older and different distribution.
The advanced search options are certain to change in the future.


**Request**

`ajax.php?action=browse`

`&page=` — page to display (default: `1`)

`&searchstr=` — string to search for

`taglist`, `tags_type`, `order_by`, `order_way`, `filter_cat`, `freetorrent`, `vanityhouse`, `scene`, `haslog`, `releasetype`, `media`, `format`, `encoding`, `artistname`, `filelist`, `groupname`, `recordlabel`, `cataloguenumber`, `year`, `remastertitle`, `remasteryear`, `remasterrecordlabel`, `remastercataloguenumber` — as in advanced search


**Response**

```json
{
    "status": "success",
    "response": {
        "currentPage": 1,
        "pages": 1,
        "results": [
            {
                "groupId": 57,
                "groupName": "Massachusetts 1:5,000 Color Ortho Imagery",
                "author": "Production Sanborn LLC",
                "picture": "",
                "tags": [
                    "data.science",
                    "one.shot",
                    "true.color",
                    "massachusetts",
                    "geography"
                ],
                "bookmarked": true,
                "groupYear": 2005,
                "groupTime": 1605710633,
                "accession": "",
                "lab": "MassGIS",
                "location": "",
                "maxSize": 24759011328,
                "totalSnatched": 0,
                "totalSeeders": 2,
                "totalLeechers": 0,
                "torrents": [
                    {
                        "torrentId": 67,
                        "authors": [
                            {
                                "id": 152,
                                "name": "Production Sanborn LLC"
                            }
                        ],
                        "platform": "Other",
                        "format": "JPEG 2000",
                        "license": "Unspecified",
                        "scope": "Whole Genome",
                        "annotated": 0,
                        "archive": "ZIP",
                        "fileCount": 1555,
                        "time": "2020-11-18 15:43:53",
                        "size": 24759011328,
                        "snatches": 0,
                        "seeders": 2,
                        "leechers": 0,
                        "isFreeleech": false,
                        "isNeutralLeech": true,
                        "isPersonalFreeleech": false,
                        "canUseToken": false,
                        "hasSnatched": false
                    }
                ]
            },
            {
                "groupId": 52,
                "groupName": "Massachusetts 1:10,000 Coastal Color Orthophoto Images",
                "author": "NOAA Photogrammetry Division, National Geodetic Survey, Massachusetts Coastal Zone Management Office",
                "picture": "",
                # etc.
            },
            # etc.
        ]
    }
}
```

## Comments 

Fetch comments from torrent pages.


**Request**

`ajax.php?action=tcomments`

`&id=` — torrent's id (required)


**Response**

```json
{
    "status": "success",
    "response": {
        "page": 1,
        "pages": 1,
        "comments": [
            {
                "postId": 2,
                "addedTime": "2020-01-16 05:31:08",
                "bbBody": "Thanks!",
                "body": "Thanks!",
                "editedUserId": 0,
                "editedTime": "",
                "editedUsername": "",
                "userinfo": {
                    "authorId": 2,
                    "authorName": "me",
                    "artist": false,
                    "donor": false,
                    "warned": false,
                    "avatar": "https://i.imgur.com/OdSSWrw.png",
                    "enabled": true,
                    "userTitle": null
                }
            }
        ]
    }
}
```


## Collage

**Request**

`ajax.php?action=collage`

`&id=` — collage's id (required)


**Response**

```json
{
    "status": "success",
    "response": {
        "id": 3,
        "name": "Kratom Genome Project",
        "description": "HTML",
        "creatorID": 2,
        "deleted": false,
        "collageCategoryID": 1,
        "collageCategoryName": "Theme",
        "locked": false,
        "maxGroups": 0,
        "maxGroupsPerUser": 0,
        "hasBookmarked": false,
        "subscriberCount": 0,
        "torrentGroupIDList": [
            7,
            8,
            9,
            10
        ],
        "torrentgroups": [
            {
                "id": 7,
                "name": "Final peer review",
                "year": 2017,
                "categoryId": 11,
                "accession": "",
                "vanityHouse": null,
                "tagList": "plants drug_discovery genomics organic_chemistry one_shot next_gen",
                "picture": "https://i.imgur.com/19Jjdtn.jpg",
                "torrents": [
                    {
                        "torrentid": 7,
                        "platform": "Literature",
                        "fileCount": 6,
                        "size": 488699,
                        "seeders": 5,
                        "leechers": 0,
                        "snatched": 4,
                        "freeTorrent": false,
                        "reported": false,
                        "time": "2019-12-10 04:18:54"
                    }
                ]
            },
            {
                "id": 8,
                "name": "DNA batch 1",
                # etc.
            },
            # etc.
        ]
    }
}
```


## Artist 

Under construction as of 2020-11-24.
Currently not returning the artist's torrent groups.
Please see the below reponse for details.


**Request**

`ajax.php?action=artist`

`&id=` — artist's id (required)

`&artistname=` — artist's name

`&artistreleases=` — if set, only include groups where the artist is the main artist


**Response**

```json
{
    "status": "success",
    "response": {
        "id": 94,
        "name": "Jackie Treehorn",
        "notificationsEnabled": false,
        "hasBookmarked": false,
        "image": "",
        "body": "",
        "vanityHouse": false,
        "tags": [],
        "statistics": {
            "numGroups": 0,
            "numTorrents": 0,
            "numSeeders": 0,
            "numLeechers": 0,
            "numSnatches": 0
        },
        "torrentgroup": [],
        "requests": []
    }
}
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
