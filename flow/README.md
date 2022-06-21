# flow

## Aggregator

### Description:
Aggregates inputs into an array until released.

A `release` signal must accompany each `data` signal, bearing the same tag.

The output reflects the order as received through `data`. Matching `release` signals may come in any order as long as each pairs up with a `data` signal.

Example:
1. true@1 is received via `release`
2. false@0 is received via `release`
3. "a"@0 is received via `data`
4. "b"@1 is received via `data`
5. ["a", "b"]@1 is sent via `aggregated`

### Input ports: 
* data: any

    Receives data items to be aggregated.


* release: boolean

    Receives flag whether to release aggregated inputs. Must be provided for each `data` input signal.


### Output ports: 
* aggregated: typeof `data`[]

    Sends the aggregated data.




## Aggregator (async)

### Description:
Aggregates inputs into an array until released.

The `release` signal is received and processed independently from those received via `data`. (As opposed to `flow/Aggregator`.)

The output reflects the order as received through `data`. 

Example:
1. "a"@0 is received via `data`
2. "b"@1 is received via `data`
3. null@2 is received via `release`
5. ["a", "b"]@2 is sent via `aggregated`

### Input ports: 
* data: any

    Receives data items to be aggregated.


* release: any

    Receives signal to release aggregated inputs. Independent of `data`.


### Output ports: 
* aggregated: typeof `data`[]

    Sends the aggregated data.




## Buffering gate (async)

### Input ports: 
* data: any

* open: any

### Output ports: 
* data: any



## Debouncer

### Description:
Debounces signals received through `data`.

Example:
1. `delay` is set to 1000.
2. "a"@0 received via `data`
3. waiting 0.5s (500ms)
4. "b"@1 received via `data`
5. waiting 1.1s (1100ms)
6. "b"@1 sent via `data` (output)

### Input ports: 
* data: any

    Receives signal to be debounced.


* delay: number

    Minimum delay in milliseconds between last signal received through `data` (input) and sent through `data` (output).
    
    Must be set as a parameter.


### Output ports: 
* data: typeof `data`

    Sends the debounced signal.




## Delayer

### Description:
Forwards each signal received via `data` (input) after waiting as many milliseconds as received or specified by `delay`.

### Input ports: 
* data: any

    Receives data to be forwarded.


* delay: number

    Receives / sets time to wait in milliseconds before forwarding the signal received via `data` (input).
    
    Can be both parameter or signal (For each input through `data`.)


### Output ports: 
* data: typeof `data`

    Data forwarded with a delay.




## Demultiplexer

### Description:
Forwards the data property of the received multiplexed signal to the output port matching the corresponding port ID (field).

Example:
1. `fields` is set to ["a", "b"]
2. Output ports `a` and `b` get created
3. {"field": "b", "data": 5} received via `multiplexed`
4. The number 5 will be sent via `b`.

### Input ports: 
* fields: (string[] or number[])

    Receives a list of output port names to send multiplexed data payload to.
    
    Must be parameter.


* multiplexed: {"field": string, "data": any}

    Receives multiplexed data.


### Output ports: 
* demultiplexed: typeof `multiplexed`["data"]

    Sends demultiplexed payload data.




## Depot

### Description:
Forwards signal received through `data` when corresponding signal was received via `trigger`.

Example:
1. "A"@0 received via `data` (input)
2. Wait 1s
3. null@0 received via `trigger`
4. "A"@0 is sent through `data` (output)

### Input ports: 
* data: any

    Receives data to be forwarded on trigger signal.


* trigger: any

    Receives a signal indicating that the corresponding `data` input signal may be forwarded.


### Output ports: 
* data: typeof `data`

    Sends signal as received through `data` (input).




## Fork

### Description:
Forwards input data to one of two outputs, depending on the condition.

Example:
1. false@0 received via `condition`
2. "A"@0 received via `data`
3. "A"@0 sent via `on false`

More:
https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/1_application_flow/1_1_junctions/README.md#example---using-forks

### Input ports: 
* data: any

    Receives the data to be forwarded to either output.


* condition: boolean

    Receives the evaluation of some condition.


### Output ports: 
* on true: typeof `data`

    Sends signal received via `data` when condition was true.


* on false: typeof `data`

    Sends signal received via `data` when condition was false.




## Forked aggregator (async)

### Description:
Aggregates data received via `data` into two output arrays, depending on whether a corresponding arbitrary input is received via `true` or `false`.

Releases both output arrays on receiving a signal on `release`.

The input `release` is independent from `data`, `true`, and `false`.

Example:
1. "foo"@0 is received via `data`
2. "bar"@1 is received via `data`
3. "baz"@2 is received via `data`
4. null@0 is received via `false`
5. null@1 is received via `true`
6. null@2 is received via `false`
7. null@3 is received via `release`
8. ["foo", "baz"]@3 is sent via `falses`, and ["bar"]@3 is sent via `trues`

### Input ports: 
* release: any

    Receives signal to release aggregated inputs. Independent of `data`.


* data: any

    Receives the data to be forwarded to either output.


* true: any

    Receives signal that corresponding `data` should be aggregated into `trues`.


* false: any

    Receives signal that corresponding `data` should be aggregated into `falses`.


### Output ports: 
* trues: typeof `data`[]

    Sends the aggregated data, that was accompanied by signals via `true`.


* falses: typeof `data`[]

    Sends the aggregated data, that was accompanied by signals via `false`.




## Forwarder

### Description:
Forwards signal received via `data` (input) to `data` (output).

Rarely necessary, and when it is used, it's usually to clean up nodes visually.

### Input ports: 
* data: any

    Receives data to be forwarded.


### Output ports: 
* data: any

    Sends forwarded data.




## Forwarder (double)

### Description:
Forwards both received signals in the order of the names of the ports.

Used for two purposes:
* Ensuring that any of a node's inputs may receive signals or be set as parameter.
* Ensuring the order in which signals are sent.

Example a) param vs. signal:
1. `2`(input) set to "B"
2. "A"@0 received via `1` (input)
3. "A"@0 sent via `1` (output)
4. "B"@0 sent via `2` (output)

Example b) signal order:
1. "B"@0 received via `2` (input)
2. "A"@0 received via `1` (input)
3. "A"@0 sent via `1` (output)
4. "B"@0 sent via `2` (output)

### Input ports: 
* 1: any

    Receives signal or takes parameter to be sent out first.


* 2: any

    Receives signal or takes parameter to be sent out second.


### Output ports: 
* 1: typeof `1`

    Forwards signal received via `1` (input).


* 2: typeof `2`

    Forwards signal received via `2` (input). Does not send before `1` (output).




## Forwarder (quadruple)

### Description:
Forwards all 4 received signals in the order of the names of the ports.

Used for two purposes:
* Ensuring that any of a node's inputs may receive signals or be set as parameter.
* Ensuring the order in which signals are sent.

For examples, see `flow/Forwarder (double)`.

### Input ports: 
* 1: any

    Receives signal or takes parameter to be sent out first.


* 2: any

    Receives signal or takes parameter to be sent out second.


* 3: any

    Receives signal or takes parameter to be sent out third.


* 4: any

    Receives signal or takes parameter to be sent out fourth.


### Output ports: 
* 1: typeof `1`

    Forwards signal received via `1` (input).


* 2: typeof `2`

    Forwards signal received via `2` (input). Does not send before `1` (output).


* 3: typeof `3`

    Forwards signal received via `3` (input). Does not send before `2` (output).


* 4: typeof `4`

    Forwards signal received via `4` (input). Does not send before `3` (output).




## Forwarder (triple)

### Description:
Forwards all 3 received signals in the order of the names of the ports.

Used for two purposes:
* Ensuring that any of a node's inputs may receive signals or be set as parameter.
* Ensuring the order in which signals are sent.

For examples, see `flow/Forwarder (double)`.

### Input ports: 
* 1: any

    Receives signal or takes parameter to be sent out first.


* 2: any

    Receives signal or takes parameter to be sent out second.


* 3: any

    Receives signal or takes parameter to be sent out third.


### Output ports: 
* 1: typeof `1`

    Forwards signal received via `1` (input).


* 2: typeof `2`

    Forwards signal received via `2` (input). Does not send before `1` (output).


* 3: typeof `3`

    Forwards signal received via `3` (input). Does not send before `2` (output).




## Gate

### Description:
Forwards signal received via `data` when corresponding signal received via `open` is true.

Example A:
1. "A"@0 received via `data`
2. false@0 received via `open`
3. No signal is sent via `data` (output)

Example B:
1. true@0 received via `open`
2. "B"@0  received via `data`
3. "B"@0 is sent via `data` (output)

### Input ports: 
* data: any

    Receives the signal to be forwarded / filtered.


* open: boolean

    Whether to forward the signal received via `data`.


### Output ports: 
* data: typeof `data`

    Forwarded / filtered signal




## Multiplexer

### Description:
Forwards data received via dynamic inputs to `multiplexed`, wrapped in a record which carries both the data and the ID of the port (field) that it was received through.

Example:
1. `fields` is set to ["a", "b"]
2. Input ports `a` and `b` get created
3. The number 5 received via `b`
4. {"field": "b", "data": 5} will be sent via `multiplexed`.

### Input ports: 
* fields: (string[] or number[])

    Receives a list of input port names to accept data payload through.


* demultiplexed: any

    Receives data payload for multiplexing.


### Output ports: 
* multiplexed: {"field": string, "data": typeof `demultiplexed`}

    Sends multiplexed data.




## Queued forwarder

### Description:
Forwards data received via `data` in the order defined by the tags of the signals received via `reference`.

Queues `reference` inputs until the first N signals have all received matching inputs via `data` then releases them one-by-one via `data` (output).

Used to signal sequence after asynchronous transformations.

Example:
1. "A"@0 received via `reference`
2. "B"@1 received via `reference`
3. "b"@1 received via 

### Input ports: 
* data: any

    Receives data to be forwarded.


* reference: any

    Receives signals that define the order of the forwarded signals, based on their tags.


### Output ports: 
* data: typeof `data`

    Sends forwarded data.




## Repeater

### Description:
Repeats the input the specified amount of times.

The tag on the repeat signals will contain the index of the current iteration.

Note that the repeats will be sent synchronously.

Example:
1. "A"@0 received via `data`
2. 3@0 received via `count`
3. "A"@"0:0" sent via `data`
4. "A"@"0:1" sent via `data`
5. "A"@"0:2" sent via `data`

### Input ports: 
* data: any

    Receives data to be repeated.


* count: number

    Receives the number of times the input is to be repeated.


### Output ports: 
* data: typeof `data`

    Sends the repeated signal.




## Shifter

### Description:
Shifts incoming data back in time by releasing the previously received data on each input. 

Example:
1. "A"@0 received via `data`.
2. "B"@1 received via `data`.
3. "A"@0 sent via `data` (output).

### Input ports: 
* data: any

    Receives signal to be shifted back.


### Output ports: 
* data: typeof `data`

    Sends previously received signal.




## Splitter

### Description:
Splits data received via `unsplit` by fields / indexes.

Do not use splitters to access optional record fields. Opt for a `data/dictionary/Item getter` in those cases instead.

Example A (record input):
1.`fields` is set to ["a", "b"]
2. Output ports `a` and `b` get created.
3. {"a": "foo", "b": "bar"}@0 received by `unsplit`
4. "foo"@0 is sent via `a`
5. "bar"@0 is sent via `b`

Example B (tuple input):
1.`fields` is set to [0, 1]
2. Output ports `0` and `1` get created.
3. ["foo", "bar"]@0 received by `unsplit`
4. "foo"@0 is sent via `0`
5. "bar"@0 is sent via `1`

More: https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/1_application_flow/1_3_synchronization/README.md#example---synchronizing-node-inputs.

### Input ports: 
* fields: (string[] or number[])

    Sets a list of output port names matching property names in the data received via `unsplit`.
    
    Must be parameter.
    
    Example:
    ["a", "b"]


* unsplit: ({string: any} or any[])

    Receives records or tuples to be split into individual items.
    
    Examples:
    * {"a": 5, "b": 2}
    * [5, 2]


### Output ports: 
* split: (typeof `unsplit`[string] or typeof `unsplit`[number])

    Sends input data split into individual fields.




## Starter

### Description:
Sends the signal null@"start" asynchronously right after the node was created at runtime.

Mostly used to kick-start the entire program.

### Output ports: 
* start: null

    Sends null@"start" right after the node's creation at runtime.




## Switch

### Description:
Routes data received via `data` to one of the outputs matching the value in `values`, or to `other` otherwise.

### Input ports: 
* values: string[]

* data: any

### Output ports: 
* data: typeof `data`

* other: typeof `data`



## Switch (deprecated)

### Description:
Use `flow/Splitter` or `flow/Switch` instead.

### Input ports: 
* fields: (string[] or number[])

* data: any

### Output ports: 
* output: typeof `data`

* bounced: typeof `data`



## Syncer

### Description:
Bundles input signals that have the same tag. All inputs must receive exactly one signal for a given tag (or be a parameter) for the bundle (record or tuple, depending on the type of `fields`) to be sent.

Example A (record):
1. `fields` is set to ["a", "b"]
2. Inputs ports `a` and `b` get created
3. `a` receives "Foo"@0
4. `b` receives "Bar"@0
5. `synced` sends {"a": "Foo", "b": "Bar"}@0

Example B (tuple):
1. `fields` is set to [0, 1]
2. Inputs ports `0` and `1` get created
3. `0` receives "Foo"@0
4. `1` receives "Bar"@0
5. `synced` sends ["Foo", "Bar"]@0

More: https://github.com/Cranq-io/cranq-tutorials/blob/main/reference/1_application_flow/1_3_synchronization/README.md#example---synchronizing-node-inputs

### Input ports: 
* fields: (string[] or number[])

    Sets a list of inupt port names matching property names in the data sent via `synced`.
    
    Must be parameter.
    
    Example values:
    * ["a", "b"] will result in record output
    * [0, 1] will result in a tuple output


* unsynced: any

    Receives individual item for syncing.


### Output ports: 
* synced: ({string: typeof `unsynced`} or typeof `unsynced`[])

    Sends synchronized inputs as a record or tuple indexed by the names of the ports they were received through.
    
    Example:
    {"a": "Foo", "b": "Bar"}




## Tag extractor

### Description:
Maps the signal received via `data` to its tag.

Example:
1. "A"@0 received via `data`
2. "0"@0 sent via `tag`

### Input ports: 
* data: any

    Receives the signal to extract the tag from.


### Output ports: 
* tag: string

    Sends the extracted tag.




## Tag incrementer

### Description:
Increments the iterable (colon-separated) part of the received signal's tag.

Bounces when tag is not iterable.

Used for lining up signals with iterations. (See eg. `data/array/Iterator`.)

Example A (success):
1. "A"@"x:1" received via `data`
2. "A"@"x:2" is sent via `data` (output)

Example B (invalid input):
1. "A"@"x" received via `data`
2. "A"@"x" is sent via `bounced`

See also:
* `flow/Tag nester`
* `flow/Tag trimer`

### Input ports: 
* data: any

    Receives signal with iterable tag.
    
    When the tag is not iterable, the signal will be bounced.


### Output ports: 
* data: typeof `data`

    Sends signal with data identical to the one received via `data`, but with incremented tag.


* bounced: typeof `data`

    Forwards the signal received through `data` when its tag was not iterable.




## Tag nester

### Description:
Creates a new level of iteration on the received tag, by appending ":0" to it.

Opposite of `flow/Tag trimmer`.

Used for lining up signals with iterations. (See eg. `data/array/Iterator`.)

Example:
1. "A"@0 received via `data`
2. "A"@"0:0" is sent via `data` (output)

See also:
* `flow/Tag incrementer`
* `flow/Tag trimer`

### Input ports: 
* data: any

    Receives the signal to be nested.


### Output ports: 
* data: typeof `data`

    Sends signal with data identical to the one received via `data`, but with nested tag.




## Tag trimmer

### Description:
Trims the last iterable (colon-separated) section of the tag on the signal received via `data`.

Bounces when tag is not iterable.

Opposite of `flow/Tag nester`.

Used for lining up signals with iterations. (See eg. `data/array/Iterator`.)

Example:
1. "A"@"x:9" received via `data`
2. "A"@"x" is sent via `data` (output)

### Input ports: 
* data: any

    Receives signal with iterable tag.


### Output ports: 
* data: typeof `data`

    Sends signal with data identical to the one received via `data`, but with the last iterable section removed from the tag.


* bounced: typeof `data`

    Forwards the signal received through `data` when its tag was not iterable.




## Throttler

### Description:
Throttles the received signal, forwarding only `count` number of signals in `delay` milliseconds.

Reports internal buffer size via `buffer size`.

Example:
1. `delay` set to 3000, `count` set to 1 
1. A@1 received via `data`
2. B@2 received via `data` a second later
3. B@2 sent immediately via `data`
4. C@3 received via `data`
5. 1@3 sent via `buffer size`
6. C@3 sent via `data` a second later
6. 0@3 sent via `buffer size`


### Input ports: 
* data: any

    Receives data to be throttled / rate limited.


* delay: number

    Receives the length of the time window in milliseconds, in which to limit the number of signals.
    
    Can be set as parameter.


* count: number

    Receives the maximum number of signals to be forwarded in the specified time window.
    
    Can be set as parameter.


### Output ports: 
* data: typeof `data`

    Forwards the signals received via `data`, throttled.


* buffer size: number

    Sends the current size of the throttler's internal buffer.
    
    Only sent when the size changes.
    
    Used for raising errors related to exceeding allowed buffer size.


