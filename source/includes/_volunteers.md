# Volunteers

## List Volunteers

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

> A successful request returns JSON structured like this:

```json
{
  "volunteers": [
    {
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
        ],
        "sites": []
      }
    }
  ],
  "links": {
    "self": "http://app.monami.io/api/volunteers?page=1&per_page=1",
    "first": "http://app.monami.io/api/volunteers?page=1&per_page=1",
    "next": "http://app.monami.io/api/volunteers?page=2&per_page=1",
    "last": "http://app.monami.io/api/volunteers?page=2&per_page=1"
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
| volunteers | The collection of results.                              |
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

> A successful request returns JSON structured like this:

```json
{
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
    ],
    "sites": []
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
--form 'person="{\"first_name\": \"John\",\"preferred_name\": \"Volunteer\",\"last_name\": \"Doe\",\"date_of_birth\": \"1940-05-30\",\"email\": \"volunteer@monami.io\",\"gender\": \"male\",\"phone_numbers\": [{\"number\": \"+17075518391\", \"primary\": true}], \"languages\": \"english,portuguese\"}"' \
--form 'address="{\"address_line1\": \"X Random St\", \"city\": \"San Francisco\", \"state\": \"CA\", \"zip\": \"94117\"}"' \
--form 'custom_fields="{\"gender_identity\": \"custom_value\", \"pronouns\": \"custom_value2\"}"'
```

```ruby
require "uri"
require "net/http"

credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')
url = URI("http://app.monami.io/api/volunteers/")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Basic #{credential}"
form_data = [['person', '{"first_name": "John","preferred_name": "Volunteer","last_name": "Doe","date_of_birth": "1940-05-30","email": "volunteer@monami.io","gender": "male","phone_numbers": [{"primary": "+17075518391"}],"languages": "english,portuguese"}'],['address', '{"address_line1": "X Random St", "city": "San Francisco", "state": "CA", "zip": "94117"}'],['custom_fields', '{"gender_identity": "custom_value", "pronouns": "custom_value2"}']]
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A successful request returns JSON structured like this:

```json
{
  "id": 3,
  "status": "applied",
  "created_at": "2024-03-13T11:38:00.900-07:00",
  "updated_at": "2024-03-13T11:38:00.900-07:00",
  "external_id": null,
  "label": "volunteer-d",
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
    "id": 79,
    "first_name": "John",
    "preferred_name": "Volunteer",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "volunteer@monami.io",
    "created_at": "2024-03-13T18:38:00.777Z",
    "updated_at": "2024-03-13T18:38:00.931Z",
    "gender": "male",
    "primary_language": null,
    "languages": ["english", "portuguese"],
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "cell"
      }
    ],
    "sites": []
  }
}
```

This endpoint retrieves the newly created volunteer.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter     | Description                       |
| ------------- | --------------------------------- |
| person        | JSON formatted person parameters  |
| address       | JSON formatted address parameters |
| custom_fields | JSON formatted custom fields      |

#### Person Parameters

| Parameter      | Description                                                                                                                                                                                                |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| first_name     | Volunteer's first name                                                                                                                                                                                     |
| preferred_name | Volunteer's preferred name                                                                                                                                                                                 |
| last_name      | Volunteer's last name                                                                                                                                                                                      |
| date_of_birth  | Volunteer's birthdate eg.: `YYYY-MM-DD`                                                                                                                                                                         |
| email          | Volunteer's email address                                                                                                                                                                                  |
| gender         | Volunteer's gender. Options are: `female`, `male`, `trans_female`, `trans_male`, `non_binary`, `trans_non_binary`, `gender_queer`, `two_spirit`, `questioning_not_sure`, `not_listed`, `prefer_not_to_say` |
| languages      | Array of Language Object type labels                                                                                                                                                        |
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
| address_line1 | Volunteer's address                              |
| city          | Volunteer's City                                 |
| state         | Volunteers State 2 letter abbreviation eg.: `CA` |
| zip           | 5 digits zip code                                |

## Create a Volunteer for a specific Person

> POST /api/people/:person_id/volunteers/

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/people/79/volunteers/ \
--form 'address="{\"address_line1\": \"X Random St\", \"city\": \"San Francisco\", \"state\": \"CA\", \"zip\": \"94117\"}"' \
--form 'custom_fields="{\"gender_identity\": \"custom_value\", \"pronouns\": \"custom_value2\"}"'
```

```ruby
require "uri"
require "net/http"

credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')
url = URI("http://app.monami.io/api/people/79/volunteers/")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Basic #{credential}"
form_data = [['address', '{"address_line1": "X Random St", "city": "San Francisco", "state": "CA", "zip": "94117"}'],['custom_fields', '{"gender_identity": "custom_value", "pronouns": "custom_value2"}']]
request.set_form form_data, 'multipart/form-data'
response = http.request(request)
puts response.read_body
```

> A successful request returns JSON structured like this:

```json
{
  "id": 4,
  "status": "applied",
  "created_at": "2024-03-13T11:42:32.745-07:00",
  "updated_at": "2024-03-13T11:42:32.745-07:00",
  "external_id": null,
  "label": "volunteer-d",
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
    "id": 79,
    "first_name": "John",
    "preferred_name": "Volunteer",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "volunteer@monami.io",
    "created_at": "2024-03-13T18:38:00.777Z",
    "updated_at": "2024-03-13T18:42:32.777Z",
    "gender": "male",
    "primary_language": null,
    "languages": ["english", "portuguese"],
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "cell"
      }
    ],
    "sites": []
  }
}
```

This endpoint creates a volunteer for a given person.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter     | Description                       |
| ------------- | --------------------------------- |
| person_id     | Integer ID present in the URL     |
| address       | JSON formatted address parameters |
| custom_fields | JSON formatted custom fields      |

#### Address Parameters

| Parameter     | Description                                      |
| ------------- | ------------------------------------------------ |
| address_line1 | Volunteer's address                              |
| city          | Volunteer's City                                 |
| state         | Volunteers State 2 letter abbreviation eg.: `CA` |
| zip           | 5 digits zip code                                |

## Update a Volunteer

> PATCH /api/volunteers/:volunteer_id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET \
-X PATCH https://app.monami.io/api/volunteers/3 \
-d '{ "person": { "email": "new_email@monami.io" }, "address": { "address_line2": "Apt 2B" } }' \
-H 'Content-Type: application/json'
```

```ruby
credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

response = Excon.put('https://app.monami.io/api/volunteers/3',
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
  "id": 3,
  "status": "applied",
  "created_at": "2024-03-13T11:38:00.900-07:00",
  "updated_at": "2024-03-13T11:38:00.900-07:00",
  "external_id": null,
  "label": "volunteer-d",
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
    "id": 79,
    "first_name": "John",
    "preferred_name": "Volunteer",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "new_email@monami.io",
    "created_at": "2024-03-13T18:38:00.777Z",
    "updated_at": "2024-03-13T18:38:00.931Z",
    "gender": "male",
    "primary_language": null,
    "languages": ["english", "portuguese"],
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "cell"
      }
    ],
    "sites": []
  }
}
```
This endpoint returns the updated volunteer.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Payload Parameters

| Parameter     | Description                       |
| ------------- | --------------------------------- |
| person        | JSON formatted person parameters  |
| address       | JSON formatted address parameters |
| custom_fields | JSON formatted custom fields      |

#### Person Parameters

| Parameter      | Description                                                                                                                                                                                             |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| first_name     | Volunteer's first name                                                                                                                                                                                     |
| preferred_name | Volunteer's preferred name                                                                                                                                                                                 |
| last_name      | Volunteer's last name                                                                                                                                                                                      |
| date_of_birth  | Volunteer's birthdate eg.: `YYYY-MM-DD`                                                                                                                                                                         |
| email          | Volunteer's email address                                                                                                                                                                                  |
| gender         | Volunteer's gender. Options are: `female`, `male`, `trans_female`, `trans_male`, `non_binary`, `trans_non_binary`, `gender_queer`, `two_spirit`, `questioning_not_sure`, `not_listed`, `prefer_not_to_say` |
| languages      | Array of Language Object type labels                                                                                                                                                     |
| phone_numbers  | Array of Phone Number parameters                                                                                                                                                                                  |

#### Phone Number Parameters

| Parameter | Description                                                                                    |
|-----------|------------------------------------------------------------------------------------------------|
| number    | Phone number including area code, e.g. '+17075518391'                                          |
| primary   | Whether or not phone is primary. Only one primary phone per person. Options: `true` or `false` |
| label     | Type of phone number. Options: `cell`, `home` or `work`                                        |

#### Address Parameters

| Parameter     | Description                                         |
| ------------- | --------------------------------------------------- |
| address_line1 | Volunteer's address                                 |
| city          | Volunteer's city                                    |
| state         | Volunteer's state. 2 letter abbreviation e.g.: `CA` |
| zip           | 5 digit zip code                                    |


## Adopt a Volunteer

> PATCH /api/volunteers/:volunteer_label/adopt

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET \
-X PATCH https://app.monami.io/api/volunteers/volunteer-d/adopt \
-H 'Content-Type: application/json'
```

```ruby
credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

response = Excon.put('https://app.monami.io/api/volunteers/volunteer-d/adopt',
  headers: {
    'Content-Type' => 'application/json',
    'Authorization' => "Basic #{credential}"
  }
)
```

> An adoptable client response contains JSON structured like this:

```json
{
  "label": "volunteer-d",
  "person": {
    "id": 79,
    "first_name": "John",
    "preferred_name": "Volunteer",
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
  "id": 3,
  "status": "applied",
  "created_at": "2024-03-13T11:38:00.900-07:00",
  "updated_at": "2024-03-13T11:38:00.900-07:00",
  "external_id": null,
  "label": "volunteer-d",
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
    "id": 79,
    "first_name": "John",
    "preferred_name": "Volunteer",
    "middle_name": null,
    "last_name": "Doe",
    "date_of_birth": "1940-05-30",
    "email": "new_email@monami.io",
    "created_at": "2024-03-13T18:38:00.777Z",
    "updated_at": "2024-03-13T18:38:00.931Z",
    "gender": "male",
    "primary_language": null,
    "languages": ["english", "portuguese"],
    "phone_numbers": [
      {
        "number": "+17075518391",
        "primary": true,
        "label": "cell"
      }
    ],
    "sites": ["my_credential_site"]
  }
}
```

This endpoint adds a specific volunteer to a site credential's site, and returns the full volunteer response.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter       | Description                            |
| --------------- | -------------------------------------- |
| volunteer_label | The label of the volunteer to adopt |
