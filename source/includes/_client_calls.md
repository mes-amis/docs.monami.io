# Client Calls

## Get Client Calls

This endpoint returns a paginated list of client calls as well as pagination links and meta information.

> GET /api/client_calls

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/client_calls?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/client_calls?page=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "client_calls": [
        {
            "id": 10,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-02-15T12:09:42.496Z",
            "slug": "97ea1e946a2a7ee4",
            "created_at": "2024-02-15T12:09:42.500Z",
            "updated_at": "2024-02-15T12:10:01.400Z",
            "completed_call_duration_in_minutes": 17.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-02-15T12:09:34.494Z",
                "updated_at": "2024-02-15T12:09:57.867Z",
                "type": "internal",
                "description": null,
                "category": null,
                "reporting_framework": "oaa",
                "label": "community_services"
            },
            "funding_source": {
                "id": 13,
                "name": "III-B",
                "status": "active",
                "created_at": "2024-02-15T12:09:57.740Z",
                "updated_at": "2024-02-15T12:09:57.740Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-02-15T12:09:57.872Z",
                "updated_at": "2024-02-15T12:09:57.872Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 2,
                "person_id": 13,
                "status": "active",
                "created_at": "2024-02-15T04:09:36.909-08:00",
                "updated_at": "2024-02-15T04:13:09.134-08:00",
                "slug": "ami-5229b359",
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "My String",
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "My String",
                    "state": "My String",
                    "zip": "My String"
                }
            },
            "volunteer": {
                "id": 1,
                "person_id": 7,
                "status": "approved",
                "created_at": "2024-02-15T04:09:35.499-08:00",
                "updated_at": "2024-02-15T04:09:35.648-08:00",
                "slug": "clinton-p-eligendi-amet-consectetur",
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "My String"
            }
        }
    ],
    "links": {
        "self": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "first": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "next": "http://app.monami.test/api/client_calls?page=2&per_page=1",
        "last": "http://app.monami.test/api/client_calls?page=23&per_page=1"
    },
    "meta": {
        "total_pages": 23,
        "current_page": 1
    }
}
```

### Response Parameters

| Parameter         | Description                                             |
| ----------------- | ------------------------------------------------------- |
| client_calls      | The collection of results.                              |
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

## Get a Specific Client Call

> GET /api/client_calls/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/client_calls/10
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/client_calls/10',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "id": 10,
    "attempt_count": 0,
    "status": "completed",
    "completed_call_start_at": "2024-02-15T12:09:42.496Z",
    "slug": "97ea1e946a2a7ee4",
    "created_at": "2024-02-15T12:09:42.500Z",
    "updated_at": "2024-02-15T12:10:01.400Z",
    "completed_call_duration_in_minutes": 17.0,
    "program": {
        "id": 1,
        "name": "Community Services",
        "short_name": null,
        "created_at": "2024-02-15T12:09:34.494Z",
        "updated_at": "2024-02-15T12:09:57.867Z",
        "type": "internal",
        "description": null,
        "category": null,
        "reporting_framework": "oaa",
        "label": "community_services"
    },
    "funding_source": {
        "id": 13,
        "name": "III-B",
        "status": "active",
        "created_at": "2024-02-15T12:09:57.740Z",
        "updated_at": "2024-02-15T12:09:57.740Z",
        "label": "iii_b"
    },
    "service_definition": {
        "id": 30,
        "created_at": "2024-02-15T12:09:57.872Z",
        "updated_at": "2024-02-15T12:09:57.872Z",
        "default_frequency": "weekly",
        "name": "Telephone socialization",
        "short_name": null,
        "label": "telephone_socialization",
        "status": "active"
    },
    "client": {
        "id": 2,
        "person_id": 13,
        "status": "active",
        "created_at": "2024-02-15T04:09:36.909-08:00",
        "updated_at": "2024-02-15T04:13:09.134-08:00",
        "slug": "ami-5229b359",
        "first_name": "My String",
        "preferred_name": "My String",
        "last_name": "My String",
        "email": "My String",
        "address": {
            "address_line1": "My String",
            "address_line2": null,
            "city": "My String",
            "state": "My String",
            "zip": "My String"
        }
    },
    "volunteer": {
        "id": 1,
        "person_id": 7,
        "status": "approved",
        "created_at": "2024-02-15T04:09:35.499-08:00",
        "updated_at": "2024-02-15T04:09:35.648-08:00",
        "slug": "clinton-p-eligendi-amet-consectetur",
        "first_name": "My String",
        "preferred_name": "My String",
        "last_name": "My String",
        "email": "My String"
    }
}
```

This endpoint retrieves a specific client call.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| id        | The id of the client call to retrieve    |


## Get Client Calls by Status

> GET /api/client_calls/?q[by_status]=:status

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/client_calls?q[status]=completed&per_page=1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/client_calls?q[status]=completed&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "client_calls": [
        {
            "id": 10,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-02-15T12:09:42.496Z",
            "slug": "97ea1e946a2a7ee4",
            "created_at": "2024-02-15T12:09:42.500Z",
            "updated_at": "2024-02-15T12:10:01.400Z",
            "completed_call_duration_in_minutes": 17.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-02-15T12:09:34.494Z",
                "updated_at": "2024-02-15T12:09:57.867Z",
                "type": "internal",
                "description": null,
                "category": null,
                "reporting_framework": "oaa",
                "label": "community_services"
            },
            "funding_source": {
                "id": 13,
                "name": "III-B",
                "status": "active",
                "created_at": "2024-02-15T12:09:57.740Z",
                "updated_at": "2024-02-15T12:09:57.740Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-02-15T12:09:57.872Z",
                "updated_at": "2024-02-15T12:09:57.872Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 2,
                "person_id": 13,
                "status": "active",
                "created_at": "2024-02-15T04:09:36.909-08:00",
                "updated_at": "2024-02-15T04:13:09.134-08:00",
                "slug": "ami-5229b359",
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "My String",
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "My String",
                    "state": "My String",
                    "zip": "My String"
                }
            },
            "volunteer": {
                "id": 1,
                "person_id": 7,
                "status": "approved",
                "created_at": "2024-02-15T04:09:35.499-08:00",
                "updated_at": "2024-02-15T04:09:35.648-08:00",
                "slug": "clinton-p-eligendi-amet-consectetur",
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "My String"
            }
        }
    ],
    "links": {
        "self": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "first": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "next": "http://app.monami.test/api/client_calls?page=2&per_page=1",
        "last": "http://app.monami.test/api/client_calls?page=20&per_page=1"
    },
    "meta": {
        "total_pages": 20,
        "current_page": 1
    }
}
```

This endpoint filters based on client call statuses.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter        | Description                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------- |
| by_status        | The status of a client call record. Available values for status are: `pending` and `completed`. |

## Get Client Calls by Volunteer

> GET /api/client_calls/?q[by_volunteer]=:volunteer_id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/client_calls?q[by_volunteer]=1&per_page=1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/client_calls?q[by_volunteer]=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "client_calls": [
        {
            "id": 15,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-02-15T12:09:42.605Z",
            "slug": "98a936ee81cd9b2a",
            "created_at": "2024-02-15T12:09:42.610Z",
            "updated_at": "2024-02-15T12:10:01.443Z",
            "completed_call_duration_in_minutes": 19.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-02-15T12:09:34.494Z",
                "updated_at": "2024-02-15T12:09:57.867Z",
                "type": "internal",
                "description": null,
                "category": null,
                "reporting_framework": "oaa",
                "label": "community_services"
            },
            "funding_source": {
                "id": 13,
                "name": "III-B",
                "status": "active",
                "created_at": "2024-02-15T12:09:57.740Z",
                "updated_at": "2024-02-15T12:09:57.740Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-02-15T12:09:57.872Z",
                "updated_at": "2024-02-15T12:09:57.872Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 5,
                "person_id": 22,
                "status": "active",
                "created_at": "2024-02-15T04:09:38.535-08:00",
                "updated_at": "2024-02-15T04:13:09.325-08:00",
                "slug": "ami-7df4163f",
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "My String",
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "My String",
                    "state": "My String",
                    "zip": "My String"
                }
            },
            "volunteer": {
                "id": 1,
                "person_id": 7,
                "status": "approved",
                "created_at": "2024-02-15T04:09:35.499-08:00",
                "updated_at": "2024-02-15T04:09:35.648-08:00",
                "slug": "clinton-p-eligendi-amet-consectetur",
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "My String"
            }
        }
    ],
    "links": {
        "self": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "first": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "next": "http://app.monami.test/api/client_calls?page=2&per_page=1",
        "last": "http://app.monami.test/api/client_calls?page=9&per_page=1"
    },
    "meta": {
        "total_pages": 9,
        "current_page": 1
    }
}
```

This endpoint filters based on the volunteer present on a client call.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter        | Description                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------- |
| by_volunteer     | The ID for the volunteer associated with the client call                                        |
