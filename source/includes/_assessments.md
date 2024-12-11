# Assessments

## List available templates for Assessment Requests

This endpoint returns a collection of Documents Templates that can be used to create Assessment Requests.

> GET /api/assessments/templates

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/assessments/templates"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/assessments/templates',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "templates": [
    {
      "name": "Screen for Consumer Services v1",
      "code": "SF-101",
      "label": "sf-101-screen-for-consumer-services-v1",
      "description": "The standard form 101",
      "full_name": "SF-101 - Screen for Consumer Services v1",
      "created_at": "2024-12-10T23:29:39.002Z",
      "updated_at": "2024-12-10T23:29:39.002Z"
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/assessments/templates?page=1&per_page=25",
    "first": "http://app.monami.io/api/assessments/templates?page=1&per_page=25",
    "last": "http://app.monami.io/api/assessments/templates?page=1&per_page=25"
  },
  "meta": {
    "total_pages": 1,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| templates | The collection of available assessment templates.       |
| links     | Pagination links to access all the pages of the results |
| meta      | Helpful response metadata                               |

#### `templates` parameters

| Parameter   | Description                                                                              |
| ----------- | ---------------------------------------------------------------------------------------- |
| label       | The persistent API ID to use when referring to the document or passing in other requests |
| name        | The name of the assessment template.                                                     |
| code        | (Optional) - The document code of the assessment template                                |
| description | A helpful description of the template                                                    |
| full_name   | A combined name of the code and name of the assessment template                          |
| created_at  | The creation DateTime of the assessment template                                         |
| updated_at  | DateTime of the most recent update to the assessment template                            |

### Query Parameters

| Parameter   | Default | Description                                                                       |
| ----------- | ------- | --------------------------------------------------------------------------------- |
| q[label_eq] | null    | Filter by a Document Template label. Ex: 'sf-101-screen-for-consumer-services-v1' |
| page        | 1       | Select the page of results.                                                       |
| per_page    | 25      | How many results per page.                                                        |

## Create an Assessment Request

This endpoint creates an assessment request

> POST /api/assessments/requests

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/assessments/requests"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.post('https://app.monami.io/api/assessments/requests',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    },
    body: '{ "client_id": "ami-010101", "document_label": "sf-101-screen-for-consumer-services-v1" }'
  )
```

> A sucessful request returns an HTTP 201 Created status and JSON structured like this:

```json
{
  "id": 2,
  "source": "api",
  "status": "requested",
  "created_at": "2024-12-10T23:48:51.180Z",
  "updated_at": "2024-12-10T23:48:51.180Z",
  "documentable": {
    "id": 22,
    "type": "Client",
    "label": "ami-010101"
  },
  "document": {
    "metadata": {
      "name": "Screen for Consumer Services v1"
    },
    "data": {}
  }
}
```

### Request Parameters

| Parameter      | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| client_id      | The label of the client to create the assessment request.    |
| document_label | The label of the document template to use for the assessment |

## List Assessment requests

This endpoint returns a collection of assessment requests and metadata

> GET /api/assessments/requests

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/assessments/requests"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/assessments/requests',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "requests": [
    {
      "id": 1,
      "source": "api",
      "status": "completed",
      "created_at": "2024-12-10T23:43:48.318Z",
      "updated_at": "2024-12-10T23:43:52.045Z",
      "documentable": {
        "id": 22,
        "type": "Client",
        "label": "ami-010101"
      },
      "document": {
        "metadata": {
          "name": "Screen for Consumer Services v1"
        },
        "data": {}
      },
      "links": {
        "pdf": "http://app.monami.io/pdf-path"
      }
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/assessments/requests?page=1&per_page=25",
    "first": "http://app.monami.io/api/assessments/requests?page=1&per_page=25",
    "last": "http://app.monami.io/api/assessments/requests?page=1&per_page=25"
  },
  "meta": {
    "total_pages": 1,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| requests  | The collection of assessment requests.                  |
| links     | Pagination links to access all the pages of the results |
| meta      | Helpful response metadata                               |

### Query Parameters

| Parameter    | Default | Description                                     |
| ------------ | ------- | ----------------------------------------------- |
| q[status_eq] | null    | Filter by request status(requested, completed). |
| page         | 1       | Select the page of results.                     |
| per_page     | 25      | How many results per page.                      |

## Show an Assessment request

This endpoint returns an assessment request and metadata.

> GET /api/assessments/requests/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/assessments/requests/5"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/assessments/requests/5',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 5,
  "status": "completed",
  "created_at": "2024-11-14T07:39:01.266Z",
  "updated_at": "2024-11-14T09:26:06.951Z",
  "documentable": {
    "id": 8,
    "type": "Client",
    "label": "ami-010101"
  },
  "document": {
    "metadata": {
      "name": "Screen for Consumer Services v1"
    },
    "data": {
      "adl_dress": "Yes",
      "iadl_shop": "NO DIFFICULTY",
      "iadl_summary": "Quis expedita reprehenderit. Fuga consequatur ipsum. Deleniti eum laboriosam.",
      "iadl_housekeeping": "NO DIFFICULTY",
      "iadl_manage_money": "NO DIFFICULTY",
      "meals_last_3_days": "No",
      "iadl_prepare_meals": "GREAT DIFFICULTY ‑ e.g., little or no involvement in the activity possible",
      "iadl_use_telephone": "GREAT DIFFICULTY ‑ e.g., little or no involvement in the activity possible",
      "iadl_transportation": "GREAT DIFFICULTY ‑ e.g., little or no involvement in the activity possible",
      "assistance_receiving": [],
      "iadl_manage_medications": "SOME DIFFICULTY ‑ e.g., needs some help, is very slow, or fatigues"
    }
  },
  "links": {
    "pdf": "https://app.monami.io/pdf-path"
  }
}
```

### Response Parameters

| Parameter    | Description                                                      |
| ------------ | ---------------------------------------------------------------- |
| id           | The unique ID of the assessment request.                         |
| status       | The status of the assessment request. (`requested`, `completed`) |
| documentable | Type and identification metadata                                 |
| document     | Document data and metadata                                       |
| links        | Links to other repreresentaions of the document                  |
