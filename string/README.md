# string

## Concatenator

### Description:
Concatenates two strings together.

Example:

1. "Hello"@0 is received via `a`
2. " world!"@0 is received via `b`
3. "Hello world!"@0 is sent via `concatenated`

### Input ports: 
* a: string

    The first string


* b: string

    The second string


### Output ports: 
* concatenated: string

    Sends the concatenation of the two inputs.




## Contains tester

### Description:
Tests whether the value received via `string` contains the value received via `substring`.

Example:

1. "Quick brown fox"@0 is received via `string`
2. "brown"@0 is received via `substring`
3. true@0 is sent via `contains`

### Input ports: 
* string: string

    The string to look for the substring in


* substring: string

    The string to find


### Output ports: 
* contains: boolean

    Whether the string contains the substring




## Custom template filler

### Description:
Substitutes parameters into a template. Parameter placeholder's (token) start/end can be customized.

Example:

1. "Hello {#subject#}!"@0 is received via `template`
2. {"subject":"world"}@0 is received via params
3. "{#"@0 is received via `token start`
4. "#}"@0 is received via `token end`
5. "Hello world!"@0 is sent via `filled`

### Input ports: 
* template: string

    Receives the template string to replace parameters in.
    
    Example:
    "Hello {#subject#}!"


* params: {string: any}

    Receives the parameters to replace in the template.
    
    Example: 
    {"subject":"world"}


* token start: string

    Receives the string that marks the start of the parameter placeholder (token) within the template.
    
    Example:
    "{#"


* token end: string

    Receives the string that marks the end of the parameter placholder (token) within the template.
    
    Example:
    "#}"


### Output ports: 
* filled: typeof `filled` of `fill template`

    Sends the template string with replaced parameters.
    
    Example:
    "Hello world!"


* error: typeof `error` of `fill template`

    Sends error in case any occurs during operation.
    
    Example: 
    {"error": "Some error message"}




## Emptiness tester

### Description:
Tells whether the value received on `string` is empty.

Example:

1. ""@0 is received via `string`
2. true@0 is sent via `empty`

### Input ports: 
* string: string

    The string to be tested for emptiness.


### Output ports: 
* empty: boolean

    Sends true if the string is empty, false otherwise.




## Equality tester

### Description:
Checks if the string received on `a` is equal to string received via `b`.

Example:

1. "foo"@0 is received via `a`
2. "bar"@0 is received via `b`
3. false@0 is sent via `equal`

### Input ports: 
* a: string

    The first string


* b: string

    The second string


### Output ports: 
* equal: boolean

    Sends true if the two strings are the same, false otherwise.




## Global regex matcher

### Description:
Executes a global regex pattern match.

Flavour depends on the running environment.

### Input ports: 
* string: string

    The string.


* regex: string

    The regex pattern


### Output ports: 
* matches: boolean

    Whether the given regex matches the given string


* groups: string[]

    Groups matched by the given regex pattern




## Handlebar style template filler

### Description:
Substitutes parameters into a template. Parameters are marked by Handlebars style tokens.

Example:

1. "Hello {{subject}}!"@0 is received via `template`
2. {"subject":"world"}@0 is received via params
3. "Hello world!"@0 is sent via `filled`

### Input ports: 
* template: string

    Receives the template string to replace parameters in.
    
    Example:
    "Hello {{subject}}!"


* params: {string: any}

    Receives the parameters to replace in the template.
    
    Example: 
    {"subject":"world"}


### Output ports: 
* filled: string

    Sends the template string with replaced parameters.
    
    Example:
    "Hello world!"


* error: {"error": string}

    Sends error in case any occurs during operation.
    
    Example: 
    {"error": "Some error message"}




## Joiner

### Description:
Joins an ordered list of strings into a single string.

Example:

1. ["Hello", "!"]@0 is received via `substrings`
2. " world"@0 is received via `separator`
3. "Hello world!"@0 is sent via `joined`

### Input ports: 
* separator: string

    The separator string


* substrings: string[]

    Array containing the parts


### Output ports: 
* joined: string

    Sends the joined parts, separated by the separator string.




## Length getter

### Description:
Determines the length of the value received on `string`.

Example:

1. "foo"@0 is received via `string`
2. 3@0 is sent via `length`

### Input ports: 
* string: string

    The string


### Output ports: 
* length: number

    The length of the string.




## Line splitter

### Description:
Splits a string by lines.

Example:
1. 'string' receives 
"line1
line2
line3"
2. 'lines' emits
["line1","line2","line3"]


### Input ports: 
* string: string

    Receives the string to split by lines.
    
    Example:
    "line1
    line2
    line3"


### Output ports: 
* lines: string[]

    Emits the array of lines.
    
    Example:
    ["line1","line2","line3"]




## Lowercaser

### Description:
Converts `string`  to lower case.

Example:
1. "Foo"@0  received via `string`
2. "Foo"@0  sent via `lowercase`

### Input ports: 
* string: string

    Receives string to be converted to lower case.
    
    Example:
    "Foo"


### Output ports: 
* lowercase: string

    Sends `string` converted to lower case.
    
    Example:
    "foo"




## Regex matcher

### Description:
Matches a string to a non-global regular expression, and returns substrings that match the regular expression's groups.

### Input ports: 
* regex: string

* string: string

### Output ports: 
* groups: (string[] or null)

* not found: any



## Regex tester

### Description:
Tests whether the input string matches a regular expression.

### Input ports: 
* string: string

    String to be tested against the specified RegEx.


* regex: string

    Regular expression to test the specified string against.
    
    Flavour depends on the running environment.


### Output ports: 
* matches: boolean

    Whether the received string matched the RegEx.




## Slugifier

### Input ports: 
* text: any

* lowercase: boolean

* separator: string

### Output ports: 
* slug: any



## Splitter

### Description:
Splits the  value received on `string` by the value received on `separator`.

Example:

1. "foo.bar.baz"@0 is received via `string`
2. "."@0 is received via `separator`
3. ["foo", "bar", "baz"]@0 is sent via `substrings`

### Input ports: 
* separator: string

    The separator string


* string: string

    The string to be splitted


### Output ports: 
* substrings: string[]

    Sends the array of the parts.




## Template filler

### Description:
Substitutes parameters into a template.

Example:

1. "Hello {subject}!"@0 is received via `template`
2. {"subject":"world"}@0 is received via params
3. "Hello world!"@0 is sent via `filled`

### Input ports: 
* template: string

    The template to be filled


* params: {string:any}

    The actual parameters used for filling the template


### Output ports: 
* filled: string

    Sends the template filled with the given values from params.




## Trimmer

### Description:
Removes whitespace from both ends of  `string` input.

Example:
1. "  foo"@0 received via `string`
2. "foo"@0 sent via `trimmed`

### Input ports: 
* string: string

    Receives string to be trimmed.
    
    Example:
    "  foo"


### Output ports: 
* trimmed: string

    Sends trimmed string.
    
    Example
    "foo"




## Type tester

### Description:
Tells whether the input is a string.

### Input ports: 
* data: any

    The value to be tested.


### Output ports: 
* is string: boolean

    Sends true if the data is a string, false otherwise.




## Uppercaser

### Description:
Converts `string`  to uppercase.

Example:
1. "Foo"@0  received via `string`
2. "FOO"@0  sent via `uppercase`

### Input ports: 
* string: string

    Receives string to be converted to uppercase.
    
    Example:
    "Foo"


### Output ports: 
* uppercase: string

    Sends `string` converted to upper case.
    
    Example:
    "FOO"




## URI component encoder

### Description:
URI component-encodes the received string.

Example:
1. "hello world"@1 received via `string`
2. "hello%20world"@1 sent via `encoded`

### Input ports: 
* string: any

    Receives a string to be URI component-encoded.


### Output ports: 
* encoded: string

    Sends the URI component-encoded string.


