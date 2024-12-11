# Visits

## List Visits

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
      "id": 126,
      "status": "completed",
      "visit_type": "service",
      "schedule_type": "fixed",
      "scheduled_duration": 210,
      "scheduled_start_at": "2024-03-10T15:00:00.000-07:00",
      "created_at": "2024-03-12T07:18:35.882-07:00",
      "updated_at": "2024-03-12T07:20:35.498-07:00",
      "start_at": "2024-03-10T15:00:00.000-07:00",
      "completed_at": "2024-03-10T18:30:00.000-07:00",
      "duration": 210,
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
        "id": 32,
        "created_at": "2024-03-12T14:18:53.409Z",
        "updated_at": "2024-03-12T14:18:53.409Z",
        "default_frequency": "weekly",
        "name": "Personal Care",
        "short_name": null,
        "label": "personal_care_2",
        "status": "active"
      },
      "client": {
        "id": 2,
        "status": "active",
        "created_at": "2024-03-12T07:17:34.014-07:00",
        "updated_at": "2024-03-12T07:19:00.423-07:00",
        "external_id": null,
        "label": "ami-3f472c50",
        "custom_fields": {},
        "address": {
          "address_line1": "My String",
          "address_line2": null,
          "city": "Palo Alto",
          "state": "CA",
          "zip": "94301"
        },
        "person": {
          "id": 13,
          "first_name": "My String",
          "preferred_name": "My String",
          "middle_name": null,
          "last_name": "My String",
          "date_of_birth": "1930-03-12",
          "email": "email@monami.io",
          "created_at": "2024-03-12T14:17:33.331Z",
          "updated_at": "2024-03-12T14:19:00.410Z",
          "gender": "prefer_not_to_say",
          "primary_language": "english",
          "languages": ["spanish"],
          "phone_numbers": [
            {
              "number": "+17075511731",
              "primary": true,
              "label": "cell"
            }
          ]
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
          "languages": ["spanish"],
          "phone_numbers": [
            {
              "number": "+17075514082",
              "primary": true,
              "label": "cell"
            }
          ]
        }
      },
      "visit_coding": null
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/visits?page=1&per_page=1",
    "first": "http://app.monami.io/api/visits?page=1&per_page=1",
    "next": "http://app.monami.io/api/visits?page=2&per_page=1",
    "last": "http://app.monami.io/api/visits?page=240&per_page=1"
  },
  "meta": {
    "total_pages": 240,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| visits    | The collection of results.                              |
| links     | Pagination links to access all the pages of the results |
| meta      | Helpful response metadata                               |

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
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/visits/126
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/visits/126',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 126,
  "status": "completed",
  "visit_type": "service",
  "schedule_type": "fixed",
  "scheduled_duration": 210,
  "scheduled_start_at": "2024-03-10T15:00:00.000-07:00",
  "created_at": "2024-03-12T07:18:35.882-07:00",
  "updated_at": "2024-03-12T07:20:35.498-07:00",
  "start_at": "2024-03-10T15:00:00.000-07:00",
  "completed_at": "2024-03-10T18:30:00.000-07:00",
  "duration": 210,
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
    "id": 32,
    "created_at": "2024-03-12T14:18:53.409Z",
    "updated_at": "2024-03-12T14:18:53.409Z",
    "default_frequency": "weekly",
    "name": "Personal Care",
    "short_name": null,
    "label": "personal_care_2",
    "status": "active"
  },
  "client": {
    "id": 2,
    "status": "active",
    "created_at": "2024-03-12T07:17:34.014-07:00",
    "updated_at": "2024-03-12T07:19:00.423-07:00",
    "external_id": null,
    "label": "ami-3f472c50",
    "custom_fields": {},
    "address": {
      "address_line1": "My String",
      "address_line2": null,
      "city": "Palo Alto",
      "state": "CA",
      "zip": "94301"
    },
    "person": {
      "id": 13,
      "first_name": "My String",
      "preferred_name": "My String",
      "middle_name": null,
      "last_name": "My String",
      "date_of_birth": "1930-03-12",
      "email": "email@monami.io",
      "created_at": "2024-03-12T14:17:33.331Z",
      "updated_at": "2024-03-12T14:19:00.410Z",
      "gender": "prefer_not_to_say",
      "primary_language": "english",
      "languages": ["spanish"],
      "phone_numbers": [
        {
          "number": "+17075511731",
          "primary": true,
          "label": "cell"
        }
      ]
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
      "languages": ["spanish"],
      "phone_numbers": [
        {
          "number": "+17075514082",
          "primary": true,
          "label": "cell"
        }
      ]
    }
  },
  "visit_coding": null
}
```

This endpoint retrieves a specific visit.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The id of the visit to retrieve |

## Get Visits by Start At Date

> GET /api/visits/?q[start_at_from]=:start_at_from&q[start_at_to]=:start_at_to

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/visits?q[start_at_from]=2024-03-10&q[start_at_to]=2024-03-11&per_page=1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/visits?q[start_at_from]=2024-03-10&q[start_at_to]=2024-03-11&per_page=1',
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
      "id": 6,
      "status": "completed",
      "visit_type": "service",
      "schedule_type": "fixed",
      "scheduled_duration": 210,
      "scheduled_start_at": "2024-03-10T15:00:00.000-07:00",
      "created_at": "2024-03-12T07:18:07.987-07:00",
      "updated_at": "2024-03-12T07:20:34.273-07:00",
      "start_at": "2024-03-10T15:00:00.000-07:00",
      "completed_at": "2024-03-10T18:30:00.000-07:00",
      "duration": 210,
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
        "id": 32,
        "created_at": "2024-03-12T14:18:53.409Z",
        "updated_at": "2024-03-12T14:18:53.409Z",
        "default_frequency": "weekly",
        "name": "Personal Care",
        "short_name": null,
        "label": "personal_care_2",
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
          "languages": ["spanish"],
          "phone_numbers": [
            {
              "number": "+17075514392",
              "primary": true,
              "label": "cell"
            }
          ]
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
          "languages": ["spanish"],
          "phone_numbers": [
            {
              "number": "+17075514082",
              "primary": true,
              "label": "cell"
            }
          ]
        }
      },
      "visit_coding": null
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/visits?page=1&per_page=1",
    "first": "http://app.monami.io/api/visits?page=1&per_page=1",
    "next": "http://app.monami.io/api/visits?page=2&per_page=1",
    "last": "http://app.monami.io/api/visits?page=20&per_page=1"
  },
  "meta": {
    "total_pages": 20,
    "current_page": 1
  }
}
```

This endpoint filters based on visit start date.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter     | Description                                               |
| ------------- | --------------------------------------------------------- |
| start_at_from | The first date a visit could happen on in the given range |
| start_at_to   | The last date a visit could happen on in the given range  |
