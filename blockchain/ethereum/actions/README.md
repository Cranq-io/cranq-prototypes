# blockchain/ethereum/actions

## Contract compiler & deployer

### Description:
Compiles and deploys a smart contract

### Input ports: 
* state: any

* params: { 
  "compile-contract": typeof `params` of `compile contract`,
  "deploy-contract": typeof `params` of `deploy contract`,
"prepare-verify-contract-params": typeof `mapping` of `prepare verify contract params`,
"verify-contract": typeof `params` of `verify contract`
}

### Output ports: 
* state: typeof `state`



## Contract dependencies installer

### Input ports: 
* state: any

* params: {
  "init-package": typeof `params` of `initialize package`,
  "install-hardhat": typeof `params` of `install Hardhat`,
  "install-dotenv": typeof `params` of `install dotenv`,
  "install-ether": typeof `params` of `install ether.js`,
  "install-contracts": typeof `params` of `install contracts`
}

### Output ports: 
* state: typeof `state`



## Contract file creator

### Description:
Creates the smart contract as file based on the parameters.

### Input ports: 
* params: {
  "cwd": string,
  "contract": "single-nft",
  "single-nft": { 
    "contract-name": string,
    "token-name": string,
    "token-symbol": string
  },
  "result-path": string,
  "message": string
}

    {
      "cwd": string, // the working directory
      "contract": "single-nft", // the contract type
      "single-nft": {  // the parameters specific to the contract type
        "contract-name": string,
        "token-name": string,
        "token-symbol": string
      },
      "result-path": string, // the path in the state to write the result to
      "message": string // the message to print on the console
    }


* state: any

    Receives script state.


### Output ports: 
* state: any

    Sends updated script state.




## Contract files creator

### Input ports: 
* state: any

* params: {
  "write-api-url": typeof `params` of `API URL -> .env`,
  "write-private-key": typeof `params` of `private key -> .env`,
  "create-hardhat-config": typeof `params` of `create hardhat config`,
  "create-contract": typeof `params` of `create contract`,
  "prepare-write-deploy-params": typeof `mapping` of `prepare write deploy params`,
  "write-deploy": typeof `params` of `create deploy script`
}

### Output ports: 
* state: typeof `state`



## Contract folder structure creator

### Input ports: 
* state: any

* params: {
  "create-working-folder": typeof `params` of `create working folder`,
  "create-contract-folder": typeof `params` of `create "contracts" folder`,
  "create-scripts-folder": typeof `params` of `create "scripts" folder`
}

### Output ports: 
* state: typeof `state`



## Contract verifier

### Input ports: 
* state: any

    Receives script state.


* params: {
"contract-address": string,
"cwd": string,
"result-path": string,
"message": string
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Contract verifier error handler

### Input ports: 
* error: any

    Receives the data to be forwarded to either output.


* command busy: any

    The "busy" signal of a `system/Command runner` node.


### Output ports: 
* retry: typeof `on true` of `trial left?`

    Sends signal received via `data` when condition was true.


* success: boolean



## Deploy script creator

### Description:
Creates the deploy script to deploy the contract using Hardhat.

### Input ports: 
* params: {
  "cwd": string,
  "path": string,
  "contract-name": string,
  "result-path": string,
  "message": string
}

    {
      "cwd": string, // the working directory
      "path": string, // the path to write the deploy script to
      "contract-name": string, // the name of the contract to deploy
      "result-path": string, // the path in the state to write the result to
      "message": string // the message to print on the console
    }


* state: any

    Receives script state.


### Output ports: 
* state: any

    Sends updated script state.




## Deploy script runner

### Input ports: 
* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "network": string,
  "regex": string
}

* state: any

    Receives script state.


### Output ports: 
* state: any

    Sends updated script state.




## Hardhat config file creator

### Description:
Creates config file for Hardhat based on the parameters.

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "path": string,
  "network": string,
  "result-path": string,
  "message": string
}

### Output ports: 
* state: any

    Sends updated script state.




## Mint script creator

### Input ports: 
* state: any

* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "contract-address": string,
  "contract-name": string,
  "token-uri": string,
  "create-file": string
}

### Output ports: 
* state: typeof `state`



## Minting dependencies installer

### Input ports: 
* state: any

* params: {
  "install-web3": typeof `params` of `install web3`,
  "install-dotenv": typeof `params` of `install dotenv`
}

### Output ports: 
* state: typeof `state`



## Minting files creator

### Input ports: 
* state: any

* params: {
  "write-api-url": typeof `params` of `API URL -> .env`,
  "write-private-key": typeof `params` of `private key -> .env`,
  "write-public-key": typeof `params` of `public key -> .env`,
  "create-mint-script": typeof `params` of `create "mint-nft.js"`
}

### Output ports: 
* state: typeof `state`



## Minting finish listener (simplified)

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string
}

### Output ports: 
* state: typeof `state`

    Forwards script state.




## NFT minter

### Input ports: 
* state: any

* params: {
  "install-dependencies": typeof `params` of `install dependencies`,
  "create-files": typeof `params` of `create files`,
  "run-script": typeof `params` of `run mint script`
}

### Output ports: 
* state: typeof `state`



## NFT minter (simplified)

### Input ports: 
* state: any

* params: {
  "cwd": string,
  "wallet-private-key": string,
  "wallet-public-key": string,
  "api-key": string,
  "token-uri": string,
  "contract-address": string,
  "contract-name": string
}

### Output ports: 
* state: typeof `state`



## Smart contract deployer

### Input ports: 
* state: any

* params: { 
  "create-folders": typeof `params` of `prepare folder structure`,
  "install-dependencies": typeof `params` of `install dependencies`,
  "create-files": typeof `params` of `create files`,
  "deploy-contract": typeof `params` of `compile & deploy contract`
}

### Output ports: 
* state: typeof `state`

    Example: 
    {
      "working-folder-created": true,
      "hardhat": {
        "contracts-folder-created": true,
        "scripts-folder-created": true,
        "installed": true,
        "config-created": true,
        "deploy-script-created": true,
        "contract-compiled": true,
        "contract-deployed": "0xC6041039D24BF7BC467Ee51423347d6015bdC68C"
      },
      "npm": {
        "package-initialized": true
      },
      "dotenv": {
        "installed": true
      },
      "etherjs": {
        "installed": true
      },
      "openzeppelin": {
        "contracts": {
          "installed": true
        }
      },
      ".env": {
        "alchemy": {
          "api-url-written": true
        },
        "metamask": {
          "private-key-written": true
        }
      },
      "blockchain": {
        "erc721": {
          "contract": {
            "contract-created": "My_Test_NFT_Contract"
          }
        }
      }
    } @start




## Smart contract deployer (simplified)

### Description:
Creates and deploys an Ethereum smart contract based on the parameters.
Using Alchemy to interact with the Ethereum network.

Example:
1. 

### Input ports: 
* state: any

* params: {
  "cwd": string,
  "wallet-private-key": string,
  "api-key": string,
  "etherscan-api-key": string,
  "blockchain": "ethereum",
  "blockchain-network": "string",
  "contract": "single-nft",
  "single-nft": { 
    "contract-name": string,
    "token-name": string,
    "token-symbol": string
  }
}

    Parameters for smart contract creation and deployment:
    
    {
      "cwd": string, // the working directory
      "wallet-private-key": string, // the private key of your Ethereum wallet
      "api-key": string, // the api key of your app on Alchemy used to interact with the Ethereum network
      "contract": "single-nft", // the contract type (only "single-nft" at the moment)
      "single-nft": {  // parameters corresponding to the requested contract type
        "contract-name": string,
        "token-name": string,
        "token-symbol": string
      }
    }


### Output ports: 
* state: typeof `state`

    Example:
    
    {
      "working-folder-created": true,
      "hardhat": {
        "contracts-folder-created": true,
        "scripts-folder-created": true,
        "installed": true,
        "config-created": true,
        "deploy-script-created": true,
        "contract-compiled": true,
        "contract-deployed": "0xC6041039D24BF7BC467Ee51423347d6015bdC68C"
      },
      "npm": {
        "package-initialized": true
      },
      "dotenv": {
        "installed": true
      },
      "etherjs": {
        "installed": true
      },
      "openzeppelin": {
        "contracts": {
          "installed": true
        }
      },
      ".env": {
        "alchemy": {
          "api-url-written": true
        },
        "metamask": {
          "private-key-written": true
        }
      },
      "blockchain": {
        "erc721": {
          "contract": {
            "contract-created": "My_Test_NFT_Contract"
          }
        }
      }
    } @start


