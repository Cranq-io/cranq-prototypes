# apis/ga/measurement protocol

## Event params builder

### Description:
Builds raw "event" parameter set for Google Analytics Measurement Protocol request.

### Input ports: 
* tracking ID: any

* client ID: any

* category: any

* action: any

* label: any

* value: any

### Output ports: 
* params: {string: typeof `merged` of `merger`} 

    Measurement Protocol parameters for "event" hit type. Key-value pairs, must be serialized to be passed as payload.




## Event tracker

### Description:
Tracks events via Google Analytics Measurement Protocol.
https://developers.google.com/analytics/devguides/collection/protocol/v1/devguide

### Input ports: 
* tracking ID: any

* client ID: any

* category: any

* action: any

* label: any

* value: any

### Output ports: 
* done: any

* error: any



## Page tracker

### Description:
Tracks page views via Google Analytics Measurement Protocol.
https://developers.google.com/analytics/devguides/collection/protocol/v1/devguide

### Input ports: 
* tracking ID: any

* client ID: any

* hostname: any

* page: any

* title: any

### Output ports: 
* done: any

* error: any



## Pageview params builder

### Description:
Builds raw "pageview" parameter set for Google Analytics Measurement Protocol request.

### Input ports: 
* tracking ID: any

* client ID: any

* hostname: any

* page: any

* title: any

### Output ports: 
* params: any

    Measurement Protocol parameters for "pageview" hit type. Key-value pairs, must be serialized to be passed as payload.


