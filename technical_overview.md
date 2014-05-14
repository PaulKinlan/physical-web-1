##Technical Overview
Details on now the current process works. This is a working system and is being used to understand and explore the system. It is a prototype so must change. This repos is here to collect feedback and insights to improve the overall system design.

###Broadcast
The current design uses Bluetooth LE (BLE) devices that broadcast the URL in the advertising packet. It doesn't do anything else, it doesn't support any GATT profiles, or responds to any connection requests. The sole job of the device is to broadcast the URL to the surrounding area. 

The reason for this is to accommodate potentially large numbers of devices in an area. If the user's phone had to query every device it would become exponentially hard in a mall with lots of people and lots of devices. By making the device constantly broadcast, it makes things it easier for lots of phones to just pick up the information passively.

This has another advantage in that it means that a user can walk through a space and 'leave no trace' the devices have no idea who is listening. 

The broadcast is currently done by using the BLE NAME parameter. This is currently for demo purposes only. There is a proposal to the BLE standards body to have a URL parameter and once that is agreed to, we'll switch over. The current limitation to the URL length is 28 bytes which is unfortunately a bit too short. Switching over to the URL parameter will allow for a tiny bit of compression but should only allow for URLs a bit longer, potentially up to 36 bytes. This is hopefully a temporary issue as the next BLE spec will allow advertising packets to be much longer, up to 100 bytes which should significantly reduce this constraint.

The current prototype broadcasts every 1 second. This is a somewhat arbitrary choice, chosen to allow users to get a complete list without having to wait too long. This should accommodate up to 100 devices with in a receive radius. However, this timing should be discussed further.

###Client
The current client is an application to prove out the technology. If you open the app, it lists the nearby beacons that it can see, sorted by signal strength. Note the signal strength is a very iffy metric to sort on as it there many reasons why it can vary. However, if you are standing in front of device and the next device is >10 feet away, it tends to work out well in practice. We are currently using ble boards that all broadcast at exactly the same signal strength. An obvious improve would be to send the TXT_POWER in the ad packet (a defined BLE spec parameter) so the client could to a better sorting. 

There are lots of different UX directions to go beyond a simple application and we hope to explore alternatives here. We're keeping with the application for now as it simpler and faster to prototype.

The client lists the meta information from the URL: TITLE, DESCRIPTION, URL, and FAVICON. These could be pulled at run time but there is a simple server that acts as a cache to speed up this process.

###Server
The server receives a request from the client with all of the URLs found and returns a JSON data structure listing all of the meta information listed about. The current prototype collects no user data, only returning the casched info. However alternative implementations could keep track of user choice and use that to help change the ranking within the client.

Just to be clear, the Client/Server combination will likely for a single service. If someone wants to try a different client, they will most likely want to try a different server.
