# data/dictionary

## Builder (key & value)

### Description:
Builds a dictionary based on an array of keys and a single value for all items.

Example:
1. [ "first", "third", "fifth" ]@0 received via `keys`
1. 1@0 received via `value`
2. `dict` sends { "first": 1, "third": 1, "fifth": 1 }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_2_builders

### Input ports: 
* key: string

    Receives the keys to construct the dictionary from.
    
    Example:
    ["first","third","fifth"]


* value: any

    Receives the value to assign to all items.
    
    Example:
    1


### Output ports: 
* dict: {string:typeof`value`}

    Sends the resulting dictionary.
    
    Example:
    { "first": 1, "third": 1, "fifth": 1 }




## Builder (key-value pairs)

### Description:
Builds a dictionary based on an array of objects with key & value properties.

Any non-conforming items in the array are discarded.

Example:
1. [ { "key":"first", "value": 1 }, { "key":"third", "value": 3 } ]@0 received via `key-value pairs`
2. `dict`sends { "first": 1, "third": 3 }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_2_builders

### Input ports: 
* key-value pairs: {"key":string,"value":any}[]

    Receives objects having key & value properties.
    
    Example:
    [ { "key":"first", "value": 1 }, { "key":"third", "value": 3 } ]


### Output ports: 
* dict: {string:typeof`key-value pairs`[number]["value"]}

    Sends the resulting dictionary.
    
    Example:
    { "first": 1, "third": 3 }




## Builder (keys & value)

### Description:
Builds a dictionary based on an array of keys and a single value for all items.

Example:
1. [ "first", "third", "fifth" ]@0 received via `keys`
1. 1@0 received via `value`
2. `dict` sends { "first": 1, "third": 1, "fifth": 1 }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_2_builders

### Input ports: 
* keys: string[]

    Receives the keys to construct the dictionary from.
    
    Example:
    ["first","third","fifth"]


* value: any

    Receives the value to assign to all items.
    
    Example:
    1


### Output ports: 
* dict: {string:typeof`value`}

    Sends the resulting dictionary.
    
    Example:
    { "first": 1, "third": 1, "fifth": 1 }




## Builder (keys & values)

### Description:
Builds a dictionary based on matching arrays of keys and values. Items are constructed from the same indices of the input arrays.

If the array received by `keys` contains duplicates,  only the last precedent is taken into effect - the other corresponding values are discarded.

If the item counts of the input arrays differ, the out-of-bounds items are ignored.

Example A:
1. [ "first", "third", "fifth" ]@0 received via `keys`
2. [ 1, 3, 5 ]@0 received via `values`
3. `dict` sends { "first": 1, "third": 3, "fifth": 5 }@0

Example B:
1. [ "first", "third", "fifth" ]@0 received via `keys`
2. [ 1, 3 ]@0 received via `values`
3. `dict` sends { "first": 1, "third": 3 }@0

Example C:
1. [ "first", "first", "fifth" ]@0 received via `keys`
2. [ 1, 3, 5 ]@0 received via `values`
3. `dict` sends { "first": 3,  "fifth": 5 }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_2_builders

### Input ports: 
* keys: string[]

    Receives the keys to construct the dictionary from.
    
    Example:
    ["first","third","fifth"]


* values: any[]

    Receives the values to construct the dictionary from.
    
    Example:
    [1, 3, 5]


### Output ports: 
* dict: {string:typeof`values`[number]}

    Sends the resulting dictionary.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }




## Has key tester

### Description:
Tests whether a dictionary has a specific key.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "first"@0 received via `key`
3. `has` sends true@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "second"@0 received via `key`
3. `has` sends false@0

### Input ports: 
* dict: {string:any}

    Receives the dictionary to test.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* key: string

    Receives the key to look for in the dictionary.
    
    Example:
    "first"


### Output ports: 
* has: boolean

    Sends a value indicating whether the dictionary has the expected key.
    
    Example:
    true
    




## Has keys tester

### Description:
Tests whether the key set of the dictionary contains the expected keys.

If `strict` is set, extra properties are not tolerated, the dictionary provided must have exactly the expected keys.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. ["first", "fifth"]@0 received via `expected keys`
3. `strict` is set to false
4. `has` sends true@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. ["second", "seventh"]@0 received via `expected keys`
3. `strict` is set to false
4. `has` sends false@0

Example C:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. ["first", "fifth"]@0 received via `expected keys`
3. `strict` is set to true
4. `has` sends false@0

### Input ports: 
* dict: {string:any}

    Receives the dictionary to test.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* expected keys: string[]

    Receives an array of expected keys.
    
    Example:
    [ "first", "third" ]


* strict: boolean

    Receives whether extra keys in `dict` are allowed.
    
    Example:
    false


### Output ports: 
* has: boolean

    Sends a value indicating whether the dictionary has the expected keys.
    
    Example:
    true
    




## Inner joiner

### Description:
Joins dictionary 'b' to dictionary `a`, by matching the values of `a` to the keys of `b`.

Items from `b` with no matching value in `a` are excluded from the result.

Items from `a` with no matching key in `b` are excluded from the result.

Example:
1. {"first":"first_id", "third":"third_id", "fifth":"fifth_id"}@0 received via `a`
2. {"first_id":1, "second_id":2, "third_id":3}@0 received via `b`
3. `joined` sends {"first": 1,"third": 3}@0

### Input ports: 
* a: {string:string}

    Receives the dictionary containing the keys to join and the values to join by.
    
    Example:
    {"first":"first_id", "third":"third_id", "fifth":"fifth_id"}


* b: {string:any}

    Receives the dictionary containing the values to join and the keys to join by.
    
    Example:
    {"first_id":1, "second_id":2, "third_id":3}


### Output ports: 
* joined: {string:typeof`b`[string]}

    Sends the resulting joined dictionary.
    
    Example:
    {"first": 1,"third": 3}




## Item deleter

### Description:
Deletes an item from a dictionary by its key. 
If the item is not found, the original dictionary is forwarded.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "first"@0 received via `key`
3. `dict` sends { "third": 3, "fifth": 5 }@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "second"@0 received via `key`
3. `dict` sends{ "first": 1, "third": 3, "fifth": 5 }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_1_setters_deleters

### Input ports: 
* dict: {string:any}

    Receives the dictionary to delete the item from.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* key: string

    Receives the key corresponding to the value to delete.
    
    Example:
    "third"


### Output ports: 
* dict: typeof`dict`

    Sends the resulting dictionary.
    
    Example:
    { "first": 1, "fifth": 5 }




## Item deleter (mutable)

### Description:
Deletes an item from the dictionary by its key.
Mutates input.

If the item is not found, the original dictionary is forwarded.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "first"@0 received via `key`
3. `dict` sends { "third": 3, "fifth": 5 }@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "second"@0 received via `key`
3. `dict` sends{ "first": 1, "third": 3, "fifth": 5 }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_1_setters_deleters

### Input ports: 
* dict: {string:any}

    Receives the dictionary to delete the item from.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* key: string

    Receives the key corresponding to the value to delete.
    
    Example:
    "third"


### Output ports: 
* dict: any

    Sends the resulting dictionary.
    
    Example:
    { "first": 1, "fifth": 5 }




## Item getter

### Description:
Retrieves an item's value by its key from a dictionary.
If the item is not found, the inputs are sent via `not found`.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "first"@0 received via `key`
3. `value` sends 1@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "second"@0 received via `key`
3. `not found` sends { "dict":  { "first": 1, "third": 3, "fifth": 5 }, "key": "second" }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/3_querying_data/3_1_getters

### Input ports: 
* dict: {string:any}

    Receives the dictionary to get the value from.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* key: string

    Receives the key corresponding to the value to get.
    
    Example:
    "third"


### Output ports: 
* value: typeof`dict`[string]

    If found, sends the value corresponding to the specified key.
    
    Example:
    1


* not found: {
  "dict": typeof `dict`,
  "key": string
} 

    Sends the input values, when the specified key is not found in the dictionary.
    
    Example:
    { "dict":  { "first": 1, "third": 3, "fifth": 5 }, "key": "second" }




## Item getter with default

### Description:
Retrieves an item's value by its key from a dictionary.
If the item is not found, the specified default value is sent.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "first"@0 received via `key`
3. `value` sends 1@0

Example B:
1. 2 assigned to `default`
2. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
3. "second"@0 received via `key`
4. `value` sends 2@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/3_querying_data/3_1_getters

### Input ports: 
* dict: {string: any}

    Receives the dictionary to get the value from.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* key: string

    Receives the key corresponding to the value to get.
    
    Example:
    "third"


* default: typeof `dict`[string]

    Receives the default value to be sent when the requested key is absent.
    
    Must be parameter.
    
    Example:
    2


### Output ports: 
* value: typeof `dict`[string]

    Sends the value corresponding to the specified key, or, when not found, the specified default value.
    
    Example:
    1




## Item setter

### Description:
Sets an item's value by its key in a dictionary.
If the item is not found, it will be created.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "first"@0 received via `key`
3. -1@0 received via `value`
4. `dict` sends { "first": -1, "third": 3, "fifth": 5 }@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "second"@0 received via `key`
3. 2@0 received via `value`
4. `dict` sends { "first": 1, "second":2, "third": 3, "fifth": 5 }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_1_setters_deleters

### Input ports: 
* dict: {string:any}

    Receives the dictionary to set the value in.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* key: string

    Receives the key corresponding to the value to set.
    
    Example:
    "second"


* value: typeof`dict`[string]

    Receives the value to set.
    
    Example:
    2


### Output ports: 
* dict: typeof`dict`

    Sends the resulting dictionary, with the new/altered item.
    
    Example:
    { "first": 1, "second":2, "third": 3, "fifth": 5 }




## Items getter

### Description:
Retrieves multiple items' values from the dictionary by their keys, in the order of the keys provided.
If any of the items are not found in the dictionary, a 'null' value will be sent in its place.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. [ "first", "third" ]@0 received via `key`
3. `values` sends  [ 1, 3 ]@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "second"@0 received via `key`
3. `values` sends  [ 1, null ]@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/3_querying_data/3_1_getters

### Input ports: 
* dict: {string:any}

    Receives the dictionary to get the values from.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* keys: string[]

    Receives the keys corresponding to the values to get.
    
    Example:
    ["first", "third"]


### Output ports: 
* values: typeof`dict`[string][]

    Sends the values corresponding to the received keys.
    
    Example:
    [1, 3]




## Iterator

### Description:
Iterates through items of a dictionary.

The tag on the output signals will contain the index of the current iteration.

Example:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. `key` sends  "first"@0:0
3. `value` sends  1@0:0
4. `key` sends  "third"@0:1
5. `value` sends  3@0:1
6. `key` sends  "fifth"@0:2
7. `value` sends  5@0:2

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/1_application_flow/1_2_iterators

### Input ports: 
* dict: {string:any}

    Receives the dictionary to iterate through.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


### Output ports: 
* value: typeof`dict`[string]

    Sends the value of the current item, with the tag corresponding to the iteration.


* key: string

    Sends the key of the current item, with the tag corresponding to the iteration.




## JSON parser

### Description:
Parses the JSON string representation of a dictionary.
If the parsing is unsuccessful, the input is forwarded via `bounced`.

Example A:
1. "{\"first\":1,\"third\":3,\"fifth\":5}"@0 received via `json`
2. `parsed` sends { "first": 1, "third": 3, "fifth": 5 }@0

Example B:
1. "malformed"@0 received via `json`
2. `bounced` sends "malformed"@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_6_serialization

### Input ports: 
* json: string

    Receives the JSON string to parse.
    
    Example:
    "{\"first\":1,\"third\":3,\"fifth\":5}"


### Output ports: 
* parsed: {string:any}

    Sends the parsed dictionary.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* bounced: typeof`json`

    Sends the value of `json`, if the parsing was unsuccessful.


* error: { "error": string }

    Sends error information if the operation has failed.
    
    Example: 
    {
      "error": "Error: ENOENT: no such file or directory, open '/home/user1/dir1/foo.txt'"
    }




## JSON serializer

### Description:
Serializes a dictionary to its JSON string representation.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 }@0 received via `dict`
2. `json` sends "{\"first\":1,\"third\":3,\"fifth\":5}"@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_6_serialization

### Input ports: 
* dict: any

    Receives the dictionary to serialize.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


### Output ports: 
* json: any

    Sends the JSON string representation of the provided dictionary.
    
    Example:
    "{\"first\":1,\"third\":3,\"fifth\":5}"




## Key-value pairs getter

### Description:
Gets the key-value pairs from the dictionary as an array.

Example:
1. { "first": 1, "third": 3 }@0 is received by `dict`
2. `key-value pairs` sends [ { "key":"first", "value": 1 }, { "key":"third", "value": 3 } ]@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/3_querying_data/3_1_getters

### Input ports: 
* dict: {string:any}

    Receives a dictionary to extract the key-value pairs from.
    
    Example:
     { "first": 1, "third": 3 }


### Output ports: 
* key-value pairs: {"key":string,"value":typeof`dict`[string]}[]

    Sends the extracted key-value pairs.
    
    Example:
    [ { "key":"first", "value": 1 }, { "key":"third", "value": 3 } ]




## Keys getter

### Description:
Gets all keys from the dictionary as an array.


Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. `keys` sends  [ "first", "third", "fifth" ]@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/3_querying_data/3_1_getters

### Input ports: 
* dict: {string:any}

    Receives to dictionary to extract the keys from.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 } 


### Output ports: 
* keys: string[]

    Sends the keys of the dictionary as an array.
    
    Example:
    [ "first", "third", "fifth" ]




## Mapper

### Input ports: 
* dict: {string: any}

* mapped value: typeof `dict`[string]

    The current (by tag) value, mapped.


### Output ports: 
* mapped: {string: typeof `mapped value`}

* value: any



## Merger

### Description:
Merges dictionary `b` to dictionary `a`. Values of `a` will be ignored on key conflict.

Example:
1. { "first": 1, "third": 0 }@0 received via `a`
2. { "third": 3, "fifth": 5 }@0 received via `b`
3. `merged` sends { "first": 1, "third": 3, "fifth": 5 }@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_4_merge_concat

### Input ports: 
* a: {string:any}

    Receives the dictionary to merge onto.
    
    Example:
    { "first": 1, "third": 0 }


* b: {string:any}

    Receives the dictionary to merge with.
    
    Example:
    { "third": 3, "fifth": 5 }


### Output ports: 
* merged: (typeof `a` and typeof `b`)

    Sends the resulting merged dictionary.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }




## Repeater

### Input ports: 
* dict: {string: any}

* data: any

    Data to be repeated


### Output ports: 
* data: typeof `data`

    Repeated data




## Size getter

### Description:
Gets the number of items in the dictionary.

Example:
1. { "first": 1, "third": 3, "fifth": 5 }@0 received via `dict`
3. `size` sends 3@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/3_querying_data/3_1_getters

### Input ports: 
* dict: {string:any}

    Receives the dictionary to count the number of items of.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


### Output ports: 
* size: number

    Sends the calculated dictionary size.
    
    Example:
    3




## Structure tester

### Description:
Tests whether a dictionary  has the same structure as another one. Values are ignored.

If `strict` is set, extra properties are not tolerated, the provided dictionaries must have the same keys.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. { "first": 0, "fifth": 0 }@0 received via `structure`
3. `strict` is set to false
4. `matches` sends true@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. { "first": 0, "seventh": 0 }@0 received via `structure`
3. `strict` is set to false
4. `matches` sends false@0

Example C:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. { "first": 0, "fifth": 0 }@0 received via `structure`
3. `strict` is set to true
4. `matches` sends false@0


### Input ports: 
* dict: {string:any}

    Receives the dictionary to test.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* structure: {string:any}

    Receives the dictionary with the reference structure, to which the comparison will be made.
    
    Example:
    { "first": 0, "fifth": 0 }


* strict: boolean

    Receives whether extra keys in `dict` are allowed.
    
    Example:
    true


### Output ports: 
* matches: boolean

    Sends a value indicating whether the dictionary matches the structure.
    
    Example:
    true




## Type tester

### Description:
Tells whether the `data` provided is a dictionary.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `data`
4. `is dict` sends true@0

Example B:
1. [ "first", "third" ]@0 received via `data`
4. `is dict` sends false@0

### Input ports: 
* data: any

    Receives the data to test for being a dictionary.
    
    Example:
    { "first": 1, "third": 0 }


### Output ports: 
* is dict: boolean

    Sends a value indicating whether the `data` received is a dictionary.
    
    Example:
    true




## Value tester

### Description:
Tests whether the value of  a certain `key` in a dictionary equals to the `value` provided.

If the `key` provided does not exist, the result will be false.

Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "third"@0 received via `key`
3. 3@0 received via `value`
4. `same` sends true@0

Example B:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "seventh"@0 received via `key`
3. 7@0 received via `value`
4. `same` sends false@0

Example C:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. "third"@0 received via `key`
3. 7@0 received via `value`
4. `same` sends false@0

### Input ports: 
* dict: {string:typeof`value`}

    Receives the dictionary to validate the value in.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 }


* key: string

    Receives the key in the dictionary to compare the value of.
    
    Example:
    "third"


* value: any

    Receives the value to test against the specified dictionary key.
    
    Example:
    3


### Output ports: 
* same: boolean

    Sends a value indicating whether the value is the same as the item with the specified key in the provided dictionary.
    
    Example:
    true
    
    




## Values getter

### Description:
Gets all values from the dictionary as an array.


Example A:
1. { "first": 1, "third": 3, "fifth": 5 } @0 received via `dict`
2. `values` sends  [ 1,3,5 ]@0

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/3_querying_data/3_1_getters

### Input ports: 
* dict: {string:any}

    Receives the dictionary to extract the values from.
    
    Example:
    { "first": 1, "third": 3, "fifth": 5 } 


### Output ports: 
* values: typeof`dict`[string]

    Sends the values of the dictionary as an array,
    
    Example:
    [ 1,3,5 ]


