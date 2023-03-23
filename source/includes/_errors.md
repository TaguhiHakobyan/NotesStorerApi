# Errors

<!-- <aside class="notice">
This error section is stored in a separate file in <code>includes/_errors.md</code>. Slate allows you to optionally separate out your docs into many files...just save them to the <code>includes</code> folder and add them to the top of your <code>index.md</code>'s frontmatter. Files are included in the order listed.
</aside>
 -->
Notes Storer API returns general HTTP status codes in any of the following ranges:

- `2xx`: The range indicates that the request is successfully processed.
- `4xx`: The range indicates that something is wrong with the request (incorrect parameters, failed authentication, and more).
- `5xx`: The range indicates that something is wrong with our server.

## HTTP Status Codes

Here are some common HTTP status codes that Notes Storer API may return

Status Code | Description
---------- | -------
200 - OK | The request is successful and the response body contains the requested data.
400 - Bad Request | The request is invalid and the response body contains explanation what's wrong.
401 - Unauthorized | The authentication failed or you don't have permission to access the requested resource.
404 - Not Found | The requested resource isn't found. 
405 - Method Not Allowed | The resource doesn't support the requested HTTP method.
500 - Internal Server Error | An error occured on the server. Try again later.
503 - Service Unavailable | Service is temporarily unavailable. Please try again later.



## Error response

The errors may also contain a JSON response body explaining what's wrong with the request. 

> An error response example:

```json
"error" : {
  "code": 400,
  "message": "The 'content' property is required.",
}

```

Property | Description
---------- | -------
code | Error code.
message | A text explaining the reason for an error. 


