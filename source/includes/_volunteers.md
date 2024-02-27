# Volunteers

## Get All Volunteers

This endpoint returns a paginated list of volunteers as well as pagination links and meta information.

> GET /api/volunteers

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/volunteers?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/volunteers?page=1&per_page=1',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "volunteers": [
    {
      "id": 1,
      "status": "approved",
      "created_at": "2024-02-27T07:40:39.407-08:00",
      "updated_at": "2024-02-27T07:40:39.988-08:00",
      "external_id": null,
      "first_name": "My String",
      "preferred_name": "My String",
      "last_name": "My String",
      "email": "sample@monami.io",
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
  ],
  "links": {
    "self": "http://app.monami.test/api/volunteers?page=1&per_page=1",
    "first": "http://app.monami.test/api/volunteers?page=1&per_page=1",
    "next": "http://app.monami.test/api/volunteers?page=2&per_page=1",
    "last": "http://app.monami.test/api/volunteers?page=2&per_page=1"
  },
  "meta": {
    "total_pages": 2,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter  | Description                                             |
| ---------- | ------------------------------------------------------- |
| volunteers | The collection of results.                             |
| links      | Pagination links to access all the pages of the results |
| meta       | Helpful response metadata                               |

### Query Parameters

| Parameter | Default | Description                 |
| --------- | ------- | --------------------------- |
| page      | 1       | Select the page of results. |
| per_page  | 25      | How many results per page.  |

<!-- <aside class="success">
Remember — the info!
</aside> -->

## Get a Specific Volunteer

> GET /api/volunteers/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/volunteers/1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/volunteers/1',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 1,
  "status": "approved",
  "created_at": "2024-02-27T07:40:39.407-08:00",
  "updated_at": "2024-02-27T07:40:39.988-08:00",
  "external_id": null,
  "first_name": "My String",
  "preferred_name": "My String",
  "last_name": "My String",
  "email": "sample@monami.io",
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
```

This endpoint retrieves a specific volunteer.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                         |
| --------- | ----------------------------------- |
| id        | The id of the volunteer to retrieve |

## Create a Volunteer

> POST /api/volunteer/

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/volunteers/ \
--form 'first_name="Jane"' \
--form 'preferred_name="Volunteer"' \
--form 'last_name="Doe"' \
--form 'date_of_birth="1940-05-30"' \
--form 'email="sample@monami.io"' \
--form 'gender="female"' \
--form 'phone="+17075518391"' \
--form 'languages=" [\"english\", \"portuguese\"]"' \
--form 'address_line1="X Random St"' \
--form 'city="San Francisco"' \
--form 'state="CA"' \
--form 'zip="94117"' \
--form 'dynamic_fields="{\"dynamic_companion_gender_identity\": \"custom_value\", \"dynamic_companion_pronouns\": \"custom_value2\"}"'
```

```ruby
require "uri"
require "net/http"

credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')
url = URI("http://app.monami.test/api/clients/")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Basic #{credential}"
form_data = [['first_name', 'Jane'],['preferred_name', 'Volunteer'],['last_name', 'Doe'],['date_of_birth', '1940-05-30'],['email', 'sample@monami.io'],['gender', 'female'],['phone', '+17075518391'],['languages', 'english,portuguese'],['address_line1', 'X Random St'],['city', 'San Francisco'],['state', 'CA'],['zip', '94117'],['country', 'United States'],['dynamic_fields', '{"dynamic_companion_gender_identity": "custom_value", "dynamic_companion_pronouns": "custom_value2"}']]
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 3,
  "status": "applied",
  "created_at": "2024-02-27T11:00:43.619-08:00",
  "updated_at": "2024-02-27T11:00:43.619-08:00",
  "external_id": null,
  "first_name": "Jane",
  "preferred_name": "Volunteer",
  "last_name": "Doe",
  "email": "sample@monami.io",
  "label": "volunteer-d",
  "custom_fields": {
    "dynamic_companion_pronouns": "custom_value2",
    "dynamic_companion_gender_identity": "custom_value"
  },
  "address": {
    "address_line1": "X Random St",
    "address_line2": null,
    "city": "San Francisco",
    "state": "CA",
    "zip": "94117"
  },
  "person": {
    "id": 82,
    "first_name": "Jane",
    "preferred_name": "Volunteer",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "sample@monami.io",
    "created_at": "2024-02-27T17:51:32.984Z",
    "updated_at": "2024-02-27T19:00:43.654Z",
    "gender": "Female",
    "primary_language": null,
    "languages": null
  }
}
```

This endpoint retrieves the newly created volunteer.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter      | Description                      |
| -------------- | -------------------------------- |
| first_name     | Volunteer's first name      |
| preferred_name | Volunteer's preferred name  |
| last_name      | Volunteer's last name       |
| date_of_birth  | Volunteer's date eg.: `YYYY-MM-DD` |
| email          | Volunteer's email address          |
| gender         | Volunteer's gender. Options are: `female`, `male`, `trans_female`, `trans_male`, `non_binary`, `trans_non_binary`, `gender_queer`, `two_spirit`, `questioning_not_sure`, `not_listed`, `prefer_not_to_say` |
| address_line1  | Volunteer's address |
| city           | Volunteer's City |
| state          | Volunteers State 2 letter abbreviation eg.: `CA` |
| zip            | 5 digits zip code |
| languages      | Comma separated list of Language Object type labels |
| dynamic_fields | JSON formatted custom fields |

## Create a Volunteer for a specific Person

> POST /api/people/:person_id/volunteers/

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/people/82/volunteers/ \
--form 'first_name="Jane"' \
--form 'preferred_name="Volunteer"' \
--form 'last_name="Doe"' \
--form 'date_of_birth="1940-05-30"' \
--form 'email="sample@monami.io"' \
--form 'gender="female"' \
--form 'phone="+17075518391"' \
--form 'languages=" [\"english\", \"portuguese\"]"' \
--form 'address_line1="X Random St"' \
--form 'city="San Francisco"' \
--form 'state="CA"' \
--form 'zip="94117"' \
--form 'dynamic_fields="{\"dynamic_companion_gender_identity\": \"custom_value\", \"dynamic_companion_pronouns\": \"custom_value2\"}"'
```

```ruby
require "uri"
require "net/http"

credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')
url = URI("http://app.monami.test/api/people/82/volunteers/")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Basic #{credential}"
form_data = [['first_name', 'Jane'],['preferred_name', 'Volunteer'],['last_name', 'Doe'],['date_of_birth', '1940-05-30'],['email', 'sample@monami.io'],['gender', 'female'],['phone', '+17075518391'],['languages', 'english,portuguese'],['address_line1', 'X Random St'],['city', 'San Francisco'],['state', 'CA'],['zip', '94117'],['country', 'United States'],['dynamic_fields', '{"dynamic_companion_gender_identity": "custom_value", "dynamic_companion_pronouns": "custom_value2"}']]
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 3,
  "status": "applied",
  "created_at": "2024-02-27T11:00:43.619-08:00",
  "updated_at": "2024-02-27T11:00:43.619-08:00",
  "external_id": null,
  "first_name": "Jane",
  "preferred_name": "Volunteer",
  "last_name": "Doe",
  "email": "sample@monami.io",
  "label": "volunteer-d",
  "custom_fields": {
    "dynamic_companion_pronouns": "custom_value2",
    "dynamic_companion_gender_identity": "custom_value"
  },
  "address": {
    "address_line1": "X Random St",
    "address_line2": null,
    "city": "San Francisco",
    "state": "CA",
    "zip": "94117"
  },
  "person": {
    "id": 82,
    "first_name": "Jane",
    "preferred_name": "Volunteer",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "sample@monami.io",
    "created_at": "2024-02-27T17:51:32.984Z",
    "updated_at": "2024-02-27T19:00:43.654Z",
    "gender": "Female",
    "primary_language": null,
    "languages": null
  }
}
```

This endpoint retrieves a specific client.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter      | Description                      |
| -------------- | -------------------------------- |
| id             | The id of the client to retrieve |
| first_name     | Client's first name      |
| preferred_name | Client's preferred name  |
| last_name      | Client's last name       |
| date_of_birth  | Client's date eg.: `YYYY-MM-DD` |
| email          | Client's email address          |
| gender         | Client's gender. Options are: `female`, `male`, `trans_female`, `trans_male`, `non_binary`, `trans_non_binary`, `gender_queer`, `two_spirit`, `questioning_not_sure`, `not_listed`, `prefer_not_to_say` |
| address_line1  | Client's address |
| city           | Client's City |
| state          | Clients State 2 letter abbreviation eg.: `CA` |
| zip            | 5 digits zip code |
| languages      | Comma separated list of Language Object type labels |
| dynamic_fields | JSON formatted custom fields |

