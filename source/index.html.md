---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Notes Storer API
---

# Introduction

Welcome to the Note Storer API, an open-source project that provides a simple and efficient way to store and manage notes. This API is designed to be easily integrated into any application that requires note-taking functionality. With our API, you can create, retrieve, update, delete and list notes with ease. 
The Note Storer API is organized around [REST](https://en.wikipedia.org/wiki/Representational_state_transfer).

# Authentication

> To authorization header looks like this:


```shell
  -H "Authorization: Basic amFuZToxMjM0NTY3OA=="
```

Note Stoer API uses Basic Authentication to authenticate the requests. Each request must include an HTTP header with the 'username' and 'password' of an authorized user. The 'username and 'password' should be encoded in `Base64` and passed as the value of the `Authorization` header.

To obtain the credentials, register for an account on the Note Storer platform. Once registered, you will receive a username and password that can be used to authenticate the requests. 

<aside class="warning">Keep the credentials secure and don't share them with others, as they provide access to your data. </aside>


`Authorization: Basic Base64{username:password}`

<aside class="notice">
You must replace `username` and`password` with your credentails and use [Base64 encoding](https://www.base64encode.org/).
</aside>

# API Reference

## Create a note

```shell
curl -L 'https://dev-api.notestorer.com/notes' \
-H 'Authorization: Basic amFuZToxMjM0NTY3OA==' \
-H 'Content-Type: application/json' \
-d '{
    "title":"My first note",
    "content": "This is my **first** note."
}'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "title": "My first note",
  "content": "This is my **first** note.",
  "created": "2023-19-03 22:26:33",
  "last_updated": "2023-19-03 22:26:33"
}

```

Use the endpoint to create a new note.

### HTTP Request

`GET https://dev-api.notestorer.com/notes`

### Request body

Parameter | Description
--------- | -----------
title | Title of the note. If no title is specified, current date and time is set as the title.
content | Text of the note. Symbols and markdown syntax is allowed. Maximum allowed length of the text is 5000 characters.


## Retrieve a note

```shell
curl -L 'https://dev-api.notestorer.com/notes/{id}' \
-H 'Authorization: Basic amFuZToxMjM0NTY3OA=='
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "title": "My first note",
  "content": "This is my **first** note.",
  "created": "2023-19-03 22:26:33",
  "last_updated": "2023-19-03 22:26:33"
}
```

Use the endpoint to retrieve a note specified by ID.

### HTTP Request

`GET https://dev-api.notestorer.com/notes/{id}`

### Path parameters

Parameter | Description
--------- | -----------
id | The ID of the note to retrieve.

## Update a note


### Quest body

Parameter | Description
--------- | -----------
title | Updated title of the note.
content | Updated text of the note. Symbols and markdown syntax is allowed. Maximum allowed length of the text is 5000 characters.


```shell
curl --location --request POST 'https://dev-api.notestorer.com/notes/:id' \
--header 'Authorization: Basic amFuZToxMjM0NTY3OA==' \
--header 'Content-Type: application/json' \
--data '{
    "content":"This is an updated note."
}'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "title": "My first note",
  "content": "This is an updated note.",
  "created": "2023-19-03 22:26:33",
  "last_updated": "2023-19-03 23:20:12"
}
```

Use the endpoint to update an existing note. Any property not provided will be left unchanged.

### HTTP Request

`POST https://dev-api.notestorer.com/notes/{id}`


### Path parameters

Parameter | Description
--------- | -----------
id | The ID of the note to update.


## Delete a note


```shell
curl --location -g --request DELETE 'https://dev-api.notestorer.com/notes/{id}' \
--header 'Authorization: Basic amFuZToxMjM0NTY3OA=='
```

> The above command returns an HTTP 200 status code. 

Use the endpoint to permanently delete a note specified by ID. The action can't be undone.

### HTTP Request

`DELETE https://dev-api.notestorer.com/notes/{id}`

### Path Parameters

Parameter | Description
--------- | -----------
id | The ID of the note to delete.


## List all notes


```shell
curl --location --request GET 'https://dev-api.notestorer.com/notes' \
--header 'Authorization: Basic amFuZToxMjM0NTY3OA=='
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "title": "My first note",
    "content": "This is an updated note.",
    "created": "2023-19-03 22:26:33",
    "last_updated": "2023-19-03 23:20:12"
  },
  {
    "id": 2,
    "title": "My second note",
    "content": "This is my second note.",
    "created": "2023-22-03 22:26:33",
    "last_updated": "2023-23-03 23:20:12"
  }
]
```

Use the endpoint to retrieve all your notes. The notes are sorted by the last update date, with the latest updates notes appearing first.


### HTTP Request

`[GET http://example.com/notes](https://dev-api.notestorer.com/notes)`