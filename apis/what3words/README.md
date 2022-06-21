# apis/what3words

## Coordinates to words

### Input ports: 
* coordinates: [number, number]

    Receives the coordinates to be converted to what3words.
    
    Format: [latitude, longitude]


* params: {
  "apiKey": string,
  optional "language": string,
  optional "format": ("json" or "geojson")
}

    Receives what3words API parameters.


### Output ports: 
* data: ({
  "country": string,
  "square": {
      "southwest": {
          "lng": number,
          "lat": number
      },
      "northeast": {
          "lng": number,
          "lat": number
      }
  },
  "nearestPlace": string,
  "coordinates": {
      "lng": string,
      "lat": string
  },
  "words": string,
  "language": string,
  "map": string
}
or
{
  "features": [
      {
          "bbox": [number, number, number, number],
          "geometry": {
              "coordinates": [number, number],
              "type": "Point"
          },
          "type": "Feature",
          "properties": {
              "country": string,
              "nearestPlace": string,
              "words": string,
              "language": string,
              "map": string
          }
      }
  ],
  "type": "FeatureCollection"
})

    Sends data structure describing the geographical area identified by the 3-word address.


* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

* error: {
  "error": string,
  optional "details": any
}



## Words to coordinates

### Description:
Converts what3words word triple to geo coordinates.

More:
https://what3words.com

### Input ports: 
* words: [string, string, string]

    Receives a word triple that identifies any 3m x 3m area on the surface of the Earth.
    
    Example:
    ["pretty", "needed", "chill"]


* params: {
  "apiKey": string,
  optional "format": ("json" or "geojson")
}

    Receives what3words API parameters.


### Output ports: 
* data: ({
  "country": string,
  "square": {
      "southwest": {
          "lng": number,
          "lat": number
      },
      "northeast": {
          "lng": number,
          "lat": number
      }
  },
  "nearestPlace": string,
  "coordinates": {
      "lng": string,
      "lat": string
  },
  "words": string,
  "language": string,
  "map": string
}
or
{
  "features": [
      {
          "bbox": [number, number, number, number],
          "geometry": {
              "coordinates": [number, number],
              "type": "Point"
          },
          "type": "Feature",
          "properties": {
              "country": string,
              "nearestPlace": string,
              "words": string,
              "language": string,
              "map": string
          }
      }
  ],
  "type": "FeatureCollection"
})

    Sends data structure describing the geographical area identified by the 3-word address.


* response: {
  "status": number,
  "headers": {string: any},
  "body": string
}

* error: {
  "error": string,
  optional "details": any
}

