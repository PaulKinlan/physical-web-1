##Technical Overview
This is a prototype system being used to understand and explore the issues involved in building the Physical Web.

###Broadcast
The current design uses Bluetooth LE (BLE) devices that broadcast the URL in the advertising packet. It doesn't do anything else: it doesn't support any GATT profiles or responds to any connection requests. The sole job of the device is to broadcast the URL to the surrounding area. 

The reason  is to accommodate potentially the worst case scenario of a large numbers of devices in an area with a large amount of people. If every user's phone had to query every device it would become exponentially hard. By making each device constantly broadcast, it makes things it easier for any number of people to just pick up the information passively.

This has another advantage in that it means that a user can walk through a space and 'leave no trace': the devices have no idea who is listening. 

The broadcast is currently done by using the BLE NAME parameter. This is for demo purposes only. There is a proposal to the BLE standards body to have a URL parameter type and once that is agreed to, we'll switch over. The current limitation to the URL length is 28 bytes which is unfortunately a bit too short. Switching over to the URL parameter will allow for a tiny bit of compression but should only allow for URLs to be a bit longer, potentially up to 36 bytes. This is hopefully a temporary issue as the next BLE spec will allow advertising packets to be much longer, up to 100+ bytes which should significantly reduce this constraint.

The current prototype broadcasts every 1 second. This is a somewhat arbitrary choice, chosen to allow users to get a complete list without having to wait too long. This should accommodate up to 100 devices with in a receive radius. However, this timing should be discussed further.

###Client
The current client is an application to prove out the technology. If you open the app, it lists the nearby beacons that it can see, sorted by signal strength. Note the signal strength is a very iffy metric as it there many reasons why it can vary. However, if you are standing in front of device and the next device is >10 feet away, it tends to work out well in practice. We are currently using BLE boards that all broadcast at exactly the same signal strength. An obvious improvement would be to send the XMT_POWER in the ad packet (a defined BLE spec parameter) so the client could to better sorting by signal strength. 

There are lots of different UX directions to go beyond a simple application and we hope to explore alternatives here. We're keeping with the application for now as it simpler and faster to prototype. The obvious alternatives would be to use silent notifications or a widget.

The client lists the meta information from the URL: TITLE, DESCRIPTION, URL, and FAVICON. These could be pulled at run time but there is a simple server that acts as a cache to speed up this process.

###Server
The server receives a request from the client with all of the URLs found and returns a JSON data structure listing all of the meta information listed about. The current prototype collects no user data, only returning the casched info. However alternative implementations could keep track of user choice and use that to help change the ranking within the client.

Just to be clear, the Client/Server combination will likely for a single service. If someone wants to try a different client, they will most likely want to try a different server.

###Meta Data
In order to use URLs, the system expects those URLs to point to a web page, which offers up the meta information described above. This somewhat limits the URLs as they much then always point to a valid HTML page. This is likely a big limitation to URLs that want to link to native applications. This is an imporant use case and needs to be discussed. Is there an alternative way to offer this meta data but not point to a web page?

###Ranking
As more devices are found, the importance of ranking the devices becomes more valuable. Sorting only be signal strength is a good start but the server could do a much better job in two ways. The first would be to track which URLs are clicked as that implies value, so higher used URLs could be ranked higher. In addition, the server could track personal use so if you tend to pick the same device at work, it would be sure to rank the device higher as well. 

### Security
At this point, the URL is broadcast as plain text so it is not really viable for personal use (as neighbors could know what devices you have in your home) There is nothing stopping a URL service from delivering obfuscated URLs or even a URL that requires login in order to see the information.
