# io/stdio

## Line writer

### Description:
Writes a line to standard output.

Example:
1. "hello world"@0 received on `line`
2. "hello world" followed by a line break is written to the standard output 

### Input ports: 
* line: string

    The line of text to be written to the standard output. (Does not need to include a line break)
    
    
    Example: "hello world"




## Line writer (conditional)

### Description:
Writes a line to the standard output when the condition is true.

### Input ports: 
* line: string

* condition: boolean



## Line writer (with param)

### Input ports: 
* line: string

* start: any



## Text writer

### Description:
Writes a text to standard output.

Example:
1. "hello world"@0 received on `line`
2. "hello world" is written to the standard output

### Input ports: 
* text: string

    The text to be written to the standard output.
    
    
    Example: "hello world"




## Text writer (with param)

### Input ports: 
* text: string

* start: any

