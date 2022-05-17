# Webhooks

Webhooks can be used to integrate apps without polling. You can setup subscriptions to events in Mon Ami and get JSON
notifications sent to the URL of your choice. You can use your API credential secret to verify the messages send from Mon Ami to provide
a secure and reliable system integration.

## Get all webhooks for a given Credential

To manage your webhook subscriptions there is an `/api/webhooks` resource that lists the webhooks created for a given credential.

> GET /api/webhooks

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
| webhook_url | The URL you want the webhook notification to POST to.                                                              |

## Create a new webhook subscription

You can create a subscription with the topic of `*` to get all webhook events or you can subscribe to individual topics,
or wildcard topics, ex: `client.*`.

> POST /api/webhooks

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

> A sucessful request returns HTTP Status `201 Created` and a JSON object representing the webhook:

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
| webhook_url | The URL you want the webhook notification to POST to.                                                              |

## Delete a webhook subscription

If you're no longer interested in getting webhook notifications, you can destroy a webhook.

> DELETE /api/webhooks/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET  -H 'Content-Type: application/json' -X 'DELETE' https://app.monami.io/api/webhooks/1
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.delete('https://app.monami.io/api/webhooks/1',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )
```

> A sucessful request returns HTTP Status `204 No Content`:

## Implementing an HTTP Handler for the webhook

> Example Webhook JSON.

```json
{
  "topic": "client.created",
  "data": {
    "id": 8,
    "person_id": 16,
    "status": "pending",
    "created_at": "2022-05-16T16:51:42.382-07:00",
    "updated_at": "2022-05-16T16:51:42.382-07:00",
    "first_name": "Client",
    "preferred_name": null,
    "last_name": "Name",
    "email": "client.name@example.monami.io",
    "address": {
      "address_line1": "123 Fake Street",
      "address_line2": null,
      "city": "San Mateo",
      "state": "CA",
      "zip": "94402"
    }
  }
}
```

### Verification

To verify the webhook, you need to verify the signature, by securely comparing the `Hmac-SHA256` request header with an HMAC of the request POST body.

> A Ruby on Rails example that verifies the request and calls a handler.

```shell
# I'm not sure how to handle an HTTP request in a shell.
# Have a look at the Ruby example.
```

```ruby
  class WebhooksController < ActionController::Base
    before_action :verify_request!

    def create
      WebhookHandler.call request.params
    end

    protected

    def verify_request!
      unless ActiveSupport::SecurityUtils::secure_compare(verified_signature, signature_header)
        raise "HMAC verification failed. Make sure it's not malicious and check hmac config."
      end
    end

    def signature_header
      request.headers['Hmac-SHA256'].chomp
    end

    def verified_signature
      Base64.strict_encode64(OpenSSL::HMAC.digest('sha256', ENV['MONAMI_SECRET'], request.raw_post)).chomp
    end
  end
```
