# Aerohive Location APIs
Aerohive Location APIs allow business access to real-time location statistics in order to improve customer engagement, loyalty, and operational efficieny across sites. Data collected by the Access Point is sent to the Aerohive Cloud Services platform, processed, and made available via APIs. You may use the data from ACS to compare visitor trends over time, map high-traffic areas of a store, or visit frequency. 

## Retail Analytics Partners:
![Cloud4Wi](http://cloud4wi.com/wp-content/uploads/2015/08/logo_cloud4wi.png)

Using Cloud4Wi, you can provide your customers with fully customizable Guest Wi-Fi and an enhanced on-site experience to connect them to your brand for increased loyalty. The platform collects valuable information on your customers behaviors and empowers youto boost your business performance. Lastly, you can design personable user journeys to push your marketing and advertising messages and influence your customers purchase intents.
Along with Aerohive, Cloud4Wi provides you maximum flexability and scalability. Using the pay-as-you-grow pricing model, you can reduce your total cost of ownership. Get started with [Cloud4Wi free today]!


![EuclidAnalytics](http://vnn2n6zoye-flywheel.netdna-ssl.com/wp-content/themes/euclid16/images/logo.png)

[Euclid Analytics] and Aerhoive make it fast and easy to collect insightful data across your entire retail chain. Rapidly understanding customer traffic and behaviors to optimize marketing, in-store operations, strategic decision-making and staffing activities. 

### Setup
To use the Location and Presence Analtytics built into the Aerohive Cloud Services platform, you must **enable presence data collection** on your hardware. The easiest way to do so is by navigating to Configure -> Common Objects -> Radio Profiles, and selecting a radio profile you use on your network. ![RadioProfile](https://raw.githubusercontent.com/aerohive/StoreSurge/master/RadioProfile.tiff)
Near the bottom of the page, you will see a section on Presence Server. Presence Analytics must be turned on in order to collect presence data.
![Presence Server](https://raw.githubusercontent.com/aerohive/StoreSurge/master/PresenceSettings.tiff)

### Location API Calls
>In order to make API calls to the Aerohive Location APIs, you must have an API Access Token. If you have not already obtained one, read the section on [authentication] before proceeding further.

### Streaming Location Data with Webhooks
The Aerohive Cloud Services plaform allows you to stream real-time location and presence analytics to your server via webhooks. To enable streaming, refer to the [webhooks documentation] for how to get started.

### Requesting Data with REST APIs
##### Client Presence & Client Presence Time Series
The client presence APIs are designed to give businesses and education insightful statistics as to the relative numbers of people that pass by or visit their locations.
Review the [API details] for more information on different calls and parametrs that can be used for these APIs. **Note:** The Location ID used by these queries may be obtained by first making a call to the [Location Folders API] to retreive your location hierarchy and ID numbers.

Client Presence Time Series is designed to give the number of visitors and passersby to a location, over a specified time period. 

```sh
curl -X GET -H "X-AH-API-CLIENT-SECRET: YOUR-CLIENT-SECRET" \
-H "X-AH-API-CLIENT-ID: YOUR-CLIENT-ID" -H \
"X-AH-API-CLIENT-REDIRECT-URI: YOUR-REDIRECT-URL" \
-H "Authorization: Bearer YOUR-ACCESS-TOKEN" \
"https://cloud-va.aerohive.com/xapi/v1/clientlocation/clientpresence?ownerId=1265&location=5433133630928&startTime=2016-03-03T22:46:14.000Z&endTime=2016-03-06T15:49:32.000-08:00&timeUnit=OneHour"
```

The Client Presence API will give 'engaged' (user has spent more than 5 minutes in a 20 minute window within moderate range of the AP) and associated (user has selected to use the AP for internet access) values for each client observed at a specified location and time period.
```sh
curl -X GET -H "X-AH-API-CLIENT-SECRET: YOUR-CLIENT-SECRET" \
-H "X-AH-API-CLIENT-ID: YOUR-CLIENT-ID" \
-H "X-AH-API-CLIENT-REDIRECT-URI: YOUR-REDIRECT-URL" \
-H "Authorization: Bearer YOUR-ACCESS-TOKEN" \
"https://cloud-va.aerohive.com/xapi/v1/clientlocation/clientpresence?ownerId=1265&location=5433133630928&startTime=2015-12-01T22:46:14.000Z&endTime=2015-12-15T15:49:32.000-08:00&timeUnit=OneHour"
```

##### Client Location
The client location API will give the current coordinates of the client devices in as XY coordinates on your building floorplan. If you have entered GPS coordinates for your AP locations, the API will return calculated GPS coordinates for the client location.

![Floorplan](https://github.com/aerohive/StoreSurge/raw/master/Floormap.tiff)
```sh
curl -X GET -H "X-AH-API-CLIENT-SECRET: YOUR-CLIENT-SECRET" \
-H "X-AH-API-CLIENT-ID: YOUR-CLIENT-ID" \
-H "X-AH-API-CLIENT-REDIRECT-URI: YOUR-REDIRECT-URL" \
-H "Authorization: Bearer YOUR-ACCESS-TOKEN" -H \
"https://cloud-va.aerohive.com/xapi/v1/location/clients/?ownerId=1265"
```
#### Data Provided
|Name       |Description        |
|:-----------|:-------------------|
|apMac      | The MAC address of the observing AP |
|clientMac	| The MAC Address of the client device. This data is currently provided as-is but may be obfuscated or hashed in future releases|
|ipv4	    | Client IPv4 address; null if not available or device is unassociated with the reporting Access Point|
|ipv6	    | Client IPv6 address; null if not available or device is unassociated with the reporting Access Point
|seenTime	| Observation time in UTC; e.g. "2015-01-01T00:00:00Z"|
|seenEpoch	| Unix timestamp in milliseconds since the current epoch.|
|ssid	    | Network SSID name to which to client device is connected; null if the device is unassociated.|
|rssi	    | The RSSI of the client device, as measured by the Access Point |
|manufacturer|	The manufacturer of the client device; null if the device manufacturer cannot be determined |
|os	        | The client device operating system or null if the OS could not be determined |
|lat	    | The GPS latitude of the client device |
|lng	    | The longitude of the client device |
|unc	    | Uncertainty in meters |
|x	        | X offset|
|y	        | Y offset|


### Version
0.95

aerohive-developer@aerohive.com

[Cloud4Wi free today]: <https://controlpanel.cloud4wi.com/freemium/aerohive>
[Euclid Analytics]: <http://euclidanalytics.com/products/>
   [configuring a User Group]: <http://docs.aerohive.com/330000/docs/help/english/ng/learning-whats-new.htm#gui/configuration/configuring-user-group.htm>
   [authentication]: <https://developer.aerohive.com/docs/authentication>
   [video tutorial]: <https://training.aerohive.com/#/courses/course/207185>
   [API details]: <https://developer.aerohive.com/docs/api-documentation#!/clientlocation>
   [Location Folders API]: <https://developer.aerohive.com/docs/api-documentation#!/configuration-device-location>
   

