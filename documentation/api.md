WindMobile API 2.0
==================

The API provides interface to real-time weather information published from various providers like [JDC](http://meteo.jdc.ch), [Windline](http://www.windline.ch), and [WindSpots](http://windspots.com) allowing you to create a real time weather application.


Making a request
----------------

```shell
curl -u user:pass -H 'User-Agent: MyApp (yourname@example.com)' http://api.windspots.com/2.0/stationlist
```


No XML, just JSON
-----------------

We only support JSON for serialization of data. **All API URLs end in .json to indicate that they return JSON.**

You'll receive a `415 Unsupported Media Type` response code if you attempt to use a different URL suffix or leave out the `Content-Type` header.


Identify your app
-----------------

You must include a `User-Agent` header with the name of your application and a link to it or your email address so we can get in touch in case you're doing something wrong (so we may warn you before you're blacklisted) or something awesome (so we may congratulate you). Here's an example:

    User-Agent: WindMobile (http://github.com/ysavary/WindMobile2-Android)

If you don't supply this header, you will get a `403 (Forbidden)`.


Authentication
--------------

Authentication is required by some providers. TBD...


Handling errors
---------------

The API attempts to return appropriate HTTP codes for every request.

    200 (OK)  
    401 (Unauthorized)	          : Authentication missing or incorrect  
    403 (Forbidden)               : Missing User-Agent that indentifies your application  
    404 (Not Found)  
    415 (Unsupported Media Type)  
    429 (Too Many Requests)  
    500 (Internal Server Error)   : Something get wrong  
    503 (Service Unavailable)  


API
---

Station

- [Detail](#station_detail)
- [List](#station_list)

User

- [Authentication](#user_authentication)

Weather

- Data
- Wind
- WindSensor
- WindForcast


### <a id="station_detail"></a> Station detail

The station detail information

    http://api.youprovider.com/2.0/station/:id 

Parameters

* **id** the id of the station    

```json
{
    "name": "Station",
    "properties": {
        "pro": {
            "title": "Provider",
            "description": "The name of the data provider of this station",
            "type": "string",
            "required": true
        },
        "id": {
            "title": "Station ID",
            "type": "string",
            "required": true
        },
        "sna": {
            "title": "Short name",
            "required": true,
            "type": "string"
        },
        "na": {
            "title": "Name",
            "required": true,
            "type": "string"
        },
        "typ": {
            "title": "Station type",
            "description": "1=paragliding takeoff, 2=paragliding landing, 3=sailing",
            "required": true,
            "type": "number",
            "enum": [1, 2, 3]
        },
        "lat": {
            "title": "Latitude wgs84",
            "required": true,
            "type": "number",
        },
        "lon": {
            "title": "Longitude wgs84",
            "required": true,
            "type": "number",
        },
        "alt": {
            "title": "Altitude",
            "required": true,
            "type": "number",
        },
        "tim": {
            "title": "Time",
            "description": "Time in rfc3339, for example 2012-12-19T16:39:57+01:00",
            "required": true,
            "type": "string"
        },
    }
}
```


### <a id="station_list"> Station list

The list with the details of each station

    http://api.youprovider.com/2.0/station?lat=46.630544&lon=6.511739&range=100&status=green&status=orange

Parameters

* **lat** WGS84 user latitude for range  
* **lon** WGS84 rser longitude for range  
* **range** The area zone in km. If lat and/or lon is provided default range is 50
* **status** 'green', 'orange' or 'red'. Default is 'green' only


```json
[{station1}, {station2}, ...]
```  


### Authentication

Authentication of the user





