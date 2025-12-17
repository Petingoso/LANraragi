---
description: Query and modify the database.
---

# Database API

## Get Statistics

<mark style="color:blue;">`GET`</mark> `http://lrr.tvc-16.science/api/database/stats`

Get tags from the database, with a value symbolizing their prevalence.

#### Query Parameters

| Name      | Type | Description                                                                                                                                           |
| --------- | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| minweight | int  | <p>Add this parameter if you want to only get tags whose weight is at least the given minimum.<br>Default is 1 if not specified, to get all tags.</p> |

{% tabs %}
{% tab title="200 " %}
```javascript
[
    {"namespace":"character","text":"jeanne alter","weight":2},
    {"namespace":"character","text":"xuanzang","weight":1},
    {"namespace":"artist","text":"wada rco","weight":2},
    {"namespace":"parody","text":"fate grand order","weight":3},
    {"namespace":"group","text":"wadamemo","weight":2},
    {"namespace":"","text":"artbook","weight":2},
]
```
{% endtab %}
{% endtabs %}

## 🔑Clean the Database

<mark style="color:green;">`POST`</mark> `http://lrr.tvc-16.science/api/database/clean`

Cleans the Database, removing entries for files that are no longer on the filesystem.

{% tabs %}
{% tab title="200 " %}
```javascript
{
  "operation": "clean_database",
  "success": 1,
  "deleted": 0,
  "unlinked": 0
}
```
{% endtab %}
{% endtabs %}

## 🔑Drop the Database

<mark style="color:green;">`POST`</mark> `http://lrr.tvc-16.science/api/database/drop`

Delete the entire database, including user preferences.\
This is a rather dangerous endpoint, invoking it might lock you out of the server as a client!

{% tabs %}
{% tab title="200 " %}
```javascript
{
    "operation":"drop_database",
    "success":1
}
```
{% endtab %}
{% endtabs %}

## 🔑Get a backup JSON

<mark style="color:blue;">`GET`</mark> `http://lrr.tvc-16.science/api/database/backup`

Scans the entire database and returns a backup in JSON form.\
This backup can be reimported manually through the Backup and Restore feature.

{% tabs %}
{% tab title="200 " %}
```javascript
{
    "archives": [
        {
            "arcid": "e4c422fd10943dc169e3489a38cdbf57101a5f7e",
            "title": "rohan",
            "tags": "language:english, parody:jojos bizarre adventure, character:rohan kishibe, date_added:1541778455",
            "summary": "",
            "thumbhash": "f0a335a3562da03b61d69242b9562592eade06b9",
            "filename": "rohan"
        },
        {
            "arcid": "e69e43e1355267f7d32a4f9b7f2fe108d2401ebf",
            "title": "saturn",
            "tags": " language:english, parody:sailor moon, character:sailor saturn, date_added:1553537268",
            "summary": "",
            "thumbhash": "631fb75a5aed97ee977783472e7d6b093c6df87d",
            "filename": "saturn"
        },
        {
            "arcid": "d1858d5dc36925aa66be072a97817650d39de166",
            "title": "test title",
            "tags": "",
            "summary": "",
            "thumbhash": "9846bb6d62949b56545c42e88d8010446b65702e",
            "filename": "[Memes]9B789D38B0784C5FBC9D59A9F24D20F2"
        },
        {
            "arcid": "28697b96f0ac5858be2614ed10ca47742c9522fd",
            "title": "Fate GO MEMO",
            "tags": "parody:fate grand order, group:wadamemo, artist:wada rco, artbook, full color, super:test, date_added:1553537258",
            "summary": "",
            "thumbhash": "ec2a0ca3a3da67a9390889f0910fe494241faa9a",
            "filename": "FateGOMEMO"
        }
    ],
    "categories": [
        {
            "archives": [
                "e69e43e1355267f7d32a4f9b7f2fe108d2401ebf",
                "d1858d5dc36925aa66be072a97817650d39de166"
            ],
            "catid": "SET_1749925373",
            "name": "saved",
            "search": ""
        },
        {
            "archives": [],
            "catid": "SET_1749925633",
            "name": "english",
            "search": "language:english"
        }
    ],
    "tankoubons": [
        {
            "archives": [
                "e69e43e1355267f7d32a4f9b7f2fe108d2401ebf"
            ]
            "tankid": "TANK_1749925516",
            "name": "sailor moon"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## 🔑Clear all&#x20;

<mark style="color:red;">`DELETE`</mark> `http://lrr.tvc-16.science/api/database/isnew`

Clears the "New!" flag on all archives.

{% tabs %}
{% tab title="200 " %}
```javascript
{
    "operation":"clear_new_all",
    "success":1
}
```
{% endtab %}
{% endtabs %}
