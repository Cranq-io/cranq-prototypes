# testing

## Array contains asserter

### Input ports: 
* array: any

* item: any

### Output ports: 
* assertion: any



## Assertion builder

### Description:
Builds an assertion record.

### Input ports: 
* success: any

    Receives individual fields for syncing.


* actual: any

    Receives individual fields for syncing.


* expected: any

    Receives individual fields for syncing.


* type: any

### Output ports: 
* assertion: {
  "success": typeof `success`,
  "actual": typeof `actual`,
  "expected": typeof `expected`,
  "type": typeof `type`
}



## Assertion duration getter

### Description:
Determines the time between the start of a test case (or suite) and a specific assertion.

### Input ports: 
* assertion: any

* start: any

### Output ports: 
* duration: any

    In milliseconds




## Case decorator

### Description:
Decorates assertion records with description and duration.

### Input ports: 
* start: any

* description: any

* assertion: any

### Output ports: 
* assertion: any



## Case template

### Input ports: 
* start: any

* description: any

### Output ports: 
* assertion: any



## Current timestamp inserter

### Description:
Inserts current timestamp into an assertion record. 

### Input ports: 
* assertion: {string:any}

### Output ports: 
* assertion: typeof `assertion`



## Description inserter

### Description:
Inserts description into list of descriptions on an assertion record.

### Input ports: 
* assertion: {string:any}

* description: any

### Output ports: 
* assertion: typeof `assertion`



## Dictionary structure asserter

### Input ports: 
* dict: any

* structure: any

* strict: any

### Output ports: 
* assertion: any



## Duration inserter

### Description:
Inserts test duration into a list of durations on an assertion record.

### Input ports: 
* assertion: {string:any}

* duration: any

### Output ports: 
* assertion: typeof `assertion`



## Equality asserter

### Input ports: 
* expected: any

* actual: any

### Output ports: 
* assertion: any



## Even asserter

### Input ports: 
* number: any

### Output ports: 
* assertion: any



## Greater or equal asserter

### Input ports: 
* actual: any

* expected: any

### Output ports: 
* assertion: any



## Greater than asserter

### Input ports: 
* actual: any

* expected: any

### Output ports: 
* assertion: any



## Has key asserter

### Input ports: 
* dict: any

* key: any

### Output ports: 
* assertion: any



## Has keys asserter

### Input ports: 
* dict: any

* keys: any

* strict: any

### Output ports: 
* assertion: any



## Has path asserter

### Input ports: 
* tree: any

* path: any

### Output ports: 
* assertion: any



## Is array asserter

### Input ports: 
* data: any

### Output ports: 
* assertion: any



## Is boolean asserter

### Input ports: 
* data: any

### Output ports: 
* assertion: any



## Is dictionary asserter

### Input ports: 
* data: any

### Output ports: 
* assertion: any



## Is number asserter

### Input ports: 
* data: any

### Output ports: 
* assertion: any



## Is string asserter

### Input ports: 
* data: any

### Output ports: 
* assertion: any



## Less or equal asserter

### Input ports: 
* actual: any

* expected: any

### Output ports: 
* assertion: any



## Less than asserter

### Input ports: 
* actual: any

* expected: any

### Output ports: 
* out: any



## Odd asserter

### Input ports: 
* number: any

### Output ports: 
* out: any



## Same array length asserter

### Input ports: 
* actual: any

* expected: any

### Output ports: 
* assertion: any



## String contains asserter

### Input ports: 
* string: any

* substring: any

### Output ports: 
* assertion: any

