# data/csv

## Dictionary array to csv converter

### Description:
Formats a dictionary array as a csv string. Does not support multi-level dictionaries.

Example:
1. 'array' receives
[
  {
    "a":1
    "b":2
  },
  {
    "a":11
    "b":22
  },
]
2. 'csv' sends 
"a,b
1,1
11,11"

### Input ports: 
* array: {string:(string or number or boolean)}[]

    Receives the array of dictionaries to format.
    
    Example:
    [
      {
        "a":1
        "b":2
      },
      {
        "a":11
        "b":22
      },
    ]


### Output ports: 
* csv: string

    The resulting csv string.




## Naive parser

### Description:
Parses CSV naively. (Only commas, all values will be strings, quotes not recognized.)

Example:
1. "foo,1\nbar,2"@1 received via `csv`
2. [["foo", "1"], ["bar", "2"]]@1 sent via `2D array`

### Input ports: 
* csv: string

### Output ports: 
* 2D array: string[][]

