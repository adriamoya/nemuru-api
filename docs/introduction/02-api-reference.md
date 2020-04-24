# API Reference

The Nemuru API is organized around [REST](https://en.wikipedia.org/wiki/Representational_state_transfer). Our API accepts [JSON-encoded](https://www.json.org/json-en.html) request bodies, returns [JSON-encoded](https://www.json.org/json-en.html) responses, and uses standard [HTTP response codes](03-status-codes.md) and authentication.

Nemuru API provides two different environments to interact with: `Integration` and `Production`. You can use `Integration` in test mode, which does not affect your live data or interact with our banking partners. The server, and corresponding API key used to [authenticate](03-authentication.md) the requests, determines whether is is live mode (`Production`) or test mode (`Integration`).

The latest version of the API is v1:

<!-- theme: info -->
> INTEGRATION BASE URL
> **https://api-release.nemuru.io/v1**

<!-- theme: success -->
> PRODUCTION BASE URL
> **https://api.nemuru.io/v1**


**Subscribe to Nemuru's API announce mailing list for updates.**