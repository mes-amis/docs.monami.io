---
title: Mon Ami REST API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Mon Ami REST API
---

# Introduction

Welcome to the Mon Ami REST API! You can use our API to access Mon Ami REST API endpoints, which can get information on various cats, clients, and breeds in our database.

We have examples in an assortment of languages! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

Mon Ami uses API keys to allow access to the API. You can register a new Mon Ami REST API key at our [developer portal](https://example.com/developers).

Mon Ami expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Basic base64(“#{uid}:#{secret}”)`

<aside class="notice">
You must replace <code>uid</code> and <code>secret</code> with your API key values.
</aside>

# Clients

## Get All clients

```shell
curl "https://app.monami.io/api/clients" \
  -H "Authorization: Basic ...."
```

> The above command returns JSON structured like this:

```json
{
  "clients": [
    {
      "id": 1,
      "status": "active",
      "first_name": "Truman",
      "preferred_name": "Moon",
      "last_name": "Haley",
      "email": "truman@example.monami.io"
    },
    {
      "id": 102,
      "status": "pending",
      "first_name": "New",
      "preferred_name": null,
      "last_name": "Client",
      "email": null
    },
    {
      "id": 103,
      "status": "pending",
      "first_name": "New",
      "preferred_name": null,
      "last_name": "Client",
      "email": null
    }
  ],
  "links": {
    "self": "https://app.monami.io/api/clients?page=1&per_page=3",
    "first": "https://app.monami.io/api/clients?page=1&per_page=3",
    "next": "https://app.monami.io/api/clients?page=2&per_page=3",
    "last": "https://app.monami.io/api/clients?page=2&per_page=3"
  },
  "meta": {
    "total_pages": 2,
    "current_page": 1
  }
}
```

This endpoint retrieves a paginated list of clients as well as pagination links and meta information.

### HTTP Request

`GET https://app.monami.io/api/clients`

### Query Parameters

| Parameter | Default | Description                 |
| --------- | ------- | --------------------------- |
| page      | 1       | Select the page of results. |
| per_page  | 25      | How many results per page.  |

<aside class="success">
Remember — the info!
</aside>

## Get a Specific Client

```shell
curl "https://app.monami.io/api/clients/1" \
  -H "Authorization: Basic ..."
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "status": "active",
  "first_name": "Truman",
  "preferred_name": "Moon",
  "last_name": "Haley",
  "email": "truman@example.monami.io"
}
```

This endpoint retrieves a specific client.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://app.monami.io/clients/<ID>`

### URL Parameters

| Parameter | Description                      |
| --------- | -------------------------------- |
| ID        | The ID of the client to retrieve |
