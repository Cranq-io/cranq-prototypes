# data/tree

## Builder (paths & values)

### Description:
Constructs a tree data structure based on the path-value pairs received via `paths` and `values`.

Bounces when the length of `values` and `path` don't match.

### Input ports: 
* paths: ((string or number)[])[]

    Receives paths that form the structure of the constructed tree.


* values: any[]

    Receives the values that will be the leaf nodes of the constructed tree.


### Output ports: 
* tree: any

* bounced: {
  "paths": ((string or number)[])[],
  "values": any[]
}



## Equality tester

### Description:
Tests whether the tree equals the reference (same structure and same values).

Example:
1. { "a":1, "b":1 }@0 is received via `tree`
2. { "a":1, "b":1 }@0 is received via `reference`
3. true@0 is sent via `equals`

### Input ports: 
* tree: (any[] or {string: any})

    The tree to test for equality with `reference`


* reference: (any[] or {string: any})

    The reference tree structure


### Output ports: 
* equals: boolean

    Whether all values in the tree are the same as the items with the same key in the reference




## Flattener

### Description:
Flattens a tree into a flat dictionary with keys created by prepending parent keys and a delimiter to child keys recursively.

Example:

1. {"a": {"a1": 1, "a2":2}}@0 is received via `tree`
2. "-"@0 is received via `delimiter`
3. {"a-a1": 1, "a-a2":2}@0 is sent via `flattened`

### Input ports: 
* tree: (any[] or {string: any})

    The tree to flatten


* delimiter: string

    The delimiter to use when prepending parent keys to child keys


### Output ports: 
* flattened: {string: any}

    The flat dictionary




## Has path tester

### Description:
Tests whether a path is found in the specified tree data structure.

Example:
1. ["foo", "bar", "baz"]@0 is received via `path`
2. {"foo": { "bar": { "baz": 0 }}}@0 is received via `tree`
3. true@0 is sent via `has`

### Input ports: 
* path: (string or number)[]

    The path to look for in the `tree`
    
    Example:
    
    ["foo", 1, "bar"] would match for the following `tree`:
    {"foo":[0, {"bar": "baz"}]}


* tree: (any[] or {string: any})

    The tree data structure to find the `path` within


### Output ports: 
* has: boolean

    Whether the `path` was found in the `tree`




## Iterator

### Description:
Iterates over nodes in a tree (deeply nested object) structure, as specified by the query.
The `query` acts as a filter for the iteration. It could hold strings for object keys, numbers for array indices, or objects describing either catch-all or a set of keys to include.

An example `query`: ["foo", 1, {"type":"wildcard"}, {"type":"options", "options": ["bar", "baz"]}]

Example:
1. {"foo": [0, {"a": { "bar": 1 }, "b": { "baz": 1 }}]}@0 is received via `tree`
2.  ["foo", 1, {"type":"wildcard"}, {"type":"options", "options": ["bar", "baz"]}]@0 is received via `query`
3. ["foo", 1, "a", "bar"]@0:0 is sent via `path`
4. 1@0:0 is sent via `node`
5. the original `tree` is sent via `tree`
6. ["foo", 1, "a", "baz"]@0:1 is sent via `path`
7. 1@0:1 is sent via `node`
8. the original `tree` is sent via `tree`
9. null@0 is sent via `done`

### Input ports: 
* tree: (any[] or {string: any})

    The tree data structure to iterate over on.


* query: (string or number or {"type": "wildcard"} or {"type":"options", "options": (string[] or number[])})[]

    Pattern for paths. Array of strings, numbers or expressions.
    Strings look for exact matches, numbers for array indices and expressions describe matching mechanisms.
    
    {"type": "wildcard"}
    Matches any key in the current node.
    
    {"type": "options", "options":[]}
    Matches the listed keys.


### Output ports: 
* path: (string or number)[]

    Sends the current path in the iteration


* node: any

    Sends the current node in the iteration


* tree: typeof `tree`

    Sends the entire tree


* done: null

    Sends null when the iteration is done




## Merger

### Description:
Merges two tree data structures. On conflict, the relevant paths / values of `b` take precedence.

### Input ports: 
* a: any

    Receives tree data structure to merge to.


* b: any

    Receives tree data structure to be merged onto the one received via `a`. Data received via this port takes precedence on conflict.


### Output ports: 
* merged: any

    Sends the merged tree structure.




## Node getter

### Description:
Retrieves the node at the specified path of the tree.

Example:
1. {"foo": {"bar": "baz"}}@0 is received via `tree`
2. ["foo", "bar"]@0 is received via `path`
3. "baz"@0 is sent via `node`


### Input ports: 
* tree: (any[] or {string:any})

    Receives the tree the node is extracted from


* path: (string or number)[]

    Receives the path segments in an array


### Output ports: 
* node: any

    Sends the node at the specified path


* not found: (string or number)[]

    Sends the `path` if it was not found




## Node setter

### Description:
Immutably stores the specified node on the specified path of the tree.

### Input ports: 
* tree: (any[] or {string:any})

    Tree data structure in which to store a node.


* path: (string or number)[]

    Specifies the location of the node.


* node: any

    The node to be stored in the tree.


### Output ports: 
* tree: typeof `tree`



## Node setter (mutable)

### Description:
Sets a node at the specified path of the tree. Mutates input.

Warning! This node mutates the tree it gets that means if any other node received the same tree as input from the original source it may get the modified tree depending on the execution order!

Example:
1. {"foo": {"bar": 1}}@0 is received via `tree`
2. ["foo", "baz"]@0 is received via `path`
3. 1@0 is received via `node`
4. {"foo": {"bar": 1, "baz": 1}}@0 is sent via `modified tree`

### Input ports: 
* tree: (any[] or {string:any})

    Tree data structure in which to store a node.
    
    Will be mutated.


* path: (string or number)[]

    Receives the path segments where the `node` should  be written to


* node: any

    Receives the node to be set


### Output ports: 
* modified tree: typeof `tree`

    Sends the modified tree




## Nodes getter

### Description:
Retrieves multiple nodes from a tree.

### Input ports: 
* tree: any

    Data to be repeated


* paths: ((string or number)[])[]

### Output ports: 
* nodes: any[]

* found indexes: number

* missing indexes: any



## Nodes setter

### Description:
Immutably stores the specified nodes on the specified paths of the tree.

Example:
1. `tree` receives 
{"a": "a"}@0
2. `path` receives
[
  ["a", "b"],
  ["a", "c"]
]@0
3. `nodes` receives
[0,1]@0
4. `tree` sends
{
  "a": {
     "b" : 0,
     "c": 1
  }
}@0

### Input ports: 
* tree: any

    Receives tree data structure in which to store a node.
    
    Example:
    {"a": "a"}


* paths: (string[] or number[])[]

    Receives the location of the nodes.
    
    Example:
    [
      ["a", "b"],
      ["a", "c"]
    ]


* nodes: any[]

    Receives nodes to be stored in the tree.
    
    Example:
    [0,1]


### Output ports: 
* tree: typeof `tree`

    Sends updated tree data structure.
    
    Example:
    {
      "a": {
         "b" : 0,
         "c": 1
      }
    }




## Path parser

### Description:
Parses a canonical string representation of a tree path. Tree paths are dot-separated, and dots in components are escaped with backslash.

Examples:
1. "foo.bar\.baz" is received via `path`
2. ["foo", "bar.baz"] is sent via `parsed`

### Input ports: 
* path: string

    Receives a serialized tree path in canonical format.
    
    Examples:
    * "foo.bar.baz"
    * "foo"
    * "foo.b\\.r"


### Output ports: 
* parsed: (string or number)[]

    Sends tree path. (Array of strings and numbers.)
    
    Example: ["foo", 0, "bar"]




## Path serializer

### Description:
Serializes tree path, producing a canonically formatted path string.
Canonical tree paths are dot-separated, with dots inside components escaped with a backslash.

### Input ports: 
* path: (string or number)[]

    Receives tree path. (Array of strings and numbers.)
    
    Example: ["foo", 0, "bar"]


### Output ports: 
* serialized: string

    Sends a serialized tree path in canonical format.
    
    Examples:
    * "foo.bar.baz"
    * "foo"
    * "foo.b\\.r"




## Paths getter

### Input ports: 
* tree: any

### Output ports: 
* paths: ((string or number)[])[]



## Paths parser

### Input ports: 
* paths: string[]

### Output ports: 
* parsed: ((string or number)[])[]



## Values getter

### Input ports: 
* tree: any

### Output ports: 
* values: any[]



## Values tester

### Description:
Tests for deep equality for `tree` and `reference`.

Example:
1. {"foo":{"bar":"baz"}}@0 is received via `tree`
2. {"foo":{"bar":"baz"}}@0 is received via `reference`
3. true@0 is sent via `all values are same`

### Input ports: 
* tree: (any[] or {string: any})

    The tree to test


* reference: (any[] or {string: any})

    The reference tree structure


### Output ports: 
* all values are same: boolean

    Whether all nodes of the `data` tree are the same as the `reference`


