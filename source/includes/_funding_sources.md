# Funding Sources

## Get Funding Sources

This endpoint returns a paginated list of Funding Sources as well as pagination links and meta information.

> GET /api/funding_sources

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/funding_sources?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/funding_sources?page=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "funding_sources": [
    {
      "id": 124,
      "name": "East O'Reilly College",
      "status": "active",
      "created_at": "2024-09-06T16:37:13.767-07:00",
      "updated_at": "2024-09-06T16:37:13.767-07:00",
      "label": "label_3"
    },
    {
      "id": 125,
      "name": "South Bahringer Academy",
      "status": "active",
      "created_at": "2024-09-06T16:37:13.779-07:00",
      "updated_at": "2024-09-06T16:37:13.779-07:00",
      "label": "label_4"
    },
    {
      "id": 126,
      "name": "Thompson Academy",
      "status": "active",
      "created_at": "2024-09-06T16:37:13.873-07:00",
      "updated_at": "2024-09-06T16:37:13.873-07:00",
      "label": "label_5"
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/funding_sources?page=1",
    "first": "http://app.monami.io/api/funding_sources?page=1",
    "last": "http://app.monami.io/api/funding_sources?page=1"
  },
  "meta": {
    "total_pages": 1,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter       | Description                                             |
| --------------- | ------------------------------------------------------- |
| funding_sources | The collection of results.                              |
| links           | Pagination links to access all the pages of the results |
| meta            | Helpful response metadata                               |

### Query Parameters

| Parameter | Default | Description                 |
| --------- | ------- | --------------------------- |
| page      | 1       | Select the page of results. |
| per_page  | 25      | How many results per page.  |

<!-- <aside class="success">
Remember — the info!
</aside> -->

## Get a Specific Funding Source

> GET /api/funding_sources/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/funding_sources/5
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/funding_sources/5',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 122,
  "name": "East Beier",
  "label": "label_1",
  "status": "active",
  "created_at": "2024-09-06T16:36:23.837-07:00",
  "updated_at": "2024-09-06T16:36:23.837-07:00"
}
```

This endpoint retrieves a specific Funding Source.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Funding Source Parameters

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| id        | The id of the funding source                               |
| name      | Name of the funding source                                 |
| label     | A friendly id that can be used on APIs and within Mon Ami. |
| status    | The status of the funding source. (active, disabled)       |
