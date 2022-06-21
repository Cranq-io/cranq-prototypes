# io/http/utils

## API key inserter

### Description:
Inserts API key into a HTTP request header.

### Input ports: 
* headers: {string: string}

* API key: string

### Output ports: 
* headers: (typeof `headers` and {"X-Api-Key": typeof `API key`})



## Bearer token checker

### Description:
Checks for the presence of the specified bearer token in the submitted request headers. Forwards request body only when found.

### Input ports: 
* bearer token: string

    Receives the bearer token to be verified.


* request: {
"headers": {string:string},
"body": string
}

    Receives the request to be authorized.


### Output ports: 
* request: {
"headers": {string:string},
"body": string
}

* error: {"error": "incorrect bearer token"}



## Bearer token inserter

### Description:
Inserts bearer token into a HTTP request header.

Example:
1. { "content-type": "application/json" }@0 received on  `headers`
2. "SomeDummyToken"@0 received on `token`
3. {"content-type": "application/json", "Authorization": "Bearer SomeDummyToken" }@0 sent on `headers`

### Input ports: 
* headers: {string: string}

    Recieves request headers. It is  used to describe a resource, or the behavior of the server or the client.
    
    Example:
    {
      "content-type": "application/json; charset=utf-8"
    }


* token: string

    Receives the string token to be inserted into the Authorization header as Bearer token.
    The token is usually used in base64 encoded form.
    
    Example: 
    - "SomeDummyToken" as plain text 
    - "U29tZUR1bW15VG9rZW4=" as base64 encoded text


### Output ports: 
* headers: typeof `headers`

    Sends the received request headers with the authorization header added to it.
    
    Example:
    {
      "content-type": "application/json", 
      "Authorization": "Bearer SomeDummyToken" 
    }




## Body-less request builder

### Description:
Builds a HTTP request that has no body.

### Input ports: 
* method: ("GET" or "POST" or "PUT" or "PATCH" or "DELETE")

* URL: string

* headers: {string: string}

### Output ports: 
* request: {
  "method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"),
  "url": string,
  "headers": {string: string}
}



## Content type inserter

### Description:
Inserts content type into a HTTP request header.

Example:
1. {}@0 received via `headers`
2. "application/json"@0 received on `content type`
3. {"Content-Type": "application/json"}@0 sent via `headers`

### Input ports: 
* headers: {string: string}

    Recieves request headers. It is  used to describe a resource, or the behavior of the server or the client.
    
    Example:
    {
      "content-type": "application/json; charset=utf-8"
    }


* content type: string

    Receives the content type to be inserted into the headers.
    
    Examples:
    * "application/json"
    * "text/plain"
    
    


### Output ports: 
* headers: typeof `headers`

    Sends the received request headers with the content type header added to it.
    
    Example:
    {
      "Content-Type": "application/json"
    }




## JSON request builder

### Description:
Builds a JSON request record with data to be sent as the request's body.

For body-less requests, see `io/http/utils/Body-less request builder`.

### Input ports: 
* method: ("GET" or "POST" or "PUT" or "PATCH" or "DELETE")

* url: string

* headers: {string: string}

* data: any

### Output ports: 
* JSON req.: {
  "method": typeof `method`,
  "url": typeof `url`,
  "headers": typeof `headers`,
  "data": typeof `data`
}



## JSON response error detector

### Description:
Wraps failed HTTP response into an error, including a message.

Example A
1. `message` set to "Response failed"
2. {"status": 200, "headers": {}, "body": "null"}@1 received via `response`
3. null@1 sent via `data`

Example B
1. `message` set to "Response failed"
2. {"status": 400, "headers": {}, "body": {"success": false}}@1 received via `response`
3. {"error": "Response failed", "details": {"success": false}}@1 sent via `error`

### Input ports: 
* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

    Receives JSON response that might contain an error.


* error msg: string

    Receives error message to appear in `error`.


### Output ports: 
* data: any

    Sends response data, when the response was successful.


* error: {
  "error": string,
  optional "details": any
}



## Multi param appender

### Description:
Appends a query parameter with multiple values received via `key` and `values` to the array of single query params received via `params` (input), and sends the result via `params` (output).

Example:
1. "Sally"@1 received via `value`
2. "name"@1 received via `key`
3. []@1 received via `params`
4. [{"key": "name", "value": "Sally"}]@1 sent via `params` (output)

### Input ports: 
* values: string[]

    Receives values associated with the same query parameter.


* key: string

    Receives the key part of a key-value pair.


* params: {"key": string, "value": string}[]

    Receives an array of single query params as key-value pairs.


### Output ports: 
* params: {"key": string, "value": string}[]

    Sends an array of single query params as key-value pairs.




## Multi params builder

### Description:
Builds an array of single query parameters as key-value pairs based on the key received via `key` and the values received via `values`.

Example:
1. ["Norah", "Smith"]@1 received via `values`
2. "name"@1 received via `key`
3. [{"key": "name", "value": "Norah"}, {"key": "name", "value": "Smith"}]@1 sent via `params`

### Input ports: 
* values: string[]

    Receives an array of query parameter values associated with the same key.


* key: string

    Receives the key part of a key-value pair.


### Output ports: 
* params: {"key": string, "value": string}[]

    Sends an array of single query params as key-value pairs.




## Query param appender

### Description:
Appends a single or array query param received via `param` to the received list of single query `params` in a key-value pair format.

Example:
1. {"key": "name", "value": ["John", "Doe"]}@1 received via `param`
2. [{"key": "age", "value": "27"}]@1 received via `params`
3. [{"key": "age", "value": "27"}, {"key": "name", "value": "John"}, {"key": "name", "value": "Doe"}]@1 sent via `params` (output)

### Input ports: 
* param: {
"key": string, 
"value": (string or string[])
}

    Receives a query parameter as a key-value pair. The query parameter may be a single value or an array.


* params: {"key": string, "value": string}[]

    Receives an array of single parameter key-value pairs.


### Output ports: 
* params: {"key": string, "value": string}[]

    Sends an array of single query parameters as key-value pairs.




## Query param builder

### Description:
Builds a single query param specified by a param name and a param value.

Example:
1. 

### Input ports: 
* name: string

    Receives the name of the query parameter.


* value: string

    Receives the value of the query parameter.


### Output ports: 
* param: string

    Sends the serialized query parameter.




## Query param serializer

### Description:
Serializes the single query received via `param` as a key-value pair.

Example:
1. {"key": "name", "value": "Sally"}@1 received via `params`
2. "name=Sally"@1 sent via string

### Input ports: 
* param: {"key": string, "value": string}

    Receives a single query parameter as key-value pair.


### Output ports: 
* string: string

    Sends the serialized single query param.




## Query params flattener

### Description:
Flattens query parameters received via `params` expressed as a dictionary, into an array of single query parameters as key-value pairs sent via `flattened`.

Example:
1. [{"key": "name", "value": "Sophie"}, {"key": "friends", "value": ["Liya", "Owen"]}]@1 received via `params`
2. [{"key": "name", "value": "Sophie"}, {"key": "friends", "value": "Liya"}, {"key": "friends", "value": "Owen"}]@1 sent via `flattened`


### Input ports: 
* params: {
string: (string or string[])
}

    Receives query parameters as dictionary.


### Output ports: 
* flattened: {"key": string, "value": string}[]

    Sends query parameter key-value pairs individually.




## Query params getter

### Description:
Retrieves the 'query' component of an HTTP request.

Example:
1. {"headers": {}, "query": {"message": "Hello"}}@1 received via `request`
2. {"message": "Hello"}@1 sent via `query`

### Input ports: 
* request: {
  "query": {string: (string or string[])}
}

    Receives an HTTP request that has query params.


### Output ports: 
* query: {string: (string or string[])}

    Sends the 'query' component of the received request.




## Query string builder

### Description:
Builds a query string by serializing the received dictionary as query params.

Example:
1. {"name": "Jane", "height": "1.63"}@1 received via `params`
2. "name=Jane&height=1.63"@1 sent via `query`

### Input ports: 
* params: {string: (string or string[])}

    Receives query parameters to be serialized as a dictionary.


### Output ports: 
* query: string

    Sends HTTP query string.




## Request authenticator

### Description:
Authenticates request using the provided authentication method.

### Input ports: 
* request: `io/http/Request`

    Receives request to be authenticated


* params: {
  optional "bearerToken": string
}

    [Inherited from port `dict` of `item getter`] 
    Receives the dictionary to get the value from.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


### Output ports: 
* request: `io/http/Request`

* error: {"error": "incorrect bearer token"}



## Request body getter

### Description:
Retrieves the 'body' component of an HTTP request.

Example:
1. {"headers": {}, "body": "Hello"}@1 received via `request`
2. "Hello"@1 sent via `body`

### Input ports: 
* request: {
  "body": any
}

    Receives an HTTP request that has a body.


### Output ports: 
* body: typeof `request`["body"]

    Sends the 'body' component of the received request.




## Response builder

### Description:
Builds a response structure out of its components: HTTP status, headers, and body.

Example:
1. 200@1 received via `status`
2. {"Content-Type": "text/plain"}@1 received via `headers`
3. "OK"@1 received via `body`
4. {"status": 200, "headers": {"Content-Type": "text/plain"}, "body": "OK"}@1 sent via `response`

### Input ports: 
* body: string

    Receives the body of the response.
    
    Example:
    "OK"


* status: number

    Receives a HTTP status code.
    
    Example:
    200


* headers: {string: string}

    Receives a record of HTTP headers.
    
    Example:
    {"Contanet-Type": "text/plain"}


### Output ports: 
* response: {"status": number, "headers": {string: string}, "body": string}

    Sends the constructed HTTP response.




## Response content type applicator

### Description:
Adds content type header to the received response.

### Input ports: 
* response: `io/http/Response`

* params: {optional "contentType": ("text" or "json")}

### Output ports: 
* response: `io/http/Response`



## Response error detector

### Description:
Wraps failed HTTP response into an error, including a message.

Example A
1. `message` set to "Response failed"
2. {"status": 200, "headers": {}, "body": "ABC"}@1 received via `response`
3. null@1 sent via `body`

Example B
1. `message` set to "Response failed"
2. {"status": 400, "headers": {}, "body": {"success": false}}@1 received via `response`
3. {"error": "Response failed", "details": {"success": false}}@1 sent via `error`

### Input ports: 
* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

    Receives response that might contain an error.


* error msg: string

    Receives error message to appear in `error`.


### Output ports: 
* body: typeof `response`["body"]

* error: {
  "error": string,
  optional "details": any
}



## Response fork by status

### Description:
Forwards `response` to either `on match` or `on mismatch` depending on whether the response matches the HTTP status received via `status`.

### Input ports: 
* status: number

    Receives HTTP status code.


* response: `io/http/Response`

    Receives HTTP response.


### Output ports: 
* on match: `io/http/Response`

    Forwards received response when it matches the HTTP status received via `status`.


* on mismatch: `io/http/Response`

    Forwards received response when it does not match the HTTP status received via `status`.




## Response header merger

### Description:
Merges the specified response headers into the response.

### Input ports: 
* response: `io/http/Response`

* headers: `io/http/Response headers`

### Output ports: 
* response: `io/http/Response`



## Response splitter

### Description:
Splits a canonical HTTP response into its components: HTTP status, headers, and body.

### Input ports: 
* response: `io/http/Response`

    Receives the canonical HTTP response to be split.


### Output ports: 
* status: typeof `response`["status"]

* headers: typeof `response`["headers"]

* body: typeof `response`["body"]



## Response success detector

### Description:
Detects whether a HTTP response was successful based on its status code.

### Input ports: 
* status: number

    HTTP response status code.


### Output ports: 
* success status: number

    Forwards the status code on success. (1XX, 2XX, 3XX)


* error status: number

    Forwards the status code on error. (4XX, 5XX)




## Single param appender

### Description:
Appends a single query parameter received via `key` and `value` to the array of single query params received via `params` (input), and sends the result via `params` (output).

Example:
1. "Sally"@1 received via `value`
2. "name"@1 received via `key`
3. []@1 received via `params`
4. [{"key": "name", "value": "Sally"}]@1 sent via `params` (output)

### Input ports: 
* value: string

    Receives a single query parameter value.


* key: string

    Receives the key part of a key-value pair.


* params: {"key": string, "value": string}[]

    Receives an array of single query params as key-value pairs.


### Output ports: 
* params: {"key": string, "value": string}[]

    Sends an array of single query params as key-value pairs.




## URL query appender

### Description:
Appends a query string based on the query parameters to the specified URLs.

### Input ports: 
* URL: string

    Receives URL without the query component.


* query params: {string: (string or string[])}

### Output ports: 
* URL + query: string

    Sends URL including the query component.




## URL-encoded request builder

### Description:
Builds a URL-encoded request record with data to be sent as the request's body.

For body-less requests, see `io/http/utils/Body-less request builder`.

### Input ports: 
* method: ("GET" or "POST" or "PUT" or "PATCH" or "DELETE")

* url: string

* headers: {string: string}

* data: {string: (string or string[])}

### Output ports: 
* URL-enc. req.: {
  "method": typeof `method`,
  "url": typeof `url`,
  "headers": typeof `headers`,
  "data": typeof `data`
}

