---
title: Create
description: Create a list
published: true
date: 2023-03-25T01:19:30.550Z
tags: 
editor: markdown
dateCreated: 2023-03-25T00:50:02.897Z
---

Create a list. Creating a list does not require an account, however having an account allows updating and deleting lists.

___


**URL:** `/v1/lists`
**HTTP Method:** `POST`
**Headers:**

| Key | Value |
|-----|-------|
| Content-Type | application/json |
| Accept | application/json |
| X-XSRF-Token | `<token value>` |

> See [Authentication](/authentication) for info on how to get the `X-XSRF-Token` value.
{.is-info}

## Body Data


| Property   | Type     | Required | Description |
|------------|----------|----------|-------------|
| name       | string   | Yes      | The name of the list |
| game       | integer  | Yes      | The ID of the game the list is for |
| description | string   | Yes      | A brief description of the list   |
| files[]    | array    | Yes      | The files of the list. At least one file is required |
| version    | string   | No       | The version of the list            |
| website    | string   | No       | The URL of the list's website     |
| discord    | string   | No       | The URL of the list's Discord server |
| readme     | string   | No       | The URL of the list's readme file |
| private    | boolean  | No       | Whether the list is private. Defaults to false |
| expires    | string   | No       | The expiration time of the list. Valid values are `3h`, `24h`, `3d`, `1w`, or `perm`. If this property is not provided, the default value will be determined based on whether the user is logged in or not. Default for anonymous lists is `24h`, for logged in is `perm` |


## Example HTTP Responses

### Success Response

**Code:** `HTTP 201 CREATED`
**Content:**

```json
{
    "data": {
        "name": "A Test List!",
        "version": null,
        "slug": "a-test-list-3",
        "url": "/v1/lists/a-test-list-3",
        "description": "A Description about the test list!",
        "website": "test.com",
        "discord": "example.com",
        "readme": null,
        "private": true,
        "expires": null,
        "created": "2023-03-25T01:19:17.000000Z",
        "updated": "2023-03-25T01:19:17.000000Z",
        "author": {
            "name": "Test22",
            "email": null,
            "verified": false,
            "admin": false,
            "created": "2023-03-25T00:11:01.000000Z",
            "updated": "2023-03-25T00:11:01.000000Z"
        },
        "game": {
            "name": "TESIII Morrowind"
        },
        "files": [
            {
                "name": "99b9f8735fbea0202267dc71047c1c31-plugins.txt",
                "clean_name": "plugins.txt",
                "bytes": 9480,
                "created": "2023-03-24T23:39:03.000000Z",
                "updated": "2023-03-24T23:39:03.000000Z"
            },
            {
                "name": "a7e2ec953166e7661b0c00d308a73c9d-modlist.txt",
                "clean_name": "modlist.txt",
                "bytes": 19253,
                "created": "2023-03-24T23:39:03.000000Z",
                "updated": "2023-03-24T23:39:03.000000Z"
            }
        ],
        "links": {
            "url": "http://localhost:3000/lists/a-test-list-3",
            "self": "http://localhost/v1/lists/a-test-list-3"
        }
    }
}
```

### Error Responses

**Code:** `HTTP 422 UNPROCESSABLE ENTITY`
**Content:**
```json
{
    "message": "The game field is required.",
    "errors": {
        "game": [
            "The game field is required."
        ]
    }
}
```

## Example Usage

`POST /v1/lists`

```json
{
    "name": "My Load Order",
    "game": 1,
    "description": "This is my amazing load order.",
    "files[]": [file, file], // Files must be, well, files.
    "version": "1.0.0",
    "website": "https://example.com/loadorder",
    "discord": "https://discord.gg/example",
    "readme": "https://example.com/loadorder/readme.txt",
    "private": true,
    "expires": "1w"
}

```

This will create a list title `My Load Order` that is private and expires in one week.