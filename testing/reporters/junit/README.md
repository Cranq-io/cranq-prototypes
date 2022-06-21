# testing/reporters/junit

## Assertion description splitter

### Input ports: 
* assertion: {string:any}

### Output ports: 
* case name: (typeof `assertion`)[number]

    Last item of the array


* suite name: string



## Assertion inserter

### Description:
Writes temporary assertions into the preprocessed JUnit output.

### Input ports: 
* context: any

### Output ports: 
* context: any



## Assertion recorder

### Description:
Records a single assertion into a preprocessed report JSON.

### Input ports: 
* assertion: any

* assertion ID: any

* pre-report: any

### Output ports: 
* pre-report: any



## Assertions consolidator

### Input ports: 
* pre-report: any

### Output ports: 
* pre-report: any



## Case time consolidator

### Input ports: 
* pre-report: any

### Output ports: 
* pre-report: any



## Case time inserter

### Input ports: 
* context: any

### Output ports: 
* context: any



## Failure inserter

### Input ports: 
* context: (any[] or {string:any})

### Output ports: 
* context: any



## Failure message builder

### Input ports: 
* assertion: any

### Output ports: 
* message: any



## Failures consolidator

### Input ports: 
* pre-report: any

### Output ports: 
* pre-report: any



## HTML report generator (from file)

### Description:
Generates an HTML report of the specified JUnit XML file, and saves it to the specified path.

### Input ports: 
* junit xml path: any

    The path to the JUnit XML file to generate the report for.
    
    Example:
    "C:\\folder\\report.xml"


* report path: any

    The desired report path.
    
    Example:
    "C:\\folder\\report.html"


### Output ports: 
* generated path: any

    Indicates, that the report was generated successfully.


* bounced: any

    Indicates, that the report has failed to generate.




## HTML report generator (from xml)

### Description:
Generates a HTML report of the specified JUnit XML, and saves it to the specified path.

### Input ports: 
* junit xml: any

    The JUnit-format XML content to generate the report for.
    
    Example:
    "<testsuites tests=\"2\" errors=\"0\" failures=\"0\" skipped=\"0\"><testsuite tests=\"2\" errors=\"0\" failures=\"0\" skipped=\"0\" name=\"GET /user/:id - for valid user IDs\" time=\"0.145\"><testcase name=\"should return status 200\" classname=\"should return status 200\" assertions=\"1\"></testcase><testcase name=\"should have &quot;id&quot; field\" classname=\"should have &quot;id&quot; field\" assertions=\"1\"></testcase></testsuite></testsuites>"


* report path: any

    The desired report path.


### Output ports: 
* generated path: any

    Indicates, that the report was generated successfully.


* bounced: any

    Indicates, that the report has failed to generate.




## Report consolidator

### Input ports: 
* pre-report: any

### Output ports: 
* JSON report: any



## Report context builder

### Input ports: 
* assertion ID: any

    Receives individual fields for syncing.


* assertion: any

    Receives individual fields for syncing.


* pre-report: any

    Receives individual fields for syncing.


### Output ports: 
* context: {
  "assertion ID": typeof `assertion ID`,
"assertion": typeof `assertion`,
"pre-report": typeof `pre-report`
}

    The report context identifies an individual assertion by suite ID, case ID, and assertion ID.
    It also contains the preprocessed report and the assertion record.




## Report preprocessor

### Input ports: 
* assertion: any

* delay: any

### Output ports: 
* pre-report: any



## Reporter

### Description:
Compiles a JUnit test result report based on incoming assertions.

### Input ports: 
* assertion: any

    Individual assertion record with properties:
    * type
    * expected
    * actual
    * success
    * description
    * timestamp
    * durations


* delay: any

    Maximum allowed delay between assertions in milliseconds.


### Output ports: 
* xml: any



## Serializer

### Description:
Serializes the JSON object representation of a JUnit report to XML.
Uses https://www.npmjs.com/package/junit-xml. 

### Input ports: 
* json: any

### Output ports: 
* xml: any



## Suite time consolidator

### Input ports: 
* pre-report: any

### Output ports: 
* pre-report: any



## Suite time inserter

### Input ports: 
* context: any

### Output ports: 
* context: any



## Suites consolidator

### Input ports: 
* pre-report: (any[] or {string:any})

### Output ports: 
* pre-report: any



## Test case name inserter

### Input ports: 
* context: any

### Output ports: 
* context: any



## Test cases consolidator

### Input ports: 
* pre-report: any

### Output ports: 
* pre-report: any



## Test suite name inserter

### Input ports: 
* context: any

### Output ports: 
* context: any



## Time node to seconds

### Input ports: 
* pre-report time: {string:any}

### Output ports: 
* seconds: number



## Visualizer

### Description:
Generates a HTML report of the specified JUnit XML, and opens it in the default browser.

### Input ports: 
* junit xml: any

