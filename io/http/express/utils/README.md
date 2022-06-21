# io/http/express/utils

## Content type middleware applicator

### Description:
Tells the Express app identified by `app ID` to use a middleware that corresponds to the request's content type.

Defaults to "text".

Example A:
1. "ID"@1 received via `app ID`
2. {"contentType": "json"}@1 received via `params`
3. Express applies the "json" middleware
4. "ID"@1 sent via `app ID` (output)

### Input ports: 
* app ID: string

    Identifies the Express app to apply the middleware on.


* params: {
  "contentType": ("text" or "json" or "urlencoded")
}

### Output ports: 
* app ID: typeof `app ID`

* error: {"error": string}

* done: any
