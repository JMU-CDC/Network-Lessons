- Network often have multiple routing protocols active
	- High probability that the same networks will be advertised by multiple routing protocols 
![[Pasted image 20230904150316.png]]
- For example: 
	- We have RIP running on the top half and OSPF running on the bottom half 
## So.. how would we determine which path is the best?
- Administrative distance is a number/value assigned to every routing protocol
	- In the event that two protocols reporting the same route: 
		- The routing protocol with the **lowest** administrative distance will win 
			- See below table for specific administrative distance based on the route
		- That protocol will then be added to the RIB
### RIB
- Routing information base
	- Data table stored in a router or a network host that lists the routes to specific network destinations 
		- Some cases it will hold metrics/distances associated with those routes

### Route Type-Administrative Distance Table
| Route Type                                                       | Administrative Distance |
| ---------------------------------------------------------------- | ----------------------- |
| Connected Interface                                              | 0                       |
| Static route                                                     | 1                       |
| Enhanced Interior Gateway Routing Protocol (EIGRP) summary route | 5                       |
| External Border Gateway protocol (BGP)                           | 20                      |
| Internal EIGRP                                                   | 90                      |
| Interior Gateway Routing Protocol (IGRP)                         | 100                     |
| Open Shortest Path First (OSPF)                                  | 110                     |
| Intermediate System - Intermediate System  (IS-IS)               | 115                     |
| routing Information Protocol (RIP)                               | 120                     |
| Exterior Gateway Protocol (EGP)                                  | 140                     |
| On Demand Routing (ODR)                                          | 160                     |
| External EIGRP                                                   | 170                     |
| Internal BGP                                                     | 200                     |
| Unknown                                                          | 255                        |
- Admin distance of 255 is NOT trusted and WILL NOT be added into the routing table 