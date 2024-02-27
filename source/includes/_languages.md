# Languages

## Get Languages

This endpoint returns a paginated list of languages as well as pagination links and meta information.

> GET /api/languages

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/languages?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/languages?page=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "languages": [
        {
            "id": 1,
            "name": "English",
            "label": "english"
        }
    ],
    "links": {
        "self": "http://app.monami.test/api/languages?page=1&per_page=1",
        "first": "http://app.monami.test/api/languages?page=1&per_page=1",
        "next": "http://app.monami.test/api/languages?page=2&per_page=1",
        "last": "http://app.monami.test/api/languages?page=63&per_page=1"
    },
    "meta": {
        "total_pages": 63,
        "current_page": 1
    }
}
```

### Response Parameters

| Parameter         | Description                                             |
| ----------------- | ------------------------------------------------------- |
| languages         | The collection of results.                              |
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

## Get a Specific Language

> GET /api/languages/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/languages/43
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/languages/43',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
    "id": 43,
    "name": "Portuguese",
    "label": "portuguese"
}
```

This endpoint retrieves a specific language.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| id        | The id of the language to retrieve       |
