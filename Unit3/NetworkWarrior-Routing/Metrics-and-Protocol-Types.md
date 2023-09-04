### Job of a routing protocol is to determine the best path to a destination network
- Best route is chosen based on a protocol-specific set of rules 
- Routes with a **lower** metric are more desirable 
## RIP 
- Simplest form of metric: 
	- Hop count
		- Simply the number of routers between the router determining the path and the network reached 
	- Has a limitation
		- Can cause a suboptimal path to be chosen 
![[Pasted image 20230904144519.png]]
- See the link connecting routers B and C?
	- A T-1 connection with a speed of 1.5 Mbps
- While the link connecting routers E, F, and G are connected via a Fiber optic cable with a speed of 1 Gbps 
	- RIP WILL PICK THE ROUTE CONNECTING B AND C
- **RIP does not know about the bandwidth of the links in use** 
	- Only the number of hops it has taken to reach a destination
#### RIP is called a **Distance-Vector** routing protocol
- Relies on distance to the destination network to determine the best path
	- Think of a problem that this could generate...
		- Counting to infinity
			- RIP has an upper limit of 15 hops with 16 being unreachable... However... this does not scale well
## OSPF
#### Called a **Link-state** routing protocol 
- Includes information about the links between the source router and the destination network 
- OSPF
	- Adds up the **cost** of each link
		- Dividing 100,000,000 by the bandwidth of the link in bits per second (bps) 
	- `100 Mbps (100,000,000 / 100,000,000 bps) = 1`
	- `10 Mbps (100,000,000 / 10,000,000 bps) = 10`
	- `1.5 Mbps (100,000,000 / 1,540,000 bps) = 64`
![[Pasted image 20230904145553.png]]
- Seen above is the calculation that OSPF goes through to pick the best route. 
	- This time, OSPF will indeed choose the bottom connection instead of the top like RIP did
## EIGRP
- Way more complicated then the two above
- It uses: 
	- Bandwidth
	- Delay 
	- Reliability 
	- Effective bandwidth 
	- Maximum transmission unit (MTU) 
- In its calculation of a metric 
- Considered a **hybrid-protocol**
