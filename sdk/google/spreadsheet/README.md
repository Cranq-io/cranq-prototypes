# sdk/google/spreadsheet

## Authenticated spreadsheet value updater

### Description:
Authenticates the service user and  updates dedicated spreadsheet.

Example:
1. `session Id` receives "spreadsheet_session"@0 
2. `auth data` receives {
  "email": "email@email.com",
  "key": "TopSecretKey!"
}@0 
3. `spreadsheet Id` "1_ewweewweFileID"@0
4. `update data` receives {
  "update meta data": {
    "range": "Sheet1!A1:B10"
  },
  "values": [
    ["A1 value", "B1 value"],
    ["A2 value", "B2 value"]
  ]
}}@0 
5. `done` sends null@0 

### Input ports: 
* session Id: string

    Receives the session id of the spreadsheet action.
    
    Example: 
    "spreadsheet_session"


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
    


* spreadsheet Id: string

    Receives the id of the spreadsheet to be updated.
    
    Example:
    "1_ewweewweFileID"


* update data: {
  "update meta data": {   string: any},
  "values": any[][]
}

    {
      "update meta data": {
        "range": "Sheet1!A1:B10"
      },
      "values": [
        ["A1 value", "B1 value"],
        ["A2 value", "B2 value"]
      ]
    }


### Output ports: 
* done: null

    Sends null if the action was successful.
    
    Example:
    null


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Example:.
    {error: "Something went wrong!"}




## Authenticator

### Description:
Authenticates the service user to use google spreadsheet drive.

Example:
1. `session Id` receives "spreadsheet_session"@0 
2. `email` receives  "email@email.com"@0
3. `key` receives "TopSecretKey"@0
4. `done` sends null@0 

### Input ports: 
* session Id: string

    Receives the session id of the spreadsheet action.
    
    Example: 
    "spreadsheet_session"


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




## Spreadsheet creator

### Description:
Creates google spreadsheet on the given drive/folder.

Example:
1. `auth data` receives {
  "email": "email@email.com",
  "key": "TopSecretKey!"
}@0 
2. `drive data` {
  "file meta data": {
    "name": "Test!",
    "driveId": "0AFITUOLHhs3T_ID",
    "corpora": "drive",
    "parents": [
      "1_ghBRrDju9oMNSy8DqqNtOEfDRIVE_Id"
    ]
  },
  "supports all drives": true
}"@0
3. `spreadsheet data` receives {
  "update meta data": {
    "range": "Sheet1!A1:B10"
  },
  "values": [
    ["A1 value", "B1 value"],
    ["A2 value", "B2 value"]
  ]
}}@0 
4. `done` sends null@0 

### Input ports: 
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


* drive data: {
   "file meta data": {string:any},
   "supports all drives": boolean
}

    Receives the data of the drive where the spreadsheet is stored.
    
    
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


* spreadsheet data: {
  "update meta data": {   string: any},
  "values": any[][]
}

    Receives the spreadsheet metadata.
    
    {
      "update meta data": {
        "range": "Sheet1!A1:B10"
      },
      "values": [
        ["A1 value", "B1 value"],
        ["A2 value", "B2 value"]
      ]
    }
    


### Output ports: 
* done: null

    Sends null if the action was successful.
    
    Example:
    null


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Example:.
    {error: "Something went wrong!"}




## Spreadsheet value updater

### Description:
Writes data to a single range of  a given spreadsheet.

Example:
1. `session Id` receives "spreadsheet_session"@0 
2. `spreadsheet Id` receives "1_ewweewweFileID"@0
3. `update meta data` receives {
 "range": "Sheet1!A1:B10"",
 "valueInputOption": "RAW" 
}@0
4. `done` sends null@0 

### Input ports: 
* session Id: string

    Receives the session id of the spreadsheet action.
    
    Example: 
    "spreadsheet_session"


* spreadsheet Id: string

    Receives the id of the spreadsheet to be updated.
    
    Example:
    "1_ewweewweFileID"


* update meta data: {
"range": string,
"valueInputOption": ("RAW" or "USER_ENTERED")
}

    Receives the metadata of the update values.
    
    range: The A1 notation of the values to update. More: 
    https://developers.google.com/sheets/api/guides/concepts
    
    valueInputOption: Determines how input data should be interpreted. More: https://developers.google.com/sheets/api/reference/rest/v4/ValueInputOption
    
    Example:
    {
     "range": "Sheet1!A1:B10"",
     "valueInputOption": "RAW" 
    }


* values: any[][]

    Receives the new cell values to update.
    It contains arrays of the row values.
    
    Example:
    [
      ["A1 value", "B1 value"],
      ["A2 value", "B2 value"]
    ]


### Output ports: 
* done: null

    Sends null if the action was successful.
    
    Example:
    null


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Example:.
    {error: "Something went wrong!"}


