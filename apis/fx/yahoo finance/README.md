# apis/fx/yahoo finance

## Daily rates getter

### Input ports: 
* symbol: string

    Receives ticker symbol.
    
    Example:
    "DIS"


* from: number

    Receives start date timestamp for querying data.
    
    Example:
    1486598400


* to: number

    Receives end date timestamp for querying data.
    
    Example:
    1644364800


* interval: ("1d" or "5d" or "1mo" or "3mo" or  "6mo" or "1y" or "2y" or "5y" or "10y" or "ytd" or "max")

    Receives the interval of the `rates per date` output


### Output ports: 
* rates per date: {string: number}

    Sent the rates of the symbol per interval


* error: {
  "error": "Service unavailable"
}



## Historical rates getter

### Input ports: 
* symbol: string

* from: number

* to: number

* interval: string

### Output ports: 
* instrument: any

* error: {
  "error": "Service unavailable"
}

