### Internet Protocol Version 4
- Internet/network is layer 3
	- Uses **packets** as the data type
	- IP addressees as the **logical addressing** (Not Physical/MAC address of layer 2)
- Internet protocol is a connectionless protocol...
	- It relies on layer 4 for forming a connection with TCP. 
#### IP addresses are 32 bit addresses
- 32 bits split into 4 blocks of bytes (**Octets**)
	- 192.168.1.4 
		- 168 is the second octet 
- Logical addresses that can potentially change
	- MAC addresses will always remain with the device, no matter where it goes. 
#### Classless Inter-Domain Routing (CIDR) 
- Lets you further break up IP ranges using **variable length, subnet masks** (VLSM)
	- Class C IP range is the equivalent of a CIDR /24, or 256 IP ranges
	- A /25 will have 128 IPs
	- a /26 will have 64 IPs
	- etc.. 
- Gives us more power in the sizing of subnets
#### Subnets
- A larger network broken into smaller chunks
- Will have its own IP range. 
	- Policies
	- **broadcast domain**
		- A broadcast message sent from a computer only goes to all the other devices on that subnet
			- Keep note of large broadcast domains and their overheard traffic..
- Gives us a way to organize IP ranges into logical units 
#### Addressing
Three private address ranges: 
1. 10.0.0.0 – 10.255.255.255
    
2. 172.16.0.0 – 172.31.255.255
    
3. 192.0.0.0 – 192.0.0.255

Self assigned IPs (DHCP no internet) 
1. 169.254.0.0 – 169.254.255.255

Device Loopback addresses 

1. 127.0.0.0 – 127.255.255.255

Multicast addresses 

1. 224.0.0.0 – 239.255.255.255

##### Private IPs
- Cannot be routed on the internet
In order to get internet access..
- We need an IP from a public range. 
- Use a **Network Address Translation** (NAT) on a router to help map the public to private IP traffic. 

### Main ways that IP addresses are assigned to devices
- #### Statically
	- Often assigned to network devices/interfaces, such as routers 
	- Requires more administrative overhead
		- Have to keep track of addresses (Cannot have duplicates)
- #### Dynamically through DHCP
	- Easier to manage
	- Once you set up a server (routers can act as DHCP servers) it will hand out addresses for whichever ranges you specify
		- Common for end point devices like computers
	- DHCP
		- Is used for telling what subnet mask it uses
		- What its gateway is
		- What DNS server to use. 
			- DHCP reservation
				- States that a particular device will always get the same IP. 
					- Servers/printers/cameras etc..

### IPv4 Header
**![](https://lh4.googleusercontent.com/IACYM4yntWtLWojqDyP-aOmfD2RaOHGCdeEQuyB0EbbrpsngPDKJUj5GlFXBoEsCise9kR0RN3I7rrUBqn_OIRdsW0QSpciToeNIt_vFBjri8J0imXGx9BQQ8ZoFVjiZ66bpX4ln1GjqZ4V5eSVeIGY)**
All fields are important but we only really care about a few of them. 
- Version (IPv4 vs IPv6)
- Total Length: The entire packet size in bytes, including the header and data
	- Used in case packets need to be fragmented
- Time to Live (TTL): Lifetime of the packet
	- Used to prevent network failure in the event of a routing loop. 
	- When TTL hits zero..
		- The router automatically discards the packet and typically sends an ICMP time exceeded message to the sender
- Protocol: TCP/UDP - Basically a way of saying what higher layer is getting used. 
- Checksum: 16-bit IPv4 header field is used for error-checking of the header. 
- Source/Destination IP address

### ARP (Address Resolution Protocol)
- Recap
	- Layer 3 stuff: We know the source and destination IP of something. 
		- Layer 3 header gets the IPs and puts them on the envelope
		- We also put our MAC address as the source address for layer 2. 
			- BUT, we have no idea what to put as the MAC address for the **destination** 
				- *Trumpet Sounds* This is where **ARP** comes into play. 
- #### ARP
	- Resolves an IP address to a MAC address

Does this by...
- Creating a new packet
- Filling out the same information as we were for our ping packet (Layer 3/2)
- But the destination MAC address is set to **FF:FF:FF:FF:FF:FF**
	- Which is a **Broadcast MAC Address** 
		- AKA this is sent to everyone within its same subnet. 
In basic terminology..
- With all the devices on the subnet it will ask "Hey is this your IP?"
	- If the answer is "No", the packet will be dropped
	- If the answer is "Yes", That device will create a return frame
		- It will put its own IP and MAC address on the frame and then return it to the sender. Updating ARP tables along the way. 
**![](https://lh4.googleusercontent.com/_5QdwoITfupKAaDyIB-3Wu6AkF3Hkyd3B0HN3QkbL2Zn831UWC7qQX8PQFAX1Y_M2LOLYCgVolGEh87dMcSqTuyU9olJQiJ8SmwE6keV-K_GiD9R4h3cStaiDrb1aUZeV1Qn92UiyT3ud71eAKqAbwI)**
#### Timeout
- Typically for clients and end devices the ARP timeout will be pretty short. 
	- 60 seconds or so..
	- On the client level..
		- Lots of mobility and movement happens, giving the reason why for not wanting to cache an ARP entry for a long time. 
- Network infrastructure devices (Routers, firewalls, etc..)
	- Typically 2-4 hours 
		- Nodes joining and leaving the network should be pretty consistent

Note: ARP is ONLY used for devices within the same subnet. 
**![](https://lh5.googleusercontent.com/1VzKXcslHQUu9lCz7HI-fAzeJ1J9rD7a8ckATNdAUK1yJEFWXmYo2Fl2TG8uqUEITm7nx6DKNLhJsUuPm1qpJbjTV6OMuvQsWJfU5BVW7bWeXxK3cGQuVYglIQEh41POuA2DUYnWBNjszujG7Wu2kUI)**
If I am on PC0 and want to ping PC1

- I won’t have an ARP entry for a device in a different subnet. 
- We WILL have an ARP entry of the interface for the router. 

When PC0 is going to send the packet, he will say “This isn’t on my subnet, so I have to send it to my default gateway.” 

If PC0 doesn’t have an ARP entry for the gateway router, PC0 will ARP for that. 
- The router would reply with the MAC address of the interface facing the sky blue box. 
	- This is NOT the MAC of the router itself. 
	- But rather the MAC of an interface on the router.

### Key things to remember
- ARP is used to match IPs to MAC addresses and is stored in a local ARP table on the device. 
- ARP traffic is contained to the same layer 2 network (subnet)
- ARP request frames are broadcast frames
	- ARP replies are unicast (They get sent back directly back to the sender)

#### OpCode: 
- Value of 1.. ARP packet is a Request 
- Value of 2.. ARP packet is a Response 

#### Router stuff to Note: 
- Will have a few things: 
- The ARP table (MACs to IPs) 
- Routing Table (What subnet is where) 

#### Example: 
- If you are a router, that gets a packet. 
	- It’ll first check the local routing table and then see what the MAC for it is..
		- First checking the ARP table 
	- Go through our nested layers
		- We know the source and destination IPs
		- We use the routers MAC as the source MAC 
	- Then we use the MAC from the ARP table as the destination (or send out an ARP request if we don’t have an entry with that IP) 

#### Cisco switch command 
- show mac-address-table 
	- Is not the same as an ARP table. 
		- Switches do not know what an IP is, therefore the whole MACs to IPs wouldn’t work. 
	- It is what MAC addresses are connected to which ports.


