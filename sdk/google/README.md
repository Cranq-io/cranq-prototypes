# sdk/google

## Drive

### Description:
Works with google drive using the googleapis sdk.

### Input ports: 
* action: {
"sessionid" : string, 
"type": ("service_account_auth" or "create_file"), 
"options": {string: any}
}

    Receives the parameters of the google drive base prototype.
    
    Example: 
    {
      "sessionid" : "drive_session",
      "type": "service_account_auth",
      "options": {
         "email" : "email@email.com",
        "keyFile":  null,
         "key": "TopSecretKey!" 
      }
    }


### Output ports: 
* done: any

    Sends the result fo the action.
    
    Example:
    null


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Example:.
    {error: "Something went wrong!"}




## Spreadsheet

### Description:
Works with google spreadsheet using the googleapis sdk.

### Input ports: 
* action: {
"sessionid" : string, 
"type": ("service_account_auth" or "update"), 
"options": {string: any}
}

    Receives the parameters of the google spreadsheet base prototype.
    
    Example: 
    {
      "sessionid" : "drive_session",
      "type": "service_account_auth",
      "options": {
         "email" : "email@email.com",
        "keyFile":  null,
         "key": "TopSecretKey!" 
      }
    }


### Output ports: 
* done: any

    Sends the result fo the action.
    
    Example:
    null


* error: {"error": string}

    Sends the error which happened during the execution of the action.
    
    Example:.
    {error: "Something went wrong!"}


