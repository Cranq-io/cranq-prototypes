# apis/googlemaps/staticmaps

## Image fetcher

### Description:
Fetches image of a specified area on a global map.

### Input ports: 
* area: ({
  optional "type": "center",
  "center": [number, number],
  "zoom": number
}
or
{
  "type": "path",
  "points": [number, number][],
  "style": {
    optional "weight": number,
    optional "color": string,
    optional "fillColor": string,
    optional "geodesic": boolean
  }
}
or
{
  "type": "markers",
  "points": [number, number][],
  "style": {
    optional "size": ("tiny" or "mid" or "small"),
    optional "color": string,
    optional "label": string
  }
})

    Defines the area to be captured.


* params: {
  "apiKey": string,
  "size": [number, number],
  optional "scale": number,
  optional "format": ("png8" or "png" or "png32" or "gif" or "jpg" or "jpg-baseline"),
  optional "mapType": ("roadmap" or "satellite" or "hybrid" or "terrain"),
  optional "language": string,
  optional "region": string
}

    Optional params are ignored ATM.


### Output ports: 
* image: string

* response: any

* error: {
  "error": string,
  optional "details": any
}

