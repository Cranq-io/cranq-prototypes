# sdk/google/drive

## Authenticated spreadsheet creator

### Description:
Authenticates the service user and creates new spreadsheet on the given shared folder.

Example:
1. `session Id` receives "drive_session"@0 
2. `auth data` receives {
  "email": "email@email.com",
  "key": "TopSecretKey!"
}@0 
3. `create spreadsheet data` receives {
  "file meta data": {
    "name": "Test!",
    "driveId": "0AFITUOLHhs3T_ID",
    "corpora": "drive",
    "parents": [
      "1_ghBRrDju9oMNSy8DqqNtOEfDRIVE_Id"
    ]
  },
  "supports all drives": true
}@0
4. `done` sends {"fileid": "1_ewweewweFileID"}@0 

### Input ports: 
* session Id: string

    Receives the session id of the drive action.
    
    Example: 
    "drive_session"


* auth data: {
  "email": string,
  "key": string
}

    Receives the authentication data of service account.
    
    Example: 
    {
      "email": "email@email.com",
      "key": "TopSecretKey!"
    }
    


* create spreadsheet data: {
   "file meta data": {string:any},
   "supports all drives": boolean
}

    Receives the data of the spreadsheet.
    
    
    Example:
    {
      "file meta data": {
        "name": "Test!",
        "driveId": "0AFITUOLHhs3T_ID",
        "corpora": "drive",
        "parents": [
          "1_ghBRrDju9oMNSy8DqqNtOEfDRIVE_Id"
        ]
      },
      "supports all drives": true
    }
    


### Output ports: 
* done: {"fileid": string}

    Sends the generated fileid.
    
    Eg.
    {"fileid": "1_ewweewweFileID"}


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Example:.
    {error: "Something went wrong!"}




## Authenticator

### Description:
Authenticates the service user to use google drive.

Example:
1. `session Id` receives "drive_session"@0 
2. `email` receives  "email@email.com"@0
3. `key` receives "TopSecretKey"@0
4. `done` sends null@0 

### Input ports: 
* session Id: string

    Receives the session id of the drive action.
    
    Example: 
    "drive_session"


* email: string

    Receives the email address of the service account.
    
    Example: 
    "email@email.com"


* key: string

    Receives the private key of the service account.
    
    Example: 
    "TopSecretKey!"


### Output ports: 
* done: null

    Sends null if the action was successful.
    
    Example:
    null


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Example:.
    {error: "Something went wrong!"}




## File creator

### Description:
Creates file on the given shared folder.

Example:
1. `session Id` receives "drive_session"@0 
2. `file meta data` receives  {
  "name": "Test from CRANQ dynamic",
  "parents": [
    "FOLDER_ID"
  ]
  "mimeType": "application/vnd.google-apps.spreadsheet"
}@0
3. `supports all drives` receives false@0
4. `done` sends {"fileid": "1_ewweewweFileID"}@0 

### Input ports: 
* session Id: string

    Receives the session id of the drive action.
    
    Example: 
    "drive_session"


* file meta data: {string:any}

    Receives the metadata of the file creation.
    
    Example in case of shared drive:
    
    {
      "name": "Test from CRANQ dynamic",
      "driveId": "0AFITUOLHhs3TUk9PVA",
      "corpora": "drive",
      "parents": [
        "FOLDER_ID"
      ],
      "mimeType": "application/vnd.google-apps.spreadsheet"
    }
    
    
    Example in case of shared folder:
    
    {
      "name": "Test from CRANQ dynamic",
      "parents": [
        "FOLDER_ID"
      ]
      "mimeType": "application/vnd.google-apps.spreadsheet"
    }
    


* supports all drives: boolean

    Receives `supportsAllDrives` parameter whether create should support both drives and shared drives.
    
    Example: 
    "true"


### Output ports: 
* done: {"fileid": string}

    Sends the result fo the action.
    
    Eg.
    {"fileid": "1_ewweewweFileID"}


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Eg.
    {error: "Something went wrong!"}




## Spreadsheet creator

### Description:
Creates new spreadsheet on the given shared folder.

Example:
1. `session Id` receives "drive_session"@0 
2. `file meta data` receives  {
  "name": "Test from CRANQ dynamic",
  "parents": [
    "FOLDER_ID"
  ]
}@0
3. `supports all drives` receives false@0
4. `done` sends {"fileid": "1_ewweewweFileID"}@0 

### Input ports: 
* session Id: string

    Receives the session id of the drive action.
    
    Example: 
    "drive_session"


* file meta data: {string:any}

    Receives the metadata of the spreadsheet creation.
    
    Example in case of shared drive:
    
    {
      "name": "Test from CRANQ dynamic",
      "driveId": "0AFITUOLHhs3TUk9PVA",
      "corpora": "drive",
      "parents": [
        "FOLDER_ID"
      ]
    }
    
    
    Example in case of shared folder:
    
    {
      "name": "Test from CRANQ dynamic",
      "parents": [
        "FOLDER_ID"
      ]
    }


* supports all drives: boolean

    Receives `supports all drives` parameter whether create should support both drives and shared drives.
    
    Example: 
    "true"


### Output ports: 
* done: {"fileid": string}

    Sends the result of the action.
    
    Eg.
    {"fileid": "1_ewweewweFileID"}


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Eg.
    {error: "Something went wrong!"}


