# Clients

## Get All Clients

This endpoint returns a paginated list of clients as well as pagination links and meta information.

> GET /api/clients

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/clients?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/clients?page=1&per_page=1',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "clients": [
    {
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
        "city": "My String",
        "state": "My String",
        "zip": "My String"
      },
      "person": {
        "id": 13,
        "first_name": "My String",
        "preferred_name": "My String",
        "middle_name": null,
        "last_name": "My String",
        "date_of_birth": "1934-02-27",
        "email": "client@monami.io",
        "created_at": "2024-02-27T15:40:42.601Z",
        "updated_at": "2024-02-27T15:45:05.848Z",
        "gender": "Prefer not to say",
        "primary_language": "english",
        "languages": [
          "spanish"
        ]
      }
    }
  ],
  "links": {
    "self": "http://app.monami.test/api/clients?page=1&per_page=1",
    "first": "http://app.monami.test/api/clients?page=1&per_page=1",
    "next": "http://app.monami.test/api/clients?page=2&per_page=1",
    "last": "http://app.monami.test/api/clients?page=24&per_page=1"
  },
  "meta": {
    "total_pages": 24,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| clients   | The collection of results.                             |
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

## Get a Specific Client

> GET /api/clients/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/clients/2
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/clients/2',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
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
    "city": "My String",
    "state": "My String",
    "zip": "My String"
  },
  "person": {
    "id": 13,
    "first_name": "My String",
    "preferred_name": "My String",
    "middle_name": null,
    "last_name": "My String",
    "date_of_birth": "1934-02-27",
    "email": "client@monami.io",
    "created_at": "2024-02-27T15:40:42.601Z",
    "updated_at": "2024-02-27T15:45:05.848Z",
    "gender": "Prefer not to say",
    "primary_language": "english",
    "languages": [
      "spanish"
    ]
  }
}
```

This endpoint retrieves a specific client.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                      |
| --------- | -------------------------------- |
| id        | The id of the client to retrieve |

## Create a Client

> POST /api/clients/

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/clients/ \
--form 'first_name="Jane"' \
--form 'preferred_name="Client"' \
--form 'last_name="Doe"' \
--form 'date_of_birth="1940-05-30"' \
--form 'email="sample@monami.io"' \
--form 'gender="female"' \
--form 'phone="+17075518391"' \
--form 'languages="english,portuguese"' \
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
form_data = [['first_name', 'Jane'],['preferred_name', 'Client'],['last_name', 'Doe'],['date_of_birth', '1940-05-30'],['email', 'sample@monami.io'],['gender', 'female'],['phone', '+17075518391'],['languages', 'english,portuguese'],['address_line1', 'X Random St'],['city', 'San Francisco'],['state', 'CA'],['zip', '94117'],['country', 'United States'],['dynamic_fields', '{"dynamic_companion_gender_identity": "custom_value", "dynamic_companion_pronouns": "custom_value2"}']]
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 26,
  "status": "active",
  "created_at": "2024-02-27T09:51:33.078-08:00",
  "updated_at": "2024-02-27T09:51:33.078-08:00",
  "external_id": null,
  "label": "ami-318cbbd8",
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
    "preferred_name": "Client",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "sample@monami.io",
    "created_at": "2024-02-27T17:51:32.984Z",
    "updated_at": "2024-02-27T17:51:33.122Z",
    "gender": "Female",
    "primary_language": null,
    "languages": null
  }
}
```

This endpoint retrieves the newly created client.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter      | Description                      |
| -------------- | -------------------------------- |
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

## Create a Client for a specific Person

> POST /api/people/:person_id/clients/

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/people/82/clients/ \
--form 'first_name="Jane"' \
--form 'preferred_name="Client"' \
--form 'last_name="Doe"' \
--form 'date_of_birth="1940-05-30"' \
--form 'email="sample@monami.io"' \
--form 'gender="female"' \
--form 'phone="+17075518391"' \
--form 'languages="english,portuguese"' \
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
url = URI("http://app.monami.test/api/people/82/clients/")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Basic #{credential}"
form_data = [['first_name', 'Jane'],['preferred_name', 'Client'],['last_name', 'Doe'],['date_of_birth', '1940-05-30'],['email', 'sample@monami.io'],['gender', 'female'],['phone', '+17075518391'],['languages', 'english,portuguese'],['address_line1', 'X Random St'],['city', 'San Francisco'],['state', 'CA'],['zip', '94117'],['country', 'United States'],['dynamic_fields', '{"dynamic_companion_gender_identity": "custom_value", "dynamic_companion_pronouns": "custom_value2"}']]
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 26,
  "status": "active",
  "created_at": "2024-02-27T09:51:33.078-08:00",
  "updated_at": "2024-02-27T09:51:33.078-08:00",
  "external_id": null,
  "label": "ami-318cbbd8",
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
    "preferred_name": "Client",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "sample@monami.io",
    "created_at": "2024-02-27T17:51:32.984Z",
    "updated_at": "2024-02-27T17:51:33.122Z",
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

