# apis/airtable

## Bulk records inserter

### Description:
Inserts multiple records into the specified AirTable table.
The input received on parameter `records` must match the target table schema.

Sends records to the AirTable API in batches of 10.

For detailed parameter information, see the AirTable API documentation:
https://airtable.com/api/meta

### Input ports: 
* records: {string: any}[]

    Receives arbitrary number of records to be inserted into AirTable.


* params: {
  "apiKey": string,
  "baseId": string,
  "tableName": string
}

### Output ports: 
* records: typeof `records`

    Sends records that were successfully inserted into AirTable.


* AT records: {
  "id": string,
  "createdTime": string,
  "fields": typeof `records`[number]
}[]

    Sends records that were successfully inserted into AirTable, including metadata like row ID, and date & time of creation.


* responses: {
  "status": number,
  "headers": {string: any},
  "body": string
}[]

    Sends the entire response from the AirTable API without modification.


* error: {
  "error": string,
  optional "details": any
}



## Record deleter

### Description:
Deletes a single record from an AirTable table.

### Input ports: 
* record ID: string

    Receives the identifier of the record relative to an AirTable table.


* params: {
  "apiKey": string,
  "baseId": string,
  "tableName": string
}

### Output ports: 
* data: {
  "deleted": boolean,
  "id": typeof `record ID`
}

* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

    Sends the entire response from the AirTable API without modification.


* error: {
  "error": string,
  optional "details": any
}



## Record fetcher

### Description:
Fetches a single record from an AirTable table.

### Input ports: 
* record ID: string

    Receives the identifier of the record relative to an AirTable table.


* params: {
  "apiKey": string,
  "baseId": string,
  "tableName": string
}

### Output ports: 
* record: {string: any}

    Sends the retrieved AirTable record.


* AT record: {
  "id": string,
  "createdTime": string,
  "fields": {string: any}
}

    Sends the retrieved AirTable record, including metadata like row ID, and date & time of creation.


* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

    Sends the entire response from the AirTable API without modification.


* error: {
  "error": string,
  optional "details": any
}



## Record inserter

### Description:
Inserts a single records into the specified AirTable table.
The input received on parameter `record` must match the target table schema.

For detailed parameter information, see the AirTable API documentation:
https://airtable.com/api/meta

### Input ports: 
* record: {string: any}

    Receives a single record to be inserted into AirTable.


* params: {
  "apiKey": string,
  "baseId": string,
  "tableName": string
}

### Output ports: 
* record: typeof `record`

    Sends the record that was successfully inserted into AirTable.


* AT record: {
  "id": string,
  "createdTime": string,
  "fields": typeof `record`
}

    Sends the record that was successfully inserted into AirTable, including metadata like row ID, and date & time of creation.


* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

    Sends the entire response from the AirTable API without modification.


* error: {
  "error": string,
  optional "details": any
}



## Records deleter

### Input ports: 
* record IDs: string[]

    Receives list of record identifiers relative to an AirTable table.


* params: {
  "apiKey": string,
  "baseId": string,
  "tableName": string
}

### Output ports: 
* data: {
  "deleted": boolean,
  "id": typeof `record IDs`[number]
}[]

* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

    Sends the entire response from the AirTable API without modification.


* error: {
  "error": string,
  optional "details": any
}



## Records insert request builder

### Input ports: 
* base ID: any

* table name: any

* API key: any

* table: any

### Output ports: 
* verb: any

* URL: any

* headers: any

* body: any



## Records inserter

### Description:
Inserts up to 10 records into the specified AirTable table.
The input received on parameter `records` must match the target table schema.

For inserting more than 10 records, or an unknown number of records, use `apis/airtable/Bulk records inserter`.

For detailed parameter information, see the AirTable API documentation:
https://airtable.com/api/meta

### Input ports: 
* records: {string: any}[]

    Receives up to 10 records to be inserted into AirTable.


* params: {
  "apiKey": string,
  "baseId": string,
  "tableName": string
}

### Output ports: 
* records: typeof `records`

    Sends records that were successfully inserted into AirTable.


* AT records: {
  "id": string,
  "createdTime": string,
  "fields": typeof `records`[number]
}[]

    Sends records that were successfully inserted into AirTable, including metadata like row ID, and date & time of creation.


* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

    Sends the entire response from the AirTable API without modification.


* error: {
  "error": string,
  optional "details": any
}



## Records inserter (deprecated)

### Description:
Inserts a list of records into the specified AirTable table.
If the table already contains data, the records are appended.
The input received on parameter `table` must match the target table schema.

For detailed parameter information, see the AirTable API documentation:
https://airtable.com/api/meta

### Input ports: 
* base ID: string

    Receives the AirTable BaseID parameter.


* table name: string

    Receives the table name to insert the records into.


* API key: string

    Receives the API key to authenticate with.


* table: {string: any}[]

    Receives the table of data to insert.


### Output ports: 
* response body: typeof `AirtableResponse`

    Outputs the response from AirTable.


