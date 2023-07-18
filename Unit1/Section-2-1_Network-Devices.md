### Three basic device types: Hubs, Switches, and Routers
- #### Hubs: (Layer 1) 
	- Aren’t in use anymore. 
	- Slow.
	- Copied all the packets to all the other ports.
	- **Collisions.**
		- The device could only process one device “talking” at once. 
			- If two PCs try to send data at the same time there would be a collision. 
			- The hub would handle one of the packets, and the other PC would be forced to send their packet again (hopefully without collision). 
  
![](https://lh6.googleusercontent.com/z8XeFb-jC_Tj8hVTXKBqqleFXJS3qVyFmeiW5n-zuCROjc3y8gfbcdCQVIDJdUtyi6Jvj04puPu171_WUCmZoES1GmST_jtGYMhMYqrWlsd5YfvjfkmlV-MZv0jIIU-yOm8dANYhoGyliRkeFX6utMQ)

For an example: If PC0 and PC1 tried to talk at the same time there would be a collision. 
This DOES NOT scale well. 


![](https://lh3.googleusercontent.com/XYVe6REuB8Bkl6jCJQbgM779Vbj-E52uba3aFhpGorFs23t9cgKXV6kbZfqh-WIff1d1rmR0l-uAJkY6ls0ASeXFkgdHyZ-GLYtY9cyUAZVB5msw67_vg2KcrynU5CwO7_HUOc7db_hrXy2AsnL5GGU)

The more devices that are added… the more collisions that will occur.
Even if you add a second hub. The entire setup is a Collision Domain. 

##### Copies all the packets to all the other ports.
- A hub will flood out the packets coming in out of every connected port. 
- In Figure 2..
	- If we would ping PC1 from PC0. The packet would hit the hub. 
	- That packet will be sent out to all connected ports (including Hub1). 
	- A packet would also be sent from Hub0 to Hub1 which would then distribute the packet to the other two PCs (PC6 and PC7). 
		- Forcing all of the devices except the destination to just throw away the packet. 

##### What if we tell our PC not to drop things that aren’t meant for us?
- It could potentially lead to information being stolen. 
- Let us inspect plaintext passwords. 
- See where the traffic is supposed to be going. 
	- Everything and anything that should leave you with a bad taste in your mouth could happen when it really shouldn’t.

### Switches: (Layer 2) 
- Vast improvement to hubs. 
- Each individual port is its own collision domain. 
	- Collisions would never occur on a switch port. 
		- If it does, usually it's some layer 1 issue - bad cable/damaged NIC/etc. 
- Improved speed, reliability, etc.. 

#### Unmanaged Switches
- Can’t connect to it in any way. 
- Cannot pull any stats or data from it. 
- Can't apply different VLANs to it. 
- Can’t troubleshoot data. 
	- Also called “dumb” switches. 
	- Fine for house or maybe small business.
	- When only extra ports are needed. 
- VERY cheap. 

#### Factors to keep in mind: 
- Is it managed or unmanaged. 
- What is the port density (How many ports does it have) 
- What is the main port speed (1 Gb is fine for most of our stuff, but we might want 10Gb uplinks) 
- How many SFP/uplink ports do we have/need
	- Some others are: 
		- Switch-stacking
		- Redundant power supplies.
		- etc..

### Layer 3 Switches: 
- A switch and a router combined into a single device. 
- Does all the router and switching all on one device. 

#### Routers: (Layer 3)
- Uses layer 3 headers (Source/destination IP addresses and packet data) in order to make their forwarding decisions. 
- Traditionally… 
	- You wouldn’t plug individual PCs into the router interfaces. 
	- You’d connect routers to other routers or to switches only. 

**Note: End devices connect to switches, Routers/firewalls handle the “backbone” infrastructure.**

### Other device types to know: 
- #### Firewalls (Multi-layer blocking/Inspection)
	- These are Layer 2-7 devices (depending)
	- They can block things based on MAC address, port, state of the packets, and block/inspect things at an application level. 
- #### Wireless devices
	- Access points
		- Is not a router. 
		- They are not forwarding things based on layer 3 information. 
	- Controllers 
		- Control/Manage access points
		- Can tunnel traffic through them. 
			- We can use common IP ranges for wireless and control of security. 
	- Three main ways of handling wireless traffic, 
		- Tunneling through the controllers. 
		- Bridging it on the local network. 
		- Combination of both (Split tunneling)
- #### VPN
	- Simply terminate VPN connections and will be the device that traffic is tunneled through. 
- #### Load Balancers (One IP to many)
	- Used to have a single IP address to correlate to multiple devices behind it. 
		- For example let us say that we have 4 DNS servers. 
			- We don’t want to have to specify each of them individually. 
			- We can use a load balancer to use a single IP address. 
				- DNS traffic hits the load balancer, then gets sent to any of the 4 DNS servers behind it.
	- Also used for web and database traffic for redundant setups. 
- #### Packet Shapers (Prioritizing Traffic) 
	- Devices that will manage bandwidth based on the application. 
		- Ensuring certain applications always get priority over others. 
	- Can inspect application level data. 
		- So we can identify people using bittorrent or tor traffic based on what flows through the packet shaper.