### OSI Physical Layer: Layer 1 (TCP/IP Network Access Layer)
- Responsible for the actual physical connection between the devices.
- Contains information in the form of bits. 
- Responsible for transmitting individual bits from one node to the next.

When receiving data, this layer will get the signal received and convert it into 0s and 1s. Then sending the bits to the **Data Link Layer**, which will put the frame back together. 

#### Think of it like this
- Upper layers nest things in envelopes to get mailed (encapsulation from the top layer down).
	- Layer 3 packs everything in an envelope, then layer 2 takes that information and puts it in its own envelope, layer 1 takes everything and packs it in its own envelope. 
- Layer 1 being the roads that the delivery truck drives on. 

##### Example
1. You want to download some files from a local webserver. So you start up your web browser and type in the URL of your favorite website. 
	1. Your computer will send a message to the web server requesting a certain webpage. 
	2. You are now using the **HTTP protocol** which lives on the **Application Layer** (Layer 7 for OSI or Layer 4 for TCP/IP). 
2. The **Presentation Layer** (Layer 6 for OSI) will structure the information of the application in a certain format.
3. The **Session Layer** (Layer 5 for OSI) will make sure to separate all the different sessions. 
4. Depending on the application.. You want a reliable **Transmission Control Protocol (TCP)** or an **Unreliable User Datagram Protocol (UDP)**
	1. For this example.. The application will choose TCP since you want to make sure the webpage makes it to your computer. 
		1. More on the difference between the two later… 
5. Your computer has a unique IP address and it will build an IP packet. 
	1. The IP packet will contain all the data of the Application, Presentation, and Session layer. 
		1. It will also specify which transport protocol it’s using (TCP or UDP) and the source IP address of your computer and the destination (web servers IP address). 
			1. AKA header information. 
6. The IP packet will then be put into an Ethernet Frame. 
	1. This frame has the source MAC address (your computer) and the destination MAC address (web server). 
7. Finally, everything is converted into bits and sent down the cable using electric signals.  
  

### OSI Data Link Layer 2: (TCP/IP Network Access Layer)
- Ensures the reliable delivery of messages between network nodes. 
- Primary function is to facilitate error-free data transfer between nodes over the physical layer. 
- Utilizes frames to transmit data and adds physical addresses (MAC Addresses) in the frame header. 
	- Specifically the MAC address of the sender and/or its receiver. 
- Error control is a crucial mechanism provided by the data link layer. 
	- Enables detection and retransmission of damaged or lost frames. 

When a packet from Layer 3 arrives in a network. The DLL transmits it to the intended host using its MAC address. 
- The packet received is further divided into frames based on the frame size of the Network Interface Card (NIC) 

To obtain the receiver’s MAC address, an Address Resolution Protocol (ARP) request is sent over the network. 
- Asking “Who has this IP address?” 
	- The destination host then replies with its MAC Address. 

##### Think of it like this
- As your address on an envelope and the address of the person you’re mailing the letter to. 
	- This information is added to a “frame header” 
- So your computer will use the Data Link Layer to create a frame from the information it receives from the upper layers. 
	- Stuff it into an envelope with your computer’s MAC address (source) and the destination MAC address. 
- Talks to layer 1 to convert it all into bits and sends it to the switch we are connected to. 
	- Switch will read the header and forward things along to the port that has the destination MAC address on it. 
- The destination computer will receive the bits at Layer 1 and their Layer 2 will convert the bits back into a proper frame. 
	- Leaving the upper layers to take everything else out of the envelope. 

### Cisco Switch Errors
- CRC errors will show up at this layer. 
	- Helps tell us if something is wrong with the physical cable or if there is some sort of mismatch of things.
- On a Cisco Switch: 
	- We can run a, “show interface g0/1” to get all the details about that port in particular. 
		- What speed/duplex that port is. 
		- The input/output rate. 
		- How many packets have gone through the port. 
		- Error information. 

```
Switch# show interface g0/1
  FastEthernet0/29 is up, line protocol is up (connected)
	  Hardware is Fast Ethernet, address is 0019.2fcd.979f 
	  (bia 0019.2fcd.979f)
	  MTU 1500 bytes, BW 100000 Kbit, DLY 100 usec,
	  reliability 255/255, txload 1/255, rxload 1/25
	  Encapsulation ARPA, loopback not set
	  Keepalive set (10 sec)
	  Full-duplex, 100Mb/s, media type is 10.100/BaseTX
	  input flow-control is off, 
	  output flow-control is unsupported
	  ARP type: ARPA, ARP Timeout 04:00:00
	  ....
	  Queuing strategy: fifo
	  Output queue: 0/40 (size/max)
	  5 minute input rate 4000 bits/sec, 4 packets/sec
	  5 minute output rate 50000 bits/sec, 16 packets/sec
		  18181044 packets input, 974345603 bytes, 0 no buffer
		  Received 22202921 broadcasts (0 multicast)
		  0 runts, 11 giants, 0 throttles
		  25650 input errors, 8559 CRC, 0 frame, 
		  0 overrun, 0 ignored
	      ...
	      0 output errors, 0 collisions, 34 interface resets
	      0 babbles, 0 late collision, 0 deferred
	      ...
```

- 8559 CRC and a ton of input errors usually means that something is wrong with the cabling.
- 0 collisions. 
	- This is a switch, not a hub, so you should never see collisions on the ports. 
		- If you do, there is definitely something wrong with the connected device. 

##### Note: Ethernet address/Physical address/MAC Address are all the same thing.  
- Ethernet lives at this layer. 

##### Note: Layer 2 addresses are MAC Addresses. 
- The data units are frames.
- Switches operate at this level. 
	- A switch has no idea what an IP address is, in terms of sending traffic. 
		- It ONLY looks at the layer 2 frame. 
- Note: 
	- Address Resolution Protocol (ARP) happens at this layer. 

### OSI - TCP/IP Network Layer 3
- Uses data units called “packets” to send traffic.
- Uses IP addresses for it’s logical addressing
	- IP Addressing are sometimes called “Layer 3 addresses”
- Uses an envelope of its own that has the source and destination IP addresses. 

Uses routers to route the packet between different networks, based on their IP addresses
- The router will route to these different networks based on information the router has. 
	- Might have multiple pathways to a destination (follows the “best” path it has) 
		- Impacted usually by the amount of hops (routers) that traffic has to go through, as well as the speed of those links. 

##### Example
While Layer 2 might be more of a local town post office picking up and delivering letters to houses.
- Only deals with connections via whatever is on that local network/subnet that we are connected to. 

Layer 3 is more sending between different towns to mail distribution sites. 
- Deals with connections between different subnets. 
	- Doesn’t care about the MAC address of anything. 
- It simply wants to get the mail to the correct distribution point and then let the local handlers (switches) deal with the delivery to the specific house. 

![](https://lh5.googleusercontent.com/fJe5wgt7k5A9beSTP4f25U_5PXwWQRIjh8HY6mSYAMjJcQDp_m1ybiSWguejscpNpcTabJbP_ya64zmlFryyVFvF18gGMhBv7HCJCshQ7MT__VlMKs9K2LKn9nNQ43gODjl_EiQimt9hE8kTPLtCeNc)

In the example above….
- Hosts connected to Switch0 that are talking to other hosts connected to Switch0. 
	- Will encapsulate everything into a packet 
		- That gets put in a frame with the host/destination MAC Address. 
	- Then will send that packet to Switch0. 
		- The switch will ONLY look at the layer 2 envelope
			- Finding the max address of the destination and sending the traffic to that specific device. 

Note: Layer 3 packets do contain the source and destination IPs of the computers but that info NEVER gets looked at by anything other than the two computers. 
- Switch doesn't know what an IP is so it never opens the Layer 

#### Layer 3 part
- So PC0 wants to talk to PC1. 
	- The data gets shoved into a layer 3 packet with PC0’s IP address as the source and PC1’s IP address as the destination.
- Given this information, the computer is now aware that it’s on a different network, based on the subnet mask. 
	- Basically the computer asks,  “Am I in the same range as this device?”
		- Given the situation above (Let's call this situation 1), the response would be “Nope”. 
		- Given a situation below there is another computer connected to Switch0 (PC2) then the response would be, “I sure am!”

![](https://lh6.googleusercontent.com/-AgGTplU5a1HnhepuUBNi4tn3HKznx73B9DXKrQ-F7IacvMElxrQ4BxfrPwbWMo8uuBWNWecWJ5yUzvovD44yYHPTMZaebokIEGsAAftiiJvq48sZspM5IPOg0UYxivXlenL4yQIeXjG9RG3iwH-0Sk)

- From a simple ping between PC0 and PC2.

![](https://lh3.googleusercontent.com/L0qNWk2EECfqARL-a5t2D35PNgC_TMNStnarDnhClEkvrP-awNJ_3kMKyAhYHn1TqYAc7H12P6z980k0MJgTBGURXfEFH95cGe-4vwj9CEsxPHxkh1MhANvAYu3eBT66V9D-cOootMng8jvxfBjh-YA)

- We can see Layer 3 headers (source and destination IPs) as well as the Layer 2 headers (Source and destination MAC address)

##### The switch - when it gets the envelope
- It takes a look at the destination MAC address and then looks at its own MAC address table. 
- The table shows “what MAC is on what port”

##### In reference to Situation 1 from above….
- The computer realizes the other computer that it wants to talk to is on another network. 
	- It still has the source and destination IPs on the Layer 3 envelope. 
		- It puts that into a layer 2 frame envelope 
- Puts the source MAC address of itself (PC0) but sets the destination MAC address of the router. 
	- Which is the default gateway. 

Basically the computer says “Hey this is a different zip code (different subnet), we can’t deliver here.. So this needs to go to the mail distribution center for that area. (the router)” 
- After the packet has reached the router it will be sent to the switch. 
	- It will open the layer 2 envelope, so that it can take a look at the layer 3 envelope inside. 
		- It’ll look at the destination network and say, “Oh hey yeah that IP is out this way to switch 1”
			- Putting back the layer 3 envelope inside of the layer 2 envelope, resealing and rewriting it. 
		- Setting the destination MAC address of PC1 and the MAC address of the router port facing Switch 1 as the source. 
	- The switch will check to see if that particular MAC address is in its MAC Address table. 
		- If it is, it will say “Hey that MAC address is through this port.. Off you go”
			- Thereby connecting PC0 to PC1. 

Reason for rewriting: 
- PC1 unpacks everything and looks at the data and needs to reply. 
- It puts together a layer 3 packet..
	- With the inverse of the source/destination IPs so it can get sent back the other way. 
- Source MAC for the frame itself and the destination is the router again. 
  

### OSI (Layer 4) - TCP/IP (Layer 3) Transport Layer
- Provides services to the Application Layer. 
	- Application layer (Layers 5-7 via the OSI Model), is the layer that is the program itself. 
		- Your web browser is operating at layer 5. 
		- Data unit is the data itself (the HTML webpage or an ISO getting downloaded) 
- Takes services from the network layer (Layer 3) and is responsible for the End to End delivery of the complete message. 
- It uses data units referred to as Segments. 
- Can also provide..
	- The acknowledgement of the successful data transmission and retransmission of the data if an error is found. 

It receives the formatted data from the Application layer, adds Source and Destination port numbers in its header, and forwards the segmented data to the Network Layer. 
- The sender needs to know the port number associated with the receiver’s application. 
	- Generally the destination port number is configured, either manually or by default. 

##### For example
- When a web application requests a web server, it typically uses port number 80 (HTTP service)
	- This would be the default port assigned to web applications. 
- On the receiver’s side..
	- Transport layer reads the port number from its header (The one sent by the sender) and forwards the Data which it has received to the respective application.
		- Performing sequencing and assembling of the segmented data. 

### Segmentation and Reassembly
- Accepts the message from the (session layer), and breaks the message into smaller units. 
	- Each of the segments produced from the smaller units has a header associated with it.
- The Transport Layer (Layer 4) at the destination station reassembles the message. 

### Note.. Ports
- Destination Ports will be the known thing (port 80/22/whatever). 
- The sender will generate a random high number port, so the server knows what to send back to. 
	- If you have three webpages open in Chrome, the computer needs to know which session is assigned to which tab. 
		- This uses the generated source ports for that. 

#### Note
- Can also use TCP and UDP
	- TCP: Connection-based. 
		- Important for things that require an established connection/confirmation of transfer. 
		- SSH uses TCP, establishing a connection between the client and a server. 
		- More reliable. 
	- UDP: Connectionless 
		- Faster than TCP, just blasts segments out. Doesn’t care if it gets there or not. 
		- DNS uses UDP, it needs to be quick and if we don’t get an answer it’ll just ask again.
