# blockchain/nftport/api v0/utils

## Error detector

### Description:
Detects errors in the JSON response of NFTPort API endpoints.

Example A)
1. {"response": "OK"}@1 received via `data`
2. No output

Example B)
1. {"response": "NOK", "error": "Invalid creator address."}@1 received via `data`
2. {"error": "Invalid creator address."}@1 sent via `error`

### Input ports: 
* data: {"response": ("OK" or "NOK"), "error": string}

    Receives parsed response body from an NFTPort API endpoint.


* status: number

    Receives HTTP status from NFTPort API response.


### Output ports: 
* error: {"error": string}

