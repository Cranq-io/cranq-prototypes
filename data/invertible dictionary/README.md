# data/invertible dictionary

## Builder (key-value pairs)

### Input ports: 
* key-value pairs: {"key": string, "value": any}[]

### Output ports: 
* dict: {string: typeof `key-value pairs`[number]["value"]}



## Item adder

### Description:
Adds an item to an invertible dictionary. Invertible dictionaries can have multiple values assigned to a single key.

### Input ports: 
* dict: {string: any[]}

* key: string

* value: typeof `dict`[string][number]

### Output ports: 
* dict: typeof `dict`

