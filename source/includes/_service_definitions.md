# Service Definitions

## Get Service Definitions

This endpoint returns a paginated list of Service Definitions as well as pagination links and meta information.

> GET /api/service_definitions

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/service_definitions?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/service_definitions?page=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "service_definitions": [
    {
      "id": 3,
      "default_frequency": "weekly",
      "name": "nutrition",
      "short_name": null,
      "label": "nutrition",
      "status": "active",
      "created_at": "2024-09-06T13:39:09.186-07:00",
      "updated_at": "2024-09-06T13:39:09.186-07:00"
    },
    {
      "id": 4,
      "default_frequency": "weekly",
      "name": "congregate dining",
      "short_name": null,
      "label": "congregate_dining",
      "status": "active",
      "created_at": "2024-09-06T13:39:09.208-07:00",
      "updated_at": "2024-09-06T13:39:09.208-07:00"
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/service_definitions?page=1",
    "first": "http://app.monami.io/api/service_definitions?page=1",
    "last": "http://app.monami.io/api/service_definitions?page=1"
  },
  "meta": {
    "total_pages": 1,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter           | Description                                             |
| ------------------- | ------------------------------------------------------- |
| service_definitions | The collection of results.                              |
| links               | Pagination links to access all the pages of the results |
| meta                | Helpful response metadata                               |

### Query Parameters

| Parameter | Default | Description                 |
| --------- | ------- | --------------------------- |
| page      | 1       | Select the page of results. |
| per_page  | 25      | How many results per page.  |

<!-- <aside class="success">
Remember — the info!
</aside> -->

## Get a Specific Service Definition

> GET /api/service_definitions/:id_or_label

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/service_definitions/nutrition
# OR
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/service_definitions/43
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/service_definitions/nutrition',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 6,
  "name": "nutrition",
  "label": "nutrition",
  "default_frequency": "weekly",
  "short_name": null,
  "status": "active",
  "created_at": "2024-09-06T13:44:30.089-07:00",
  "updated_at": "2024-09-06T13:44:30.089-07:00"
}
```

This endpoint retrieves a specific Service Definition.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Service Definition Parameters

| Parameter         | Description                                                                                                                            |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| id                | The id of the service definition                                                                                                       |
| name              | The common name of the service definition                                                                                              |
| label             | The label which can be used as a friendly id on the API in within Mon Ami                                                              |
| default_frequency | How frerquently services are delivered by default. (weekly, monthly, once, daily, quarterly, yearly, per_bid, twice_weekly, bi_weekly) |
| short_name        | (Optional) - An abbreviated name for really long names. definition                                                                     |
| status            | The id of the service definition. (pending, active, finished, canceled)                                                                |
