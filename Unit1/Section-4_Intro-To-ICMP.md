### Internet Control Message Protocol (ICMP)
- Layer 3 protocol that is used for troubleshooting/diagnostics
	- Ping uses ICMP
- Doesn't use traditional ports
	- Uses different types of codes within the ICMP messages themselves. 
#### Pinging something
- If you don't get the first reply, chances are that the first lack of reply is your device going through the ARP process first. 
#### ICMP Messages
- Destination unreachable
	- I can't get to this IP or it doesn't exist
- Time exceeded
	- I went through enough routers, but my TTL ran out before I could get there 
### Trace route 
- Extremely useful tool, uses ICMP
- Used to show:
	- All the hops (routers) that a packet travels through to reach a destination
```
traceroute to www.jmu.edu (134.126.126.99), 30 hops max, 60 byte packets 

1 192.168.64.1 (192.168.64.1) 0.259 ms 0.215 ms 0.240 ms 

2 204.111.39.1 (204.111.39.1) 3.291 ms 3.349 ms 3.157 ms 

3 10.25.0.137 (10.25.0.137) 6.186 ms 6.263 ms 10.25.0.109 (10.25.0.109) 6.236 ms 

4 ae-82.a04.asbnva02.us.bb.gin.ntt.net (128.242.179.97) 5.442 ms 5.374 ms 5.348 ms 

5 ae-0.lumos-networks..gin.ntt.net (128.241.3.230) 6.319 ms 5.887 ms 6.447 ms 

6 67-221-118-166.unassigned.ntelos.net (67.221.118.166) 9.559 ms 9.053 ms 9.100 ms 

7 * * * 

8 * * * 

9 * * * 

10 * * * 

11 * * *
```
- The three stars (***) means:
	- Something isn't replying back. 
		- The device is able to to talk to the end device, but some device along the way isn't showing/saying what it is. 
- Things to note:
	- It has the routers interface IP facing that subnet, but also tries to do a DNS lookup

#### Layer 3 header:
**![](https://lh6.googleusercontent.com/RFUie0JIPL6UsIopxniaiTmWU3h887DXVQoXPzjnanaGaSQca7d_gw7JecNWGBIRGnGHfpt6cs6PrQ1pMArglEKDe3FhmomAlxVm0Lai8qzv_sqGtxdlXcUBHBiN-cDJ6F4ZGIwwqW4MAfimYUpKwT8)**
- ICMP would be specified in the "Protocol"field 
	- As is TCP/UDP