# Client Calls

## Get Client Calls

This endpoint returns a paginated list of client calls as well as pagination links and meta information.

> GET /api/client_calls

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/client_calls?page=6&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/client_calls?page=6&per_page=1',
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
            "id": 11,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-02-27T15:40:55.980Z",
            "slug": "481a1528509286d5",
            "created_at": "2024-02-27T15:40:55.994Z",
            "updated_at": "2024-02-27T15:41:21.358Z",
            "completed_call_duration_in_minutes": 25.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-02-27T15:40:36.959Z",
                "updated_at": "2024-02-27T15:41:16.780Z",
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
                "created_at": "2024-02-27T15:41:16.651Z",
                "updated_at": "2024-02-27T15:41:16.651Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-02-27T15:41:16.785Z",
                "updated_at": "2024-02-27T15:41:16.785Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 2,
                "status": "active",
                "created_at": "2024-02-27T07:40:43.088-08:00",
                "updated_at": "2024-02-27T07:45:05.875-08:00",
                "external_id": null,
                "label": "ami-f3e8ee17",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "Palo Alto",
                    "state": "CA",
                    "zip": "94306"
                },
                "person": {
                    "id": 13,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1934-02-27",
                    "email": "sample@monami.io",
                    "created_at": "2024-02-27T15:40:42.601Z",
                    "updated_at": "2024-02-27T15:45:05.848Z",
                    "gender": "Prefer not to say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ]
                }
            },
            "volunteer": {
                "id": 1,
                "status": "approved",
                "created_at": "2024-02-27T07:40:39.407-08:00",
                "updated_at": "2024-02-27T07:40:39.988-08:00",
                "external_id": null,
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "sample@monami.io",
                "label": "danielle-r-nihil-a-et",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "Palo Alto",
                    "state": "CA",
                    "zip": "94306"
                },
                "person": {
                    "id": 7,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1946-02-27",
                    "email": "sample@monami.io",
                    "created_at": "2024-02-27T15:40:38.788Z",
                    "updated_at": "2024-02-27T15:40:40.006Z",
                    "gender": "Prefer not to say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ]
                }
            }
        }
    ],
    "links": {
        "self": "http://app.monami.test/api/client_calls?page=6&per_page=1",
        "first": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "prev": "http://app.monami.test/api/client_calls?page=5&per_page=1",
        "next": "http://app.monami.test/api/client_calls?page=7&per_page=1",
        "last": "http://app.monami.test/api/client_calls?page=23&per_page=1"
    },
    "meta": {
        "total_pages": 23,
        "current_page": 6
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
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/client_calls/11
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/client_calls/11',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
            "id": 11,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-02-27T15:40:55.980Z",
            "slug": "481a1528509286d5",
            "created_at": "2024-02-27T15:40:55.994Z",
            "updated_at": "2024-02-27T15:41:21.358Z",
            "completed_call_duration_in_minutes": 25.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-02-27T15:40:36.959Z",
                "updated_at": "2024-02-27T15:41:16.780Z",
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
                "created_at": "2024-02-27T15:41:16.651Z",
                "updated_at": "2024-02-27T15:41:16.651Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-02-27T15:41:16.785Z",
                "updated_at": "2024-02-27T15:41:16.785Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 2,
                "status": "active",
                "created_at": "2024-02-27T07:40:43.088-08:00",
                "updated_at": "2024-02-27T07:45:05.875-08:00",
                "external_id": null,
                "label": "ami-f3e8ee17",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "Palo Alto",
                    "state": "CA",
                    "zip": "94306"
                },
                "person": {
                    "id": 13,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1934-02-27",
                    "email": "sample@monami.io",
                    "created_at": "2024-02-27T15:40:42.601Z",
                    "updated_at": "2024-02-27T15:45:05.848Z",
                    "gender": "Prefer not to say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ]
                }
            },
            "volunteer": {
                "id": 1,
                "status": "approved",
                "created_at": "2024-02-27T07:40:39.407-08:00",
                "updated_at": "2024-02-27T07:40:39.988-08:00",
                "external_id": null,
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "sample@monami.io",
                "label": "danielle-r-nihil-a-et",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "Palo Alto",
                    "state": "CA",
                    "zip": "94306"
                },
                "person": {
                    "id": 7,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1946-02-27",
                    "email": "sample@monami.io",
                    "created_at": "2024-02-27T15:40:38.788Z",
                    "updated_at": "2024-02-27T15:40:40.006Z",
                    "gender": "Prefer not to say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ]
                }
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
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/client_calls?q[by_status]=completed&per_page=1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/client_calls?q[by_status]=completed&per_page=1',
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
            "id": 4,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-02-27T15:40:54.928Z",
            "slug": "7939893dfb5eec24",
            "created_at": "2024-02-27T15:40:54.936Z",
            "updated_at": "2024-02-27T15:41:21.310Z",
            "completed_call_duration_in_minutes": 29.0,
            "program": null,
            "funding_source": null,
            "service_definition": null,
            "client": {
                "id": 6,
                "status": "active",
                "created_at": "2024-02-27T07:40:48.408-08:00",
                "updated_at": "2024-02-27T07:45:05.995-08:00",
                "external_id": null,
                "label": "ami-c8e79ee7",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "My String",
                    "state": "My String",
                    "zip": "My String"
                },
                "person": {
                    "id": 25,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1946-02-27",
                    "email": "client@monami.io",
                    "created_at": "2024-02-27T15:40:47.904Z",
                    "updated_at": "2024-02-27T15:45:05.983Z",
                    "gender": "Prefer not to say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ]
                }
            },
            "volunteer": {
                "id": 1,
                "status": "approved",
                "created_at": "2024-02-27T07:40:39.407-08:00",
                "updated_at": "2024-02-27T07:40:39.988-08:00",
                "external_id": null,
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "volunteer@monami.io",
                "label": "My String",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "My String",
                    "state": "My String",
                    "zip": "My String"
                },
                "person": {
                    "id": 7,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1946-02-27",
                    "email": "volunteer@monami.io",
                    "created_at": "2024-02-27T15:40:38.788Z",
                    "updated_at": "2024-02-27T15:40:40.006Z",
                    "gender": "Prefer not to say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ]
                }
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
            "id": 14,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-02-27T15:40:56.271Z",
            "slug": "739d4fec31ddb231",
            "created_at": "2024-02-27T15:40:56.289Z",
            "updated_at": "2024-02-27T15:41:21.373Z",
            "completed_call_duration_in_minutes": 8.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-02-27T15:40:36.959Z",
                "updated_at": "2024-02-27T15:41:16.780Z",
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
                "created_at": "2024-02-27T15:41:16.651Z",
                "updated_at": "2024-02-27T15:41:16.651Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-02-27T15:41:16.785Z",
                "updated_at": "2024-02-27T15:41:16.785Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 4,
                "status": "active",
                "created_at": "2024-02-27T07:40:46.042-08:00",
                "updated_at": "2024-02-27T07:45:05.912-08:00",
                "external_id": null,
                "label": "ami-06701072",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "My String",
                    "state": "My String",
                    "zip": "My String"
                },
                "person": {
                    "id": 19,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1945-02-27",
                    "email": "client@monami.io",
                    "created_at": "2024-02-27T15:40:45.482Z",
                    "updated_at": "2024-02-27T15:45:05.881Z",
                    "gender": "Prefer not to say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ]
                }
            },
            "volunteer": {
                "id": 1,
                "status": "approved",
                "created_at": "2024-02-27T07:40:39.407-08:00",
                "updated_at": "2024-02-27T07:40:39.988-08:00",
                "external_id": null,
                "first_name": "My String",
                "preferred_name": "My String",
                "last_name": "My String",
                "email": "volunteer@monami.io",
                "label": "My String",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "My String",
                    "state": "My String",
                    "zip": "My String"
                },
                "person": {
                    "id": 7,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1946-02-27",
                    "email": "volunteer@monami.io",
                    "created_at": "2024-02-27T15:40:38.788Z",
                    "updated_at": "2024-02-27T15:40:40.006Z",
                    "gender": "Prefer not to say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ]
                }
            }
        }
    ],
    "links": {
        "self": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "first": "http://app.monami.test/api/client_calls?page=1&per_page=1",
        "next": "http://app.monami.test/api/client_calls?page=2&per_page=1",
        "last": "http://app.monami.test/api/client_calls?page=13&per_page=1"
    },
    "meta": {
        "total_pages": 13,
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
