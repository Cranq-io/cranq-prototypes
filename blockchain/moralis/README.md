# blockchain/moralis

## Folder upload metadata builder

### Input ports: 
* item URLs: string[]

* item names: string[]

### Output ports: 
* item metadata: {
"image": string,
"name": string,
"description": string
}[]



## Folder uploader

### Description:
Posts upload file data to  https://deep-index.moralis.io/api/v2/ipfs/uploadFolder endpoint

More: 
https://docs.moralis.io/moralis-server/web3-sdk/ipfs-storage-new

Example:
1. [
    {
      "path": "moralis/logo.jpg",
      "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
    }
  ]"@0 received via `folder data`  
2. "ffdfdhdhgdjjhggkjcvxc"@0 received via `API key` 
3. [  :"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/moralis/logo.jpg" 
]@0 sent via `file URLs`

### Input ports: 
* folder data: {
 "path": string,
 "content": 
 string
} []

    Receives moralis post data.
    
    Example:
    [
        {
          "path": "moralis/logo.jpg",
          "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
        }
      ]


* API key: string

    Receives moralis API key.
    
    Example: 
    "ffdfdhdhgdjjhggkjcvxc" 


### Output ports: 
* file URLs: string[]

    Sends file ipfs URLs.
    
    Example:
     [
    "https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/moralis/logo.jpg" 
    ]
    


* error: any



## Image upload data builder

### Input ports: 
* image paths: string[]

### Output ports: 
* image data: {"path": string, "content": string}[]

