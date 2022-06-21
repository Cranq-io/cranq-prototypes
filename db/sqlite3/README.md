# db/sqlite3

## Closer

### Description:
Closes the specified SQLite database.

### Input ports: 
* params: {
  "db-id": string
}

### Output ports: 
* done: null

* error: string



## Closer (deprecated)

### Description:
Closes the specified SQLite database.

### Input ports: 
* DB ID: any

### Output ports: 
* done: any

* error: any

* DB ID: any



## Executor

### Description:
Executes all queries in the received SQL script.

### Input ports: 
* params: {
  "dbId": string,
  "sql": string
}

### Output ports: 
* done: null

* error: string



## Opener

### Description:
Opens the specified SQLite database.
Mode is normally 6.
(More on modes: https://www.sqlite.org/c3ref/c_open_autoproxy.html)

### Input ports: 
* params: {
  "dbId": string,
  "filename": string,
  "mode": number
}

### Output ports: 
* done: null

* error: string



## Opener (deprecated)

### Description:
Opens the specified SQLite database.
Mode is normally 6.
(More on modes: https://www.sqlite.org/c3ref/c_open_autoproxy.html)

### Input ports: 
* DB ID: any

* file name: any

* mode: any

### Output ports: 
* done: any

* error: any

* DB ID: any



## Opener-creator

### Description:
Opens the specified SQLite database. When the database doesn't exist, creates it and runs the specified SQL script to create tables.

### Input ports: 
* params: {
  "dbId": string,
  "filename": string,
  "initSql": string
}

### Output ports: 
* done: null

* error: string



## Row getter

### Description:
Retrieves a single row from the specified database.

### Input ports: 
* DB ID: any

* SQL: any

* params: any

### Output ports: 
* row: any

* error: any

* DB ID: any



## Row iterator

### Description:
Retrieves multiple rows one by one from the specified database.

### Input ports: 
* DB ID: any

* SQL: any

* params: any

### Output ports: 
* row: any

* done: any

* error: any

* DB ID: any



## Rows getter

### Description:
Retrieves multiple rows as a single array from the specified database.

### Input ports: 
* params: {
  "dbId": string,
  "sql": string,
  optional "params": (string or number)[]
}

### Output ports: 
* data: {string: any}[]

* done: null

* error: string



## Rows getter (deprecated)

### Description:
Retrieves multiple rows as a single array from the specified database.

### Input ports: 
* DB ID: any

* SQL: any

* params: any

### Output ports: 
* rows: any

* error: any

* DB ID: any



## Runner

### Description:
Runs a single SQL statement on the specified SQLite database, with the specified parameters.

Further on SQLite3 syntax:
https://www.sqlite.org/syntax.html

### Input ports: 
* params: {
  "db-id": string,
  "sql": string,
  optional "params": (string or number)[]
}

### Output ports: 
* done: string

* last ID: string

* changes: number

* error: string



## Runner (deprecated)

### Description:
Runs a single SQL statement on the specified SQLite database, with the specified parameters.

### Input ports: 
* DB ID: any

* SQL: any

* params: any

### Output ports: 
* done: any

* last ID: any

* changes: any

* error: any

* DB ID: any



## Sqlite3

### Description:
Generic SQLite 3 integration node.
This is an internal node. Use specific SQLite nodes instead.

### Input ports: 
* action: {
  "id": string,
  "type": ("open" or "run" or "get" or "all" or "each" or "close"),
  "options":{
    "sql": string,
    optional "options": {string: any}
  }
}

### Output ports: 
* data: any

* done: null

* error: string

