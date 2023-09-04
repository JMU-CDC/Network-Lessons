- Means whereby devices exchange information about the state of the network
	- Information collected by other devices are used to make decisions about the best path for packets to flow
- Both: 
	- Protocols 
		- Sits at Layer 3
	- Applications
		- Makes the routing decisions
		- Runs at Layer 7
- Some firewalls and servers may support a limited scope of routing protocols
	- Routing Information Protocol (RIP) 
	- Open Shortest Path First (OSPF) 
		- For simplicity, all devices that participate in a routing protocol will be called routers
- Allows networks to be **dynamic** and **resistant** to failure
	- Dynamic routing protocols usually allow all routers participating in the protocol to learn about any failures on the network through regular communication 
## Communication between routers
- Most modern routing protocols communicate on broadcast networks: 
	- Using ***Multicast Packets*** 
		- Specific IPs
		- Corresponding MAC addresses 
			- Which references predetermined groups of devices
### More common multicast addresses
```
224.0.0.0  Base Address (Reserved)                   [RFC1112,JBP]
224.0.0.1  All Systems on this Subnet                [RFC1112,JBP]
224.0.0.2  All Routers on this Subnet                        [JBP]
224.0.0.4  DVMRP    Routers                          [RFC1075,JBP]
224.0.0.5  OSPFIGP  OSPFIGP All Routers             [RFC2328,JXM1]
224.0.0.6  OSPFIGP  OSPFIGP Designated Routers      [RFC2328,JXM1]
224.0.0.9  RIP2 Routers                            [RFC1723,GSM11]
224.0.0.10 IGRP Routers                                [Farinacci]
224.0.0.12 DHCP Server / Relay Agent                     [RFC1884]
224.0.0.18 VRRP                                          [RFC3768]
224.0.0.102 HSRP                                          [Wilson]
```
- Shows that all IGRP (Internal Gateway Routing Protocol) routers will listen to packets sent to the address 244.0.0.10
	- NOTE :
		- Not all routing protocols uses multicasts to communicate
			- BGP does not discover neighbors, so it has NO need for multicasts
			- Other routing protocols can configure neighbors statically 
### Multiple Routing Protocols
![[Pasted image 20230831171051.png]]
- Example above: 
	- There are five routers: 
		- 3 are running OSPF
		- 2 are running EIGRP
	- There is no reason for the EIGRP routers to receive OSPF updates or vise versa
		- Using multicast ensures that only the routers running the SAME routing protocols communicate with and discover each other 
![[Pasted image 20230831171606.png]]
- A network may also contain multiple instances of the same routing protocol
	- In EIGRP, these separated areas of control are called ***autonomous systems**
	- In OSPF, they are called ***domains***
		- OSPF is more complicated to configure and understand, so for now don't worry about the specifics of this protocol in this case
- Each EIGRP instance is referenced with an **autonomous system number** (ASN) 
- Multicast packets sent by an EIGRP router will be destined for ALL EIGRP routers
	- All the routers, using EIGRP, will listen to updates, 
	- The individual routers will determine, based on the autonomous system ID, if they need to retain or discard them. 
#### Redistribution 
- Act of passing routes from one process or routing protocol to another
![[Pasted image 20230904143531.png]]
- Router E is configured to be a member of both EIGRP 100 AND EIGRP 200
- Internal
	- Route is learned within a routing process 
	- More reliable 
		- Because of a metric called ***administrative distance***
- External
	- Route is learned outside the routing process and redistributed into the process
#### Exceptions to internal reliability
- BGP
	- Prefers external routes over internal ones 
- OSPF
	- Does not assign different administrative distances to internal versus external