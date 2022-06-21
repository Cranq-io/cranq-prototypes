# io/http/express

## DELETE handler

### Description:
Receives DELETE requests on the specified route and dispatches the corresponding response.

Example:
1. "my-express-server"@0 received on `app ID`
2. "/users/"@0 received on `route`
3. a client DELETE request received by express with URL "http://api.mydomain.com/users/2
4. the following signals are sent to other node(s) processing the request
- {
 "accept": "application/json"
}@0 sent on `headers`
- {}@0 sent `body`
5. The following signals are received back from processing nodes and sent out to the client:
- 200@0 on `status`,
- {
    "content-type": "application/json" 
  }@0 on `headers`,
-  { id:2, "name": "John Doe", "age": 29 }@0 on `body`
6. null@0 sent on `done`

### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* route: (string or string[])

    Receives the route(s) to handle requests for. Route be specified as exact match (1) or as pattern match (2).
    
    Example:
    1) "/status" will just match "/status"
    2) "/s*s" will match "status", "shoes", etc..


* status: number

    Receives the HTTP status code to be sent with the response to the client.
    
    Example: 
    200


* headers: {string:string}

    Receives the HTTP headers to be sent with the response to the client.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Receives the content to send to the client as response body.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


### Output ports: 
* headers: typeof `headers`

    Forwards  the headers of the request to be processed.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Forwards the body of the request to be processed.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


* done: any

    Event triggered when the request has been processed.




## Endpoint listener

### Description:
Sets up a listener on an HTTP route. Starts an Express server if one is not started yet.

### Input ports: 
* response: {
"status": number,
"headers": {string:string},
"body": string
}

* params: {
  "appId": string,
  "port": number,
  "method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"),
  "route": string,
  optional "request": {
    optional "bearerToken": string,
    optional "contentType": ("text" or "json" or "urlencoded")
  },
  optional "response": { 
   optional "contentType": ("text" or "json")
  }
}

### Output ports: 
* request: `io/http/Request`

* error: any



## Express

### Description:
Core interface to Express.js. Use higher level nodes to interact with Express.

### Input ports: 
* action: {
"id": string, 
"type": string, 
"options": {string: any}
}

    Receives the parameters of the action to execute.
    
    Example: 
    {
      "id": "my-express-server",
      "type": "listen",
      "options": {
        "port": 3000
      }
    }


* response: {
"status": number,
"headers": {string:string},
"body": any
}

    Receives the response to be sent out to the client.
    
    Example:
    {
      "status": 200,
      "headers": {
        "content-type": "application/json" 
      },
      "body": "Done"
    }


### Output ports: 
* request: {
"baseUrl": string, 
"body": any, 
"cookies": any, 
"hostname": string, 
"headers": {string:string}, 
"ip": string, 
"ips": string[], 
"method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"), 
"originalUrl": string,
"params": {string:string}, 
"path": string, 
"protocol": ("http" or "https"), 
"query": {string: any}, 
"route": string, 
"secure": boolean, 
"signedCookies": any, 
"stale": boolean, 
"subdomains": string[], 
"xhr": boolean
}

    Sends the request processed by  defined handlers. Can be used to post-process the request.


* done: null

    Event triggered when the specified action has been executed.


* error: {"error": string}

    Sends error information in case the specified action could not be successfully executed.
    
    Example:
    {
      "error": "Error: listen EADDRINUSE: address already in use :::3000"
    }




## GET handler

### Description:
Receives GET requests on the specified route and dispatches the corresponding response.

Example:
1. "my-express-server"@0 received on `app ID`
2. "/status/"@0 received on `route`
3. a client GET request received by express with URL "http://api.mydomain.com/status?q=1&p=2"
4. the following signals are sent to other node(s) processing the request
- {
 "accept": "application/json"
}@0 sent on `headers`
- { "q": "1", "p": "2" }@0 sent `query`
5. The following signals are received back from processing nodes and sent out to the client:
- 200@0 on `status`,
- {
    "content-type": "application/json" 
  }@0 on `headers`,
- { status: "OK" }@0 on `body`
7. null@0 sent on `done`


### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* route: (string or string[])

    Receives the route(s) to handle requests for. Route be specified as exact match (1) or as pattern match (2).
    
    Example:
    1) "/status" will just match "/status"
    2) "/s*s" will match "status", "shoes", etc..


* status: number

    Receives the HTTP status code to be sent with the response to the client.
    
    Example: 
    200


* headers: {string:string}

    Receives the HTTP headers to be sent with the response to the client.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Receives the content to send to the client as response body.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


### Output ports: 
* headers: typeof `headers`

    Forwards  the headers of the request to be processed.
    
    Example: 
    {
      "content-type": "application/json"
    }


* query: {string: any}

    Forwards the query parameters to process.


* done: null

    Event triggered when the request has been processed.




## JSON listener

### Description:
Starts an express server set up for handling requests and also responding with JSON bodies.

### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* port: number

    The port number express should listen to.
    
    Example: 
    3000


### Output ports: 
* done: any

* error: {"error": string}

    Sends error information in case the server could not be started or a middleware could not be applied.




## Listener

### Description:
Sets up the specified Express server to listen on the specified port.

Example:
1. "my-express-server"@0 received on `app ID`
2. 3000@0 received on `port`
3. Express server is started to listen on http//localhost:3000
4/a. In case of success
-  null@0 sent on `done`
- "my-express-server"@0 sent on `app iD`
4/b. In case of failure
-  {
  "code": "EADDRINUSE",
  "errno": -98,
  "syscall": "listen",
  "address": "::",
  "port": 3000
}@0 sent on `error`


### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* port: number

    The port number express should listen to.
    
    Example: 
    3000


### Output ports: 
* done: null

    Event triggered when the action has been executed.


* error: {"error": string}

    Sends error information in case the specified action could not be successfully executed.
    
    Example:
    {
      "code": "EADDRINUSE",
      "errno": -98,
      "syscall": "listen",
      "address": "::",
      "port": 3000
    }


* app ID: typeof `app ID`

    DEPRECATED
    
    The id of the express instance the action was executed on. Emitted when the action was executed.
    To be used when chaining multiple actions on the same express instance.
    
    Example: 
    "my-express-server"




## Middleware applicator

### Description:
Applies a known middleware to the specified express app.

Accepted middleware identifiers:
* "json"
* "urlencoded"
* "cors"

### Input ports: 
* app ID: string

    Identifies the Express app to apply the middleware on.


* middleware: ("text" or "json" or "urlencoded" or "cors")

### Output ports: 
* done: any

* app ID: typeof `app ID`

* error: {"error": string}

    Sends error information in case the middleware could not be applied.




## Middlewares applicator

### Description:
Applies multiple Express middlewares.

### Input ports: 
* app ID: any

* middlewares: ("text" or "json" or "urlencoded" or "cors")[]

### Output ports: 
* done: any

* error: {"error": string}

    Sends error information in case any of the specified the middlewares could not be applied.




## PATCH handler

### Description:
Receives PATCH requests on the specified route and dispatches the corresponding response.

Example:
1. "my-express-server"@0 received on `app ID`
2. "/users/"@0 received on `route`
3. a client PATCH request received by express with URL "http://api.mydomain.com/users/2
4. the following signals are sent to other node(s) processing the request
- {
 "accept": "application/json"
}@0 sent on `headers`
- { "age": 29 }@0 sent `body`
5. The following signals are received back from processing nodes and sent out to the client:
- 200@0 on `status`,
- {
    "content-type": "application/json" 
  }@0 on `headers`,
-  { id:2, "name": "John Doe", "age": 29 }@0 on `body`
6. null@0 sent on `done`

### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* route: (string or string[])

    Receives the route(s) to handle requests for. Route be specified as exact match (1) or as pattern match (2).
    
    Example:
    1) "/status" will just match "/status"
    2) "/s*s" will match "status", "shoes", etc..


* status: number

    Receives the HTTP status code to be sent with the response to the client.
    
    Example: 
    200


* headers: {string:string}

    Receives the HTTP headers to be sent with the response to the client.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Receives the content to send to the client as response body.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


### Output ports: 
* headers: typeof `headers`

    Forwards  the headers of the request to be processed.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Forwards the body of the request to be processed.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


* done: any

    Event triggered when the request has been processed.




## POST handler

### Description:
Receives POST requests on the specified route and dispatches the corresponding response.

Example:
1. "my-express-server"@0 received on `app ID`
2. "/users/"@0 received on `route`
3. a client POST request received by express with URL "http://api.mydomain.com/users/
4. the following signals are sent to other node(s) processing the request
- {
 "accept": "application/json"
}@0 sent on `headers`
- { "name": "John Doe", "age": 27 }@0 sent `body`
5. The following signals are received back from processing nodes and sent out to the client:
- 200@0 on `status`,
- {
    "content-type": "application/json" 
  }@0 on `headers`,
-  { id:2, "name": "John Doe", "age": 27 }@0 on `body`
6. null@0 sent on `done`


### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* route: (string or string[])

    Receives the route(s) to handle requests for. Route be specified as exact match (1) or as pattern match (2).
    
    Example:
    1) "/status" will just match "/status"
    2) "/s*s" will match "status", "shoes", etc..


* status: number

    Receives the HTTP status code to be sent with the response to the client.
    
    Example: 
    200


* headers: {string:string}

    Receives the HTTP headers to be sent with the response to the client.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Receives the content to send to the client as response body.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


### Output ports: 
* headers: typeof `headers`

    Forwards  the headers of the request to be processed.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Forwards the body of the request to be processed.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


* done: any

    Event triggered when the request has been processed.


* error: {"error": string}

    Sends error information in case the request could not be handled.




## PUT handler

### Description:
Receives PUT requests on the specified route and dispatches the corresponding response.

Example:
1. "my-express-server"@0 received on `app ID`
2. "/users/"@0 received on `route`
3. a client POST request received by express with URL "http://api.mydomain.com/users/2
4. the following signals are sent to other node(s) processing the request
- {
 "accept": "application/json"
}@0 sent on `headers`
- { id:2, "name": "John Doe", "age": 29 }@0 sent `body`
5. The following signals are received back from processing nodes and sent out to the client:
- 200@0 on `status`,
- {
    "content-type": "application/json" 
  }@0 on `headers`,
-  { id:2, "name": "John Doe", "age": 29 }@0 on `body`
6. null@0 sent on `done`

### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* route: (string or string[])

    Receives the route(s) to handle requests for. Route be specified as exact match (1) or as pattern match (2).
    
    Example:
    1) "/status" will just match "/status"
    2) "/s*s" will match "status", "shoes", etc..


* status: number

    Receives the HTTP status code to be sent with the response to the client.
    
    Example: 
    200


* headers: {string:string}

    Receives the HTTP headers to be sent with the response to the client.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Receives the content to send to the client as response body.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


### Output ports: 
* headers: typeof `headers`

    Forwards  the headers of the request to be processed.
    
    Example: 
    {
      "content-type": "application/json"
    }


* body: any

    Forwards the body of the request to be processed.
    
    Example:
    - "OK"
    - 3.14
    - { "status": "OK" }


* done: any

    Event triggered when the request has been processed.




## Route handler

### Description:
Receives requests on the specified route and dispatches the corresponding response.
You may also consider method specific route handlers for easier use.

Example:
1. "my-express-server"@0 received on `app ID`
2. "GET"@0 received on `method`
3. "/status/"@0 received on `route`
4. a client GET request received by express with URL "http://api.mydomain.com/status"
5. {
"body": "", 
"hostname": "api.mydomain.com", 
"method": "GET", 
"path": "/status", 
"protocol": "http", 
}@0 sent on `request`to other node for processing
6. {
  "status": 200,
  "headers": {
    "content-type": "application/json" 
  },
  "body": { status: "OK" } 
}@0 received back on `response` from processing nodes and sent out to the client
7.
- null@0 sent on `done`
- "my-express-server"@0 sent on `app ID`

### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* method: ("GET" or "POST" or "PUT" or "PATCH" or "DELETE")

    Receives the method to handle request for. 
    
    Example:
    "GET"


* route: (string or string[])

    Receives the route(s) to handle requests for. Route be specified as exact match (1) or as pattern match (2).
    
    Example:
    1) "/status" will just match "/status"
    2) "/s*s" will match "status", "shoes", etc..
    


* response: {
"status": number,
"headers": {string:string},
"body": any
}

    Receives the response to be sent out to the client.
    
    Example:
    {
      "status": 200,
      "headers": {
        "content-type": "application/json" 
      },
      "body": "Done"
    }


### Output ports: 
* request: {
"baseUrl": string, 
"body": any, 
"cookies": any, 
"hostname": string, 
"headers": {string:string}, 
"ip": string, 
"ips": string[], 
"method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"), 
"originalUrl": string,
"params": {string:string}, 
"path": string, 
"protocol": ("http" or "https"), 
"query": {string: any}, 
"route": string, 
"secure": boolean, 
"signedCookies": any, 
"stale": boolean, 
"subdomains": string[], 
"xhr": boolean
}

    Forwards the request to be processed.


* done: null

    Event triggered when the specified action has been executed.


* app ID: typeof `app ID`

    The id of the express instance the action was executed on. Emitted when the action was executed.
    To be used when chaining multiple actions on the same express instance.
    
    Example: 
    "my-express-server"


* error: {"error": string}

    Sends error information in case the request could not be handled.




## Text listener

### Description:
Starts an express server set up for handling requests and also responding with text bodies.

### Input ports: 
* app ID: string

    The id of the express instance.
    
    Example: 
    "my-express-server"


* port: number

    The port number express should listen to.
    
    Example: 
    3000


### Output ports: 
* done: any

* error: {"error": string}

    Sends error information in case the server could not be started or a middleware could not be applied.


