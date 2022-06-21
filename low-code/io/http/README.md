# low-code/io/http

## Error response generator

### Description:
Generates a default error response based on the error received from an `io/http/express/Endpoint listener`.

### Input ports: 
* error: {
  "error": "incorrect bearer token"
}

### Output ports: 
* response: ({
  "status": 400,
  "headers": {string: string},
  "body": "Bad request"
} or {
  "status": 403,
  "headers": {string: string},
  "body": "Unauthorized"
})

