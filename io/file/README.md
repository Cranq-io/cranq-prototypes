# io/file

## Binary reader

### Description:
Reads binary files Base64 encoded.

### Input ports: 
* path: string

### Output ports: 
* base64: string

* bounced: string



## Binary writer

### Input ports: 
* path: string

* base64: string

### Output ports: 
* written: null

* error: {"error": string}



## Deleter

### Description:
Deletes a file or directory specified by the path input.

Example (success):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2 false@0 received on `recursive`
3. { path: "/home/user1/dir1/foo.txt", recursive: false } sent on `deleted`

Example (failure): 
1. "/home/user1/dir1"@0 received on `path`
2 true@0 received on `recursive`
3.
- { path: "/home/user1/dir1", recursive: true } sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, stat '/home/user1/dir1'"
} sent on `error`

### Input ports: 
* path: string

    Receives the path of the file or directory to delete.
    
    Example:
    - "/home/user1/dir1"
    - "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


* recursive: boolean

    Receives boolean flag which, when set, performs a recursive delete of all files & folders under the specified path.
    
    Example:
    false
    
    (Be VERY cautious with recursive delete as it may cause irreversible harm on the host running the application if applied to a wrong path!)


### Output ports: 
* bounced: { "path": typeof `path`, "recursive": typeof `recursive` }

    Sends synced parameters if operation has failed.
    
    Example:
    - { path: "/home/user1/dir1", recursive: true }
    - { path: "/home/user1/dir1/foo.txt", recursive: false }


* deleted: { "path": typeof `path`, "recursive": typeof `recursive` }

    Sends synced parameters if the operation has succeeded.
    
    Example:
    - { path: "/home/user1/dir1", recursive: true }
    - { path: "/home/user1/dir1/foo.txt", recursive: false }


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, stat 'home/user1'"
    }




## Directory creator

### Description:
Creates an empty directory under the specified path

Example:
1. "/home/user1/newdir"@0 received on `path`
2/a. "/home/user1/newdir"@0 sent on `created` if directory has been successfully created
2/b. "/home/user1/newdir"@0 sent on `bounced` if any error occured during directory creation

### Input ports: 
* path: string

    Receives the path of the  directory to create.
    
    Example:
    "/home/user1/newdir"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* created: typeof `path`

    Sends the path if the operation has succeeded.
    
    Example:
    "/home/user1/newdir"
    
    


* bounced: typeof `path`

    Sends the path if the operation has failed.
    
    Example:
    "/home/user1/newdir"


* error: { "message": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "message": "ENOENT: no such file or directory, mkdir '/home/user1/newdir'"
    }




## Directory lister

### Description:
Non-recursively lists the names of files & directories under the specified path.

Example (success): 
1. "/home/user1/dir1"@0 received on `path`
2. [ "foo.txt", "bar.txt" ]@0 sent on `child names`

Example (failure): 
1. "/home/user1/dir1"@0 received on `path`
2. 
- "/home/user1/dir1"@0 sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, scandir '/home/user1/dir1'"
}@0 sent on `error`

### Input ports: 
* path: string

    Receives the path of the directory to list the content of.
    
    Example:
    "/home/user1/dir1"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* child names: string[]

    Sends the names of files & directories under the specified path.
    
    Example:
    [
      "foo.txt",
      "subdir1"
    ]


* bounced: typeof `path`

    Sends the path if the operation has failed.
    
    Example:
    "/home/user1/dir1"


* error: {"error": string}

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, scandir '/home/user1/dir1'"
    }




## Directory lister (paths)

### Description:
Non-recursively lists the paths of files & directories under the specified path.

Example (success): 
1. "/home/user1/dir1"@0 received on `path`
2. [ "/home/user1/dir1/foo.txt", "/home/user1/dir1/bar.txt" ]@0 sent on `child names`

Example (failure): 
1. "/home/user1/dir1"@0 received on `path`
2. 
- "/home/user1/dir1"@0 sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, scandir '/home/user1/dir1'"
}@0 sent on `error`

### Input ports: 
* path: string

    Receives the path of the directory to list the content of.
    
    Example:
    "/home/user1/dir1"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* child paths: string[]

    Sends the path of files & directories under the specified path.
    
    Example:
    [
      "/home/user1/dir1/foo.txt",
      "/home/user1/dir1/subdir1"
    ]


* bounced: string

    Sends the path if the operation has failed.
    
    Example:
    "/home/user1/dir1"


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, scandir 'home/user1'"
    }




## Directory tester

### Description:
Determines whether the specified path points to a directory.

Example:
1. "/home/user1/dir1"@0 received on `path`
2. true@0 sent on `is directory`

### Input ports: 
* path: string

    Receives the path to test whether it is a directory or not.
    
    Example:
    "/home/user1/dir1"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* is directory: boolean

    Sends boolean value that indicates whether the specified path is a directory.
    
    Example:
    true




## Extension setter

### Description:
Sets the extension on the received path.

Example:
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. ".json"@0 received on `extension`
3. "/home/user1/dir1/foo.json"@0 sent on `path`

### Input ports: 
* path: string

    Receives the path to set the extension on.
    
    Example:
    "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


* extension: string

    Receives the extension to set on `path`.
    
    Example:
    ".json"


### Output ports: 
* path: string

    Sends the resulting path.
    
    Example:
    "/home/user1/dir1/foo.json"




## File copier

### Description:
Copies a file specified by the path in `source` to the path in `destination`.

Example (success): 
1. "/home/user1/dir1/foo.txt"@0 received on `source`
2. "/home/user2/dir2/bar.txt"@0 received on `destination`
3. { 
source: "/home/user1/dir1/foo.txt", 
destination: "/home/user1/dir2/bar.txt"
}@ sent on `copied`

Example (failure): 
1. "/home/user1/dir1/foo.txt"@0 received on `source`
2. "/home/user1/dir2/bar.txt"@0 received on `destination`
3. 
- { 
source: "/home/user1/dir1/foo.txt", 
destination: "/home/user1/dir2/bar.txt"
}@0 sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, copyfile '/home/user1/dir1/foo.txt' -> '/home/user1/dir2/bar.txt'"
}@0 sent on `error`

### Input ports: 
* source: string

    Receives the path of the source file to copy.
    
    Example:
    "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


* destination: string

    Receives the path of the desired target file.
    
    Example:
    "/home/user1/dir2/bar.txt"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* bounced: { "source": string, "destination": string }

    Sends synced parameters if operation has failed.
    
    Example:
    { 
      source: "/home/user1/dir1/foo.txt", 
      destination: "/home/user1/dir2/bar.txt"
    }
    


* copied: { "source": string, "destination": string }

    Sends synced parameters if operation has succeeded.
    
    Example:
    { 
      source: "/home/user1/dir1/foo.txt", 
      destination: "/home/user1/dir2/bar.txt"
    }


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, copyfile '/home/user1/dir1/foo.txt' -> '/home/user2/dir2/bar.txt'"
    }




## File mover

### Description:
Moves a file specified by the path in `source` to the path in `destination`.

Example (success): 
1. "home/user1/dir1/foo.txt"@0 received on `source`
2. "home/user1/dir2/bar.txt"@0 received on `destination`
3. { 
source: "/home/user1/dir1/foo.txt", 
destination: "home/user1/dir2/bar.txt"
}@ sent on `moved`

Example (failure): 
1. "home/user1/dir1/foo.txt"@0 received on `source`
2. "home/user1/dir2/bar.txt"@0 received on `destination`
3. 
- { 
source: "/home/user1/dir1/foo.txt", 
destination: "home/user1/dir2/bar.txt"
}@0 sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, rename 'home/user1/dir1/foo.txt' -> 'home/user1/dir2/bar.txt'"
}@0 sent on `error`

### Input ports: 
* source: string

    Receives the path of the source file to move.
    
    Example:
    "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


* destination: string

    Receives the path of the desired target file.
    
    Example:
    "/home/user1/dir2/bar.txt"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* bounced: { "source": string, "destination": string }

    Sends synced parameters if operation has failed.
    
    Example:
    { 
      source: "/home/user1/dir1/foo.txt", 
      destination: "/home/user1/dir2/bar.txt"
    }


* moved: { "source": string, "destination": string }

    Sends synced parameters if operation has succeeded.
    
    Example:
    { 
      source: "/home/user1/dir1/foo.txt", 
      destination: "/home/user1/dir2/bar.txt"
    }


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, rename '/home/user1/dir1/foo.txt' -> '/home/user1/dir2/bar.txt'"
    }




## File renamer

### Description:
Renames a file specified by the path in `source path` to the new file name in `new name`.

Example (success): 
1. "home/user1/foo.txt"@0 received on `source path`
2. "bar.txt"@0 received on `new name`
3. { 
source: "/home/user1/dir1/foo.txt", 
destination: "/home/user1/dir1/bar.txt"
}@ sent on `renamed`

Example (failure): 
1. "/home/user1/foo.txt"@0 received on `source path`
2. "bar.txt"@0 received on `new name`
3. 
- { 
source: "/home/user1/dir1/foo.txt", 
destination: "/home/user1/dir1/bar.txt"
}@0 sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, rename '/home/user1/dir1/foo.txt' -> '/home/user2/dir1/bar.txt'"
}@0 sent on `error`

### Input ports: 
* source path: string

    Receives the path of the file to rename.
    
    Example:
    "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


* new name: string

    Receives the desired new file name.
    
    Example:
    "bar.txt"


### Output ports: 
* bounced: any

    Sends synced parameters if operation has failed.
    
    Example:
    { 
      source: "/home/user1/dir1/foo.txt", 
      destination: "/home/user1/dir1/bar.txt"
    }


* renamed: any

    Sends synced parameters if operation has succeeded.
    
    Example:
    { 
      source: "/home/user1/dir1/foo.txt", 
      destination: "/home/user1/dir1/bar.txt"
    }


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, rename '/home/user1/dir1/foo.txt' -> '/home/user1/dir1/bar.txt'"
    }




## File tester

### Description:
Determines whether the the specified path points to a file.

Example:
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. true sent on `is file`

### Input ports: 
* path: string

    Receives the path to test whether it is a file or not.
    
    Example:
    "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* is file: boolean

    Boolean value that indicates, whether the specified path is a file.
    
    Example:
    true




## Info getter

### Description:
Reads common file system information of the file or directory, specified by `path`.

Example (success):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. {
  "size_bytes": 3128,
  "created": "2021-12-09T15:47:56.441Z",
  "accessed": "2021-12-09T15:47:56.441Z",
  "modified": "2021-12-09T15:47:56.441Z",
  "changed": "2021-12-09T22:08:22.314Z"
}@0 sent on `info`

Example (failure):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2."/home/user1/dir1/foo.txt"@ sent on `bounced`

### Input ports: 
* path: string

    Receives the path of the file or directory to get information of.
    
    Example:
    - "/home/user1/dir1"
    - "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* info: {
  "size_bytes": number,
  "created": string,
  "accessed": string,
  "modified": string,
  "changed": string
}

    The resulting file/directory information.
    
    Example:
    {
      "size_bytes": 3128,
      "created": "2021-12-09T15:47:56.441Z",
      "accessed": "2021-12-09T15:47:56.441Z",
      "modified": "2021-12-09T15:47:56.441Z",
      "changed": "2021-12-09T22:08:22.314Z"
    }


* bounced: typeof `path`

    Sends the path if the operation has failed.
    
    Example:
    - "/home/user1/dir1"
    - "/home/user1/dir1/foo.txt"




## JSON reader

### Description:
Reads a JSON file from the specified path and outputs its content.

Example (success):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. {
  "foo": 1,
  "bar": 2,
  "foobar": [1,2]
}@0 sent on `text`

Example (failure):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. 
- "/home/user1/dir1/foo.txt"@0 sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, open '/home/user1/dir1/foo.txt'"
}@0 sent on `error`

### Input ports: 
* path: string

    Receives the path of the file to read content of as JSON.
    
    Example:
    "/home/user1/dir1/foo.json"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* data: {string:any}

    Sends the parsed JSON content read from the file specified by `path`.
    
    Example:
    {
      "foo": 1,
      "bar": 2,
      "foobar": [1,2]
    }
    


* bounced: typeof `path`

    Sends the path if the operation has failed.
    
    Example:
    "/home/user1/dir1/foo.json"


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example (file access error): 
    {
      "error": "Error: ENOENT: no such file or directory, open '/home/user1/dir1/foo.txt'"
    }
    
    Example (json parse error):
    {
      "error": "SyntaxError: Unexpected token } in JSON at position 45"
    }




## JSON reader (with param)

### Description:
Reads a JSON file from the specified path and outputs its content.

### Input ports: 
* path: string

* start: any

### Output ports: 
* data: any

* bounced: typeof `bounced` of `json reader`



## JSON writer

### Input ports: 
* path: string

* data: any

### Output ports: 
* written: null

* bounced: {"data": any, "path": string}



## Path builder

### Description:
Constructs an operating system specific path of the specified segments.

Example:
1. {
  "directory": "/home/user1/dir1",
  "basename": "foo",
  "extension": ".txt"
}@0 received on `components`
2. "/home/user1/dir1/foo.txt"@0 sent on `path`

### Input ports: 
* components: {
  "directory": string,
  "basename": string,
  "extension": string
}

    Receives the components to build the path from.
    
    Example (Windows): 
    {
      "directory": "C:/Users/User1/dir1",
      "basename": "foo",
      "extension": ".txt"
    }
    
    Example (OSX & *nix): 
    {
      "directory": "/home/user1/dir1",
      "basename": "foo",
      "extension": ".txt"
    }
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* path: string

    Sends the resulting path.
    
    Example (Windows):
    "C:/Users/User1/dir1/foo.txt"
    
    Example (OSX & *nix):
    "/home/user1/dir1/foo.txt"




## Path creator

### Description:
Creates a path in the filesystem.

### Input ports: 
* path: string

### Output ports: 
* success: boolean



## Path deleter

### Description:
Deletes the specified path recursively, and forced.

### Input ports: 
* path: string

    Deletes all folders on the specified path from the filesystem.


### Output ports: 
* success: boolean

* error: string



## Path exist tester

### Description:
Tests whether the specified path exists in the filesystem.

### Input ports: 
* path: string

### Output ports: 
* exists: boolean



## Path joiner

### Description:
Joins the specified relative path to a base path in an operating system-specific manner.

Example:
1. "/home/user1/" received on `base`
2. "dir1/foo.txt" received on `relative`
3. "/home/user1/dir1/foo.txt" sent on `joined`

### Input ports: 
* base: string

    Receives the base path to concatenate onto.
    
    Example:
    "/home/user1/"
    
    (To keep the application portable use "/" as path separator.)


* relative: string

    Receives the path relative to `base`.
    
    Example:
    "dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* joined: string

    Sends the resulting path.
    
    Example:
    "/home/user1/dir1/foo.txt"




## Path parser

### Description:
Parses a file system path into its components.

Example:
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. {
  "directory": "/home/user1/dir1",
  "basename": "foo",
  "extension": ".txt"
}@0 sent on `components`

### Input ports: 
* path: string

    Receives the path to parse.
    
    Example:
    - "/home/user1/dir1/foo.txt"
    - "C:/Users/User1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* components: {
  "directory": string,
  "basename": string,
  "extension": string
}

    Sends the resulting path components.
    
    Example:
    - {
      "directory": "/home/user1/dir1",
      "basename": "foo",
      "extension": ".txt"
    }
    - {
      "directory": "C:/Users/User1/dir1",
      "basename": "foo",
      "extension": ".txt"
    }




## Path resolver

### Description:
Resolves a file system path into a fully qualified one relative to the current working directory.

Example:
1. "dir1"@0 received on `path`
2. "/home/user1/.cranq/runtime/dir1"@0 sent on `resolved` 
("/home/user1/.cranq/runtime" being the current working directory)

### Input ports: 
* path: string

    Receives the path to resolve to absolute path.
    
    Example:
    - "dir1"
    - "dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)
    


### Output ports: 
* resolved: string

    Sends the resolved absolute path.
    
    Example:
    - "/home/user1/.cranq/runtime/dir1"
    - "/home/user1/.cranq/runtime/dir1/foo.txt"




## Path tester

### Description:
Determines whether a file or directory exists under the specified path.

Example: 
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. true@0 sent on `exists`

### Input ports: 
* path: string

    Receives the path to test whether it exists or not.
    
    Example:
    Example:
    - "/home/user1/dir1"
    - "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* exists: boolean

    Sends boolean value that indicates whether a file or directory exists under the specified path.
    
    Example:
    true




## Paths joiner

### Description:
Joins an array of path parts to a common base

### Input ports: 
* base: string

    The base path portion


* children: string[]

    The array of path parts to join onto the base


### Output ports: 
* paths: any

    The resulting paths




## Text appender

### Description:
Appends the input text to a file specified on `path`.

Example (success):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. "Hello World"@0 received on `text`
3. { 
  path: "/home/user1/dir1/foo.txt", 
  text: "Hello World"
}@0 sent on `written`

Example (failure):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. "Hello World"@0 received on `text`
3.
- { 
  path: "/home/user1/dir1/foo.txt", 
  text: "Hello World"
}@0 sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, open '/home/user1/dir1/foo.txt'"
}@0 sent on `error`

### Input ports: 
* path: string

    Receives the path of the file to append text to.
    
    Example:
    "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


* text: string

    Receives the text to append to the specified file.
    
    Example:
    "Hello World"


### Output ports: 
* bounced: any

    Sends synced parameters if operation has failed.
    
    Example:
    { 
      path: "/home/user1/dir1/foo.txt", 
      text: "Hello World"
    }


* written: any

    Sends synced parameters if operation has succeeded..
    
    Example:
    { 
      path: "/home/user1/dir1/foo.txt", 
      text: "Hello World"
    }


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, open '/home/user1/dir1/foo.txt'"
    }




## Text reader

### Description:
Reads a text file from the specified path and outputs its content.

Example (success):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. "Hello World"@0 sent on `text`

Example (failure):
1. "/home/user1/dir1/foo.txt"@0 received on `path`
2. 
- "/home/user1/dir1/foo.txt"@0 sent on `bounced`
- {
  "error": "Error: ENOENT: no such file or directory, open '/home/user1/dir1/foo.txt'"
}@0 sent on `error`

### Input ports: 
* path: string

    Receives the path of the file to read content of as text.
    
    Example:
    "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


### Output ports: 
* text: string

    Sends the text content read from the file specified by `path`.
    
    Example:
    "Hello World"


* bounced: string

    Sends the path if the operation has failed.
    
    Example:
    "/home/user1/dir1/foo.txt"


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, open '/home/user1/dir1/foo.txt'"
    }




## Text writer

### Description:
Writes the input text to the specified path as a text file.

### Input ports: 
* path: string

    Receives the path of the file to write the specified text to.
    
    Example:
    "/home/user1/dir1/foo.txt"
    
    (To keep the application portable use "/" as path separator.)


* text: string

    Receives the text to write to the specified file. (Will overwrite existing content of the file if exists!)
    
    Example:
    "Hello World"


### Output ports: 
* bounced: string

    Sends synced parameters if operation has failed.
    
    Example:
    { 
      path: "/home/user1/dir1/foo.txt", 
      text: "Hello World"
    }


* written: null

    Sends synced parameters if operation has succeeded..
    
    Example:
    { 
      path: "/home/user1/dir1/foo.txt", 
      text: "Hello World"
    }


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, open '/home/user1/dir1/foo.txt'"
    }


