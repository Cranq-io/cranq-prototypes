# data

## Equality tester (strict)

### Description:
Tests whether `a` and `b` are equal by reference. (Primitives by value.) 

### Input ports: 
* a: any

* b: any

### Output ports: 
* equal: any



## Sameness tester

### Input ports: 
* a: any

* b: any

### Output ports: 
* same: any



## Store

### Description:
Stores data and sends it via `data` when read. When the store is empty, any attempt to read the contents will result in a signal sent out via `not found`.

Example:
1. `data` set to "hello"
2. null@1 received via `read`
3. "hello"@1 sent via `data` (output)

### Input ports: 
* data: any

    Receives contents of the store. San be set as parameter, or received as signal.


* read: any

    Receives a signal that triggers the contents being sent via `data` (output), or `not found` when has no content.


### Output ports: 
* data: typeof `data`

    Sends store contents.


* written: null

    Sends signal when contents were set in flow.


* not found: null

    Sends signal on read attempt while store has no content.




## Store (async)

### Description:
Stores data and sends it via `data` when read. When the store is empty, read attempts will be buffered until the store gets initialized via `data`.

Example: late initialization
1. null@1 received via `read`
2. null@2 received via `read`
3. "hello"@3 received via `data`
4. "hello"@1 sent via `data` (output)
5. "hello"@2 sent via `data` (output)

### Input ports: 
* data: any

    Receives contents of the store. San be set as parameter, or received as signal. When received as a signal, will complete previous read attempts.


* read: any

    Receives a signal that triggers the contents being sent via `data` (output). When store has no content yet, read signals will be buffered until a signal is received via `data`.


### Output ports: 
* data: typeof `data`

    Sends store contents.


* written: null

    Sends signal when contents were set in flow.


* not found: null

    Sends signal on read attempt while store has no content.


