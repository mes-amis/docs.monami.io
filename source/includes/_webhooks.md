# Webhooks

Webhooks can be used to integrate apps without polling. You can setup subscriptions to events in Mon Ami and get JSON
notifications sent to the URL of your choice. You can use your API credential secret to verify the messages send from Mon Ami to provide
a secure and reliable system integration.

## Get all webhooks for a given Credential

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/webhooks
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/webhooks',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "webhooks": [
    {
      "id": 1,
      "topic": "*",
      "webhook_url": "https://app.monami.io/api/webhooks/test",
      "created_at": "2022-05-13T00:34:45.851Z"
    }
  ],
  "links": {
    "self": "https://app.monami.io/api/webhooks?page=1",
    "first": "https://app.monami.io/api/webhooks?page=1",
    "last": "https://app.monami.io/api/webhooks?page=1"
  },
  "meta": {
    "total_pages": 1,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter   | Description                                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------------------------------ |
| id          | The id of the webhook.                                                                                             |
| topic       | The name of the topic or topics to be notified for. Allows wildcards. Ex `client.*` will receive all client events |
| webhook_url | The URL you want the webhook notification sent to.                                                                 |

## Create a new webhook subscription

You can create a subscription with the topic of `*` to get all webhook events or you can subscribe to individual topics,
or wildcard topics, ex: `client.*`.

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET -d '{ "topic": "client.created", "webhook_url": "https://app.monami.io/api/webhooks/test" }' -H 'Content-Type: application/json' https://app.monami.io/api/webhooks
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.post('https://app.monami.io/api/webhooks/test',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    },
    body: '{ "topic": "client.created", "webhook_url": "https://app.monami.io/api/webhooks/test" }'
  )
```

> A sucessful request returns HTTP Status 201 Created and a JSON object representing the webhook:

```json
{
  "id": 4,
  "topic": "client.created",
  "webhook_url": "https://app.monami.io/api/webhooks/test",
  "created_at": "2022-05-14T01:21:30.998Z"
}
```

### Request Parameters

| Parameter   | Description                                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------------------------------ |
| topic       | The name of the topic or topics to be notified for. Allows wildcards. Ex `client.*` will receive all client events |
| webhook_url | The URL you want the webhook notification sent to.                                                                 |
