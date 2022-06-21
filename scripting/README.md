# scripting

## Action finished tester

### Description:
Tests whether there's a result recorded on the specified result path of the state.

### Input ports: 
* state: any

    Receives script state.


* result path: (string or number)[]

    Locates an action result in the state.


### Output ports: 
* on finished: typeof `state`

    Forwards state when result path exists.


* on not started: typeof `state`

    Forwards state when result path does not exist.




## Action maintainer

### Input ports: 
* action result: any

* params: {
  "cwd": string,
  "result-path": string,
  "message": string
}

* state: any

    Receives script state.


### Output ports: 
* state: typeof `state`

    Sends script state as it was written.




## Action result logger

### Input ports: 
* params: {
  "message": string
}

* action result: any



## Action template

### Input ports: 
* state: any

* params: {
  "cwd": string,
  "result-path": string,
  "message": string
}

### Output ports: 
* state: typeof `state`



## Config reader

### Input ports: 
* path: string

### Output ports: 
* config: {string: any}



## Config reader (with param)

### Input ports: 
* path: string

* start: any

### Output ports: 
* config: {
"api-url": string,
"private-key": string,
"public-key": string,
"token-uri": string
}



## One-time action result maintainer

### Input ports: 
* action result: boolean

* params: {
  "cwd": string,
  "result-path": string,
  "message": string
}

* state: any

    Receives script state.


### Output ports: 
* state (action not started): typeof `state`

* state (action finished): typeof `state`



## Params copier

### Description:
Copies values from state over to a params structure.

### Input ports: 
* source: any

* destination: any

* mapping: {string: string}

### Output ports: 
* params: typeof `destination`



## Params copier (simplified)

### Input ports: 
* source: any

* params & mapping: {
  "params": any,
  "mapping": {string: string}
}

### Output ports: 
* params: typeof `params & mapping`["params"]



## Starter

### Description:
Starts a script, by reading the persisted state, or if there is none, initializes an blank state.

Example:
1. {"cwd": "foo"}@0 received via `params`
2. {}@0 sent via `state`

### Input ports: 
* params: {
  "cwd": string
}

    Receives essential parameters for initializing the state of the script.
    
    Property 'cwd' defaults to "./temp".
    
    Examples:
    * {}
    * {"cwd": "./foo"}


### Output ports: 
* state: any

    Initial state of the program. Sends either the contents of the previously persisted state, or a blank state record.
    
    Examlpe: {}




## State reader

### Description:
Reads the contents of "state.json", or, when absent, forwards the received `state`. The initial state is required to contain the current working directory (cwd) on the specified path.

### Input ports: 
* state: any

    Receives initial script state.


* config: {
"working-folder": string
}

* params: {
"cwd-path": (string or number)[]
}

### Output ports: 
* state: typeof `state`

    Receives script state read from path.




## State writer

### Input ports: 
* state: any

    Receives script state.


* cwd: string

### Output ports: 
* state: typeof `state`

    Sends script state as it was written.




## Status to params mapping creator

### Description:
Creates mapping to be used with `scripting/Params copier` to map from a previous action's result to a param for a next action.

### Input ports: 
* action params: {string:any}

    Params of the previous action.
    
    Example:
    {
    ...
    "result-path": "foo.bar"
    ...
    }


* mapping key: string

    The key in params of the next action to receive the result of the specified action from its status.
    
    Example:
    "foobar"


### Output ports: 
* mapping: {string: string}

    The mapping the copy a previous action result from its status to a next action's params.
    
    Example:
    { "foobar": "foo.bar" }


