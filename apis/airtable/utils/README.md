# apis/airtable/utils

## Attachment object creator

### Input ports: 
* URL: string

### Output ports: 
* attachment: {"url": typeof `URL`}



## Attachment object list creator

### Input ports: 
* file URLs: string[]

### Output ports: 
* attachments: {"url": typeof `file URLs`[number]}[]



## First record extractor

### Description:
Extracts the first record from an AirTable API response.

### Input ports: 
* resp. data: {
  "records": {
    "id": string,
    "createdTime": string,
    "fields": {string: any}
  }
}

    JSON body of the record insertion response from AirTable.


### Output ports: 
* record: typeof `resp. data`["records"][number]["fields"]

* AT record: typeof `resp. data`["records"]

    Record as is sent to / received from the AirTable API.




## Record insert request builder

### Input ports: 
* API key: string

* base ID: string

* table name: string

* AT record: {"fields": {string: any}}

    Record as is sent to / received from the AirTable API.


### Output ports: 
* JSON req.: {
  "method": ("GET" or "POST" or "PUT" or "PATCH" or "DELETE"),
  "url": string,
  "headers": {string: string},
  "data": {
    "records": [typeof `AT record`]
  }
}



## Record to AirTable record converter

### Description:
Converts plain record to an AirTable record.

### Input ports: 
* record: {string: any}

### Output ports: 
* AT record: {"fields": typeof `record`}

    Record as is sent to / received from the AirTable API.




## Record URL builder

### Description:
Builds a URL for record in an AirTable table.

### Input ports: 
* base ID: any

    Receives the ID of an AirTable base.


* table name: string

    Receives a table's identifier relative to an AirTable base.


* record ID: string

    Receives a record's identifier relative to an AirTable table.


### Output ports: 
* URL: string



## Records extractor

### Description:
Extracts all records from an AirTable API response.

### Input ports: 
* resp. data: {
  "records": {
    "id": string,
    "createdTime": string,
    "fields": {string: any}
  }
}

    JSON body of the record insertion response from AirTable.


### Output ports: 
* records: typeof `resp. data`["records"][number]["fields"][]

* AT records: typeof `resp. data`["records"][]

    Record as are sent to / received from the AirTable API.




## Records to AirTable records converter

### Description:
Converts plain list of records (table) to a list of AirTable records.

### Input ports: 
* records: {string: any}[]

### Output ports: 
* AT records: {
  "fields": typeof `records`[number]
}[]

    Records as are sent to / received from the AirTable API.




## Table URL builder

### Description:
Builds a URL for an AirTable table.

### Input ports: 
* base ID: string

    Receives the ID of an AirTable base.


* table name: string

    Receives a table's identifier relative to an AirTable base.


### Output ports: 
* URL: string

