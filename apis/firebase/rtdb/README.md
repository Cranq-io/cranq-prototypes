# apis/firebase/rtdb

## Query context builder

### Description:
Builds a Firebase Realtime Database query context from a Firebase ID token and a database URL (found on the Firebase Realtime Database console) to be passed around among related data querying and manipulation nodes.

### Input ports: 
* ID token: string

    Receives individual fields for syncing.


* DB URL: string

    Receives individual fields for syncing.


### Output ports: 
* sync context-synced: {
  "ID token": typeof `ID token`,
  "DB URL" : typeof `DB URL`
}

    Sends synchronized inputs as a dictionary, indexed by field.


