---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors
  - contact-us

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Note Storer API
---

# Introduction

Welcome to the Note Storer API, an open-source project that provides a simple and efficient way to store and manage notes. This API is designed to be easily integrated into any application that requires note-taking functionality. The Note Storer application can be helpful for projects who need to store and retrieve notes within their application. 

The task management tools, in particular, can benefit from this integration. By integrating the Note Storer API, your users can create notes related to their tasks and make the task management process a lot smoother. For instance, users can store their findings or useful information about their tasks in their notes and then access them when working on the task. Moreover, they can get all their notes and quickly find relevant information across multiple tasks. 

With our API, you can create, retrieve, update, delete and list notes with ease. It is designed to be flexible and customizable, allowing you to adjust and build your own unique note-taking experience for your users.

The Note Storer API is organized around [REST](https://en.wikipedia.org/wiki/Representational_state_transfer).


# Authentication

> The authorization header looks like this:


```shell
  -H "Authorization: Basic amFuZToxMjM0NTY3OA=="
```

Note Stoer API uses Basic Authentication to authenticate the requests. Each request must include an HTTP header with the 'username' and 'password' of an authorized user. The 'username and 'password' should be encoded in `Base64` and passed as the value of the `Authorization` header.

To obtain the credentials, register for an account on the Note Storer platform. Once registered, you will receive a username and password that can be used to authenticate the requests. 


<aside class="warning">Keep the credentials secure and don't share them with others, as they provide access to your data. </aside>


`Authorization: Basic Base64{username:password}`

You must replace `username` and`password` with your credentails and use [Base64 encoding](https://www.base64encode.org/).

If you have trouble authenticating your requests, [contact the help center](https://taguhihakobyan.github.io/NotesStorerApi/#contact-us) for assistance.


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

Use the endpoint to create a new note.

### HTTP Request

`POST https://dev-api.notestorer.com/notes`

#### Request body

Parameter | Type | Description
--------- | ---- | -----------
title | string |Title of the note. If no title is specified, current date and time is set as the title.
content <br/><sup>Required</sup>  | string | Text of the note. Symbols and markdown syntax is allowed. Maximum allowed length of the text is 5000 characters.


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

#### Response body

Parameter | Type | Description
--------- | ---- | -----------
id | string | A unique identifier for the note. 
title | string | Title of the note.
content | string | Text of the note.
created | string | Date and time when the note is created. The date is in the UTC format.
last_updated | string | Date and time when the note is last updated. The date is in the UTC format.

## Retrieve a note

```shell
curl -L 'https://dev-api.notestorer.com/notes/{id}' \
-H 'Authorization: Basic amFuZToxMjM0NTY3OA=='
```

Use the endpoint to retrieve a note specified by ID.

### HTTP Request

`GET https://dev-api.notestorer.com/notes/{id}`

#### Path parameters

Parameter | Description
--------- | -----------
id | The ID of the note to retrieve.


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

#### Response body

Parameter | Type | Description
--------- | ---- | -----------
id | string | A unique identifier for the note. 
title | string | Title of the note.
content | string | Text of the note.
created | string | Date and time when the note is created. The date is in the UTC format.
last_updated | string | Date and time when the note is last updated. The date is in the UTC format.

## Update a note

```shell
curl --location --request POST 'https://dev-api.notestorer.com/notes/:id' \
--header 'Authorization: Basic amFuZToxMjM0NTY3OA==' \
--header 'Content-Type: application/json' \
--data '{
    "content":"This is an updated note."
}'
```
Use the endpoint to update an existing note. Any property not provided will be left unchanged.

### HTTP Request

`POST https://dev-api.notestorer.com/notes/{id}`


#### Path parameters

Parameter | Description
--------- | -----------
id | The ID of the note to update.


#### Request body

Parameter | Type | Description
--------- | ---- |-----------
title | string | Updated title of the note.
content | string | Updated text of the note. Symbols and markdown syntax is allowed. Maximum allowed length of the text is 5000 characters.



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

#### Response body

Parameter | Type | Description
--------- | ---- | -----------
id | string | A unique identifier for the note. 
title | string | Title of the note.
content | string | Text of the note.
created | string | Date and time when the note is created. The date is in the UTC format.
last_updated | string | Date and time when the note is last updated. The date is in the UTC format.


## Delete a note


```shell
curl --location -g --request DELETE 'https://dev-api.notestorer.com/notes/{id}' \
--header 'Authorization: Basic amFuZToxMjM0NTY3OA=='
```

> The above command returns an HTTP `200 OK` status code. 

Use the endpoint to permanently delete a note specified by ID. The action can't be undone.

### HTTP Request

`DELETE https://dev-api.notestorer.com/notes/{id}`

#### Path Parameters

Parameter | Description
--------- | -----------
id | The ID of the note to delete.


## List all notes


```shell
curl --location --request GET 'https://dev-api.notestorer.com/notes' \
--header 'Authorization: Basic amFuZToxMjM0NTY3OA=='
```


Use the endpoint all your notes. The notes are sorted by the last update date, with the latest updates notes appearing first.


### HTTP Request

`GET https://dev-api.notestorer.com/notes`

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

#### Response body

Parameter | Type | Description
--------- | ---- | -----------
id | string | A unique identifier for the note. 
title | string | Title of the note.
content | string | Text of the note.
created | string | Date and time when the note is created. The date is in the UTC format.
last_updated | string | Date and time when the note is last updated. The date is in the UTC format.
