# Requests

Endpoints related to torrent requests.


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
