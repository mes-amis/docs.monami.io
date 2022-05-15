---
title: Mon Ami REST API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - clients
  - webhooks
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Mon Ami REST API
---

# Introduction

Welcome to the Mon Ami REST API! You can use our API to access Mon Ami REST API endpoints, which can get information on clients from our database, or setup webhooks so you get live notifications when things happen within the Mon Ami platform.

We have examples in an assortment of languages! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

A Mon Ami API credential has a `uid` and a `secret` that you will need to use to create Authentication headers and verify webhook signatures. Each of these examples will assume that these are available as environment variables `MONAMI_UID` and `MONAMI_SECRET`.

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.tofu.monami.io/api/clients
```

```ruby
  uid, secret = ENV['MONAMI_UID'], ENV['MONAMI_SECRET']
  base64_encoded_credential = Base64.strict_encode64 [uid, secret].join(':')
  response = Excon.get('https://app.tofu.monami.io/api/clients',
    headers: {
      'Content-Type' => 'application/json',
      'Authorization' => "Basic #{base64_encoded_credential}"
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
