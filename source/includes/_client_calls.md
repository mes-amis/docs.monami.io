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
            "id": 11,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-03-12T14:17:51.196Z",
            "slug": "43e98a9667ab8be7",
            "created_at": "2024-03-12T14:17:51.219Z",
            "updated_at": "2024-03-12T14:18:59.225Z",
            "completed_call_duration_in_minutes": 10.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-03-12T14:17:24.975Z",
                "updated_at": "2024-03-12T14:18:53.381Z",
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
                "created_at": "2024-03-12T14:18:53.053Z",
                "updated_at": "2024-03-12T14:18:53.053Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-03-12T14:18:53.391Z",
                "updated_at": "2024-03-12T14:18:53.391Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 3,
                "status": "active",
                "created_at": "2024-03-12T07:17:35.597-07:00",
                "updated_at": "2024-03-12T07:19:00.470-07:00",
                "external_id": null,
                "label": "ami-2bff7b48",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "Palo Alto",
                    "state": "CA",
                    "zip": "94306"
                },
                "person": {
                    "id": 16,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1943-03-12",
                    "email": "email@monami.io",
                    "created_at": "2024-03-12T14:17:34.924Z",
                    "updated_at": "2024-03-12T14:19:00.465Z",
                    "gender": "prefer_not_to_say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ],
                    "phone_numbers": [
                        {
                            "number": "+17075511226",
                            "primary": true,
                            "label": "cell"
                        }
                    ],
                    "sites": []
                }
            },
            "volunteer": {
                "id": 1,
                "status": "approved",
                "created_at": "2024-03-12T07:17:28.069-07:00",
                "updated_at": "2024-03-12T07:17:29.032-07:00",
                "external_id": null,
                "label": "twyla-r-earum-rerum-eum",
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
                    "date_of_birth": "1930-03-12",
                    "email": "email@monami.io",
                    "created_at": "2024-03-12T14:17:27.096Z",
                    "updated_at": "2024-03-12T14:17:29.037Z",
                    "gender": "prefer_not_to_say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ],
                    "phone_numbers": [
                        {
                            "number": "+17075514082",
                            "primary": true,
                            "label": "cell"
                        }
                    ],
                    "sites": []
                }
            }
        }
    ],
    "links": {
        "self": "http://app.monami.io/api/client_calls?page=1&per_page=1",
        "first": "http://app.monami.io/api/client_calls?page=1&per_page=1",
        "next": "http://app.monami.io/api/client_calls?page=2&per_page=1",
        "last": "http://app.monami.io/api/client_calls?page=23&per_page=1"
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
    "completed_call_start_at": "2024-03-12T14:17:51.196Z",
    "slug": "43e98a9667ab8be7",
    "created_at": "2024-03-12T14:17:51.219Z",
    "updated_at": "2024-03-12T14:18:59.225Z",
    "completed_call_duration_in_minutes": 10.0,
    "program": {
        "id": 1,
        "name": "Community Services",
        "short_name": null,
        "created_at": "2024-03-12T14:17:24.975Z",
        "updated_at": "2024-03-12T14:18:53.381Z",
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
        "created_at": "2024-03-12T14:18:53.053Z",
        "updated_at": "2024-03-12T14:18:53.053Z",
        "label": "iii_b"
    },
    "service_definition": {
        "id": 30,
        "created_at": "2024-03-12T14:18:53.391Z",
        "updated_at": "2024-03-12T14:18:53.391Z",
        "default_frequency": "weekly",
        "name": "Telephone socialization",
        "short_name": null,
        "label": "telephone_socialization",
        "status": "active"
    },
    "client": {
        "id": 3,
        "status": "active",
        "created_at": "2024-03-12T07:17:35.597-07:00",
        "updated_at": "2024-03-12T07:19:00.470-07:00",
        "external_id": null,
        "label": "ami-2bff7b48",
        "custom_fields": {},
        "address": {
            "address_line1": "My String",
            "address_line2": null,
            "city": "Palo Alto",
            "state": "CA",
            "zip": "94306"
        },
        "person": {
            "id": 16,
            "first_name": "My String",
            "preferred_name": "My String",
            "middle_name": null,
            "last_name": "My String",
            "date_of_birth": "1943-03-12",
            "email": "email@monami.io",
            "created_at": "2024-03-12T14:17:34.924Z",
            "updated_at": "2024-03-12T14:19:00.465Z",
            "gender": "prefer_not_to_say",
            "primary_language": "english",
            "languages": [
                "spanish"
            ],
            "phone_numbers": [
                {
                    "number": "+17075511226",
                    "primary": true,
                    "label": "cell"
                }
            ],
            "sites": []
        }
    },
    "volunteer": {
        "id": 1,
        "status": "approved",
        "created_at": "2024-03-12T07:17:28.069-07:00",
        "updated_at": "2024-03-12T07:17:29.032-07:00",
        "external_id": null,
        "label": "twyla-r-earum-rerum-eum",
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
            "date_of_birth": "1930-03-12",
            "email": "email@monami.io",
            "created_at": "2024-03-12T14:17:27.096Z",
            "updated_at": "2024-03-12T14:17:29.037Z",
            "gender": "prefer_not_to_say",
            "primary_language": "english",
            "languages": [
                "spanish"
            ],
            "phone_numbers": [
                {
                    "number": "+17075514082",
                    "primary": true,
                    "label": "cell"
                }
            ],
            "sites": []
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
            "id": 11,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-03-12T14:17:51.196Z",
            "slug": "43e98a9667ab8be7",
            "created_at": "2024-03-12T14:17:51.219Z",
            "updated_at": "2024-03-12T14:18:59.225Z",
            "completed_call_duration_in_minutes": 10.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-03-12T14:17:24.975Z",
                "updated_at": "2024-03-12T14:18:53.381Z",
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
                "created_at": "2024-03-12T14:18:53.053Z",
                "updated_at": "2024-03-12T14:18:53.053Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-03-12T14:18:53.391Z",
                "updated_at": "2024-03-12T14:18:53.391Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 3,
                "status": "active",
                "created_at": "2024-03-12T07:17:35.597-07:00",
                "updated_at": "2024-03-12T07:19:00.470-07:00",
                "external_id": null,
                "label": "ami-2bff7b48",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "Palo Alto",
                    "state": "CA",
                    "zip": "94306"
                },
                "person": {
                    "id": 16,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1943-03-12",
                    "email": "email@monami.io",
                    "created_at": "2024-03-12T14:17:34.924Z",
                    "updated_at": "2024-03-12T14:19:00.465Z",
                    "gender": "prefer_not_to_say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ],
                    "phone_numbers": [
                        {
                            "number": "+17075511226",
                            "primary": true,
                            "label": "cell"
                        }
                    ],
                    "sites": []
                }
            },
            "volunteer": {
                "id": 1,
                "status": "approved",
                "created_at": "2024-03-12T07:17:28.069-07:00",
                "updated_at": "2024-03-12T07:17:29.032-07:00",
                "external_id": null,
                "label": "twyla-r-earum-rerum-eum",
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
                    "date_of_birth": "1930-03-12",
                    "email": "email@monami.io",
                    "created_at": "2024-03-12T14:17:27.096Z",
                    "updated_at": "2024-03-12T14:17:29.037Z",
                    "gender": "prefer_not_to_say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ],
                    "phone_numbers": [
                        {
                            "number": "+17075514082",
                            "primary": true,
                            "label": "cell"
                        }
                    ],
                    "sites": []
                }
            }
        }
    ],
    "links": {
        "self": "http://app.monami.io/api/client_calls?page=1&per_page=1",
        "first": "http://app.monami.io/api/client_calls?page=1&per_page=1",
        "next": "http://app.monami.io/api/client_calls?page=2&per_page=1",
        "last": "http://app.monami.io/api/client_calls?page=20&per_page=1"
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
            "id": 6,
            "attempt_count": 0,
            "status": "completed",
            "completed_call_start_at": "2024-03-12T14:17:50.280Z",
            "slug": "a11523f3174c8718",
            "created_at": "2024-03-12T14:17:50.299Z",
            "updated_at": "2024-03-12T14:18:59.185Z",
            "completed_call_duration_in_minutes": 7.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-03-12T14:17:24.975Z",
                "updated_at": "2024-03-12T14:18:53.381Z",
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
                "created_at": "2024-03-12T14:18:53.053Z",
                "updated_at": "2024-03-12T14:18:53.053Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-03-12T14:18:53.391Z",
                "updated_at": "2024-03-12T14:18:53.391Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 1,
                "status": "active",
                "created_at": "2024-03-12T07:17:30.034-07:00",
                "updated_at": "2024-03-12T07:19:00.671-07:00",
                "external_id": null,
                "label": "ami-5b3d9f58",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "Palo Alto",
                    "state": "CA",
                    "zip": "94306"
                },
                "person": {
                    "id": 9,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1946-03-12",
                    "email": "email@monami.io",
                    "created_at": "2024-03-12T14:17:29.266Z",
                    "updated_at": "2024-03-12T14:19:00.668Z",
                    "gender": "prefer_not_to_say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ],
                    "phone_numbers": [
                        {
                            "number": "+17075514392",
                            "primary": true,
                            "label": "cell"
                        }
                    ],
                    "sites": []
                }
            },
            "volunteer": {
                "id": 1,
                "status": "approved",
                "created_at": "2024-03-12T07:17:28.069-07:00",
                "updated_at": "2024-03-12T07:17:29.032-07:00",
                "external_id": null,
                "label": "twyla-r-earum-rerum-eum",
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
                    "date_of_birth": "1930-03-12",
                    "email": "email@monami.io",
                    "created_at": "2024-03-12T14:17:27.096Z",
                    "updated_at": "2024-03-12T14:17:29.037Z",
                    "gender": "prefer_not_to_say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ],
                    "phone_numbers": [
                        {
                            "number": "+17075514082",
                            "primary": true,
                            "label": "cell"
                        }
                    ],
                    "sites": []
                }
            }
        }
    ],
    "links": {
        "self": "http://app.monami.io/api/client_calls?page=1&per_page=1",
        "first": "http://app.monami.io/api/client_calls?page=1&per_page=1",
        "next": "http://app.monami.io/api/client_calls?page=2&per_page=1",
        "last": "http://app.monami.io/api/client_calls?page=13&per_page=1"
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

## Get Client Calls by Completed Call Start At

> GET /api/client_calls/?q[completed_call_start_at_from]=:date&q[completed_call_start_at_to]=:date

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/client_calls?q[completed_call_start_at_from]=2024-03-12&q[completed_call_start_at_to]=2024-03-13&per_page=1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/client_calls?q[completed_call_start_at_from]=2024-03-12&q[completed_call_start_at_to]=2024-03-13&per_page=1',
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
            "completed_call_start_at": "2024-03-12T14:17:51.196Z",
            "slug": "43e98a9667ab8be7",
            "created_at": "2024-03-12T14:17:51.219Z",
            "updated_at": "2024-03-12T14:18:59.225Z",
            "completed_call_duration_in_minutes": 10.0,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-03-12T14:17:24.975Z",
                "updated_at": "2024-03-12T14:18:53.381Z",
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
                "created_at": "2024-03-12T14:18:53.053Z",
                "updated_at": "2024-03-12T14:18:53.053Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 30,
                "created_at": "2024-03-12T14:18:53.391Z",
                "updated_at": "2024-03-12T14:18:53.391Z",
                "default_frequency": "weekly",
                "name": "Telephone socialization",
                "short_name": null,
                "label": "telephone_socialization",
                "status": "active"
            },
            "client": {
                "id": 3,
                "status": "active",
                "created_at": "2024-03-12T07:17:35.597-07:00",
                "updated_at": "2024-03-12T07:19:00.470-07:00",
                "external_id": null,
                "label": "ami-2bff7b48",
                "custom_fields": {},
                "address": {
                    "address_line1": "My String",
                    "address_line2": null,
                    "city": "Palo Alto",
                    "state": "CA",
                    "zip": "94306"
                },
                "person": {
                    "id": 16,
                    "first_name": "My String",
                    "preferred_name": "My String",
                    "middle_name": null,
                    "last_name": "My String",
                    "date_of_birth": "1943-03-12",
                    "email": "email@monami.io",
                    "created_at": "2024-03-12T14:17:34.924Z",
                    "updated_at": "2024-03-12T14:19:00.465Z",
                    "gender": "prefer_not_to_say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ],
                    "phone_numbers": [
                        {
                            "number": "+17075511226",
                            "primary": true,
                            "label": "cell"
                        }
                    ],
                    "sites": []
                }
            },
            "volunteer": {
                "id": 1,
                "status": "approved",
                "created_at": "2024-03-12T07:17:28.069-07:00",
                "updated_at": "2024-03-12T07:17:29.032-07:00",
                "external_id": null,
                "label": "twyla-r-earum-rerum-eum",
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
                    "date_of_birth": "1930-03-12",
                    "email": "email@monami.io",
                    "created_at": "2024-03-12T14:17:27.096Z",
                    "updated_at": "2024-03-12T14:17:29.037Z",
                    "gender": "prefer_not_to_say",
                    "primary_language": "english",
                    "languages": [
                        "spanish"
                    ],
                    "phone_numbers": [
                        {
                            "number": "+17075514082",
                            "primary": true,
                            "label": "cell"
                        }
                    ],
                    "sites": []
                }
            }
        }
    ],
    "links": {
        "self": "http://app.monami.io/api/client_calls?page=1&per_page=1",
        "first": "http://app.monami.io/api/client_calls?page=1&per_page=1",
        "next": "http://app.monami.io/api/client_calls?page=2&per_page=1",
        "last": "http://app.monami.io/api/client_calls?page=20&per_page=1"
    },
    "meta": {
        "total_pages": 20,
        "current_page": 1
    }
}
```

This endpoint filters based on the volunteer present on a client call.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter                    | Description                                                             |
| ---------------------------- | ----------------------------------------------------------------------- |
| completed_call_start_at_from | The first date a client call could be completed at in the given range   |
| completed_call_start_at_to   | The last date a client call could be completed at in the given range    |
