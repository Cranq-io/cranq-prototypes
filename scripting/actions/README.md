# scripting/actions

## Command runner

### Description:
Runs an OS command.

### Input ports: 
* state: any

    Receives script state.


* params: {
"cwd": (string or number)[],
"result-path": string,
"message": string,
"command": string
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Directory lister

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd-path": (string or number)[],
  "result-path": string,
  "message": string,
  "directory-path": string
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Dotenv appender

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "name": string,
  "value": string,
  "append": boolean
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Express endpoint creator (simplified)

### Description:
Sets up a route for Express to receive requests on. Routes are expected to follow a format as per Express documentation.

Receiving `state` and `params` inputs initializes the route. Once the route is inialized, incoming requests will be sent out on `request`, and corresponding responses will be expected on `response`, bearing the same tag.

Example:
1. {}@0 received via state
2. {
  "cwd": "express",
  "method": "GET",
  "route": "/status"
}@0 is received via `params`
3. State with route information added is sent via `state`
4. An arbitrary GET request comes in via `request`
5. {"status": 200, "headers": {}, "body": "OK"}@1 is received via `response`
6. The received response is sent to the client.

Links:
* https://expressjs.com/en/guide/routing.html

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"),
  "route": string,
  "app-id": string
}

    Receives method and route to match incoming requests against. Also specifies which running Express server instance to use via 'app-id'. The parameter 'app-id' must match the ID of a previously started Express server.


* response: {
"status": number,
"headers": {string:string},
"body": any
}

    Receives the response for a corresponding request prepared by the logic that connects `request` to `response`.
    
    Properties:
    * 'status' specifies HTTP status code
    * 'headers' list HTTP response headers
    * 'body' specifies the body of the response. Format potentially depends on middlewares.


### Output ports: 
* state: typeof `state`

    Sends updated script state.


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

    Sends incoming requests matching the route and method received via `params`.




## Express route creator

### Description:
Sets up an API endpoint using Express. An express server must be started in the script before the flow gets to this one.

See `scripting/actions/Express server starter`.

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"),
  "route": string,
  "app-id": string
}

* response: {
"status": number,
"headers": {string:string},
"body": any
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.


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



## Express server starter

### Input ports: 
* state: any

* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "app-id": string,
  "port": number,
  "middlewares": ("json" or "cors" or "urlencoded")[]
}

### Output ports: 
* state: typeof `state`



## Express server starter (simplified)

### Description:
Starts an express server on the specified port and with the specified middlewares.

Specifying an 'app-id' allows running multiple express servers at the same time.

Writes the app ID of the started server to state.

Repeatable action.

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "app-id": string,
  "port": number,
  "middlewares": ("json" or "cors" or "urlencoded")[]
}

    Receives:
    * 'cwd' locates directory for persisted state
    * 'app-id' identifies Express server (default: "default")
    * 'port' specifies port to run server on (default: 8080)
    * 'middlewares' lists express middlewares to be activated (default: [])
    
    Example:
    {
      "cwd": "./express",
      "middlewares": ["json"]
    }


### Output ports: 
* state: typeof `state`

    Sends updates script state.




## File appender

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "path": string,
  "text": string
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## File creator

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "path": string,
  "text": string,
  "result-path": string,
  "message": string
}

### Output ports: 
* state: any

    Sends updated script state.




## Folder creator

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "path": string
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Matched command runner

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "command": string,
  "regex": string
}

### Output ports: 
* state: any

    Sends updated script state.




## One-time action template

### Description:
Template for creating actions that run only once during the execution of the script and record their result into the state. Once a result is recorded, the action will be skipped on the next run.

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Paths joiner

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "child-paths": string[],
  "base-path": string
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Wait

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "delay": number
}

### Output ports: 
* state: typeof `state`

    Forwards script state.


