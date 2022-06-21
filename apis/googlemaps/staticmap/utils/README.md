# apis/googlemaps/staticmap/utils

## Area definition classifier

### Input ports: 
* area: (
{
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
}
)

### Output ports: 
* center area: {
  "center": [number, number],
  "zoom": number
}

* unknown: any



## Size stringifier

### Input ports: 
* size: [number, number]

### Output ports: 
* string: string

