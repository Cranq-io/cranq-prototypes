# examples/api testing/junit reporter

## Authenticator

### Input ports: 
* start: any

### Output ports: 
* token: string



## ID field test

### Input ports: 
* description: any

* user: any

### Output ports: 
* assertion: any



## JUnit reporter example

### Input ports: 
* start: any

### Output ports: 
* JUnit XML: any



## Status 200 test

### Input ports: 
* description: any

* status: any

### Output ports: 
* assertion: any



## User endpoint tests

### Input ports: 
* description: any

* token: any

### Output ports: 
* assertion: any



## User record fetcher

### Input ports: 
* token: any

### Output ports: 
* user: (typeof `value` of `item getter`)[string]

* status: any



## Valid user ID tester

### Input ports: 
* description: any

* token: any

### Output ports: 
* assertion: any

