# boolean

## And

### Description:
Performs a boolean AND operation on the values received via inputs `a` and `b`.

Example:

1. true@0 is received via `a`
2. true@0 is received via `b`
3. true@0 is sent via `and`

### Input ports: 
* a: boolean

    Receives the first operand.


* b: boolean

    Receives the second operand.


### Output ports: 
* and: boolean

    Sends the result of the logical AND operation.




## Condition

### Description:
Sends either on the `true` or the `false` output port, depending on the input value received on the `boolean` port.

Example:

1. true@0 is received on `boolean`
2. null@0 is sent via `true`

### Input ports: 
* boolean: boolean

    Input condition value


### Output ports: 
* true: null

    Sends null if the input value is true.


* false: null

    Sends null if the input value is false.




## Equality tester

### Description:
Checks if boolean `a` is equal to boolean `b`.

Example:

1. false@0 is received via `a`
2. false@0 is received via `b`
3. true@0 is sent via `equal`

### Input ports: 
* a: boolean

    First operand


* b: boolean

    Second operand


### Output ports: 
* equal: boolean

    Sends true if the provided values are equal, false otherwise.




## Evaluator

### Description:
Determines whether the input is truthy or falsy.

Example A (for truthy):

1. 23@0 is received via `value`
2. true@0 is sent via `boolean`

Example B (for falsy):
1. null@0 is received via `value`
2. false@0 is sent via `boolean`

### Input ports: 
* value: any

    Data to be evaulated as boolean


### Output ports: 
* boolean: boolean

    The value evaulated as boolean.




## Not

### Description:
Performs a boolean NOT operation on the value received via input `a`.

Example:

1. false@0 is received via `a`
2. true@0 is sent via `not`

### Input ports: 
* a: boolean

    The value to be negated.


### Output ports: 
* not: boolean

    Sends the negated value of the input `a`.




## Or

### Description:
Performs a boolean OR operation on the received values via inputs `a` and `b`.

Example:

1. false@0 is received via `a`
2. true@0 is received via `b`
3. true@0 is sent via `or`

### Input ports: 
* a: boolean

    Receives the first operand


* b: boolean

    Receives the second operand


### Output ports: 
* or: boolean

    Sends the result of the OR operation.




## Reverse condition

### Description:
Turns binary independent signals into a boolean.

Example A:
1. null@0 is received via `true`
2. true@0 is sent via `boolean`

Example B:
1. "foo"@1 is received via `false`
2. false@1 is sent via `boolean`

### Input ports: 
* to true: any

    Receives signals to be evaluated to true.


* to false: any

    Receives signals to be evaluated to false.


### Output ports: 
* boolean: boolean

    Sends boolean depending on which input the signal was received through.




## Type tester

### Description:
Checks whether the `data` input is a boolean.

Example:

1.  false@0 is received via `data`
2. true@0 is sent via `is boolean`

### Input ports: 
* data: any

    Input value to be checked


### Output ports: 
* is boolean: boolean

    Sends true if the input is a boolean, false otherwise.


