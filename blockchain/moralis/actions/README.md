# blockchain/moralis/actions

## Bulk auto-metadata uploader

### Description:
Builds and uploads images meta data and stores the ipfs URLs in the state.

Example:
1. {
  "image-names": [
    "logo.jpg"
  ],
  "image-paths": [
    "nft\\batch-images\\logo.jpg"
  ],
  "image-upload-data": [
    {
      "path": "nft\\batch-images\\logo.jpg",
      "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
    }
  ],
  "image-urls": [
	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
  ]
}@ received via `state`
2. {
  "build-data": {
    "cwd": "./nft",
    "result-path": "ipfs.image-metadata",
    "message": "Building metadata for images...",
    "image-urls": [],
    "image-names": []
  },
  "upload": {
    "params": {
      "cwd": "./nft",
      "result-path": "ipfs.metadata-urls",
      "message": "Uploading metadata to IPFS...",
      "api-key": "API_KEY"
    },
    "mapping": {
      "folder-upload-data": "ipfs.image-metadata"
    }
  }
}@0 received via params
3. {
  "image-names": [
    "logo.jpg"
  ],
  "image-paths": [
    "nft\\batch-images\\logo.jpg"
  ],
  "image-upload-data": [
    {
      "path": "nft\\batch-images\\logo.jpg",
      "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
    }
  ],
  "image-urls": [
	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
  ],
  "ipfs": {
      "image-metadata": [
		  {
			"content": {
			  "description": "Image",
			  "image": "https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg",
			  "name": "logo.jpg"
			},
			"path": "logo.jpg"
		  }
	  ],
	  "metadata-urls": [
		"https://ipfs.moralis.io:2053/ipfs/Qmf3QmpGzz5vZ4TkrSJapRwD36f9sQ9zZJUwj6CCmA2bAs/logo.json"
	  ]	
  }
}@0 sent via `state`

### Input ports: 
* state: any

    Receives script state.
    
    Example:
    {
      "image-names": [
        "logo.jpg"
      ],
      "image-paths": [
        "nft\\batch-images\\logo.jpg"
      ],
      "image-upload-data": [
        {
          "path": "nft\\batch-images\\logo.jpg",
          "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
        }
      ],
      "image-urls": [
    	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
      ]
    }


* params: {
  "build-data": typeof `params` of `build image metadata`,
  "upload": typeof `params` of `folder uploader`
}

    Recieves upload metadata script parameters.
    
    Example:
    {
      "build-data": {
        "cwd": "./nft",
        "result-path": "ipfs.image-metadata",
        "message": "Building metadata for images...",
        "image-urls": [],
        "image-names": []
      },
      "upload": {
        "params": {
          "cwd": "./nft",
          "result-path": "ipfs.metadata-urls",
          "message": "Uploading metadata to IPFS...",
          "api-key": "API_KEY"
        },
        "mapping": {
          "folder-upload-data": "ipfs.image-metadata"
        }
      }
    }


### Output ports: 
* state: typeof `state`

    Sends updated script state.
    
    Example:
    {
      "image-names": [
        "logo.jpg"
      ],
      "image-paths": [
        "nft\\batch-images\\logo.jpg"
      ],
      "image-upload-data": [
        {
          "path": "nft\\batch-images\\logo.jpg",
          "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
        }
      ],
      "image-urls": [
    	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
      ],
      "ipfs": {
          "image-metadata": [
    		  {
    			"content": {
    			  "description": "Image",
    			  "image": "https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg",
    			  "name": "logo.jpg"
    			},
    			"path": "logo.jpg"
    		  }
    	  ],
    	  "metadata-urls": [
    		"https://ipfs.moralis.io:2053/ipfs/Qmf3QmpGzz5vZ4TkrSJapRwD36f9sQ9zZJUwj6CCmA2bAs/logo.json"
    	  ]	
      }
    }




## Bulk auto-metadata uploader (simplified)

### Description:
Builds and uploads images meta data and stores the ipfs URLs in the state.

Example: 
1. {
  "image-names": [
    "logo.jpg"
  ],
  "image-paths": [
    "nft\\batch-images\\logo.jpg"
  ],
  "image-upload-data": [
    {
      "path": "nft\\batch-images\\logo.jpg",
      "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
    }
  ],
  "image-urls": [
	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
  ]
}@0 received via `state`
2. {
  "cwd": "./nft",
  "moralis-api-key": "API_KEY",
  "images-urls" : ["https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"],
  "image-names": ["logo.jpg"]
}@0 received via `params`
3. {
  "image-names": [
    "logo.jpg"
  ],
  "image-paths": [
    "nft\\batch-images\\logo.jpg"
  ],
  "image-upload-data": [
    {
      "path": "nft\\batch-images\\logo.jpg",
      "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
    }
  ],
  "image-urls": [
	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
  ],
  "ipfs": {
      "image-metadata": [
		  {
			"content": {
			  "description": "Image",
			  "image": "https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg",
			  "name": "logo.jpg"
			},
			"path": "logo.jpg"
		  }
	  ],
	  "metadata-urls": [
		"https://ipfs.moralis.io:2053/ipfs/Qmf3QmpGzz5vZ4TkrSJapRwD36f9sQ9zZJUwj6CCmA2bAs/logo.json"
	  ]	
  }
}@0 sent via `state`

### Input ports: 
* state: any

    Receives script state.
    
    Example:
    {
      "image-names": [
        "logo.jpg"
      ],
      "image-paths": [
        "nft\\batch-images\\logo.jpg"
      ],
      "image-upload-data": [
        {
          "path": "nft\\batch-images\\logo.jpg",
          "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
        }
      ],
      "image-urls": [
    	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
      ]
    }


* params: {
  "cwd": string,
  "moralis-api-key": string,
  "image-urls": string[],
  "image-names": string[]
}

    Recieves upload metadata script parameters.
    
    Example:
    {
      "cwd": "./nft",
      "moralis-api-key": "API_KEY",
      "image-urls" : ["https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"],
      "image-names": ["logo.jpg"]
    }


### Output ports: 
* state: typeof `state`

    Sends updated script state.
    
    Example:
    {
      "image-names": [
        "logo.jpg"
      ],
      "image-paths": [
        "nft\\batch-images\\logo.jpg"
      ],
      "image-upload-data": [
        {
          "path": "nft\\batch-images\\logo.jpg",
          "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
        }
      ],
      "image-urls": [
    	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
      ],
      "ipfs": {
          "image-metadata": [
    		  {
    			"content": {
    			  "description": "Image",
    			  "image": "https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg",
    			  "name": "logo.jpg"
    			},
    			"path": "logo.jpg"
    		  }
    	  ],
    	  "metadata-urls": [
    		"https://ipfs.moralis.io:2053/ipfs/Qmf3QmpGzz5vZ4TkrSJapRwD36f9sQ9zZJUwj6CCmA2bAs/logo.json"
    	  ]	
      }
    }




## Bulk image uploader

### Description:
Uploads multiple images and place them in a folder directory and stores the ipfs URLs in the state.

Example:
1. {}@0 received via `state`
2. {
  "get-names": {
    "cwd": "./nft",
    "result-path": "image-names",
    "message": "Reading list of images...",
    "directory-path": "nft/batch-images"
  },
  "build-paths": {
    "params": {
      "cwd": "./nft",
      "result-path": "image-paths",
      "message": "Constructing image paths...",
      "base-path": "nft/batch-images"
    },
    "mapping": {
      "child-paths": "image-names"
    }
  },
  "build-data": {
    "params": {
      "cwd": "./nft",
      "result-path": "image-upload-data",
      "message": "Preparing image upload data..."
    },
    "mapping": {
      "image-paths": "image-paths"
    }
  },
  "upload": {
    "params": {
      "cwd": "./nft",
      "result-path": "image-urls",
      "message": "Uploading images to IPFS...",
      "api-key": "API_KEY"
    },
    "mapping": {
      "folder-upload-data": "image-upload-data"
    }
  }
}@0 received via `params`
3. {
  "image-names": [
    "logo.jpg"
  ],
  "image-paths": [
    "nft\\batch-images\\logo.jpg"
  ],
  "image-upload-data": [
    {
      "path": "nft\\batch-images\\logo.jpg",
      "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
    }
  ],
  "image-urls": [
	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
  ]
}@0 sent via `state`

### Input ports: 
* state: any

    Receives script state.
    
    Example:
    {}


* params: {
  "get-names": typeof `params` of `get image names`,
  "build-paths": typeof `params` of `build image paths`,
  "build-data": typeof `params` of `build image data`,
  "upload": typeof `params` of `upload images`
}

    Recieves upload images params.
    
    Example:
    {
      "get-names": {
        "cwd": "./nft",
        "result-path": "image-names",
        "message": "Reading list of images...",
        "directory-path": "nft/batch-images"
      },
      "build-paths": {
        "params": {
          "cwd": "./nft",
          "result-path": "image-paths",
          "message": "Constructing image paths...",
          "base-path": "nft/batch-images"
        },
        "mapping": {
          "child-paths": "image-names"
        }
      },
      "build-data": {
        "params": {
          "cwd": "./nft",
          "result-path": "image-upload-data",
          "message": "Preparing image upload data..."
        },
        "mapping": {
          "image-paths": "image-paths"
        }
      },
      "upload": {
        "params": {
          "cwd": "./nft",
          "result-path": "image-urls",
          "message": "Uploading images to IPFS...",
          "api-key": "API_KEY"
        },
        "mapping": {
          "folder-upload-data": "image-upload-data"
        }
      }
    }


### Output ports: 
* state: typeof `state`

    Sends updated script state.
    
    Example:
    {
      "image-names": [
        "logo.jpg"
      ],
      "image-paths": [
        "nft\\batch-images\\logo.jpg"
      ],
      "image-upload-data": [
        {
          "path": "nft\\batch-images\\logo.jpg",
          "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
        }
      ],
      "image-urls": [
    	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
      ]
    }




## Bulk image uploader (simplified)

### Description:
Uploads multiple images  and stores the ipfs URLs in the state.

Example:
1. {}@0 receiced via `state`
2. {
  "cwd": "./nft",
  "images-directory": "nft/batch-images",
  "moralis-api-key": "API_KEY"
}@0 received via `params`
3.{
  "image-names": [
    "logo.jpg"
  ],
  "image-paths": [
    "nft\\batch-images\\logo.jpg"
  ],
  "image-upload-data": [
    {
      "path": "nft\\batch-images\\logo.jpg",
      "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
    }
  ],
  "image-urls": [
	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
  ]
}@0 sent via `state`

### Input ports: 
* state: any

    Receives script state.
    
    Example:
    {}@0


* params: {
  "cwd": string,
  "images-directory": string,
  "moralis-api-key": string
}


    Recieves upload images script parameters.
    
    Example:
    {
      "cwd": "./nft",
      "images-directory": "nft/batch-images",
      "moralis-api-key": "API_KEY"
    }


### Output ports: 
* state: typeof `state`

    Sends updated script state.
    
    Example:
    {
      "image-names": [
        "logo.jpg"
      ],
      "image-paths": [
        "nft\\batch-images\\logo.jpg"
      ],
      "image-upload-data": [
        {
          "path": "nft\\batch-images\\logo.jpg",
          "content": "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAApgAAAKYB3X3"
        }
      ],
      "image-urls": [
    	"https://ipfs.moralis.io:2053/ipfs/QmVsdDLF8gmZeUCdrqgjXHLZ4VupdvxQaCiCdDvVApmR2o/nft\\batch-images\\logo.jpg"
      ]
    }




## Folder uploader

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "folder-upload-data": any,
  "api-key": string
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Image data builder

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "image-paths": string[]
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.




## Image metadata builder

### Input ports: 
* state: any

    Receives script state.


* params: {
  "cwd": string,
  "result-path": string,
  "message": string,
  "image-urls": string[],
  "image-names": string[]
}

### Output ports: 
* state: typeof `state`

    Sends updated script state.


