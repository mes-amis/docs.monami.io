# Errors

Errors will be returned a JSON with the following format.

<aside class="notice">
The errors will sometimes have links with more details that will be helpful when debugging.
</aside>

```json
{
  "errors": [
    {
      "message": "The Authorization header is invalid."
    },
    {
      "message": "first_name must be provided"
    },
    {
      "message": "last_name must be provided"
    }
  ]
}
```

The Mon Ami API uses the following error codes:

| Status Code | Meaning               | Description                                                                  |
| ----------- | --------------------- | ---------------------------------------------------------------------------- |
| 400         | Bad Request           | Your request is invalid.                                                     |
| 401         | Unauthorized          | Your API key is wrong.                                                       |
| 404         | Not Found             | The specified record could not be found.                                     |
| 405         | Method Not Allowed    | You tried to access a record with an invalid method.                         |
| 406         | Not Acceptable        | You requested a format that isn't json.                                      |
| 410         | Gone                  | The record requested has been removed from our servers.                      |
| 422         | Unprocessable Entity  | The request has invalid parameters. See the error messages in the response.  |
| 429         | Too Many Requests     | You're requesting too many records! Slow down!                               |
| 500         | Internal Server Error | We had a problem with our server. Try again later.                           |
| 503         | Service Unavailable   | We're temporarily offline for maintenance. Please try again later.           |
