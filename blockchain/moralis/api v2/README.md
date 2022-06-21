# blockchain/moralis/api v2

## NFT data getter

### Description:
Retrieves information of the NFT for the specified contract and token ID using the Moralis API. Also returns the original API response for additional information.

Requires Moralis account.

API key and endpoint documentation can be found at:
https://admin.moralis.io/web3Api

### Input ports: 
* API key: string

* address: string

    Receives the contract address for a token.


* token ID: string

    Receives the identifier of the token in the context of its governing contract.


* params: {
  "chain": ("eth" or "ropsten" or "rinkeby" or "goerli" or "kovan" or "polygon" or "mumbai" or "bsc" or "bsc testnet" or "avalanche" or "avalanche testnet" or "fantom"),
  "format": ("decimal" or "hex"),
  "offset": number,
  "limit": number,
  "order": string,
  "cursor": string
}

    Receives parameters refining the transfers query.
    
    Example:
    {
      "chain": "ropsten"
    }


### Output ports: 
* NFT data: `blockchain/moralis/NFT data`

    Sends a list of NFT transfers as returned by the Moralis API


* response: {"status": number, "headers": {string: string}, "data": `blockchain/moralis/NFT data response`}

    Sends the entire response from the Moralis API, including status and header.


* error: {"error": string}



## NFT transfers lister

### Description:
Retrieves a list of transfers matching the specified contract address and token ID using the Moralis API. Also returns the original API response for additional information.

Requires Moralis account.

API key and endpoint documentation:
https://docs.moralis.io/introduction/readme

### Input ports: 
* API key: string

    Receives the Moralis API key.


* address: string

    Receives the contract address for a token.


* token ID: string

    Receives the identifier of the token in the context of its governing contract.


* params: {
  "chain": ("eth" or "ropsten" or "rinkeby" or "goerli" or "kovan" or "polygon" or "mumbai" or "bsc" or "bsc testnet" or "avalanche" or "avalanche testnet" or "fantom"),
  "format": ("decimal" or "hex"),
  "offset": number,
  "limit": number,
  "order": string,
  "cursor": string
}

    Receives parameters refining the transfers query.
    
    Example:
    {
      "chain": "ropsten"
    }


### Output ports: 
* transfers: `blockchain/moralis/NFT transfer`[]

    Sends a list of NFT transfers as returned by the Moralis API


* response: {"status": number, "headers": {string: string}, "data": `blockchain/moralis/NFT transfers response`}

    Sends the entire response from the Moralis API, including status and header.


* error: {"error": string}

