How to know when to pick up a router versus a switch?
- Routers tend to be WAN-centric
	- If you are connecting T1s, you might want a router
- Switches tend to be LAN-centric
	- If you are connecting Ethernet, you might want a switch
## Routing Tables
- In **Cisco** routers, the routing table is called: 
	- ***Route Information Base*** (RIB) 
		- "show ip route"
			- Formatted view of the RIB
- "Add link to Routing protocols down the line"
	- Each Routing Protocol has its own table of information
		- Metric value:
			- Is determined by the routing protocol from which the route was learned. 
		- If the same route is learned from two sources within a single routing protocol. 
			- One with the best metric will win
			- Or the one with the lowest administrative distance will win
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

- ### When a packet arrives at a router, 
	- Determines if the packet needs to be forwarded to another network. 
		- If it does: 
			- It check the RIB to see whether it contains a route to the destination network. 
				- If there is a match; the packet is adjusted and forwarded out the proper interface. 
				- If there is not a match; the packet is forwarded to the default gateway. 
					- Gets dropped if there is no default gateway

## IP Routing Table
```
R2# show ip route
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route

Gateway of last resort is 11.0.0.1 to network 0.0.0.0

     172.16.0.0/16 is variably subnetted, 6 subnets, 2 masks
D       172.16.200.0/23 is a summary, 00:56:18, Null0
C       172.16.200.0/24 is directly connected, Loopback2
C       172.16.201.0/24 is directly connected, Serial0/0
C       172.16.202.0/24 is directly connected, Loopback3
C       172.16.100.0/23 is directly connected, Loopback4
D       172.16.101.0/24 [90/2172416] via 11.0.0.1, 00:53:07, FastEthernet0/1
C    10.0.0.0/8 is directly connected, FastEthernet0/0
C    11.0.0.0/8 is directly connected, FastEthernet0/1
     192.168.1.0/32 is subnetted, 1 subnets
D       192.168.1.11 [90/156160] via 11.0.0.1, 00:00:03, FastEthernet0/1
S*   0.0.0.0/0 [1/0] via 11.0.0.1
D    10.0.0.0/7 is a summary, 00:54:40, Null0
```
- First block of code explains the codes listed down the left side of the routing table
```
Gateway of last resort is 11.0.0.1 to network 0.0.0.0
```
- If there are two or more default gateways, they will all be listed 
	- Packets will be equally balanced between the two links using per-packet load balancing
```
Gateway of last resort is not set
```
- No default gateway(s) has been configured/learned
```
     172.16.0.0/16 is variably subnetted, 6 subnets, 2 masks
D       172.16.200.0/23 is a summary, 00:56:18, Null0
C       172.16.200.0/24 is directly connected, Loopback2
C       172.16.201.0/24 is directly connected, Serial0/0
C       172.16.202.0/24 is directly connected, Loopback3
C       172.16.100.0/23 is directly connected, Loopback4
D       172.16.101.0/24 [90/2172416] via 11.0.0.1, 00:53:07, FastEthernet0/1
C    10.0.0.0/8 is directly connected, FastEthernet0/0
C    11.0.0.0/8 is directly connected, FastEthernet0/1
     192.168.1.0/32 is subnetted, 1 subnets
D       192.168.1.11 [90/156160] via 11.0.0.1, 00:00:03, FastEthernet0/1
S*   0.0.0.0/0 [1/0] via 11.0.0.1
D    10.0.0.0/7 is a summary, 00:54:40, Null0
```

```
D       172.16.101.0/24 [90/2172416] via 11.0.0.1, 00:53:07, FastEthernet0/1
```
- From left to right
- Route code: 
	- **D** in this case
		- Indicates the route was learned via **EIGRP** 
- Route itself
	- `172.16.101.0/24`
		- Route to the subnet
- Two numbers in the brackets
	- `[90/2172416]`
	- 90 (First number) 
		- Administrative distance
	- 2172416 (Second number) 
		- Metric for the route 
			- Determined by the routing protocol
			- In this case **EIGRP** 
- Next hop the router needs to send packets to in order to reach this subnet
	- `via 11.0.0.1` 
		- Packets destined for the subnet `172.16.101.0/24` should be forwarded to the IP address `11.0.0.1`
- Age of the route
	- (`00:53:07`)
- Interface out which the router will forward the packet
	- `FastEthernet0/1`
## Route Types
- ### Host Route
	- Is a route to a host. 
		- The route is not to a network
	- Has a subnet mask of 255.255.255.255 and a prefix length of /32
	- In the sample routing table:
		- Route to `192.168.1.11` is a host route
		- Denoted by the /32 at the end of the IP
- ### Subnet
	- Portion of a major network 
	- Used to determine the size of the subnet. 
		- 10.10.10.0/24 (255.255.255.0) is a subnet
	- Are indented under their source major networks
		- The major network `172.16.0.0/16` has been subnetted
			- Has been subnetted under the rules of Variable Length Subnet Masks (VLSM) 
				- Allows each subnet to have a different subnet mask 
- ### Summary
	- Is a single route that references a group of subnets
		- 10.10.0.0/16 (255.255.0.0) given that subnets with longer masks (10.10.10.0/24) exists 
	- Used in a routing table to represent any group of routes
		- Cisco states that a summary is a group of subnets
			- Super net is a group of major networks
	- In our example:
		- `D   172.16.200.0/23 is a summary, 00:56:18, Null0
			- This one is technically a summary route
		- `D    10.0.0.0/7 is a summary, 00:54:40, Null0`
			- This one is technically a super net reported as a summary 
	- Note the destinations of either summaries: `Null0`
		- Means that packets sent to this network will be dropped 
- ### Major Network 
	- Any class-full network, along with its native mask
		- 10.0.0.0/8 (255.0.0.0) is a major network 
	- In our example: 
		- `C    10.0.0.0/8 is directly connected, FastEthernet0/0
		- `C    11.0.0.0/8 is directly connected, FastEthernet0/1
			- Note the /8
				- Referencing 10.0.0.0 with a prefix mask 
					- Longer than /8 changes the route to a subnet
					- Shorter than /8 changes the route to a super net
- ### Supernet
	- Is a single route that references a group of major networks. 
		- 10.0.0.0/7 is a super net that references 10.0.0.0/8 and 11.0.0.0/8
	- In our example: 
		- `D    10.0.0.0/7 is a summary, 00:54:40, Null0`
			- Has the same reference as the information above
			- Notice the destination is `Null0`
				- On a connected router, we will only see the summary
					- NOT the more specific routes: 
				- `D    10.0.0.0/7 [90/30720] via 11.0.0.2, 04:30:22, FastEthernet0/1`
- ### Default Route
	- Is shown as 0.0.0.0/0 (0.0.0.0) 
		- Route of last resort
	- Used when no other route matches the destination IP address in a packet
	- In our example: 
		- `Gateway of last resort is 11.0.0.1 to network 0.0.0.0`
		- `S*   0.0.0.0/0 [1/0] via 11.0.0.1`
			- Static route, as indicated by the `S`
				- The asterisk next to the **S** indicates that this route is a candidate for the default route
					- Can be more than one 