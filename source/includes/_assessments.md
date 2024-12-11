# Assessments

## List available templates for assessments

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
        "pdf": "http://app.monami.io/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBBYlk9IiwiZXhwIjoiMjAyNC0xMi0xMVQwMDoyNDoxNy4yMDNaIiwicHVyIjoiYmxvYl9pZCJ9fQ==--60ce994086da61699e1d05034c0afad08588582a/Screen%20for%20Consumer%20Services%20v1_1733874231"
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
