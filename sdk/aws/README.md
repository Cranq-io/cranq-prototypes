# sdk/aws

## S3

### Description:
Core interface to aws-s3. Use higher level nodes to interact with aws-s3.

### Input ports: 
* action: {
"sessionid": number,
"type": "auth",
"options": {string: any}
}

    Receives the parameters of the action to execute.
    
    Example: 
    {
      "id": "aws-s3",
      "type": "auth",
    "options": {
        "accessKeyId": "ACCESS_KEY_ID",
        "secretAccessKey": "SECRET_ACCES:KEY"
      }
    }


### Output ports: 
* done: any

* error: {
"error": string
}



## S3 authenticator

### Input ports: 
* session id: string

    Receives the id of the S3 session.
    
    Example: 
    "s3-session-id"


* access key id: string

    Receives the AWS user's access key id.
    
    Example:
    "23478207027842073230762374023 "


* secret access key: string

    Receives the AWS user's secret access key.
    
    Example:
    "v3QoTTO2fmr5Wbh/v3QoTTO2fmr5Wbh+ASDF"


### Output ports: 
* done: null

    It is triggered if the authentication was successful.


* error: {"error": string}

    Sends error information in case the authenticatiomn was not successful.




## S3 uploader

### Input ports: 
* session id: string

    Receives the id of the S3 session.
    
    Example: 
    "s3-session-id"


* bucket name: string

    Receives the name of the S3 bucket to upload to.
    
    Example: 
    "buckat-name"


* file name: any

    Receives the name of the file  to be uploaded.
    
    Example: 
    "test.tx"


* file content: any

    Receives the content of the file  to be uploaded.
    
    Example: 
    "test content"


### Output ports: 
* done: {
  "ETag": string,
  "Location": string,
  "key": string,
  "Key": string,
  "Bucket": string
} 

    Sent the data about the successful upload.
    
    Example:
    {
      "ETag": "\"7c36f14325954cd6cf996f8ee1261d56\"",
      "Location": "https://bucket-name.s3.amazonaws.com/test.txt",
      "key": "test.txt",
      "Key": "test.txt",
      "Bucket": "bucket-name"
    } 


* error: {
"error": string
}

