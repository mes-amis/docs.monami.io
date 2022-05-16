# Clients

## Get All clients

This endpoint returns a paginated list of clients as well as pagination links and meta information.

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/clients
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/clients',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

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

### Response Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| clients   | The collection of results .                             |
| links     | Pagination links to access all the pages of the results |
| meta      | Helpful response metadata                               |

### HTTP Request

`GET https://app.monami.io/api/clients`

### Query Parameters

| Parameter | Default | Description                 |
| --------- | ------- | --------------------------- |
| page      | 1       | Select the page of results. |
| per_page  | 25      | How many results per page.  |

<!-- <aside class="success">
Remember — the info!
</aside> -->

## Get a Specific Client

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/clients/1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/clients/1',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

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

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### HTTP Request

`GET https://app.monami.io/clients/<ID>`

### URL Parameters

| Parameter | Description                      |
| --------- | -------------------------------- |
| ID        | The ID of the client to retrieve |
