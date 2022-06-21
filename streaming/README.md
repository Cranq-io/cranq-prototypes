# streaming

## Moving buffer

### Description:
Stores the last N inputs received via `sample` and sends them via `buffer`.

Errors on invalid `size`.

Data sent via `buffer` is immutable.

Example:
1. `size` set to 2
2. "A"@0 received via `sample`
3. ["A"] sent via `buffer`
4. "B"@1 received via `sample`
5. ["A","B"] sent via `buffer`
6. "C"@2 received via `sample`
7. ["B", "C"] sent via `buffer`

### Input ports: 
* sample: any

    Receives individual samples to be buffered.


* size: number

    Specifies the maximum number of samples stored in the buffer.
    
    Must be parameter.


### Output ports: 
* buffer: typeof `sample`[]

    Sends current contents of moving buffer.


* error: {"message": string}

    Sends error when:
    * size is equal or less than 0 or not set


* bounced: typeof `sample`

    Forwards input received via `sample` on error.




## Time-based moving buffer

### Description:
Stores the "value" property of samples received in the last `length` seconds and sends them via `buffer`.

Errors on invalid `size`.

Expects samples to be received in ascending order of "timestamp".

Data sent via `buffer` is immutable.

Example:
1. `size` set to 2 (seconds)
2. {value: "A", timestamp: 0}@0 received via `sample`
3. [{value: "A", timestamp: 0}]@0 sent via `buffer`
4. {value: "B", timestamp: 1}@1 received via `sample`
5. [{value: "A", timestamp: 0}, {value: "B", timestamp: 1}]@1 sent via `buffer`
6. {value: "C", timestamp: 3}@2 received via `sample`
7. [{value: "B", timestamp: 1}, {value: "C", timestamp: 3}]@1 sent via `buffer`

### Input ports: 
* sample: {"value": any, "timestamp": number}

    Receives individual samples to be buffered.


* size: number

    Size of the buffer in seconds.


### Output ports: 
* buffer: (typeof `sample`["value"])[]

    Sends current contents of moving buffer.


* error: {"message": string}

    Sends error when:
    * size is equal or less than 0 or not set


* bounced: typeof `sample`

    Forwards input received via `sample` on error.


