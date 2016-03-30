## Presence Webhooks
The Aerohive presence webhooks enable steaming presence and location data to your server in near-realtime. We will make a POST call to your web server with fresh information about the physical clients in your network every 60 seconds.

### Setup
##### Creating Your Web Server
The first thing you will need to use Presence Webhooks is a webserver that is configured to accept incoming JSON. 
For development, you can use Sinatra & Ruby to quickly set up a webserver to listen to POST requests at /presence.

```rb
require 'sinatra'
require 'json'

post '/presence' do
  push = JSON.parse(request.body.read)
  puts "I got some data from HiveManager: #{push.inspect}"
end
```

To learn more about Sinatra, check out the [Sinatra guide.]

Save the above script somewhere and run it. You should see some output like this:
```sh
== Sinatra/1.4.4 has taken the stage on 4567 for development with backup from Thin
>> Thin web server (v1.5.1 codename Straight Razor)
>> Maximum connections set to 1024
>> Listening on localhost:4567, CTRL+C to stop
```
Now we're ready to listen for incoming data. Of course, in production, you'll want to set up something more robust than this.

#### Configuring Hive Manager to Send Presence Analytics Data
HiveManager may be configured to send data to your server either through the user interface, or by using the webhooks configuration API.
##### Using the HiveManger WebApp
In order to receive streaming presence data, you must configure HiveManager to communicate with your sever. Log into HiveManager, and click the 'settings' icon. In the left navigation bar, click on 'API Data Management'. After clicking the '+' icon, you should see a screen like this:
!(New Data Feed)

The Post URL should match exactly where you expect the data to arrive on your server.
"Access Token" is a secret value which your server should check accompanies each POST to ensure no one is attempting to forge requests.

##### Using the Webhooks Configuration APIs (beta)
Make a POST request to <your datacenter>/xapi/beta/configuration with the following headers:
|Header                         |   Value               |
|-------------------------------|:----------------------|
|X-AH-API-CLIENT-SECRET         | (your client secret)  |
|X-AH-API-CLIENT-ID             | (your client ID)      |
|X-AH-API-CLIENT-REDIRECT-URI   | (your redirect URL)   |
|Authorization                  | (your access token)   |
|Content-Type                   | application/json      |

The JSON body of the POST request must contain the following:
```
{
  "application": "string",
  "ownerId": 0,
  "secret": "string",
  "url": "string"
}
```
Application is the name of the application receiving the data.

Secret is a string value (may be random) which you should verify on all incoming data to ensure that it's really from HiveManager and not forged.

URL is the exact address where we should send the data to your server.

#### Sample Data:
```
{
"ownerId" : "1082983976",
"apMac" : "3a1e6d8c785c",
"observations" : [ {
"clientMac" : "dcac3da506b4",
"ipv4" : "191.45.252.67",
"ipv6" : null,
"seenTime" : "2015-10-09T07:00:00.000+0000",
"seenEpoch" : 1264988544,
"ssid" : "Retail World",
"rssi" : -50,
"manufacturer" : "Apple",
"os" : "ios",
"lat" : 45,
"lng" : 122,
"unc" : 5,
"x" : 0,
"y" : 0
}, {
"clientMac" : "dcac3da506b4",
"ipv4" : "191.45.252.67",
"ipv6" : null,
"seenTime" : "2015-10-09T07:00:00.000+0000",
"seenEpoch" : 1264988544,
"ssid" : "Retail World",
"rssi" : -50,
"manufacturer" : "Apple",
"os" : "ios",
"lat" : 45,
"lng" : 122,
"unc" : 5,
"x" : 0,
"y" : 0
}, {
"clientMac" : "dcac3da506b4",
"ipv4" : "191.45.252.67",
"ipv6" : null,
"seenTime" : "2015-10-09T07:00:00.000+0000",
"seenEpoch" : 1264988544,
"ssid" : "Retail World",
"rssi" : -50,
"manufacturer" : "Apple",
"os" : "ios",
"lat" : 45,
"lng" : 122,
"unc" : 5,
"x" : 0,
"y" : 0
} ]
}
```

[Sinatra guide.]: http://www.sinatrarb.com/