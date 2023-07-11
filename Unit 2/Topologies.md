### Core Layer
- Is the network's high-speed switching backbone that is crucial to corporate communications. 
- Referred to as the **backbone**
- #### Has the following characteristics for the core layer:
	- Fast transport 
	- High reliability 
	- Redundancy 
	- Fault tolerance
	- Low latency and good manageability
	- Avoidance of CPU-intensive packet manipulation 
		- Caused by security, inspection, quality of service (QoS) classification, or other processes. 
	- Limited and consistent diameter
	- [QoS](https://www.techtarget.com/searchunifiedcommunications/definition/QoS-Quality-of-Service)

### Distribution Layer 
- Is the isolation point between the network's access and core layers. Can have many roles, including implementing 
- #### The following functions for the distribution layer:
	- Policy-based connectivity 
		- Ensuring that traffic sent from a particular network is forwarded out one interface while all other traffic is forwarded out another interface
	- Redundancy and load balancing 
	- Aggregation of LAN wiring closets 
	- Aggregation of WAN connection 
	- [QoS](https://www.techtarget.com/searchunifiedcommunications/definition/QoS-Quality-of-Service)
	- Security filtering 
	- Address or area aggregation or summarization 
	- Departmental or workgroup access
	- Broadcast or multicast domain definition
	- Routing between virtual LANs ([VLANs](/VLANS.md))
	- Media translations 
		- Between Ethernet and Token Ring
	- Redistribution between routing domains 
		- Between two different routing protocols 
	- Demarcation between static and dynamic routing protocols.

### Access Layer
- Provides user access to local segment on the network. Characterized by switched [Intro to LANs](/Intro-to-LANs.md) segments in a campus environment. Micro segmentation using LAN switches provides high bandwidth to workgroups by reducing the number of devices on Ethernet segments. 
- #### Following functions for the Access Layer:
	- Layer 2 switching 
	- High availability
	- Port security
	- Broadcast suppression
	- QoS classification and marking and trust boundaries
	- Rate limiting/policing 
	- Address Resolution Protocol (ARP) inspection 
	- Virtual access control lists (VACLs) 
	- Spanning tree
	- Trust classification
	- Power over Ethernet (PoE) and auxiliary VLANs for VoIP
	- Network Access Control (NAC) 
	- Auxiliary VLANs
