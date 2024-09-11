# Service Records

## Create a Service Record

> POST /api/service_records

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/service_records \
--form '"{\"recipient_id\":\"ami-54709fe3\",\"program_label\":\"nutrition\",\"service_definition_label\":\"nutrition_definition_name_1\",\"funding_source_label\":\"label_1\",\"provider_label\":\"kihn-mcdermott\",\"service_rate_id\":1,\"unit_count\":2.5,\"service_delivered_on\":\"2024-09-10\",\"comment\":\"Hello API!\"}"'
```

```ruby
require "uri"
require "net/http"

credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')
url = URI("http://app.monami.test/api/service_records")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Basic #{credential}"
form_data = {"recipient_id":"ami-54709fe3","program_label":"nutrition","service_definition_label":"nutrition_definition_name_1","funding_source_label":"label_1","provider_label":"kihn-mcdermott","service_rate_id":1,"unit_count":2.5,"service_delivered_on":"2024-09-10","comment":"Hello API!"}
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 1,
  "status": "active",
  "unit_type": "each",
  "unit_count": 2.5,
  "per_unit_expenditure_cents": 1000,
  "recipient_count": 1,
  "service_delivered_on": "2024-09-10",
  "service_detail": null,
  "service_rate_id": 1,
  "program_label": "nutrition",
  "provider_label": "helping_hands",
  "service_definition_label": "congregate_dining",
  "funding_source_label": "state_funding",
  "site_label": null,
  "recipient_type": "Client",
  "recipient_id": "ami-54709fe3",
  "volunteer_id": null,
  "comment": "Hello API!",
  "links": {
    "recipient_url": "http://app.monami.test/api/clients/ami-54709fe3"
  }
}
```

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Request Parameters

| Parameter                | Description                                                             |
| ------------------------ | ----------------------------------------------------------------------- |
| recipient_id             | The unique ID of the recipient of the service. Ex: `ami-54709fe3`       |
| program_label            | The label of the Program associated with the service record.            |
| service_definition_label | The label of the Service Definition associated with the service record. |
| funding_source_label     | The label of the Funding Source associated with the service record.     |
| provider_label           | The label of the Provider associated with the service record.           |
| service_rate_id          | The ID of the service rate associated with the service record.          |
| unit_count               | The number of service units delivered.                                  |
| service_delivered_on     | The date the service was rendered.                                      |
| comment                  | Notes about the service record                                          |

### Response Parameters

| Parameter                  | Description                                                                                                                                                           |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                         | The unique ID of the service record                                                                                                                                   |
| status                     | Status of the service record. (active, pending, canceled)                                                                                                             |
| unit_type                  | The unit type of the service. (fifteen_minute, daily, each, per_service, per_month, per_meal, per_hour, per_trip, per_session, per_contact, per_activity, per_person) |
| unit_count                 | The number of service units delivered.                                                                                                                                |
| per_unit_expenditure_cents | The per unit cost in Cents.                                                                                                                                           |
| recipient_count            | The number of recipients of the service.                                                                                                                              |
| service_delivered_on       | The date the service was rendered.                                                                                                                                    |
| service_detail             | Notes about the service delivery.                                                                                                                                     |
| service_rate_id            | The ID of the service rate associated with the service record.                                                                                                        |
| program_label              | The label of the Program associated with the service record. This can be used as an ID on other APIs.                                                                 |
| provider_label             | The label of the Provider associated with the service record. This can be used as an ID on other APIs.                                                                |
| service_definition_label   | The label of the Service Definition associated with the service record. This can be used as an ID on other APIs.                                                      |
| funding_source_label       | The label of the Funding Source associated with the service record. This can be used as an ID on other APIs.                                                          |
| site_label                 | The label of the Site associated with the service record. This can be used as an ID on other APIs.                                                                    |
| recipient_type             | The type of recipient of the service. Usually Client, but something service groups are used.                                                                          |
| recipient_id               | The unique ID of the recipieint of the service                                                                                                                        |
| volunteer_id               | The unique ID of a volunteer if they're associated with the service record.                                                                                           |
| comment                    | Notes about the service record                                                                                                                                        |
| links                      | A map of URLs to related API endpoints.                                                                                                                               |

## Get All service records

This endpoint returns a paginated list of service records as well as pagination links and meta information.

> GET /api/service_records

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/clients?page=1&per_page=3&q[date_from]=8/05/2014&q[date_to]=9/06/2024&q[with_status]=active"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/service_records?page=1&per_page=3&q[date_from]=8/05/2014&q[date_to]=9/06/2024&q[with_status]=active',
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

| Parameter       | Description                                             |
| --------------- | ------------------------------------------------------- |
| service_records | The collection of results.                              |
| links           | Pagination links to access all the pages of the results |
| meta            | Helpful response metadata                               |

### Query Parameters

| Parameter      | Default | Description                                                              |
| -------------- | ------- | ------------------------------------------------------------------------ |
| page           | 1       | Select the page of results.                                              |
| per_page       | 25      | How many results per page.                                               |
| q[date_from]   | Null    | The first date a service record could be delivered on in the given range |
| q[date_to]     | Null    | The last date a service record could be delivered on in the given range  |
| q[with_status] | Null    | Filter service records by a status. (active, canceled, pending)          |

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
  "id": 2,
  "status": "active",
  "unit_type": "each",
  "recipient_count": 1,
  "service_delivered_on": "2024-09-06",
  "service_detail": "MyString",
  "service_rate_id": null,
  "program_label": "sint_rem_dicta_sunt",
  "provider_label": "welch-kohler",
  "service_definition_label": "event_definition_name_1",
  "funding_source_label": "label_2",
  "site_label": "dietrich_schmitt",
  "unit_count": 1.0,
  "per_unit_expenditure_cents": 100,
  "recipient_type": "Client",
  "recipient_id": "ami-bb6ff3ef",
  "volunteer_id": null,
  "comment": null,
  "links": {
    "recipient_url": "http://app.monami.test/api/clients/ami-bb6ff3ef"
  }
}
```

This endpoint retrieves a specific service record.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| id        | The id of the service record to retrieve |
