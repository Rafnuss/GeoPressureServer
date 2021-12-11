# GeoPressureServer

## Introduction

GeoPressureServer is a JSON API that makes it easy to compute the mismatch of a geolocator pressure timeserie with reanalysis data.



This docs describe how to use the [GeoPressureServer](http://glp.mgravey.com/GeoLocPressure/) API. We hope you enjoy these docs, and please don't hesitate to [file an issue](https://github.com/Rafnuss/GeoPressureServer/issues/new) if you see anything missing.


## Requests

```http
http://glp.mgravey.com/
```


### Pressure map

```http
GET /GeoLocPressure/v1/pressureMap.py/?api_key=12345678901234567890123456789012
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `W` | `number` | **Required**. West coordinate. -180° to 180°. |
| `S` | `number` | **Required**. South coordinate. 0° to 90°. |
| `E` | `number` | **Required**. East coordinate. -180° to 180°. |
| `N` | `number` | **Required**. North coordinate. 0° to 90°. |
| `scale` | `number` | Number of pixel per latitude, longitude. 10 for a resultion of 0.1° (~10) and 4 for a resolution of 0.25° (~30km). To avoid interpolating the ERA5 data, `scale` should be smaller than 10. Read more about `scale` on [Google earth Engine documention.](https://developers.google.com/earth-engine/guides/scale) |
| `pressure` | `array of number` | **Required**. Atmospheric pressure to match in Pascal. |
| `time` | `array of number` | **Required**. [UNIX time](https://en.wikipedia.org/wiki/Unix_time) of the pressure data (i.e., number of second since 1-janv-1970.  |
| `label` | `array of string` | **Required**. Define the grouping of the pressure data. All pressure with the same label will be match together |


## Responses

Many API endpoints return the JSON representation of the resources created or edited. However, if an invalid request is submitted, or some other error occurs, Gophish returns a JSON response in the following format:

```javascript
{
  "message" : string,
  "success" : bool,
  "data"    : string
}
```

 - The `message` attribute contains a message commonly used to indicate errors or, in the case of deleting a resource, success that the resource was properly deleted.

 - The `success` attribute describes if the transaction was successful or not.

 - The `data` attribute contains any other metadata associated with the response. This will be an escaped string containing JSON data.

## Status Codes

GeoLocPressure returns the following status codes in its API:

| Status Code | Description |
| :--- | :--- |
| 200 | `OK` |
| 201 | `CREATED` |
| 400 | `BAD REQUEST` |
| 404 | `NOT FOUND` |
| 500 | `INTERNAL SERVER ERROR` |

