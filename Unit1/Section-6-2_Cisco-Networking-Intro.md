
All from this reading [Cisco Intro to Basic Switching Concepts](https://www.ciscopress.com/articles/printerfriendly/2181836)


### Recovering from a System Crash
- Boot loader provides access into the switch if the operating system cannot be used because of missing or damaged system files
- #### Steps for recovering from a system crash
	- Connect a console cable from the PC to the switch. 
		- Configure terminal emulation software to connect to the switch. 
	- Unplug the switch power cord
	- Reconnect the power cord to the switch and within **15** seconds press and hold down the "Mode" button while the system LED is still flashing green
		- Keep holding till the LED turns briefly amber and then solid green
			- Release after this
	- Boot loader switch: Prompt appears in the terminal emulation software on the PC

### Preparing a switch for remote management access
- Must be configured with an IP address and subnet mask. 
	- To manage the switch from a remote network, the switch must be configured with a default gateway
	- The "switch virtual interface (SVI)" should be assigned an IP address
		- Not a physical port on the switch 
		- Does NOT allow the switch to route Layer 3 packets
		- On the VLAN interface configuration mode
#### Configuring the Management interface
**![](https://lh4.googleusercontent.com/YsGbPj14rIuw2YEldLhd5LIl0Frch8d9mgsdPlMkrDefn6a1PHOHoGtOte-wXvpdI26JUPkBr1IxP_6z1cY73LgnAcDT_BlljCGI4r5_EE0S3Td40my1TbeR0g2effrxCgg0odUs8K22OkH5zyazUMs)**
- In the figure above, 
	- VLAN 99 is configured with the IP address of 172.17.99.11 and a mask of 255.255.0.0
#### How to create a VLAN on a Cisco switch
**![](https://lh6.googleusercontent.com/_sOA4hbtQxF-8zHS3TvdyBM8vzdXEh7IlKJzIc55VZM7OCXnQEtrbgX8R5uZN19DJe6OOt3bp4hwPwG9T6r1_RZSNNZIIM4Gy7jAC5o28UwWNPHsKrPCx5_4W6TOfeDQE9YPvX1QfmQPUt-cRr1kmz0)**
- This would be how you create a VLAN with the **vlan_id** of "99" and associate it to an interface of your desire. 
- NOTE: 
	- SVI for VLAN 99 will NOT appear as "up/up" until...
		- VLAN 99 is created
		- An IP address is assigned to the SVI 
		- The "no shutdown" command is entered
		- AND either:
			- A device is connected to an access port associated with VLAN 99 
			- A trunk link connects to another network devices 
#### Configuring the Default Gateway
- Should be configured with a default gateway if the switch will be managed remotely from networks that are not directly connected. 
	- Default gateways is the first **Layer 3** device (such as a router) on the same management VLAN network that the switch connects. 
		- The switch will forward IP packets with destination IP addresses outside the local network to the default gateway
			- Quick question... Isn't a switch a layer 2 device... how can it handle IPs?
**![](https://lh5.googleusercontent.com/F0zojhN9kmDe6PE_TYV6pXiZ2PtnOppEA70-KBM60BBlA2p_lBO8jcs3JKt63KiDGz0-WJXg7ee4bAs2lJous3wCiH4rm8HI8N1prDZIbmisanjUcZdpF2d1A5beJZ035EXlN19uVh5geA4zG-51fdE)**
- Default gateway in specifics is the IP address of the router interface **facing** the switch that it connects to. 
#### Auto-MDIX
- Automatic Medium-Dependent Interface Crossover
	- When enabled..
		- The interface automatically detects the required cable connection type (straight-through or crossover) and configures the connection appropriately 
		- Note:
			- Interface speed and duplex must be set to "auto" so that the feature operates correctly. 
	- Without this enabled..
		- A **straight-through** cable must be used to connect devices such as servers, workstations, or routers.
		- A **cross-over** cable must be used to connect a switch to another switch or repeater. 
**![](https://lh5.googleusercontent.com/mnRJSHrHd1Ugx8mNj_aSo26CcsNTGtSoxPwdFVXg-aJEAsw4mwgODzi4I4rCIMCD-DbMG6zeR-rqQILOys7k3ORIoXiOQU6lsp8kiOk05UaL_G3FOu3Nje6nDQoaGyw-EfjpYQS6fGKbQMKnsnRsqgg)**
Note: 
- auto-MDIX feature is enabled by default on newer switches but not available on older models. 
- To view auto-MDIX setting for a specific interface
	- "show controllers ethernet-controller "interface id" phy | include Auto-MDIX"
#### Verification Commands 
**![](https://lh5.googleusercontent.com/hWRofCdBlkPbFLOxTutJZf_wRgMhsC7LMFZGOq3fqf2FKA709RUUCyL8I1AaBo9i62Pkx1OHkUjoM9-2PIQMp_mWq-EnQ3uIdtJIJDF2nZtKvvDapMIQP7UeS9Jp1n2Id0XUVhpXYaMk4PBMdYsDi1E)**

### Show interface problems
- If the interface is up and line protocol is down
	- Problem exists
		- Encapsulation type mismatch
		- Interface on the other end could be error-disabled 
		- Hardware problem
- Line protocol and the interface are down
	- Cable is not attached
	- Some other interface problem
		- Back to back connection 
			- Connection where the transmitter of one device connects directly to the receiver of another device without a transmission media between the two devices. 
			- One end my be administratively down

### Security concerns in LANs
- Wired LANs are a common source of attack because of the information that can be gained about the wired network.
	- By examining download frames, attackers can determine..
		- The IP addresses of network devices
		- Protocols being used
		- Valid server names 
			- With this information.. attackers can launch a multitude of attacks
- #### MAC Address Flooding
	- If the destination MAC address does not exist in the MAC address table, the switch floods the frame out of every port on the switch
		- Except the one where it came from
- #### DHCP Spoofing 
	- DHCP is the protocol that automatically assigns a host a valid IP address out of a DHCP pool
		- Attackers can configure a fake DHCP server on the network to issue DHCP addresses to clients, giving them all the information they could ask for. 
	- DHCP Starvation attack
		- An attacker floods the DHCP server with DHCP request to use all the available IP addresses that the DHCP server can issue. 
		- Produces a **Denial-of-Service (DoS)** attack
	- How to prevent
		- There is a Cisco Catalyst feature that determines which devices attached to switch ports can respond to DHCP requests
			- Prevents unauthorized DHCP messages that contain information being provided to legitimate network devices. 

```
ip dhcp snooping
ip dhcp snooping vlan 10, 20
interface fa0/1
	ip dhcp snooping trust
interface fa0/2
	ip dhcp snooping limit rate 5
```

- #### Cisco Discovery Protocol (CDP)
	- Allows other Cisco devices that are directly connected, which allows the devices to auto-configure their connection
		- By default, most Cisco routers and switches have CDP enabled on all ports. 
	- CDP information is sent in periodic **unencrypted** broadcasts
		- Contains information about the device, such as IP addresses, software version, platform, capabilities, and the native VLAN
			- I wonder what one could do with all that information...
### SSH Configuration 
- Configuring SSH (Config)
	- Configure the IP domain
		- "ip domain-name (domain-name)"
	- Generate RSA key pairs
		- "crypto key generate rsa"
			- Minimum of 1024 bits
		- To delete 
			- "crypto key zeroize rsa"
				- SSH server is automatically disabled
	- Configure user authentication (local)
		- username (username) password (password)
			- Note... password will be in plain text
			- Use the "secret" command to encrypt the password
	- Configure the vty lines
		- line vty 0 15
		- transport input ssh
			- Prevents non-ssh (such as Telnet) connections and limits the switch to accept only SSH connections
			- Use the "line vty" global configuration mode command and then the "login local" line configuration mode to require local authentication for SSH connections from the local username database. 
- Verifying SSH 
	- "show ip ssh"
		- Show if it's enabled and a few other summary settings
	- "show ssh" 
		- Shows ssh connection to that device
