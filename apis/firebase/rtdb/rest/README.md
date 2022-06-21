# apis/firebase/rtdb/rest

## Data pusher

### Description:
Adds a new data entry to a Firebase Realtime Database under 'parent path'.
Returns the path of the new entry.

### Input ports: 
* query context: any

    idToken
    dbUrl


* parent path: any

    Identifies parent data entry that will contain the new entry.
    
    type: string[]


* data: any

### Output ports: 
* path: any

    Identifies data actually written.
    
    type: string[]


* data: any

* error: any

* query context: any

    idToken
    dbUrl




## Data reader

### Description:
Reads the data entry identified by 'path', from a Firebase Realtime Database.

### Input ports: 
* query context: any

    idToken
    dbUrl


* path: any

    Identifies data entry to be read.
    
    type: string[]


### Output ports: 
* data: any

* error: any

* query context: any

    idToken
    dbUrl




## Data remover

### Description:
Removes the data entry identified by 'path', from a Firebase Realtime Database.

### Input ports: 
* query context: any

    idToken
    dbUrl


* path: any

    Identifies data entry to be deleted.
    
    type: string[]


### Output ports: 
* done: any

* error: any

* query context: any

    idToken
    dbUrl




## Data updater

### Description:
Updates multiple data entries (fields) under 'path', in a Firebase Realtime Database.

### Input ports: 
* query context: any

    idToken
    dbUrl


* path: any

    Identifies data entry to be updated.
    
    type: string[]


* data: any

### Output ports: 
* data: any

* error: any

* query context: any

    idToken
    dbUrl




## Data writer

### Description:
Creates or replaces a data entry  identified by 'path', in a Firebase Realtime Database.

### Input ports: 
* query context: any

    idToken
    dbUrl


* path: any

    Identifies data entry to be written.
    
    type: string[]


* data: any

### Output ports: 
* data: any

* error: any

* query context: any

    idToken
    dbUrl




## Request dispatcher

### Description:
Dispatches an HTTP request for running a query in a Firebase Realtime Database via its REST API.

https://firebase.google.com/docs/reference/rest/database

### Input ports: 
* query context: any

    idToken
    dbUrl


* method: any

    HTTP method as required by the Firebase Realtime Database REST API.
    
    https://firebase.google.com/docs/reference/rest/database


* path: any

    Identifies data entry that the query will interact with.


* data: any

    Data to be sent via the HTTP request. Usually data to be set or updated.


### Output ports: 
* data: {string:any}

* error: string

* query context: any

    idToken
    dbUrl




## URL builder

### Input ports: 
* query context: any

    idToken
    dbUrl


* path: any

### Output ports: 
* URL: any

