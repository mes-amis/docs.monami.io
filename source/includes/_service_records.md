# Service Records

## Get All service records

This endpoint returns a paginated list of service records as well as pagination links and meta information.

> GET /api/service_records

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/clients?page=1&per_page=3"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/serivce_records?page=1&per_page=3',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "service_records": [
    {
      "id": 19,
      "status": "active",
      "unit_count": 1.0,
      "unit_type": "each",
      "recipient_count": 1,
      "service_delivered_on": "2020-08-05",
      "service_detail": "MyString",
      "program_id": null,
      "provider_id": null,
      "service_definition_id": 19,
      "service_funding_source_id": null,
      "service_rate_id": null,
      "per_unit_expenditure_cents": 0,
      "activity_type": "Meeting",
      "activity_id": 19,
      "recipient_type": "Client",
      "recipient_id": "ami-e0852a7e",
      "volunteer_id": null,
      "links": {
        "recipient_url": "http://app.monami.test/api/clients.ami-e0852a7e"
      }
    },
    {
      "id": 20,
      "status": "active",
      "unit_count": 1.0,
      "unit_type": "each",
      "recipient_count": 1,
      "service_delivered_on": "2020-08-05",
      "service_detail": "AnotherString",
      "program_id": null,
      "provider_id": null,
      "service_definition_id": 20,
      "service_funding_source_id": null,
      "service_rate_id": null,
      "per_unit_expenditure_cents": 0,
      "activity_type": "Meeting",
      "activity_id": 20,
      "recipient_type": "Client",
      "recipient_id": "ami-6969e283",
      "volunteer_id": null,
      "links": {
        "recipient_url": "http://app.monami.test/api/clients.ami-6969e283"
      }
    },
    {
      "id": 21,
      "status": "active",
      "unit_count": 1.0,
      "unit_type": "each",
      "recipient_count": 1,
      "service_delivered_on": "2020-08-05",
      "service_detail": "OneMoreString",
      "program_id": null,
      "provider_id": null,
      "service_definition_id": 21,
      "service_funding_source_id": null,
      "service_rate_id": null,
      "per_unit_expenditure_cents": 0,
      "activity_type": "Meeting",
      "activity_id": 21,
      "recipient_type": "Client",
      "recipient_id": "ami-dfcabdc4",
      "volunteer_id": null,
      "links": {
        "recipient_url": "http://app.monami.test/api/clients.ami-dfcabdc4"
      }
    }
   ],
   "links": {
      "self": "http://app.monami.test/api/service_records?page=1",
      "first": "http://app.monami.test/api/service_records?page=1",
      "last": "http://app.monami.test/api/service_records?page=1"
    },
    "meta": {
      "total_pages": 1,
      "current_page": 1
    }
}

```

### Response Parameters

| Parameter         | Description                                             |
| ----------------- | ------------------------------------------------------- |
| service_records   | The collection of results .                             |
| links             | Pagination links to access all the pages of the results |
| meta              | Helpful response metadata                               |

### Query Parameters

| Parameter | Default | Description                 |
| --------- | ------- | --------------------------- |
| page      | 1       | Select the page of results. |
| per_page  | 25      | How many results per page.  |

<!-- <aside class="success">
Remember — the info!
</aside> -->

## Get a Specific Service Record

> GET /api/service_records/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/service_records/1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/service_records/1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "id": 1,
    "status": "active",
    "unit_count": 1.0,
    "unit_type": "each",
    "recipient_count": 1,
    "service_delivered_on": "2020-08-05",
    "service_detail": "MyString",
    "program_id": null,
    "provider_id": null,
    "service_definition_id": 43,
    "service_funding_source_id": null,
    "service_rate_id": null,
    "per_unit_expenditure_cents": 0,
    "activity_type": "Meeting",
    "activity_id": 43,
    "recipient_type": "Client",
    "recipient_id": "ami-2b2e2f7d",
    "volunteer_id": null,
    "links": {
      "recipient_url": "http://app.monami.test/api/clients.ami-2b2e2f7d"
    }
}

```

This endpoint retrieves a specific service record.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| id        | The id of the service record to retrieve |


## Get a Specific Service Record

> GET /api/service_records/:date_from&:date_to

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/service_records/date_from
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/service_records/1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

