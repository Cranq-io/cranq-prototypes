# blockchain/nftport/api v0

## Counterfeit NFT finder with token ID

### Description:
Retrieves list of duplicate (i.e. counterfeit) NFTs. 

Requires NFTPort account.

https://docs.nftport.xyz/docs/nftport/b3A6MjQ1OTQxMDc-find-counterfeit-nf-ts-w-token-id

### Input ports: 
* API key: string

    Receives the NFTPort API key.


* contract address: string

    Receives the address of the NFT.


* token ID: any

    Receives the token ID of the NFT.


* params: { 
  optional "chain": ("ethereum" or "polygon"),
  optional "page_number": number,
  optional "page_size": number,
  optional "threshold": number
}

    Receives parameters that customize the result NFT list.
    
    https://docs.nftport.xyz/docs/nftport/b3A6MjQ1OTQxMDc-find-counterfeit-nf-ts-w-token-id#request-body


### Output ports: 
* similar NFTs: `blockchain/nftport/api v0/SimilarNft`[]

* error: {"error": string}

* response: any



## Counterfeit NFT URL finder with token ID

### Description:
Retrieves list of file URLs for duplicate (i.e. counterfeit) NFTs.

Requires NFTPort account.

https://docs.nftport.xyz/docs/nftport/b3A6MjQ1OTQxMDc-find-counterfeit-nf-ts-w-token-id

### Input ports: 
* NFT ID: {
  "contractAddress": string,
  "tokenId": string
}

* params: {
  "apiKey": string,
  optional "chain": ("ethereum" or "polygon"),
  optional "page_number": number,
  optional "page_size": number,
  optional "threshold": number
}

### Output ports: 
* file URLs: string[]

* error: {"error": string}



## Created NFT lister

### Description:
Retrieves a list of NFTs created by the specified address, using the NFTPort API.

Requires NFTPort account.

https://docs.nftport.xyz/docs/nftport/b3A6MzA2ODYzMjM-retrieve-nf-ts-created-by-an-account

### Input ports: 
* API key: string

    Receives the NFTPort API key.


* creator address: string

    Receives the address of the NFT creator.


* params: {
  "chain": "ethereum",
  "continuation": string,
  "include": ("default" or "metadata"),
  "page_size": number
}

    Receives parameters that customize the result NFT list.
    
    https://docs.nftport.xyz/docs/nftport/b3A6MzA2ODYzMjM-retrieve-nf-ts-created-by-an-account#Query-Parameters


### Output ports: 
* nfts: `blockchain/nftport/api v0/CreatorNft`[]

    Sends the list of NFTs associated with a given creator.


* response: any

* error: {
  "error": {
    "response": string,
    "error": {
      "status_code": number,
      "code": string,
      "message": string
    }
  }
}



## GET request dispatcher

### Description:
Dispatches a GET request to one of the NFTPort API endpoints.

### Input ports: 
* API key: string

* URL: string

    [Inherited from port `url` of `dispatch request`] 
    Receives the target of the HTTP request. Also called "resource" 
    
    Example:
    "https://jsonplaceholder.typicode.com/todos/1"


### Output ports: 
* data: any

* error: {"error": string}

* response: typeof `response` of `dispatch request`

    Sends the reconstructed HTTP response.




## NFT details getter

### Input ports: 
* API key: string

* contract address: string

* token ID: string

* params: {
  optional "chain": ("ethereum" or "polygon"),
  optional "refresh_metadata": boolean
}

### Output ports: 
* NFT: {
  "chain": ("ethereum" or "polygon"),
  "contract_address": string,
  "token_id": string,
  "metadata_url": string,
  "metadata": {
    "attributes": {"trait_type": string, "value": string}[],
    "description": string,
    "external_url": string,
    "image": string,
    "name": string,
    "properties": {string: any}
  },
  "file_information": {string: any},
  "file_url": string,
  "cached_file_url": string,
  "mint_date": string,
  "updated_date": string
}

* response: {
"status": number,
"headers": {string: string},
"body": any
}

* error: {"error": string}



## NFT transaction lister by contract

### Description:
Retrieves a list of transfers matching the specified contract address and token ID using the NFTPort API. Also returns the original API response for additional information.

Requires NFTPort account.

API key and endpoint documentation:
https://docs.nftport.xyz/docs/nftport/b3A6MzAxNDQ3NzY-retrieve-transactions-by-contract

### Input ports: 
* API key: string

    Receives the NFTPort API key.


* address: string

    Receives the contract address for a token.


* params: {
  "chain": "ethereum",
  "continuation": string,
  "include": ("default" or "metadata"),
  "page_size": number
}

    Receives parameters that customize the result transfer list.
    
    https://docs.nftport.xyz/docs/nftport/b3A6MzAxNDQ3NzY-retrieve-transactions-by-contract#Query-Parameters


* token ID: string

    Receives the identifier of the token in the context of its governing contract.


### Output ports: 
* transactions: `blockchain/nftport/NFT transaction`[]

* error: {"error": string}

* response: {"status": number, "headers": {string: string}, "data": `blockchain/nftport/NFT transactions by contract response`}



## POST request dispatcher

### Description:
Dispatches a POST request to one of the NFTPort API endpoints.

### Input ports: 
* API key: string

    Receives the NFT port API key.


* URL: string

    Receives the target NFT port endpoint.
    


* data: {string:any}

    Receives the post data.


### Output ports: 
* data: any

* error: {"error": string}

* response: typeof `response` of `dispatch request`

    Sends the reconstructed HTTP response.




## Request dispatcher

### Description:
Dispatches a POST request to one of the NFTPort API endpoints.

### Input ports: 
* API key: string

    Receives the NFT port API key.


* URL: string

    Receives the target NFT port endpoint.
    


* body: string

    Receives the post data.


* method: any

### Output ports: 
* data: any

* error: {"error": string}

* response: typeof `response` of `rebuild response`

    Sends the reconstructed HTTP response.


