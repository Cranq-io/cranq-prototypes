# low-code/io/http/express

## Endpoint listener

### Description:
Opinionated low-code version of `io/http/express/Endpoint listener`.

Sets up a listener on an HTTP route, and handles bad request errors. Starts an Express server if one is not started yet.

Possible error responses:
* {
    "status": 400,
    "headers": {},
    "body": "Bad request"
  }
* {
    "status": 403,
    "headers": {},
    "body": "Unauthorized"
  }

### Input ports: 
* response: typeof `response` of `endpoint`

* params: (typeof `params` of `endpoint` and {"timeout": number})

### Output ports: 
* request: typeof `request` of `endpoint`

