# data/array

## Aggregation iterator

### Description:
Iterates through items of an array, specifically for the purpose of being aggregated later.

### Input ports: 
* array: any[]

    Recieves array to be iterated over.
    
    Example:
    [1,2,3]


### Output ports: 
* item: typeof `array`[number]

    Sends current item.
    
    Example:
    1


* is last: boolean

    Sends flag whether current item is the last one.
    
    To be connected directly to the `release` input of a `flow/Aggregator`.




## All same as expected tester

### Description:
Tests whether all elements of an array are the same as the expected value.

Example:
1. `array` recieved  [1,1]@0  
2. `expected` recieved  1]@0  
3.  true@0 sent via `same`

### Input ports: 
* array: any

    Receives array to be tested.
    
    Example: 
    [1,2,3]


* expected: any

    Receives the expected value that all elements of the array will be tested against.
    
    Example:
    1


### Output ports: 
* same: boolean

    Sends whether all elements of the `array` are the same as the `expected` value.
    
    Example:
    true




## Array to string concatenator

### Description:
Concatenates an array to string, using the specified delimiter.

### Input ports: 
* array: any[]

    Receives array to be concatenated.
    
    Example:
    ["A", "B", "C"]


* delimiter: string

    Receives the delimiter to use between array elements.
    
    Example:
    ","


### Output ports: 
* concatenated: string

    Sends the concatenated array.
    
    Example:
    "A,B,C"




## Builder

### Description:
Builds an array of identical items.

Example:
1. "Foo"@0 recieved via  `item`
2. 3@0 recieved via `count` 
3. ["Foo", "Foo", "Foo"]@0 sent  via `array`

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/2_constructing_data/2_2_builders

### Input ports: 
* item: any

    Receives item to be added to the array.
    
    Example:
    "Foo"


* count: number

    Receives the number of times the item is to be add to the array.
    
    Example:
    3


### Output ports: 
* array: typeof `item`[]

    Sends the built array.
    
    Example:
    ["Foo", "Foo", "Foo"]




## Concatenator

### Description:
Concatenates two arrays.

Example:
1. [1,2]@0 recieved via `a`
1. [3,4]@0 recieved via `b`
3. [1,2,3,4]@0 sent via `concatenated`

More:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/2_constructing_data/2_4_merge_concat/README.md#example---concatenating-arrays

### Input ports: 
* a: any[]

    Receives array `a` to concatenate.
    
    Example:
    [1,2]


* b: any[]

    Receives array `b` to concatenate.
    
    Example:
    [3,4]


### Output ports: 
* concatenated: (typeof `a` or typeof `b`)

    Sends the concatenated array.
    
    Example:
    [1,2,3,4]




## Contains tester

### Description:
Tests whether the array contains a given item

Example:
Example:
1. [1,2]@0 received via `array` 
2. 1@0 received via `item` 
3. true@0 sent via `contains`

### Input ports: 
* array: any[]

    Recieves array look for the item in.
    
    Example:
    [1,2]


* item: any

    Recieves item to find in the array.
    
    Example:
     1


### Output ports: 
* contains: boolean

    Sends whether the `item` was found in the `array`.
    
    Example:
    true




## Emptiness tester

### Description:
Tests whether array is empty.

Example:
1. []@0 received via `array` 
2. true@0 sent via `empyty`

### Input ports: 
* array: any[]

    Receives array to be tested.
    
    Example:
    []


### Output ports: 
* empty: boolean

    Sends whether the `array` does not contain any element.
    
    Example:
    true




## Filter

### Description:
Filters array. External node(s) receive each item and decide whether to include them in the result.

Example:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/3_querying_data/3_2_filters/README.md#using-filters

### Input ports: 
* array: any[]

    Receives array to be filtered.
    
    Example:
    [1,2,3,4]


* include item: boolean

    Receives whether to include the current (by tag) item.
    
    Example:
    true


### Output ports: 
* filtered: typeof `array`

    Sends the filtered array.
    
    Example:
    [1,2]


* item: typeof `array`[number]

    Sends the current item.
    
    Example:
    1




## First item getter

### Description:
Retrieves first item of the array.

Example:
1. [1,2]@0 received via `array`
2. 1@0 sent via `item`

More:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/3_querying_data/3_1_getters/README.md#getting-the-first--last-array-elements

### Input ports: 
* array: any[]

    Receives array to retrieve first item from.
    
    Example:
    [1,2]


### Output ports: 
* item: typeof `array`[number]

    Sends first item of the array.
    
    Example:
    1




## Flattener

### Description:
Flattens a 2D array into a  1 D array with.

Example:
1. [[1,2], [3,4]]@0 recieved via `2D array`
2. [1,2,3,4]@0 sent via `array` 

### Input ports: 
* 2D array: any[][]

    Recieves 2D arrays to be flattened.
    
    Example:
    [[1,2], [3,4]]


### Output ports: 
* array: (typeof `2D array`[number][number])[]

    Sends flattened array.
    
    Example:
    [1,2,3,4]




## Has same length tester

### Description:
Tests whether two arrays have the same length

Example:
1. [1,2]@0 recieved via `array1` 
2. [3,4]@0 recieved via `array2`
3. true@0 sent via `has same length`

### Input ports: 
* array1: any[]

    Recieves array1 to compare its lenght.
    
    Example:
    [1,2]


* array2: any[]

    Recieves array2 to compare its lenght.
    
    Example:
    [3,4]


### Output ports: 
* has same length: boolean

    Sends whether length of array1 and array1 is the same.
    
    Example:
    true




## Item appender

### Description:
Appends item to the array.

Example: 
1. [1,2,3]@0 recieved via `array` 
2. 1@0 recieved via `item` 
3. [1,2,3,1]@0 sent via `array`

### Input ports: 
* array: any[]

    Receives array to append item to.
    
    Example:
    [1,2,3]


* item: any

    Receives item to append to the array.
    
    Example:
    1


### Output ports: 
* array: typeof `array`

    Sends the new array with the appended item.
    
    Example:
    [1,2,3,1]




## Item deleter

### Description:
Deletes item from the array at the specified index.

Example: 
1.  [1,2,3]@0 recieved via array 
2. 1@0 recieved via `index` 
3. [1,3]@0 sent via `array`

More:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/2_constructing_data/2_1_setters_deleters/README.md#example---deleting-items-from-arrays

### Input ports: 
* array: any[]

    Recieves array to delete item from.
    
    Example:
    [1,2,3]


* index: number

    Recieves index which identifies item to be deleted from the array.
    
    Example:
    1


### Output ports: 
* array: typeof `array`

    Sends array with specified item deleted.
    
    Example:
    [1,3]




## Item getter

### Description:
Retrieves item from the specified index.
If the item is not found, the inputs are sent via `not found`.

Example A:
1. [1,2]@0  received via `array`
2. 1@0  recieved via `index`
3. 2@0  sent via `item`

Example B:
1. [1,2]@0  received via `array`
2. 9@0  recieved via `index`
3. {"array":[1,2], "index":9}@0  sent via `not found`

More:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/3_querying_data/3_1_getters/README.md#getting-array-element-by-index

### Input ports: 
* array: any[]

    Recieves array to retrieve item from.
    
    Example:
    [1,2]


* index: number

    Recieves index which identifies item to be retrieved in the array.
    
    Example:
    1


### Output ports: 
* item: typeof `array`[number]

    Sends item at the specified index.
    
    Example:
    2


* not found: typeof `not found` of `get item`



## Item inserter

### Description:
Inserts item into the array at the specified index.

Example: 
1. [1,2,3]@0 recieved via `array` 
2.  1@0 recieved via `index` 
2. 1@0 recieved via `item` 
3. [1,1,2,3]@0 sent via `array`

More:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/2_constructing_data/2_1_setters_deleters/README.md#example---inserting-items-into-arrays

### Input ports: 
* array: any[]

    Recieves array to insert into.
    
    Example:
    [1,2,3]


* index: number

    Recieves index at which to insert.
    
    Example:
    1


* item: any

    Recieves item to be inserted.
    
    Example:
    1


### Output ports: 
* array: (typeof `array`[number])[]

    Sends array with specified item inserted.
    
    Example:
    [1,1,2,3]




## Item prepender

### Description:
Inserts item into the beginning of the  array.
Example: 
1. [1,2,3]@0 recieved via `array` 
2.  4@0 recieved via `index` 
3. [4,1,2,3]@0 sent via `array`



### Input ports: 
* array: any[]

    Recieves array to prepend to.
    
    Example:
    [1,2,3]


* item: typeof`array`[number]

    Recieves item to prepend.
    
    Example:
    4


### Output ports: 
* array: typeof `array`

    Sends array with specified item inserted to the begining.
    
    Example:
    [4,1,2,3]




## Iteration aggregator

### Input ports: 
* data: any

    Receives data items to be aggregated.
    
    Signal tag is expected to have an index. (From iteration)


* release: boolean

    Receives flag whether to release aggregated inputs. Must be provided for each `data` input signal.
    
    Signal tag is expected to have an index. (From iteration)


### Output ports: 
* aggregated: typeof `data`[]

    Sends the aggregated data.
    
    Last index will be removed from the input's tag.




## Iterator

### Description:
Iterates through items of an array.


Examples:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/1_application_flow/1_2_iterators

### Input ports: 
* array: any[]

    Recieves array to be iterated over.
    
    Example:
    [1,2,3]
    


### Output ports: 
* item: typeof`array`[number]

    Sends current item.
    
    Example:
    1


* index: number

    Sends current index.
    
    Example:
    0


* done: typeof `array`



## JSON parser

### Description:
Parses a JSON string to  array.

Examples:
A.
1. "[1,2]"@0 recieved via `json`
2. [1,2]@0 sent via `parsed`

B.
1. "{}]"@0 recieved via `json`
2. "{}]"@0 sent via `bounced`

### Input ports: 
* json: string

    Recieves JSON string.
    
    Example:
    "[1,2]"


### Output ports: 
* parsed: any[]

    Sends the parsed array.
    
    Example:
    [1,2]


* bounced: string

    In case of error during parsing or when the result of the parseisng is not array it sends the `json` input string.
    
    Example:
    "{}]"




## Last index tester

### Input ports: 
* array: any[]

* index: number

### Output ports: 
* is last: boolean



## Last item getter

### Description:
Retrieves last item of the array.

Example:
1. [1,2]@0 received via `array`
2. 2@0 sent via `item`

More:
https://github.com/Cranq-io/cranq-tutorials/tree/main/reference/3_querying_data/3_1_getters#getting-the-first--last-array-elements

### Input ports: 
* array: any[]

    Recieves array to retrieve last item from.
    
    Example:
    [1,2]


### Output ports: 
* item: typeof`array`[number]

    Sends last item of the array.
    
    Example:
    2




## Length getter

### Description:
Determines the length of the input array.

Example:
1. [1,2]@0 received via `array`
2. 2@0 sent via `length`

### Input ports: 
* array: any[]

    Recieves array to determine length of.
    
    Example:
    [1,2]


### Output ports: 
* length: number

    Sends `array` length.
    
    Example:
    2




## Mapper

### Description:
Maps array. External node(s) receive each item and send back a mapped item.

Example:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/3_querying_data/3_3_mappers/README.md#using-mappers

### Input ports: 
* array: any[]

    Recieves array to be mapped.
    
    Example:
    ["Foo", "Bar"]


* mapped item: typeof`array`[number]

    Recieves the current (by tag) item, mapped.
    
    Example:
    "Foo A"


### Output ports: 
* mapped: typeof`mapped item`[]

    Sends the mapped array.
    
    Example:
    ["Foo A", "Bar A"]


* item: typeof`array`[number]

    Sends the current item.
    
    Example:
    "Foo"


* index: number



## Order reverser

### Description:
Reverses the order of items in the received array.

Example:
1. [1,2,3]@0 received via `array`
2. [3,2,1]@0 sent via `reversed`

### Input ports: 
* array: any[]

    Recieves array to reserve.
    
    Example:
    [1,2,3]


### Output ports: 
* reversed: typeof`array`

    Sends reversed array.
    
    Example:
    [3,2,1




## Reducer

### Description:
Reduces array. External node(s) receive the partial result and each item and send back a new partial result.

Example:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/3_querying_data/3_4_reducers/README.md#using-reducers

### Input ports: 
* array: any[]

    Receives array to be reduced.
    
    Example:
    ["A", "B", "C"]


* initial: typeof `array`[number]

    Receives initial value for the reduced array
    
    Example:
    ""


* part reduced: typeof `initial`

    Receives reduced array before the current (by tag) item.
    
    Example:
    "AB"


### Output ports: 
* reduced: typeof `initial`

    Sends the reduced array.
    
    Example:
    "ABC"


* item: typeof `array`[number]

    Sends the current item.
    
    Example:
    "C"


* part reduced: typeof `initial`

    Sends reduced array after the current (by tag) item.
    
    Example:
    "A"




## Repeater

### Description:
Repeats the input data for each item in the array.

Example:
1. [1,2,3]@0 receiced via `array`
2. "foo"@0 received via `data`
3. "foo"@0:0
    "foo"@0:1
    "foo"@0:2
sent via `data`
    

### Input ports: 
* array: any[]

    Recieves array which specifies number of times to repeat data.
    
    Example:
    [1,2,3]


* data: any

    Recieves data to be repeated.
    
    Example:
    "foo"


### Output ports: 
* data: typeof`data`

    Sends repeated data with tag.
    
    Example:
    "foo"




## Slicer

### Description:
Slices a section out of an array.

Example: 
1. [1,2,3]@0 received via `array`
2. 0@0 received via `from`
3. 2@0 received via `from`
4. [1,2]@0 sent via `array`

### Input ports: 
* array: any[]

    Receives array to slice out of.
    
    Example:
    [1,2,3]


* from: number

    Receives start position of the slice (included).
    
    Example:
    0


* to: number

    Receives end position of the slice (not included.
    
    Example:
    2


### Output ports: 
* slice: typeof`array`

    Sends section sliced out of the input array.
    
    Example:
    [1,2]




## Sorter

### Description:
Sorts an array according to the specified reference array (`params`["order"]).

### Input ports: 
* array: any[]

* params: {
  "order": any[],
  optional "direction": (1 or -1)
}

### Output ports: 
* sorted: typeof `array`



## Splitter

### Description:
Create 2D array from 1D array.

Example:
1. [1,2,3]@0 recieved via  array`
2. 2@0 recieved via  `count`
3.  [[1,2],[3]]@0 sent via `array` 

### Input ports: 
* array: any

    Receives array to be splitted.
    
    Example:
    [1,2,3,2]


* count: any

    Receives the size of the columns of the 2D array.
    
    Example:
    2


### Output ports: 
* 2D array: any

    Sends the created 2D array.
    
    Example:
    [[1,2],[3,4]]




## Step iterator

### Description:
Iterates over the items of an array, asynchronously.

Tags are controlled:

On receiving the array, the node sends out the first item (if any) using a nested tag. (":0" appended to the original tag.)

Subsequent items will be sent out on receiving signals on `next`, with incremented tags.

### Input ports: 
* array: any[]

    Sets up iteration and sends out the first item and index 0 with an iterable tag based on the original tag.
    
    When the array has only one or zero elements, a signal with the same tag will also be sent through `done`.
    
    Example:
    [1,2,3]


* next: any

    Triggers sending out the next item and index, or, when there are no more items, the done signal.
    
    Tags on signals received through `next` are expected to be iterable, and identical to the tag sent out for the previous item. (This allows for simple loopbacks between `item` and `next`.)
    
    Tags on signals sent out on `item` and `index` are incremented versions of what was received through `next`.
    
    Example:
    0


### Output ports: 
* item: typeof`array`[number]

    Sends the next item in the array.
    
    Tags are iterable, and nested versions of the tag of the received array. (If the array tag was "start", item tags will be "start:0", "start:1", etc.)
    
    Example:
    1


* index: number

    Sends the next index in the array.
    
    Tags are iterable, and nested versions of the tag of the received array. (If the array tag was "start", item tags will be "start:0", "start:1", etc.)
    
    Example:
    0


* done: typeof`array`

    Sends out the iterated array when there are no more items in the array and a signal received through `next`, or, when an array is received through `array` that has one or 0 items.
    
    The tag of the outgoing signal matches that of he original array.
    
    Example:
    [1,2,3]


* bounced: any

    Sends any `next` signal that didn't satisfy the iterable tag requirement.
    




## Step iterator (manual tags)

### Description:
Iterates over the items of an array asynchronously.

On receiving the array, the node sends out the first item (if any) using the same tag.

Subsequent items will be sent out on receiving signals on `next`, using the same tag.

### Input ports: 
* array: any[]

    Sets up iteration and sends out the first item and index 0 with the tag associated with the received array.
    When the array has only one or zero elements, a signal will also be sent through `done`. 
    
    Example:
    ["A","B","C"]


* next: any

    Triggers sending out the next item and index, or, when there are no more items, the done signal.
    
    Signals sent out on `item` and `index` bear the same tag as the signal received through `next`.
    
    Example:
    0


### Output ports: 
* item: typeof`array`[number]

    The next item in the array.
    
    The first item (index 0) bears the tag of the received array, subsequent items bear the tag of the corresponding signals received through `next`.
    
    Example:
    "A"


* index: number

    The next index in the array.
    
    The first index (0) bears the tag of the received array, subsequent indexes bear the tag of the corresponding signals received through `next`.
    
    Example:
    0


* done: typeof`array`

    Sends out the iterated array when there are no more items in the array and a signal was received through `next`, or, when an array was received through `array` that has one or 0 items.
    
    The tag of the outgoing signal matches that of he original array.
    
    Example:
    ["A","B","C"]




## Step mapper

### Input ports: 
* array: any[]

* mapped item: any

### Output ports: 
* mapped: typeof `mapped item`[]

* item: typeof `array`[number]

* done: any

* bounced: any



## Type tester

### Description:
Tells whether the input is an array.

Example:
1. [1,2,3]@0 received via `data`
2. true@0 sent via `is array`

### Input ports: 
* data: any[]

    Receives data to test if its type is array.
    
    Example:
    [1,2,3]


### Output ports: 
* is array: boolean

    Sends if the type of the recieved `data` is array.
    
    Example:
    true




## Wrapper

### Description:
Wraps input in a 1-element array

### Input ports: 
* data: any

### Output ports: 
* array: [typeof `data`]

