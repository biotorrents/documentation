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

Note that [BioTorrents.de](https://biotorrents.de) still uses Oppaitime metadata behind the scenes.
These docs are also adapted from What.CD, an older and different distribution.
The advanced search options are certain to change in the future.

**Request**

`ajax.php?action=browse`

`&searchstr=` — string to search for

`&page=` — page to display (default: `1`)

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
                },
                # etc.
            }
        ]
    }
}
```

# Torrent features

Various features around the torrents themselves.

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
Please see the response below for details.

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

## Request

**Request**

`ajax.php?action=request`

`&id=` — request id (required)

`&page=` — page of the comments to display (default: last page)

**Response**

```json
{
  "status": "success",
  "response": {
    "requestId": 2,
    "requestorId": 2,
    "requestorName": "me",
    "isBookmarked": false,
    "requestTax": 0.1,
    "timeAdded": "2020-04-23 02:02:37",
    "canEdit": true,
    "canVote": true,
    "minimumVote": 20971520,
    "voteCount": 1,
    "lastVote": "2020-11-15 06:51:56",
    "topContributors": [
      {
        "userId": 2,
        "userName": "me",
        "bounty": 15461882266
      }
    ],
    "totalBounty": 15461882266,
    "categoryId": 10,
    "categoryName": "Models",
    "title": "Markov State Model Database of Protein Folding Datasets",
    "year": 0,
    "image": "",
    "bbDescription": "BBcode",
    "description": "HTML",
    "artists": [
      {
        "id": 88,
        "name": "Thomas Lane"
      }
    ],
    "isFilled": false,
    "fillerId": 0,
    "fillerName": "",
    "torrentId": 0,
    "timeFilled": "",
    "tags": [
      "coding",
      "proteomics",
      "biochemistry",
      "data.science",
      "gene.expression"
    ],
    "comments": [],
    "commentPage": 1,
    "commentPages": 0
  }
}
```

## Request search

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
{
    "status": "success",
    "response": {
        "currentPage": 1,
        "pages": 1,
        "results": [
            {
                "requestId": 3,
                "requestorId": 2,
                "requestorName": "me",
                "timeAdded": "2020-11-15 06:49:10",
                "lastVote": "2020-11-15 06:49:27",
                "voteCount": 1,
                "bounty": 7825312768,
                "categoryId": 8,
                "categoryName": "Images",
                "authors": [
                    {
                        "id": 148,
                        "name": "Oliver Batchelor"
                    }
                ],
                "title": "trees.tar.gz",
                "year": 0,
                "picture": "",
                "description": "BBcode",
                "isFilled": false,
                "fillerId": 0,
                "fillerName": "",
                "torrentId": 0,
                "timeFilled": ""
            },
            {
                "requestId": 2,
                "requestorId": 2,
                # etc.
            },
            # etc.
        ]
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
{
    "status": "success",
    "response": [
        {
            "caption": "Most Active Torrents Uploaded in the Past Day",
            "tag": "day",
            "limit": 10,
            "results": [
                {
                    "torrentId": 67,
                    "groupId": 57,
                    "author": "Production Sanborn LLC",
                    "groupName": "Massachusetts 1:5,000 Color Ortho Imagery",
                    "groupCategory": 9,
                    "groupYear": 2005,
                    "platform": "Other",
                    "tags": [
                        "data.science",
                        "one.shot",
                        "true.color",
                        "massachusetts",
                        "geography"
                    ],
                    "snatched": 0,
                    "seeders": 2,
                    "leechers": 0,
                    "data": 0,
                    "size": 24759011328,
                    "picture": ""
                },
                {
                    "torrentId": 18,
                    "groupId": 18,
                    # etc.
                },
                # etc.
            ]
        },
        {
            "caption": "Most Active Torrents Uploaded in the Past Week",
            "tag": "week",
            "limit": 10,
            "results": [
                {
                    "torrentId": 30,
                    "groupId": 15,
                    # etc.
                },
                {
                    "torrentId": 32,
                    "groupId": 27,
                    # etc.
                },
                # etc.
            ]
        },
        {
            "caption": "Most Active Torrents of All Time",
            "tag": "overall",
            "limit": 10,
            "results": [
                {
                    "torrentId": 1,
                    "groupId": 1,
                    # etc.
                },
                {
                    "torrentId": 25,
                    "groupId": 25,
                    # etc.
                },
                # etc.
            ]
        },
        {
            "caption": "Most Snatched Torrents",
            "tag": "snatched",
            "limit": 10,
            "results": [
                {
                    "torrentId": 40,
                    "groupId": 32,
                    # etc.
                },
                {
                    "torrentId": 43,
                    "groupId": 34,
                    # etc.
                },
                # etc.
            ]
        },
        {
            "caption": "Most Data Transferred Torrents",
            "tag": "data",
            "limit": 10,
            "results": [
                {
                    "torrentId": 28,
                    "groupId": 17,
                    # etc.
                },
                {
                    "torrentId": 10,
                    "groupId": 10,
                    # etc.
                },
                # etc.
            ]
        },
        {
            "caption": "Best Seeded Torrents",
            "tag": "seeded",
            "limit": 10,
            "results": [
                {
                    "torrentId": 50,
                    "groupId": 40,
                    # etc.
                },
                {
                    "torrentId": 48,
                    "groupId": 38,
                    # etc.
                },
                # etc.
            ]
        }
    ]
}
```

### Tags

```json
{
    "status": "success",
    "response": [
        {
            "caption": "Most Used Torrent Tags",
            "tag": "ut",
            "limit": 10,
            "results": [
                {
                    "name": "one.shot",
                    "uses": 24
                },
                {
                    "name": "humans",
                    "uses": 22
                },
                {
                    "name": "data.science",
                    "uses": 20
                },
                # etc.
            ]
        },
        {
            "caption": "Most Used Request Tags",
            "tag": "ur",
            "limit": 10,
            "results": [
                {
                    "name": "coding",
                    "uses": 2
                },
                {
                    "name": "biochemistry",
                    "uses": 2
                },
                {
                    "name": "plants",
                    "uses": 1
                },
                # etc.
            ]
        }
    ]
}
```

### Users

Usernames are masked to `null` in the output unless you have moderator permissions.

```json
{
    "status": "success",
    "response": [
        {
            "caption": "Uploaders",
            "tag": "ul",
            "limit": 10,
            "results": [
                {
                    "id": 28,
                    "username": "seedbox",
                    "uploaded": 100918879562,
                    "upSpeed": 4893.906,
                    "downloaded": 12327881516,
                    "downSpeed": 600.9437,
                    "numUploads": 0,
                    "joinDate": "2020-04-01 15:50:04"
                },
                # etc.
            ]
        },
        {
            "caption": "Downloaders",
            "tag": "dl",
            "limit": 10,
            "results": [
                {
                    "id": 28,
                    "username": "seedbox",
                    # etc.
                },
                # etc.
            ]
        },
        {
            "caption": "Torrents Uploaded",
            "tag": "numul",
            "limit": 10,
            "results": [
                {
                    "id": 28,
                    "username": "seedbox",
                    # etc.
                },
                # etc.
            ]
        },
        {
            "caption": "Fastest Uploaders",
            "tag": "uls",
            "limit": 10,
            "results": [
                {
                    "id": 28,
                    "username": "seedbox",
                    # etc.
                },
                # etc.
            ]
        },
        {
            "caption": "Fastest Downloaders",
            "tag": "dls",
            "limit": 10,
            "results": [
                {
                    "id": 28,
                    "username": "seedbox",
                    # etc.
                },
                # etc.
            ]
        }
    ]
}
```
