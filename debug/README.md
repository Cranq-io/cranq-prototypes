# debug

## Logger

### Description:
Logs received data and tag to the output. Formats data as JSON.

### Input ports: 
* data: any



## Logger (unformatted)

### Description:
Logs received data to the output, using default formatting options.

Not recommended for complex data types.

### Input ports: 
* data: any



## Logger (with message)

### Input ports: 
* data: any

* message: string



## Output formatter

### Description:
Formats output based on received data and a custom message.

### Input ports: 
* data: any

* message: string

### Output ports: 
* prepare output-filled: string



## Unsuccessfull http response logger

### Description:
Logs received 4xx and 5xx responses with a custom message.

### Input ports: 
* response: {
 "status": number, 
 "headers": {string: string}, 
 "body": string
}

    Receives request dispatcher response.
    
    Example: 
    {
     "status": 200, 
     "headers": {}, 
     "body": "OK"
    }


* message: string

    Receives additional log message.
    
    Example: 
    "unsuccessfull call"


