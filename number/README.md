# number

## Abs

### Description:
Returns the absolute value of the input number.

Example:

1. -23@0 is received via `number`
2. 23@0 is sent via `abs`

### Input ports: 
* number: number

    Input value


### Output ports: 
* abs: number

    The absolute value of the input.




## Adder

### Description:
Performs an addition operation on the input values.

Example:

1. 19@0 is received via `a`
2. 2@0 is received via `b`
3. 21@0 is sent via `sum`

### Input ports: 
* a: number

    The first operand


* b: number

    Second operand


### Output ports: 
* sum: number

    The sum of the two operands.




## Ceiling

### Description:
Returns the number rounded up to the nearest integer.

Example:

1. 1.23@0 is received via `number`
2. 2@0 is sent via `ceiling`

Example (negative number):

1. -1.23@0 is received via `number`
2. -1@0 is sent via `ceiling`

### Input ports: 
* number: number

    Input number


### Output ports: 
* ceiling: number

    The nearest integer which is greater than or equal to the input.




## Counter

### Description:
Counts the received input signals.

Example:

1. true@0 is received via `trigger`
2. 1@0 is sent via `count`
3. false@1 is received via `trigger`
4. 2@1 is sent via `count`

### Input ports: 
* trigger: any

    The input signals to be counted


### Output ports: 
* count: number

    Total count of the signals received.




## Differ

### Description:
Sends the difference of the last two numbers received. The (n-1)th number will be subtracted from the nth number.

Example:
1. 10@0 is received via `number`
2. 20@1 is received via `number`
3. 10@1 is sent via `diff`

### Input ports: 
* number: number

    Receives numbers to be subtracted


### Output ports: 
* diff: number

    The difference of the last two numbers received.




## Divider

### Description:
Divides the received inputs. Bounces synced operands on division by zero.

Example (valid division):

1. 1@0 is received via `a`
2. 2@0 is received via `b`
3. 0.5@0 is sent via `fraction`

Example (divide by zero):

1. 13@0 is received via `a`
2. 0@0 is received via `b`
3. {"a":13, "b":0}@0 is sent via `bounced`

### Input ports: 
* a: number

    The counter part of the fraction.


* b: number

    Denominator part of the fraction.


### Output ports: 
* fraction: number

    The fraction of the received numbers.


* bounced: {"a":number,"b":number}

    Sends synced inputs on error.




## Equality tester

### Description:
Checks the received numbers for equality.

Example:

1. 23@0 is received via `a`
2. 23@0 is received via `b`
3. true@0 is sent via `equal`

### Input ports: 
* a: number

    The first number


* b: number

    The second number


### Output ports: 
* equal: boolean

    Sends true if the received numbers are equal, false otherwise.




## Even tester

### Description:
Tells whether a number is even.

Example:

1. 26@0 is received via `number`
2. true@0 is sent via `even`

### Input ports: 
* number: number

    Number to be tested for evenness.


### Output ports: 
* even: boolean

    Sends true if the input value is even, false otherwise.




## Floor

### Description:
Returns the number rounded down to the nearest integer.

Example:

1. 5.23@0 is received via `number`
2. 5@0 is sent via `floor`

Example (negative number):

1. -1.23@0 is received via `number`
2. -2@0 is sent via `floor`

### Input ports: 
* number: number

    The number to be rounded.


### Output ports: 
* floor: number

    The nearest integer which is less than or equal to the input number.




## Greater or equal than tester

### Description:
Tests whether the value is greater or equal than the reference.

Example:

1. 23@0 is received via `value`
2. 19@0 is received via `reference`
3. true@0 is sent via `greater or equal`

### Input ports: 
* value: number

    The value to test against the reference


* reference: number

    The reference to compare the value with


### Output ports: 
* greater or equal: boolean

    Whether the value is greater or equal than the reference




## Greater than tester

### Description:
Checks if the value received on `value` is greater than the value received on `reference`. If the values are equal, it outputs false.

Example:

1. 20@0 is received via `value`
2. 19@0 is received via `reference`
3. true@0 is sent via `greater`

### Input ports: 
* value: number

    The first operand of the comparison.


* reference: number

    The second operand of the comparison.


### Output ports: 
* is greater: boolean

    Sends true if "a" is greater than "b"




## Less or equal than tester

### Description:
Tests whether the value is less or equal than the reference.

Example:

1. 19@0 is received via `value`
2. 21@0 is received via `reference`
3. true@0 is sent via `less or equal`

### Input ports: 
* value: number

    The value to test against the reference


* reference: number

    The reference to compare the value with


### Output ports: 
* less or equal: boolean

    Whether the value is less or equal than the reference




## Less than tester

### Description:
Checks if the value received via `value` is less than the value received via `reference`. If the values are equal, it outputs false.

Example:

1. 19@0 is received via `value`
2. 23@0 is received via `reference`
3. true@0 is sent via `less`

### Input ports: 
* value: number

    The first operand of the comparison


* reference: number

    The second operand of the comparison


### Output ports: 
* less: boolean

    Sends true if 'a' is less than 'b'.




## Max picker

### Description:
Picks the maximum out of two numbers.

Example:

1. 3@0 is received via `a`
2. 12@0 is received via `b`
3. 12@0 is sent via `max`

### Input ports: 
* a: number

    The first value to pick the max from


* b: number

    The second value to pick the max from


### Output ports: 
* max: number

    Sends the maximum of the provided two values.




## Min picker

### Description:
Picks the minimum out of two numbers.

Example:

1. 12@0 is received via `a`
2. 22@0 is received via `b`
3. 12@0 is sent via `min`

### Input ports: 
* a: number

    The first value to pick the minimum from


* b: number

    The second value to pick the minimum from


### Output ports: 
* min: number

    Sends the minimum of the provided values.




## Modulo

### Description:
Takes modulo of 'a' and 'b'. Bounces synced operands on division by zero.

Example:

1. 10@0 is received via `a`
2. 9@0 is received via `b`
3. 1@0 is sent via `remainder`

### Input ports: 
* a: number

    The divident of the operation.


* b: number

    The divisor of the operation.


### Output ports: 
* remainder: number

    The remainder of the operation.


* bounced: {"a":number,"b":number}

    Sends synced inputs on error.




## Multiplier

### Description:
Multiplies two numbers together.

Example:

1. 2@0 is received via `a`
2. 2@0 is received via `b`
3. 4@0 is sent via `product`

### Input ports: 
* a: number

    The first operand of the multiplication


* b: number

    The second operand of the multiplication


### Output ports: 
* product: number

    Sends the product of the two inputs.




## Odd tester

### Description:
Tells whether a number is odd.

Example:

1. 23@0 is received via `number`
2. true@0 is sent via `odd`

### Input ports: 
* number: number

    Number to be tested for oddness.


### Output ports: 
* odd: boolean

    Sends true if the number is odd, false otherwise.




## Parser

### Description:
Converts a string to number. If the string cannot be converted to number, it will be bounced.

Example:

1. "23.05"@0 is received via `string`
2. 23.05@0 is sent via `number`

### Input ports: 
* string: string

    String input to parse


### Output ports: 
* number: number

    Sends the parsed number if the parsing was successful.


* bounced: string

    Sends the input data if the parsing has failed.




## Power

### Description:
Performs a power arithmetical operation on the inputs. Sends base ^ exponent.

Example:

1. 2@0 is received via `base`
2. 3@0 is received via `exponent`
3. 8@0 is sent via `power`

### Input ports: 
* base: number

    The base operand of the power operation.


* exponent: number

    The exponent operand of the power operation.


### Output ports: 
* power: number

    Sends the power of the provided inputs.




## Random generator

### Description:
Generates a random number, that is greater than or equal to a specified minimum, and less than or equal to the specified maximum value.

Example:

1. 3@0 is received via `min`
2. 19@0 is received via `max`
3. 14@0 is sent via `random`

### Input ports: 
* min: number

    The minimum value


* max: number

    The maximum value


### Output ports: 
* random: number

    Random number




## Rounder

### Description:
Returns the number rounded to the nearest integer.

Example:

1. 1.51@0 is received via `number`
2. 2@0 is sent via `rounded`

Example (negative number):

1. -1.23@0 is received via `number`
2. -1@0 is sent via `rounded`

### Input ports: 
* number: number

    The number to be rounded.


### Output ports: 
* rounded: number

    Sends the nearest integer to the number.




## Stringifier

### Description:
Serializes the given number to a string.

Example:

1. 23.45@0 is received via `number`
2. "23.45"@0 is sent via `string`

### Input ports: 
* number: number

    The number to be converted.


### Output ports: 
* string: string

    Sends the serialized number.




## Subtractor

### Description:
Takes the difference of the value received on `a` and the value received on `b`.

Example:

1. 23@0 is received via `a`
2. 22@0 is received via `b`
3. 1@0 is sent via `diff`

### Input ports: 
* a: number

    The first operand of the subtraction


* b: number

    The second operand of the subtraction


### Output ports: 
* diff: number

    Sends the difference of 'a' from 'b'




## Type tester

### Description:
Tells whether the received value on `data` is a number.

Example (not a number):

1. "some string"@0 is received via `data`
2. false@0 is sent via `is number`

Example (receives a number):

1. 23.23@0 is received via `data`
2. true@0 is sent via `is number`

### Input ports: 
* data: any

    the value to be tested.


### Output ports: 
* is number: boolean

    Sends true if the data is a number, false otherwise.


