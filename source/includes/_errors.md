# Errors

The Occasion API uses the following error codes:


Error Code | Meaning
---------- | -------
401 | Unauthorized -- Your API key(s) are wrong, or you provided insufficient credentials to a private endpoint.
404 | Not Found -- The specified resource could not be found.
409 | Conflict -- Using the resource in the attempted way conflicts with its state.
422 | Unprocessable Entity -- The request data could not be processed into a valid entity. (missing params, invalid format, etc.).
429 | Too Many Requests -- You've made too many requests in the last 24 hours.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
