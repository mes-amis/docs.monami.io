# Clients

## List Clients

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

> A successful request returns JSON structured like this:

```json
{
  "clients": [
    {
      "id": 12,
      "status": "pending",
      "created_at": "2024-03-12T07:19:02.114-07:00",
      "updated_at": "2024-03-12T07:19:02.122-07:00",
      "external_id": null,
      "label": "ami-9776d470",
      "custom_fields": {},
      "address": {
        "address_line1": "My String",
        "address_line2": null,
        "city": "San Mateo",
        "state": "CA",
        "zip": "94402"
      },
      "person": {
        "id": 54,
        "first_name": "My String",
        "preferred_name": null,
        "middle_name": null,
        "last_name": "My String",
        "date_of_birth": "1959-03-12",
        "email": "email@monami.io",
        "created_at": "2024-03-12T14:19:02.091Z",
        "updated_at": "2024-03-12T14:19:02.115Z",
        "gender": "prefer_not_to_say",
        "primary_language": "english",
        "languages": null,
        "phone_numbers": [
          {
            "number": "+15044791643",
            "primary": true,
            "label": "home"
          }
        ],
        "sites": []
      }
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/clients?page=1&per_page=1",
    "first": "http://app.monami.io/api/clients?page=1&per_page=1",
    "next": "http://app.monami.io/api/clients?page=2&per_page=1",
    "last": "http://app.monami.io/api/clients?page=21&per_page=1"
  },
  "meta": {
    "total_pages": 21,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| clients   | The collection of results.                              |
| links     | Pagination links to access all the pages of the results |
| meta      | Helpful response metadata                               |

### Query Parameters

| Parameter      | Default | Description                                                    |
|----------------|---------|----------------------------------------------------------------|
| page           | 1       | Select the page of results.                                    |
| per_page       | 25      | How many results per page.                                     |
| first_name     |      | Filters by the user's first name                               |
| last_name      |      | Filters by the user's last name                                |
| phone_number   |      | Filters by any of the user's phone numbers, e.g. `+15044791643` |
| date_of_birth  |      | Filters by the user's date of birth. Format: `YYYY-MM-DD`      |
| address_county |      | Filters by the user's county                                   |
| social_security_number_last_4 |      | Filters by the last 4 digits of the user's SSN                 |
| status |      | Filters by the user's status                                   |

<!-- <aside class="success">
Remember — the info!
</aside> -->

## Get a Specific Client

> GET /api/clients/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/clients/12
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/clients/12',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A successful request returns JSON structured like this:

```json
{
  "id": 12,
  "status": "pending",
  "created_at": "2024-03-12T07:19:02.114-07:00",
  "updated_at": "2024-03-12T07:19:02.122-07:00",
  "external_id": null,
  "label": "ami-9776d470",
  "custom_fields": {},
  "address": {
    "address_line1": "My String",
    "address_line2": null,
    "city": "San Mateo",
    "state": "CA",
    "zip": "94402"
  },
  "person": {
    "id": 54,
    "first_name": "My String",
    "preferred_name": null,
    "middle_name": null,
    "last_name": "My String",
    "date_of_birth": "1959-03-12",
    "email": "email@monami.io",
    "created_at": "2024-03-12T14:19:02.091Z",
    "updated_at": "2024-03-12T14:19:02.115Z",
    "gender": "prefer_not_to_say",
    "primary_language": "english",
    "languages": null,
    "phone_numbers": [
      {
        "number": "+15044791643",
        "primary": true,
        "label": "home"
      }
    ],
    "sites": []
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
--form 'person="{\"first_name\": \"John\",\"preferred_name\": \"Client\",\"last_name\": \"Doe\",\"date_of_birth\": \"1940-05-30\",\"email\": \"test@monami.io\",\"gender\": \"female\",\"phone_numbers\": [{\"number\": \"+17075518391\", \"primary\": true}],\"languages\": \"english,portuguese\"}"' \
--form 'address="{\"address_line1\": \"X Random St\", \"city\": \"San Francisco\", \"state\": \"CA\", \"zip\": \"94117\"}"' \
--form 'custom_fields="{\"gender_identity\": \"custom_value\", \"pronouns\": \"custom_value2\"}"'
```

```ruby
require "uri"
require "net/http"

credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')
url = URI("http://app.monami.io/api/clients/")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Basic #{credential}"
form_data = [['person', '{"first_name": "Jane","preferred_name": "Client","last_name": "Doe","date_of_birth": "1940-05-30","test": "test@monami.io","gender": "female","phone_numbers": [{"primary": "+17075518391"}],"languages": "english,portuguese"}'],['address', '{"address_line1": "X Random St", "city": "San Francisco", "state": "CA", "zip": "94117"}'],['custom_fields', '{"gender_identity": "custom_value", "pronouns": "custom_value2"}']]
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A successful request returns JSON structured like this:

```json
{
  "id": 22,
  "status": "active",
  "created_at": "2024-03-13T09:04:33.346-07:00",
  "updated_at": "2024-03-13T09:04:33.346-07:00",
  "external_id": null,
  "label": "ami-c090e55c",
  "custom_fields": {
    "pronouns": "custom_value2",
    "gender_identity": "custom_value"
  },
  "address": {
    "address_line1": "X Random St",
    "address_line2": null,
    "city": "San Francisco",
    "state": "CA",
    "zip": "94117"
  },
  "person": {
    "id": 78,
    "first_name": "Jane",
    "preferred_name": "Client",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "test@monami.io",
    "created_at": "2024-03-13T16:04:33.256Z",
    "updated_at": "2024-03-13T16:04:33.399Z",
    "gender": "female",
    "primary_language": null,
    "languages": ["english", "portuguese"],
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "home"
      }
    ],
    "sites": []
  }
}
```

This endpoint returns the newly created client.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter     | Description                       |
| ------------- | --------------------------------- |
| person        | JSON formatted person parameters  |
| address       | JSON formatted address parameters |
| custom_fields | JSON formatted custom fields      |

#### Person Parameters

| Parameter      | Description                                                                                                                                                                                             |
| -------------- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| first_name     | Client's first name                                                                                                                                                                                     |
| preferred_name | Client's preferred name                                                                                                                                                                                 |
| last_name      | Client's last name                                                                                                                                                                                      |
| date_of_birth  | Client's birthdate, e.g. `YYYY-MM-DD`                                                                                                                                                                   |
| email          | Client's email address                                                                                                                                                                                  |
| gender         | Client's gender. Options are: `female`, `male`, `trans_female`, `trans_male`, `non_binary`, `trans_non_binary`, `gender_queer`, `two_spirit`, `questioning_not_sure`, `not_listed`, `prefer_not_to_say` |
| languages      | Array of Language Object type labels                                                                                                                                                                    |
| phone_numbers  | Array of Phone Number parameters                                                                                                                                                                        |

#### Phone Number Parameters

| Parameter | Description                                                                                    |
|-----------|------------------------------------------------------------------------------------------------|
| number    | Phone number including area code, e.g. '+17075518391'                                          |
| primary   | Whether or not phone is primary. Only one primary phone per person. Options: `true` or `false` |
| label     | Type of phone number. Options: `cell`, `home` or `work`                                        |

#### Address Parameters

| Parameter     | Description                                   |
| ------------- | --------------------------------------------- |
| address_line1 | Client's address                              |
| city          | Client's City                                 |
| state         | Clients State 2 letter abbreviation eg.: `CA` |
| zip           | 5 digits zip code                             |

## Create a Client for a specific Person

> POST /api/people/:person_id/clients/

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/people/78/clients/ \
--form 'custom_fields="{\"gender_identity\": \"custom_value\", \"pronouns\": \"custom_value2\"}"'
```

```ruby
require "uri"
require "net/http"

credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')
url = URI("http://app.monami.io/api/people/82/clients/")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Basic #{credential}"
form_data = [['custom_fields', '{"gender_identity": "custom_value", "pronouns": "custom_value2"}']]
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A successful request returns JSON structured like this:

```json
{
  "id": 22,
  "status": "active",
  "created_at": "2024-03-13T09:04:33.346-07:00",
  "updated_at": "2024-03-13T09:04:33.346-07:00",
  "external_id": null,
  "label": "ami-c090e55c",
  "custom_fields": {
    "pronouns": "custom_value2",
    "gender_identity": "custom_value"
  },
  "person": {
    "id": 78,
    "first_name": "Jane",
    "preferred_name": "Client",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "test@monami.io",
    "created_at": "2024-03-13T16:04:33.256Z",
    "updated_at": "2024-03-13T16:04:33.399Z",
    "gender": "female",
    "primary_language": null,
    "languages": ["english", "portuguese"],
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "home"
      }
    ],
    "sites": []
  }
}
```

This endpoint creates a client for a specific person.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter     | Description                       |
| ------------- | --------------------------------- |
| person_id     | Integer ID present in the URL     |
| address       | JSON formatted address parameters |
| custom_fields | JSON formatted custom fields      |

## Update a Client

> PATCH /api/clients/:client_id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET \
-X PATCH https://app.monami.io/api/clients/22 \
-d '{ "person": { "email": "new_email@monami.io" } }' \
-H 'Content-Type: application/json'
```

```ruby
credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

response = Excon.put('https://app.monami.io/api/clients/22',
  headers: {
    'Content-Type' => 'application/json',
    'Authorization' => "Basic #{credential}"
  },
  body: {
    person: { email: 'new_email@monami.io' },
    address: { address_line2: 'Apt 2B' }
  }.to_json
)
```

> A successful request returns JSON structured like this:

```json
{
  "id": 22,
  "status": "active",
  "created_at": "2024-03-13T09:04:33.346-07:00",
  "updated_at": "2024-03-13T09:04:33.346-07:00",
  "external_id": null,
  "label": "ami-c090e55c",
  "custom_fields": {
    "pronouns": "custom_value2",
    "gender_identity": "custom_value"
  },
  "address": {
    "address_line1": "X Random St",
    "address_line2": "Apt 2B",
    "city": "San Francisco",
    "state": "CA",
    "zip": "94117"
  },
  "person": {
    "id": 78,
    "first_name": "Jane",
    "preferred_name": "Client",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "new_email@monami.io",
    "created_at": "2024-03-13T16:04:33.256Z",
    "updated_at": "2024-03-13T16:04:33.399Z",
    "gender": "female",
    "primary_language": null,
    "languages": ["english", "portuguese"],
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "home"
      }
    ],
    "sites": []
  }
}
```
This endpoint returns the updated client.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter     | Description                       |
| ------------- | --------------------------------- |
| person        | JSON formatted person parameters  |
| address       | JSON formatted address parameters |
| custom_fields | JSON formatted custom fields      |

#### Person Parameters

| Parameter      | Description                                                                                                                                                                                            |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| first_name     | Client's first name                                                                                                                                                                                    |
| preferred_name | Client's preferred name                                                                                                                                                                                |
| last_name      | Client's last name                                                                                                                                                                                     |
| date_of_birth  | Client's birthdate eg.: `YYYY-MM-DD`                                                                                                                                                                   |
| email          | Client's email address                                                                                                                                                                                 |
| gender         | Client's gender. Options are: `female`, `male`, `trans_female`, `trans_male`, `non_binary`, `trans_non_binary`, `gender_queer`, `two_spirit`, `questioning_not_sure`, `not_listed`, `prefer_not_to_say` |
| languages      | Array of Language Object type labels                                                                                                                                                                   |
| phone_numbers  | Array of Phone Number parameters                                                                                                                                                                                  |

#### Phone Number Parameters

| Parameter | Description                                                                                    |
|-----------|------------------------------------------------------------------------------------------------|
| number    | Phone number including area code, e.g. '+17075518391'                                          |
| primary   | Whether or not phone is primary. Only one primary phone per person. Options: `true` or `false` |
| label     | Type of phone number. Options: `cell`, `home` or `work`                                        |

#### Address Parameters

| Parameter     | Description                                      |
| ------------- | ------------------------------------------------ |
| address_line1 | Client's address                                 |
| city          | Client's city                                    |
| state         | Client's state. 2-letter abbreviation e.g.: `CA` |
| zip           | 5 digits zip code                                |

## Adopt a Client

> PATCH /api/clients/:client_label/adopt

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET \
-X PATCH https://app.monami.io/api/clients/ami-c090e55c/adopt \
-H 'Content-Type: application/json'
```

```ruby
credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

response = Excon.put('https://app.monami.io/api/clients/ami-c090e55c/adopt',
  headers: {
    'Content-Type' => 'application/json',
    'Authorization' => "Basic #{credential}"
  }
)
```

> An adoptable client response contains JSON structured like this:

```json
{
  "label": "ami-c090e55c",
  "person": {
    "id": 78,
    "first_name": "Jane",
    "preferred_name": "Client",
    "middle_name": null,
    "last_name": "Doe",
    "email": "new_email@monami.io",
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "home"
      }
    ],
    "sites": []
  }
}
```

> A sucessful adoption request returns JSON structured like this:

```json
{
  "id": 22,
  "status": "active",
  "created_at": "2024-03-13T09:04:33.346-07:00",
  "updated_at": "2024-03-13T09:04:33.346-07:00",
  "external_id": null,
  "label": "ami-c090e55c",
  "custom_fields": {
    "pronouns": "custom_value2",
    "gender_identity": "custom_value"
  },
  "address": {
    "address_line1": "X Random St",
    "address_line2": "Apt 2B",
    "city": "San Francisco",
    "state": "CA",
    "zip": "94117"
  },
  "person": {
    "id": 78,
    "first_name": "Jane",
    "preferred_name": "Client",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "new_email@monami.io",
    "created_at": "2024-03-13T16:04:33.256Z",
    "updated_at": "2024-03-13T16:04:33.399Z",
    "gender": "female",
    "primary_language": null,
    "languages": ["english", "portuguese"],
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "home"
      }
    ],
    "sites": ["my_credential_site"]
  }
}
```

This endpoint adds a specific client to a site credential's site, and returns the full client response.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter    | Description                         |
| ------------ | ----------------------------------- |
| client_label | The label of the client to adopt |


## List Documents for a Client

This endpoint returns a paginated list of Documents that have been completed for a Client.

> GET /api/clients/:client_id/documents

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/clients/ami-abc1234/documents"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/clients/ami-abc1234/documents',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A successful request returns JSON structured like this:

```json
{
  "documents": [
    {
      "document": {
        "metadata": {
          "name": "Nutrition Assessment",
          "label": "nutrition-assessment",
          "status": "completed"
        },
        "data": {
          "person.first_name": "Robert",
          "person.last_name": "Johnson"
        }
      }
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/clients/ami-6f22e351/documents?page=1",
    "first": "http://app.monami.io/api/clients/ami-6f22e351/documents?page=1",
    "last": "http://app.monami.io/api/clients/ami-6f22e351/documents?page=1"
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
| documents | The collection of results.                              |
| links     | Pagination links to access all the pages of the results |
| meta      | Helpful response metadata                               |

### Query Parameters

| Parameter          | Default | Description                                                                    |
| ------------------ | ------- | ------------------------------------------------------------------------------ |
| q[label]           | null    | Filter by a Document Template label. Ex: 'nutrition-assessment'                |
| q[completed_at_gt] | null    | Filter by completed_at date greater than a cutoff date in 'YYYY-MM-DD' format. |
| page               | 1       | Select the page of results.                                                    |
| per_page           | 25      | How many results per page.                                                     |
