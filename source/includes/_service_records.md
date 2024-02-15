# Service Records

## Get All service records

This endpoint returns a paginated list of service records as well as pagination links and meta information.

> GET /api/service_records

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/clients?page=1&per_page=3"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/service_records?page=1&per_page=3',
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
        "recipient_url": "http://app.monami.test/api/clients/ami-e0852a7e"
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
        "recipient_url": "http://app.monami.test/api/clients/ami-6969e283"
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
        "recipient_url": "http://app.monami.test/api/clients/ami-dfcabdc4"
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
| service_records   | The collection of results.                              |
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
      "recipient_url": "http://app.monami.test/api/clients/ami-2b2e2f7d"
    }
}

```

This endpoint retrieves a specific service record.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| id        | The id of the service record to retrieve |


## Get Service Records by Date Delivered On

> GET /api/service_records/?q[date_from]=:date_from&q[date_to]=:date_to

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/service_records?q[date_from]=8/05/2014&q[date_to]=8/05/2023
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/service_records?q[date_from]=8/05/2014&q[date_to]=8/05/2023',
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
            "id": 3,
            "status": "pending",
            "unit_count": 3.0,
            "unit_type": "each",
            "recipient_count": 1,
            "service_delivered_on": "2023-07-01",
            "service_detail": "MyString",
            "program_id": 14,
            "provider_id": 8,
            "service_definition_id": 29,
            "service_funding_source_id": 18,
            "service_rate_id": null,
            "per_unit_expenditure_cents": 0,
            "activity_type": "Meeting",
            "activity_id": 9,
            "recipient_type": "Client",
            "recipient_id": "ami-fbfa7c51",
            "volunteer_id": null,
            "links": {
                "recipient_url": "http://app.monami.test/api/clients/ami-fbfa7c51"
            }
        },
        {
            "id": 8,
            "status": "pending",
            "unit_count": 3.0,
            "unit_type": "each",
            "recipient_count": 1,
            "service_delivered_on": "2023-07-01",
            "service_detail": "MyString",
            "program_id": 15,
            "provider_id": 8,
            "service_definition_id": 30,
            "service_funding_source_id": 18,
            "service_rate_id": null,
            "per_unit_expenditure_cents": 0,
            "activity_type": "Meeting",
            "activity_id": 10,
            "recipient_type": "Client",
            "recipient_id": "ami-f5ab6afa",
            "volunteer_id": null,
            "links": {
                "recipient_url": "http://app.monami.test/api/clients/ami-f5ab6afa"
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

This endpoint filters based on service record delivery date.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter        | Description                                                              |
| ---------------- | ------------------------------------------------------------------------ |
| date_from        | The first date a service record could be delivered on in the given range |
| date_to          | The last date a service record could be delivered on in the given range  |


## Get Service Records by Status

> GET /api/service_records?q[with_status]=:pending

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET http://app.monami.test/api/service_records?q[with_status]=:status
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/api/service_records?q[with_status]=:status
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
            "id": 1,
            "status": "pending",
            "unit_count": 1.0,
            "unit_type": "each",
            "recipient_count": 1,
            "service_delivered_on": "2023-08-10",
            "service_detail": "MyString",
            "program_id": 12,
            "provider_id": 8,
            "service_definition_id": 29,
            "service_funding_source_id": 18,
            "service_rate_id": null,
            "per_unit_expenditure_cents": 0,
            "activity_type": "Meeting",
            "activity_id": 9,
            "recipient_type": "Client",
            "recipient_id": "ami-fc970dcb",
            "volunteer_id": null,
            "links": {
                "recipient_url": "http://app.monami.test/api/clients.ami-fc970dcb"
            }
        },
        {
            "id": 2,
            "status": "pending",
            "unit_count": 3.0,
            "unit_type": "each",
            "recipient_count": 1,
            "service_delivered_on": "2023-08-10",
            "service_detail": "MyString",
            "program_id": 12,
            "provider_id": 8,
            "service_definition_id": 29,
            "service_funding_source_id": 18,
            "service_rate_id": null,
            "per_unit_expenditure_cents": 0,
            "activity_type": "Meeting",
            "activity_id": 9,
            "recipient_type": "Client",
            "recipient_id": "ami-d311dce8",
            "volunteer_id": null,
            "links": {
                "recipient_url": "http://app.monami.test/api/clients.ami-d311dce8"
            }
        },
        {
            "id": 3,
            "status": "pending",
            "unit_count": 3.0,
            "unit_type": "each",
            "recipient_count": 1,
            "service_delivered_on": "2023-07-02",
            "service_detail": "MyString",
            "program_id": 12,
            "provider_id": 8,
            "service_definition_id": 29,
            "service_funding_source_id": 18,
            "service_rate_id": null,
            "per_unit_expenditure_cents": 0,
            "activity_type": "Meeting",
            "activity_id": 9,
            "recipient_type": "Client",
            "recipient_id": "ami-ff0a7ac4",
            "volunteer_id": null,
            "links": {
                "recipient_url": "http://app.monami.test/api/clients.ami-ff0a7ac4"
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

This endpoint filters based on service record status.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter     | Description                       |
| ------------- | --------------------------------- |
| status        | The status of the service record  |


