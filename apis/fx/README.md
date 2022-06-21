# apis/fx

## Yahoo Finance

### Input ports: 
* symbol: any

### Output ports: 
* instrument: any



## Yahoo Finance historical adjusted closed price & timestamp getter

### Input ports: 
* instrument: typeof `tree` of `select adjusted prices`

    [Inherited from port `tree` of `select adjusted prices`] 
    Receives the tree the node is extracted from


### Output ports: 
* timestamps: typeof `synced` of `syncer`

    [Inherited from port `synced` of `syncer`] 
    Sends synchronized inputs as a record or tuple indexed by the names of the ports they were received through.
    
    Example:
    {"a": "Foo", "b": "Bar"}


* adjustedcloses: any



## Yahoo Finance rates per date converter

### Input ports: 
* timestamps: typeof `array` of `create rates per date mapping`

    [Inherited from port `array` of `create rates per date mapping`] 
    Receives array to be reduced.
    
    Example:
    ["A", "B", "C"]


* prices: typeof `array` of `iterate over adjusted close prices`

    [Inherited from port `array` of `iterate over adjusted close prices`] 
    Recieves array to be iterated over.
    
    Example:
    [1,2,3]
    


### Output ports: 
* rates per date: typeof `reduced` of `create rates per date mapping`

    [Inherited from port `reduced` of `create rates per date mapping`] 
    Sends the reduced array.
    
    Example:
    "ABC"




## Yahoo index getter

### Input ports: 
* symbol: any

### Output ports: 
* index: any

