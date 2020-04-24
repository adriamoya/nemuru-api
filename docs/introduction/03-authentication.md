# Authentication

The Nemuru API uses API keys to authenticate requests. Your API keys carry many privileges, so be sure to keep them secure! 

To get started and receive API credentials please contact us from our [website](http://www.nemuru.com).

<!-- theme:warning -->
>Bear in mind that you might want to interact with the Nemuru API for different use cases:
>* For **creating Merchants** use the API credentials — username and password — provided to you. Once your Merchants are created, our risk algorithms will analyze the documentation provided by them (and this process may be delayed in time). If the documentation passes our checks, your Merchants will be granted with credentials — username and password —, which will be sent over to them via email.
>
>* Use the Merchant's credentials in case you want to interact with our API **on behalf of the Merchant**. In other words, if the Merchant needs to create a Loan or get her list of Loans, the coresponding request should be sent with the Merchant's credentials.

In any case, in order to call our API, it will be necessary to request the access token with a username and password:

### Request

```bash
curl --request POST \
     --url https://api.nemuru.com/api/auth/login \
     --header 'Content-Type: application/json' \
     --data '{"username": "username@email.com", "password": "12345"}'
```

### Response

```json
{
  "token_type": "Bearer",
  "expires_in": 2678400,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjVhOTQzNZjk4ZjgwIn0...",
  "refresh_token": "def50200d7cef7d466cc4132310b098f86721272d301aed4c97f7e34b1b701d8..."
}
```

You should include your API access token in the header of your requests as follows:

```bash
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjVhOTQzNZjk4ZjgwIn0...'
```

The authentication process can be pictured as:

![authentication-process](../../assets/images/authentication-process.png)

All API requests myst be made over HTTP. API requests without authentication will fail.