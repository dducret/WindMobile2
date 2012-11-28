WindMobile API
===========
Version 2.0
===========

This API is based on Wind Mobile developed by la-haut.info and on WindSpots.com

The API provides interface to real-time weather information published from various provider like JDC, Windline, and WindSpots.com allowing you to create a real time weather application

Data are returned in JSON format

API V2 Reference
================

* Station  
  List
     
* User  
  Authentication

* Weather  
  Data  
  Wind  
  WindSensor  
  WindForecast  

* Error Codes


## Station List

The list with the details of each station


Parameters

token

mandatory in header

The API User token

allstation

optional

To get running (true) or all stations

true or false, default is false

wgs84latitude

optional

User latitude for range

wgs84longitude

optional

User longitude for range

range

Optional

The area zone in km.

If wgs84lat and/or wgs84lon provided default range is 50

#### Example request

    http://api.windspots.com/2.0/stationlist/allStation/true

[
Providerproviderwindspots
Station IdidstationCHGE01
Station Short NameshortnameLe reposoir
Station NamenameGenève – Le reposoir
Station Location Typetype1 = Paragliding Take of, 2 = Paragliding Landing, 3 = Sailing
Latitude wgs84wgs84latitude
Longitude wgs84wgs84longitude
Altitudealtitude
Number of Wind Sensornbwindsensor
Main Wind Sensorwindsensor
Number of Cameranbcamera
Main Cameracamera
Timedatetime
Wind Averagewindaverage
Wind Directionwinddirection
Wind Gust Speedwindgustspeed
Wind Gust Directionwindgustdirection
Maintenance Statusmaintenance
], …




## User Authentication


Authentication of the user 


Parameters

api

mandatory in header

The API key

user

mandatory

User ID

password

mandatory

User password

#### Example request

    http://api.windspots.com/2.0/userauthetication/user/544/password/Password01

{
  "provider": windspots,
  "token":12345678,
}




## Weather Data

The last weather data for a station.


Parameters

token

mandatory in header

The API User token

idstation

mandatory

The ID of the station

#### Example request

    http://api.windspots.com/2.0/weatherdata/idstation/windspots:CHGE01

[
Providerproviderwindspots
Station IdidstationCHGE01
Last Updatelastupdate
Wind Averagewindaverage
Wind Directionwinddirection
Wind Gust Speedwindgustspeed
Wind Gust Directionwindgustdirection
Wind Trendwindtrend
Wind Sensor idsensor
Air Temperatureairtemperature
Air Humidityairhumidity
Water Temperaturewatertemperature
Barometerbarometer
Maintenance Statusmaintenance
]




## Weather Wind

The wind data for a time period for a station


Parameters

token

mandatory in header

The API User token

idstation

mandatory

The ID of the station

duration

optional

The duration in minutes
default is 60

###### Example request

    http://api.windspots.com/2.0/weatherwind/idstation/windspots:CHGE01/duration/60

[
Providerproviderwindspots
Station IdidstationCHGE01
Timedatetime
Wind Averagewindaverage
Wind Directionwinddirection
Wind Gust Speedwindgustspeed
Maintenance Statusmaintenance
], …



## Weather WindSensor

The wind data for a time period for sensor of a station


Parameters

token

mandatory in header

The API User token

idstation

mandatory

The ID of the station

duration

optional

The duration in minutes

Default 60 minutes

Sensor

optional

The sensor id

Default 1

###### Example request

    http://api.windspots.com/2.0/weatherwindsensor/idstation/windspots:CHGE01/duration/60/sensor/1

[
Provider  provider  windspots
Station Id idstation CHGE01
Wind Sensor idsensor
Maintenance Status maintenance
[
  Time  datetime
  Wind Average  windaverage
  Wind Direction  winddirection
  Wind Gust Speed windgustspeed
  Wind Gust Direction windgustdirection
], …


## Weather ForeCast

The wind forecast data for a station location


Parameters

token

mandatory in header

The API User token

idstation

mandatory

The ID of the station

###### Example request

    http://api.windspots.com/2.0/weatherforecast/idstation/windspots:CHGE01


Provider provider windspots
Station Id idstation CHGE01
[
 Time datetime
 Wind Average windaverage
  Wind Direction winddirection
], …


## Error Codes

The API attempts to return appropriate HTTP codes for every request.


Code  Text  Description
200 OK  Success
401 Unauthorized  Authentication missing or incorrect
403 Forbidden The request has been refused or access denied
404 Not Found A
429 Too Many Requests A
500 Internal Server Error Something get wrong.
503 Service Unavailable a

The API returns error messages

In JSON:
{"errors":[{"message":"Sorry, that function does not exist","code":20}]}

In XML:
<?xml version="1.0" encoding="UTF-8"?>
<errors>
  <error code="20">Sorry, that function does not exist</error>
</errors>

Code Text Description
20  Sorry, that function does not exist Corresponds with an HTTP 404 - the specified resource was not found.
