
#### Recap: 
- MAC Addresses
	- First 6 characters (first 24 bits): Organizationally Unique Identifier (OUI) 
		- Identifies the vendor that made the device. 
		- AA:BB:CC:DD:EE:FF
			- The 'AA:BB:CC' is the OUI 
	- MAC address table
		- Used by switches to know which devices are out which ports
- ARP Table
	- We can view the ARP table to see things like our gate way. 
		- Potentially see what model of a router the place is using. 
- Routing Table
	- Used by the router to determine which subnets are out which port. 
- Default gateway
	- Is given to a device by DHCP (or set statically)
	- It will be the IP of the router interface facing the LAN that the device is on. 

### Local Area Network (LAN)
**![](https://lh6.googleusercontent.com/q20qOu97oCvRymjEZWNa8iYB31O44j_zX5UV5GGGT9_NY0tEz3TaoRpU9TtLYSq94HFmUzEGykK51zotosB6Q8bUOeh27jpjQuJN91evGW2LB97xaozjMtvCUumeCuiaZUBDrQDyK83WmWEPhvdk6U0)**
In the figure above. We are **only** using switches. 
- Only connecting **Layer 2** capable devices
	- AKA.. everything will be in the same subnet at the moment. 

If we were to add a router in between the building connection
- Connecting one switch to one router interface and the other to another router interface. 
	- We would then have **TWO** LANs. 

Broadcast Traffic (ARP requests and such) will be contained to that LAN. 
- Terminology: "Everything is layer 2 adjacent"
	- These devices are all in the same LAN. 
	- By default: 
		- Everything in the LAN will be able to talk to each other/see each other

### Ethernet
Is a collection of different standards that are used for LAN communication. [[Etherchannels]]
- Family of standards, defined by the IEEE that describes the data link and physical layer.
**![](https://lh3.googleusercontent.com/Kdd6cxycFmYDgdJ5iO2Ancz-PWJX0KkRNIQle_JLGNOogcP0F7xMpQ5EPiwVHRJQjRS0kYMeNUyp-QDV5ARAYELC4vdk2pEFkwAQcLxxA0Le453odGSTQMM7CU2OZ-xlrCz0xSKNabtvdIzQjsUjrHA)**
- Each different speed of connection is a different **Ethernet** standard. 
For example: 

**![](https://lh6.googleusercontent.com/coYb-TdPcMzZq7JMwXc8MvtLBdTjMfOp7ItGJDwpXJ1RLdhYYIqkGnaGd57649IPh8N_x8ApGBd8Je_IuCJ76avCT_Hh1HWAASUH2h3mmNlUICX7HhmLl7QNq8AiqWtO3AiiOhfpYSHwR3N7UXaYc_U)**
- In the figure above, we are using **FOUR** different Ethernet standards. 

### Domains
#### Collision Domains
- All devices connected to a Hub is one big collision domain
- Each individual port on a switch is itself a collision domain
	- Meaning... you SHOULD NOT have any collision, as there is nothing to collide with. 
#### Broadcast Domain
**![](https://lh4.googleusercontent.com/tjbJBrxyYrwDw3IcWcTkwm3LAWyeGXdnsm8EWUu73sSbOrNElCkCYwgOvpKc0JeWWe5By-HgyGREkfdEeKVGg78B8o5lxyJ2q-JGrTC2t_6hcbAqoNhrpSTtqj_VV2peAMLlSsdNH8OG62mw3Qo5oj0)**

- Switches will send broadcasts out every connected interface minus the one that the broadcast came in from. 
- A **LAN** (broadcast domain) can be huge. 
	- Note the problem with this. Any time a PC sends a single ARP request. Every single connected port (minus one) will be flooded. 
- Broadcast storm
	- Devices might start freaking out and flooding non-stop broadcasts. Which can grind that particular LAN/Broadcast domain to a halt. 
		- Can even affect devices all the way up to the router itself. Which is discarding the broadcasts. 
- Breaking up broadcast storms
**![](https://lh5.googleusercontent.com/EtNSQqagHsKO_8lXE91TpGMJs6JrwJsSFgETg4nH0nKCz7JN6Z66ku7xgCuwEtRsrwE--FrkkSg2TOFNDRYAuQYYNsVV5xN-m27laVQLlT8_KA9HSCm_l5bnaCZPtyLTur9Ce4fhCjh3bI2dbvozkoo)**
- We replaced SW1 with a router. So now instead of a single broadcast domain, we have three broadcast domains. As seen in the figure below. 
	- This can be a bit inefficient. Note that this is where [[VLANS]] come into play. 
![[Pasted image 20230711123115.png]]

### Switches 
- A switch will start to build its MAC address table as it receives traffic from devices on its own. 
	- When a device ARPs, the switch will receive that frame and then learn the AMC address of the device based on that frame. 
		- Only learning from the Source MAC address and not the destination. 
	- When the destination device replies with its own MAC address, the switch will receive that frame and learn the MAC address of that device; adding it to the MAC address table. 
		- Basically.. "Okay, this MAC address is VIA this port. This one is via that one."
- MAC address table entries will time out over a specific time. 
	- Devices are generally continuing to send traffic, so the entries are continually getting updated. 
		- Meaning the MAC address table is constantly changing, increasing and decreasing entries. 
- Example: 
	- Let us say that we have a PC that DOES have an ARP entry for another PC, but our switch DOESN'T have an entry in the MAC address table. 
		- The switch will learn the MAC address of the source (our PC). Then look if there is a specific entry for the destination MAC on one of its ports. 
			- In this case, the answer will be; "No there is not a entry with that MAC address"
		- It will flood that frame out to all connected interfaces. 
		- Then the other PC will eventually respond back with its own MAC address. Which will update the MAC address table. 


