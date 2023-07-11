Much like regular [[VLANS]]
- But a sort of "Sub-VLAN" within a VLAN. 

Sometimes we want to further isolate devices, without creating a whole new VLAN for them. 

### Three types of Private VLAN ports
1. Promiscuous
	1. These can send/receive frames from any other port on the VLAN
2. Isolated
	1. These ports can only communicate with promiscuous ports..
		1. These usually connect to the host themselves
3. Community
	1. These ports can talk to each other freely and devices in the primary VLAN, but not devices in isolated or other community VLANs

### VLAN Example
Say you own several apartment buildings, all connected to the same network. We could have a VLAN per building or floor and have **private VLANs** for each tenant. 
- Remember you need a different subnet for each VLAN. 
- We could give the building one large subnet and use **Private VLANs** to separate the traffic 


#### In Depth Reading for Private VLANs
[Cisco Private VLANs Reading](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus3000/sw/layer2/503_U2_1/b_Cisco_n3k_layer2_config_guide_503_U2_1/b_Cisco_n3k_layer2_config_gd_503_U2_1_chapter_0101.pdf)

#### Intro to VLANs
- [Cisco Intro to VLANs](https://www.ciscopress.com/articles/printerfriendly/2181837)
- [Another Guide - Cisco](https://www.ciscopress.com/articles/printerfriendly/2208697)
- [VLANs - Trunks - VTP](https://www.ciscopress.com/articles/printerfriendly/2348266)

