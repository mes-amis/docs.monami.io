# Authentication

A Mon Ami API credential consists of a `uid` and a `secret`. You will need to use these to create Authorization headers and verify webhook signatures. Each of these examples will assume that these values are available as the environment variables `MONAMI_UID` and `MONAMI_SECRET`.

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/clients
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/clients',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{credential}"
    }
  )

  JSON.load response.body
```

Mon Ami uses API keys to allow access to the API. You can register a new Mon Ami REST API key at our [developer portal](https://example.com/developers).

Mon Ami expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Basic BASE_64_ENCODED_CREDENTIAL`

<aside class="notice">
 <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization#basic_authentication">Example on MDN Web Docs</a>
</aside>
