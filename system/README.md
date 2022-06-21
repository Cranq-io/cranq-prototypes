# system

## Command runner

### Description:
Runs the received command string with the received options.

Sends stdout, stderr and optionally error message when the process finished.

Bounces command and options when the node is already in the state of executing a command.

### Input ports: 
* command: string

* options: {
"cwd": string,
"env": {string: string}
}

### Output ports: 
* stdout: string

* stderr: string

* error: (string or null)

    Null on success.


* on busy: {
"command": typeof `command`,
"options": typeof `options`
}

    The received command and options when the node is still executing another command.


* bounced: any



## Environment variable getter

### Description:
Gets a variable from the system environment by name

### Input ports: 
* name: string

    The name of the environment variable to get


### Output ports: 
* value: string

    The value of the environment variable if found


* not found: string

    The name of the environment variable that was not found




## Environment variable getter with fallback

### Description:
Gets a variable from the system environment by name or the provided fallback if not found

### Input ports: 
* name: string

    The name of the environment variable to get


* fallback: string

    The fallback value in case the variable is not found in the environment


### Output ports: 
* value: string

    The value of the environment variable or the fallback value if not found




## Environment variables getter with fallback

### Description:
Gets a list variable from either the system environment by name or the provided fallback default values. Sends a dictionary with a dictionary of names that have been resolved either way.

Example: 
1. `variable names` receives a list of environment variable names ["Var1", "Var2"]@0
2. `default values` receives optional default values { "var1": "value1" }@0

### Input ports: 
* variable names: string[]

    Receives a list of variable names to be resolved from the environment.
    
    Example:
    ["Var1", "Var2"]


* default values: {string:string}

    Receives optional default values for undefined environment variables.
    
    Example:
    { "var1": "value1" }


### Output ports: 
* resolved variables: {string:string}

    Sends the dictionary of resolved environment variables as a name:value dictionary.
    
    Contains the environment value if found, otherwise the specified default value if any.
    
    
    Example:
    {
      "V1": "value 1",
      "V2": "default value 2"
    }




## Matched command runner

### Description:
Runs the received command and matches standard output against the specified regular expression.

Sends matched RegEx groups through `groups`.

Sends empty array on no match.

### Input ports: 
* cwd: any

    Receives individual fields for syncing.


* command: string

* regex: string

### Output ports: 
* groups: string[]

    Matched RegEx groups




## Simple command runner

### Input ports: 
* command: string

    Command to be executed. Must be valid in the context of the current OS.
    
    It's recommended to verify the OS before attempting to execute.


* cwd: string

### Output ports: 
* success: boolean



## Timer

### Description:
Sets a timer which triggers `done` port after as many milliseconds as received or specified by `delay.  Timer can be canceled with ˙stop` (input).

Examples:
1. "timer1"@0 received via `start`
2. 300@0 received via `delay`
3. after 300 ms "timer1"@0 sent via `done`

1. "timer1"@0 received via `start`
2. `delay` set to 300
3.. "timer1"@0 received via `stop`
4. "timer1"@0 sent via `stopped`


### Input ports: 
* start: (string or number)

    Receives the timerId which identifies the timer.
    
    Example:
    "timer1"


* stop: (string or number)

    Receives the timerId which identifies the timer to be stopped.
    
    
    Example:
    "timer1"


* delay: number

    Receives the time in milliseconds that the timer should wait before the `done` port is triggered.
    
    Example: 
    300


### Output ports: 
* done: typeof `start`

    Sends timerId when the delayed timeout is reached.
    
    Example:
    "timer1" 


* stopped: typeof `stop`

    Sends timerId when the timer is stopped.
    
    Example:
    "timer1" 


