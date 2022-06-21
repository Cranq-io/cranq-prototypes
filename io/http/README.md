# io/http

## HTML Form POST request dispatcher

### Description:
Dispatches HTML form POST request and outputs response or error.

Example: 
1. "https://httpbin.org/post"@0 recieved via `URL` 
2.  {}@0 recieved via `headers` 
3. 
{
  "custname": "John Doe",
  "custtel": "1234567890", 
  "custemail": "john.doe@email.doe",  
  "size": "small",
  "topping": ["bacon", "cheese", "onion"]
}@0 recieved via `item` 
4. 200@0 sent via `status`
5. "OK"@0 sent via `body`

### Input ports: 
* URL: string

    Receives the target of the HTML form post.
    
    Example:
    "https://httpbin.org/post"


* headers: {string:string}

    Receives request headers. 
    
    Example:
    {}


* form data: {
string: (string or string[])
}

    Receives the form data to be posted.
    
    Example:
    {
      "custname": "John Doe",
      "custtel": "1234567890", 
      "custemail": "john.doe@email.doe",  
    "size": "small",
    "topping": ["bacon", "cheese", "onion"]
    }


### Output ports: 
* status: number

    Sends HTTP response status code. Indicates whether the request has been  successfully completed.
    
    Example:
    200


* headers: {string:string}

    Sends HTTP response headers.


* body: string

    Sends HTTP response message body data.
    
    Example:
    "OK"


* errors: {"error": string}

    Sends HTTP response communication error.
    
    
    Example:
    {
      "error": "Error: getaddrinfo ENOTFOUND x.y"
    } 




## JSON request dispatcher

### Description:
Dispatches HTTP request, expects response as JSON, parses it and outputs it as data. Outputs error if failed.

More: https://github.com/Cranq-io/cranq-tutorials/tree/main/http_request

### Input ports: 
* JSON req.: {
  "method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"),
  "url": string,
  "headers": {string: string},
  optional "data": any
}

    Receives request with JSON body.


### Output ports: 
* data: any

    Sends HTTP response message body as data.
    
    Example:
    {
      "userId": 1, 
      "id": 1, 
      "title": "delectus aut autem",  
      "completed": false
    }"


* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

    Sends original response.


* error: {"error": string}



## JSON request dispatcher (deprecated)

### Description:
Dispatches HTTP request, expects response as JSON, parses it and outputs it as data. Outputs error if failed.

More: https://github.com/Cranq-io/cranq-tutorials/tree/main/http_request

### Input ports: 
* method: ("GET" or "POST" or "PUT" or "PATCH" or "DELETE")

    Receives http method. Indicates the desired action to be performed for a given target or resource.
    
    Example:
    "GET"
    


* URL: string

    Receives the target of the HTTP request. Also called "resource" 
    
    Example:
    "https://jsonplaceholder.typicode.com/todos/1"
    


* headers: {string:string}

    Receives request headers. It is  used to describe a resource, or the behavior of the server or the client.
    
    Any received headers are added to the defaults.
    
    Default:
    {
      "content-type": "application/json; charset=utf-8"
    }
    
    Example: 
    {
    "Accept": "application/json"
    }
    


* data: any

    Receives the http request body as data. Some requests send data to the server in order to update it. In case of GET or DELETE request the body should be empty (will be ignored).
    
    Example:
    {}


### Output ports: 
* status: number

    Sends http response status code. Indicates whether the request has been  successfully completed.
    
    Example:
    200
    


* headers: {string:string}

    Sends http response headers.
    
    Example:
    {
    "content-type": "application/json; charset=utf-8",
    "cache-control":"max-age=43200"
    }


* data: any

    Sends http response message body as data.
    
    Example:
    {
      "userId": 1, 
      "id": 1, 
      "title": "delectus aut autem",  
      "completed": false
    }"


* error: {"error": string}

    Sends http response communication error.
    
    
    Example:
    {
      "error": "Error: getaddrinfo ENOTFOUND x.y"
    }


* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}



## Request dispatcher

### Description:
Dispatches HTTP request and outputs response or error.

More: https://github.com/Cranq-io/cranq-tutorials/tree/main/http_request

### Input ports: 
* params: {
  "method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"),
  "url": string,
  "headers": {string: string},
  optional "body": string
}

    Receives parameters of the HTTP request.
    
    Example:
    
    {
      "verb":"GET,
      "url": "https://jsonplaceholder.typicode.com/todos/1",
      "headers": {
        "content-type": 
      "application/json; charset=utf-8"
      }
    }


### Output ports: 
* response: {
  "status": number,
  "headers": {string: string},
  "body": string
}

    Sends HTTP response object.
    
    Example:
    
    {
      "status": 200,
      "headers": {
        "content-type": "application/json; charset=utf-8",
        "cache-control": "max-age=43200"
      },
      "body": "{\"userId\": 1, \"id\": 1, \"title\": \"delectus aut autem\",  \"completed\": false
    }"
    }


* error: {"error": string}

    Sends error on failing to send or receive the request.
    
    Example:
    
    {
      "error": "Error: getaddrinfo ENOTFOUND x.y"
    } 




## Request dispatcher (deprecated)

### Description:
Use `io/http/Request dispatcher` instead.

Dispatches HTTP request and outputs response or error.

More: https://github.com/Cranq-io/cranq-tutorials/tree/main/http_request

### Input ports: 
* method: ("GET" or "POST" or "PUT" or "PATCH" or "DELETE")

    Receives http method. Indicates the desired action to be performed for a given target or resource.
    
    Example:
    "GET"


* URL: string

    Receives the target of the HTTP request. Also called "resource" 
    
    Example:
    "https://jsonplaceholder.typicode.com/todos/1"


* headers: {string:string}

    Receives request headers. It is  used to describe a resource, or the behavior of the server or the client.
    
    Example:
    {
      "content-type": "application/json; charset=utf-8"
    }


* body: string

    Receives the http request body. Some requests send data to the server in order to update it. In case of GET or DELETE request the body should be empty (will be ignored).
    
    Example:
    ""


### Output ports: 
* status: number

    Sends http response status code. Indicates whether the request has been  successfully completed.
    
    Example:
    200


* headers: {string:string}

    Sends http response headers.
    
    Example:
    {
    "content-type": "application/json; charset=utf-8",
    "cache-control":"max-age=43200"
    }
    


* body: string

    Sends http response message body data.
    
    Example:
    "{\"userId\": 1, \"id\": 1, \"title\": \"delectus aut autem\",  \"completed\": false
    }"


* error: {"error": string}

    Sends http response communication error.
    
    
    Example:
    {
      "error": "Error: getaddrinfo ENOTFOUND x.y"
    } 


* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}



## URL search params serializer

### Description:
Serializes URL search parameters.

Example:
1. { "term1": "foo", "term2": "bar"}@0 received on `params`
2. "term1=foo&term2=bar"@0 sent on `serialized`

1.[["term1", "foo"], ["term2", "bar"]]@0 received on `params`
2. "term1=foo&term2=bar"@0 sent on `serialized`

### Input ports: 
* params: ({string: any} or [string, any][])

    Received URL search parameters.
    
    Example:
    1. { "term1": "foo", "term2": "bar"}
    2. [["term1", "foo"], ["term2", "bar"]]


### Output ports: 
* serialized: string

    Serialized parameters
    
    Example:
    "term1=foo&term2=bar"




## URL-encoded request dispatcher

### Description:
Dispatches HTTP request with an URL encoded body, expects response as JSON, parses it and outputs it as data. Outputs error if failed.

### Input ports: 
* URL-enc. req.: {
  "method": string,
  "url": string,
  "headers": {string: string},
  "data": {string: (string or string[])}
}

### Output ports: 
* data: any

    Sends HTTP response message body as data.
    
    Example:
    {
      "userId": 1, 
      "id": 1, 
      "title": "delectus aut autem",  
      "completed": false
    }"


* response: {
  "status": number,
  "headers": {string: string},
  "body": string
}

    Sends original response.


* error: {"error": string}

