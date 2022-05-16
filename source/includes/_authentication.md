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
```

<aside class="notice">
 <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization#basic_authentication">Example on MDN Web Docs</a>
</aside>
