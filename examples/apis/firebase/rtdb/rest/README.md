# examples/apis/firebase/rtdb/rest

## Login & query

### Description:
Demonstrates basic authentication and querying in a Firebase Realtime Database. Requires an API key and a database URL. (Obtained from the Firebase console's "Project Overview" and "Realtime Database" tabs.)

For the example to work the Firebase project must allow anonymous login and database rules must be set up as follows:

{
  "rules": {
    ".read": false,
    ".write": false,
    "$user_id": {
      ".read": "$user_id === auth.uid",
      ".write": "$user_id === auth.uid"
    }
  }
}

### Input ports: 
* API key: any

* DB URL: any

### Output ports: 
* data: any

    Sends forwarded data.


* error: any

    Sends forwarded data.


