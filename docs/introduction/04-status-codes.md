# Status codes

Nemuru uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a merchant was already created, etc.). Codes in the 5xx range indicate an error with Nemuru's servers.

HTTP STATUS CODE

Code | Label | Description
---------|----------|---------
 200 | OK | Everything worked as expected.
 201 | Created | The requested resource was created.
 400 | Bad Request | The request was unacceptable, often due to missing a required parameter.
 401 | Unauthorized | The parameters were valid but the request failed.
 403 | Forbidden | The access to the requested resource is forbidden.
 404 | Not Found | The requested resource doesn't exist.
 409 | Conflict | The request conflicts with another request.
 500 | Server Errors | Something went wrong on Nemuru's end.