# Visits

## Get All visits

This endpoint returns a paginated list of visits as well as pagination links and meta information.

> GET /api/visits

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/visits?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/visits?page=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "visits": [
        {
            "id": 157,
            "status": "tentative",
            "visit_type": "service",
            "schedule_type": "fixed",
            "scheduled_duration": 120,
            "scheduled_start_at": "2024-02-15T17:15:00.000-08:00",
            "created_at": "2024-02-13T11:06:11.059-08:00",
            "updated_at": "2024-02-13T11:09:17.922-08:00",
            "start_at": "2024-02-15T17:15:00.000-08:00",
            "completed_at": "2024-02-15T19:15:00.000-08:00",
            "duration": 120,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-02-13T19:05:55.578Z",
                "updated_at": "2024-02-13T19:06:38.201Z",
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
                "created_at": "2024-02-13T19:06:38.081Z",
                "updated_at": "2024-02-13T19:06:38.081Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 32,
                "created_at": "2024-02-13T19:06:38.213Z",
                "updated_at": "2024-02-13T19:06:38.213Z",
                "default_frequency": "weekly",
                "name": "Personal Care",
                "short_name": null,
                "label": "personal_care_2",
                "status": "active"
            },
            "client": {
                "id": 2,
                "person_id": 15,
                "status": "active",
                "created_at": "2024-02-13T11:05:58.520-08:00",
                "updated_at": "2024-02-13T11:09:17.324-08:00",
                "slug": "ami-1193ec7f",
                "first_name": "Alden",
                "preferred_name": "Retta",
                "last_name": "Connelly",
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
                "id": 2,
                "person_id": 11,
                "status": "approved",
                "created_at": "2024-02-13T11:05:58.029-08:00",
                "updated_at": "2024-02-13T11:05:58.140-08:00",
                "slug": "kendal-g-et-culpa-doloremque",
                "first_name": "Hosea",
                "preferred_name": "Kendal",
                "last_name": "Goyette",
                "email": "My String"
            },
            "visit_coding": null
        }
    ],
    "links": {
        "self": "http://app.monami.test/api/visits?page=1&per_page=1",
        "first": "http://app.monami.test/api/visits?page=1&per_page=1",
        "next": "http://app.monami.test/api/visits?page=2&per_page=1",
        "last": "http://app.monami.test/api/visits?page=240&per_page=1"
    },
    "meta": {
        "total_pages": 240,
        "current_page": 1
    }
}
```

### Response Parameters

| Parameter         | Description                                             |
| ----------------- | ------------------------------------------------------- |
| visits            | The collection of results.                              |
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

## Get a Specific Visit

> GET /api/visits/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/visits/157
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/visits/1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "id": 157,
    "status": "tentative",
    "visit_type": "service",
    "schedule_type": "fixed",
    "scheduled_duration": 120,
    "scheduled_start_at": "2024-02-15T17:15:00.000-08:00",
    "created_at": "2024-02-13T11:06:11.059-08:00",
    "updated_at": "2024-02-13T11:09:17.922-08:00",
    "start_at": "2024-02-15T17:15:00.000-08:00",
    "completed_at": "2024-02-15T19:15:00.000-08:00",
    "duration": 120,
    "program": {
        "id": 1,
        "name": "Community Services",
        "short_name": null,
        "created_at": "2024-02-13T19:05:55.578Z",
        "updated_at": "2024-02-13T19:06:38.201Z",
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
        "created_at": "2024-02-13T19:06:38.081Z",
        "updated_at": "2024-02-13T19:06:38.081Z",
        "label": "iii_b"
    },
    "service_definition": {
        "id": 32,
        "created_at": "2024-02-13T19:06:38.213Z",
        "updated_at": "2024-02-13T19:06:38.213Z",
        "default_frequency": "weekly",
        "name": "Personal Care",
        "short_name": null,
        "label": "personal_care_2",
        "status": "active"
    },
    "client": {
        "id": 2,
        "person_id": 15,
        "status": "active",
        "created_at": "2024-02-13T11:05:58.520-08:00",
        "updated_at": "2024-02-13T11:09:17.324-08:00",
        "slug": "ami-1193ec7f",
        "first_name": "Alden",
        "preferred_name": "Retta",
        "last_name": "Connelly",
        "email": "aurelio+tennie@monami.io",
        "address": {
            "address_line1": "My String",
            "address_line2": null,
            "city": "My String",
            "state": "My String",
            "zip": "My String"
        }
    },
    "volunteer": {
        "id": 2,
        "person_id": 11,
        "status": "approved",
        "created_at": "2024-02-13T11:05:58.029-08:00",
        "updated_at": "2024-02-13T11:05:58.140-08:00",
        "slug": "kendal-g-et-culpa-doloremque",
        "first_name": "Hosea",
        "preferred_name": "Kendal",
        "last_name": "Goyette",
        "email": "My String"
    },
    "visit_coding": null
}

```

This endpoint retrieves a specific visit.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| id        | The id of the visit to retrieve          |


## Get Visits by Start At Date

> GET /api/visits/?q[start_at_from]=:start_at_from&q[start_at_to]=:start_at_to

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/visits?q[start_at_from]=8/05/2014&q[start_at_to]=8/05/2023
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/visits?q[start_at_from]=2/15/2024&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "visits": [
        {
            "id": 26,
            "status": "tentative",
            "visit_type": "service",
            "schedule_type": "fixed",
            "scheduled_duration": 120,
            "scheduled_start_at": "2024-02-17T17:15:00.000-08:00",
            "created_at": "2024-02-13T11:06:07.285-08:00",
            "updated_at": "2024-02-13T11:09:18.265-08:00",
            "start_at": "2024-02-17T17:15:00.000-08:00",
            "completed_at": "2024-02-17T19:15:00.000-08:00",
            "duration": 120,
            "program": {
                "id": 1,
                "name": "Community Services",
                "short_name": null,
                "created_at": "2024-02-13T19:05:55.578Z",
                "updated_at": "2024-02-13T19:06:38.201Z",
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
                "created_at": "2024-02-13T19:06:38.081Z",
                "updated_at": "2024-02-13T19:06:38.081Z",
                "label": "iii_b"
            },
            "service_definition": {
                "id": 32,
                "created_at": "2024-02-13T19:06:38.213Z",
                "updated_at": "2024-02-13T19:06:38.213Z",
                "default_frequency": "weekly",
                "name": "Personal Care",
                "short_name": null,
                "label": "personal_care_2",
                "status": "active"
            },
            "client": {
                "id": 4,
                "person_id": 21,
                "status": "active",
                "created_at": "2024-02-13T11:05:59.483-08:00",
                "updated_at": "2024-02-13T11:09:17.385-08:00",
                "slug": "ami-def6e24a",
                "first_name": "James",
                "preferred_name": "Hong",
                "last_name": "Huels",
                "email": "My String",
                "address": {
                    "address_line1": "My String",
                    "address_line2": "My String",
                    "city": "My String",
                    "state": "My String",
                    "zip": "My String"
                }
            },
            "volunteer": {
                "id": 1,
                "person_id": 9,
                "status": "approved",
                "created_at": "2024-02-13T11:05:57.062-08:00",
                "updated_at": "2024-02-13T11:05:57.235-08:00",
                "slug": "naida-b-culpa-repudiandae-autem",
                "first_name": "Verlene",
                "preferred_name": "Naida",
                "last_name": "Boyle",
                "email": "My String"
            },
            "visit_coding": null
        }
    ],
    "links": {
        "self": "http://app.monami.test/api/visits?page=1&per_page=1",
        "first": "http://app.monami.test/api/visits?page=1&per_page=1",
        "next": "http://app.monami.test/api/visits?page=2&per_page=1",
        "last": "http://app.monami.test/api/visits?page=144&per_page=1"
    },
    "meta": {
        "total_pages": 144,
        "current_page": 1
    }
}
```

This endpoint filters based on visit start date.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter        | Description                                                              |
| ---------------- | ------------------------------------------------------------------------ |
| start_at_from    | The first date a visit could happen on in the given range                |
| start_at_to      | The last date a visit could happen on in the given range                 |
