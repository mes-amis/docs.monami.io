# People

## Get People

This endpoint returns a paginated list of people as well as pagination links and meta information.

> GET /api/people

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/people?page=2&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/people?page=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "people": [
        {
            "id": 6,
            "first_name": "Karma",
            "preferred_name": null,
            "middle_name": null,
            "last_name": "Marty",
            "date_of_birth": null,
            "email": "My String",
            "created_at": "2024-01-25T15:56:29.766Z",
            "updated_at": "2024-01-25T15:56:29.766Z",
            "gender": "Female",
            "phone_numbers": [
              {
                "number": "+15044791643",
                "primary": true,
                "label": "home"
              }
            ],
            "primary_language": "english",
            "languages": ["spanish"]
        }
    ],
    "links": {
        "self": "http://app.monami.io/api/people?page=2&per_page=1",
        "first": "http://app.monami.io/api/people?page=1&per_page=1",
        "prev": "http://app.monami.io/api/people?page=1&per_page=1",
        "last": "http://app.monami.io/api/people?page=2&per_page=1"
    },
    "meta": {
        "total_pages": 2,
        "current_page": 2
    }
}
```

### Response Parameters

| Parameter         | Description                                             |
| ----------------- | ------------------------------------------------------- |
| people            | The collection of results.                              |
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

## Get a Specific Person

> GET /api/people/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/people/6
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/people/6',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "id": 6,
    "first_name": "Karma",
    "preferred_name": null,
    "middle_name": null,
    "last_name": "Marty",
    "date_of_birth": null,
    "email": "My String",
    "created_at": "2024-01-25T15:56:29.766Z",
    "updated_at": "2024-02-16T20:33:51.338Z",
    "gender": "Female",
    "phone_numbers": [
      {
        "number": "+15044791643",
        "primary": true,
        "label": "home"
      },
    ],
    "primary_language": "english",
    "languages": ["spanish"]
}
```

This endpoint retrieves a specific person.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| id        | The id of the person to retrieve         |


## Get People by email

> GET /api/people/?q[by_email]=:email

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/people?q[by_email]=some@email.com&per_page=1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/people?q[by_email]=some@email.com&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "people": [
        {
            "id": 6,
            "first_name": "Karma",
            "preferred_name": null,
            "middle_name": null,
            "last_name": "Marty",
            "date_of_birth": null,
            "email": "some@email.com",
            "created_at": "2024-01-25T15:56:29.766Z",
            "updated_at": "2024-02-16T20:33:51.338Z",
            "gender": "Female",
            "phone_numbers": [
              {
                "number": "+15044791643",
                "primary": true,
                "label": "home"
              },
            ],
            "primary_language": "english",
            "languages": ["spanish"]
        }
    ],
    "links": {
        "self": "http://app.monami.io/api/people?page=1",
        "first": "http://app.monami.io/api/people?page=1",
        "last": "http://app.monami.io/api/people?page=1"
    },
    "meta": {
        "total_pages": 1,
        "current_page": 1
    }
}
```

This endpoint filters based on the person's email.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter        | Description                                                                                     |
| ---------------- | ------------------------------------- |
| by_email         | The email address of a person record. |

## Get Person by Volunteer

> GET /api/people/?q[by_volunteer]=:volunteer_id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/people?q[by_volunteer]=1&per_page=1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/people?q[by_volunteer]=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "people": [
        {
            "id": 9,
            "first_name": "Lenny",
            "preferred_name": "Herma",
            "middle_name": null,
            "last_name": "Mann",
            "date_of_birth": "1941-01-25",
            "email": "My String",
            "created_at": "2024-01-25T15:56:30.555Z",
            "updated_at": "2024-01-25T15:56:30.959Z",
            "gender": "Prefer not to say",
            "phone_numbers": [
              {
                "number": "+15044791643",
                "primary": true,
                "label": "home"
              },
            ],
            "primary_language": "english",
            "languages": ["german"]
        }
    ],
    "links": {
        "self": "http://app.monami.io/api/people?page=1",
        "first": "http://app.monami.io/api/people?page=1",
        "last": "http://app.monami.io/api/people?page=1"
    },
    "meta": {
        "total_pages": 1,
        "current_page": 1
    }
}
```

This endpoint returns the Person record for a given Volunteer.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter        | Description                                          |
| ---------------- | ---------------------------------------------------- |
| by_volunteer     | The ID for the volunteer associated with the person  |

## Get Person by Client

> GET /api/people/?q[by_client]=:client_id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/people?q[by_client]=10
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/people?q[by_client]=10',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "people": [
        {
            "id": 9,
            "first_name": "Lenny",
            "preferred_name": "Herma",
            "middle_name": null,
            "last_name": "Mann",
            "date_of_birth": "1941-01-25",
            "email": "My String",
            "created_at": "2024-01-25T15:56:30.555Z",
            "updated_at": "2024-01-25T15:56:30.959Z",
            "gender": "Prefer not to say",
            "phone_numbers": [
              {
                "number": "+15044791643",
                "primary": true,
                "label": "home"
              },
            ],
            "primary_language": "english",
            "languages": ["german"]
        }
    ],
    "links": {
        "self": "http://app.monami.io/api/people?page=1",
        "first": "http://app.monami.io/api/people?page=1",
        "last": "http://app.monami.io/api/people?page=1"
    },
    "meta": {
        "total_pages": 1,
        "current_page": 1
    }
}
```

This endpoint returns the Person record for a given Client.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter        | Description                                          |
| ---------------- | ---------------------------------------------------- |
| by_client        | The ID for the client associated with the person     |
