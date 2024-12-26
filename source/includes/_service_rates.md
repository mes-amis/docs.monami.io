# Service Rates

## Get Service Rates

This endpoint returns a paginated list of Service Rates as well as pagination links and meta information.

> GET /api/service_rates

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/service_rates?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/service_rates?page=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A successful request returns JSON structured like this:

```json
{
  "service_rates": [
    {
      "id": 6,
      "start_on": "2024-08-30",
      "end_on": null,
      "unit_rate_in_cents": 1000,
      "rate_details": null,
      "created_at": "2024-09-06T14:49:23.408-07:00",
      "updated_at": "2024-09-06T14:49:23.408-07:00",
      "provider_label": "cole_marvin",
      "service_definition_label": "nutrition"
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/service_rates?page=1",
    "first": "http://app.monami.io/api/service_rates?page=1",
    "last": "http://app.monami.io/api/service_rates?page=1"
  },
  "meta": {
    "total_pages": 1,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter     | Description                                             |
| ------------- | ------------------------------------------------------- |
| service_rates | The collection of results.                              |
| links         | Pagination links to access all the pages of the results |
| meta          | Helpful response metadata                               |

### Query Parameters

| Parameter | Default | Description                 |
| --------- | ------- | --------------------------- |
| page      | 1       | Select the page of results. |
| per_page  | 25      | How many results per page.  |

<!-- <aside class="success">
Remember — the info!
</aside> -->

## Get a Specific Service Rate

> GET /api/service_rates/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/service_rates/5
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/service_rates/5',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A successful request returns JSON structured like this:

```json
{
  "id": 5,
  "start_on": "2024-08-30",
  "end_on": null,
  "unit_rate_in_cents": 1000,
  "rate_details": null,
  "provider_label": "abshire_hintz_and_robel",
  "service_definition_label": "nutrition",
  "created_at": "2024-09-06T14:47:48.061-07:00",
  "updated_at": "2024-09-06T14:47:48.061-07:00"
}
```

This endpoint retrieves a specific Service Rate.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Service Rate Parameters

| Parameter                | Description                                                    |
| ------------------------ | -------------------------------------------------------------- |
| id                       | The id of the service definition                               |
| starts_on                | The start date of the rate being valid.                        |
| end_on                   | (Optional) - If set, the final date of the rate being valid.   |
| unit_rate_in_cents       | The cost in cents. 100 cents = 1 Dollar.                       |
| rate_details             | (Optional) - A short description of the service rate.          |
| provider_label           | The label of the provider associated with the rate.            |
| service_definition_label | The label of the service definition associated with this rate. |
