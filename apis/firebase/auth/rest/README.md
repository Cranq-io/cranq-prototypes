# apis/firebase/auth/rest

## Anonymous login

### Description:
Logs in a Firebase user anonymously.

Anonymous authentication must be enabled for the relevant Firebase Project.

### Input ports: 
* API key: any

### Output ports: 
* ID token: any

* user ID: any

* error: any

* auth context: any

    idToken
    email
    refreshToken
    expiresIn
    localId




## Email login

### Description:
Logs in a Firebase user by their email & password.

User must be signed up, and email authentication must be enabled for the relevant Firebase Project.

### Input ports: 
* API key: any

* email: any

* password: any

### Output ports: 
* ID token: any

* user ID: any

* error: any

* auth context: any

    idToken
    email
    refreshToken
    expiresIn
    localId
    registered




## Request dispatcher

### Input ports: 
* action: any

    Identifies account action in the Google Identity Toolkit API.
    
    Possible values:
    
    "signInWithCustomToken"
    "signUp"
    "signInWithPassword"
    "signInWithIdp"
    "createAuthUri"
    "sendOobCode"
    "resetPassword"
    "update"
    "lookup"
    "delete"


* API key: any

* data: any

### Output ports: 
* ID token: any

* user ID: any

* error: any

* auth context: any

