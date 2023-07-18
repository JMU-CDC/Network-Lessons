### Basic Commands

|   |   |
|---|---|
|Cisco Command|Description|
|show running-config (show run)|Shows current running configuration of the device|
|show ip interface brief|Displays quick status of the interfaces (up/down) on the device, including the IP address|
|show ip interface|Displays information about the config status of the IP on all interfaces.|
|show interfaces (show int)|Displays the status of the interface (up/down), utilization, errors, protocol status, and MTU.|
|show interfaces (interface)|Displays detailed information and statistics on a single interface|
|show running-config interfaces (interface) (show run int int)|Displays the config of the device|
|show interface status (show int status)|Displays interface summary|
|show arp|Displays the ARP table|
|show controllers|Displays information related to interface errors|
|show version (show ver)|Displays information of the device hardware, software version, and uptime|
|show log|Displays information about past commands|
|show ip route|Shows the IP routing table|
|show mac-address table|Displays the ARP cache and table|
|show vlan brief|Displays quick status of the VLAN|

USE “?” EARLY AND OFTEN

REAL WORLD: SECURE ACCESS TO THE SWITCH… NOT JUST LOCKING THE IDF (CLOSET) THAT THE SWITCH IS IN… HAVING A USERNAME AND PASSWORD ACCESS TO THE CLI, STRONG “ENABLE” PASSWORD TO GET INTO PRIVILEGED MODE, ACLs FOR THINGS LIKE “SSH”

### Link state table: 

|   |   |
|---|---|
|Interface/Line Protocol State|Link State/Problem|
|Up/Up|Link is in operational state|
|Up/Down|Connection problem. Physical is up, but the data link layer is not converging correctly. (Issue with STP or ISL/Dot1Q)|
|Down/Down|Cable is unplugged, or the other end equipment interface is shut down/disconnected|
|Down/Down (notconnect)|Problem with interface|
|Administratively down|Interface has been manually disabled.|

  

### Interface Error Table: 

|   |   |
|---|---|
|Parameter|Description|
|Runts|Discarded packets that are smaller than the min packet size for the medium. (Normally caused by collisions)|
|Giants|Vise-versa of runts|
|CRC errors|When the checksum calculated by the sender does not match the checksum on the data received at its endpoint. (Collisions, bad NIC cable, etc)|
|Overrun|Amount of time the receiving hardware was unable to store into a packet buffer. (Hardware configuration)|
|Ignored|Received packets ignored. (Broadcast storms and noise)|
|Collisions|Number of retransmissions. Number of collisions divided by the number of output packets should be less than 0.1%|
|Interface resets|Number of times an interface has been reset.|
|Restarts|Number of times the Ethernet controller was restarted due to errors.|
|Input errors|Sum of all input errors on an interface. (no buffer, CRC frame, overrun, ignored counts, runts, and giants)|
|Output errors|Sum of all outputs errors that prevents datagrams from being transmitted|
|Late collisions|Signal could not reach the end.|**


### User Modes
- Exec mode (>)
	- Can do plenty of show commands
			- Viewing port status, speed, etc.. 
			- Troubleshooting abilities
	- No ACTUAL changes can be made on this mode. 
- Privilege Exec Mode (#) 
	- Use the 'enable' command to get into privilege mode. 
		- Mode used for configurations changes and to show more info
	- Use the 'configuration terminal' command to enter **global configuration** mode
		- Makes global changes to the switch:
			- Hostname
			- Adding users 
			- Etc..
		- 'Interface fa0/1' 
			- Goes into a sub prompt for the specified interface. 
			- Modifies the interface itself
	- "copy running-config startup-config"
		- running-config == What is running now
		- startup-config == What gets loaded at boot
		- "write mem" == Shorter version of the code above

### Cisco CLI
- Text based interface we use to monitor, manage, and configure a Cisco switch
- Few ways to access the CLI
	- Console interface on the switch
		- By using the "console cable" in order to connect to it via its port. 
		- It is a local session that is independent of the network. 
		- More secure
			- Used during initial switch configuration, troubleshooting network issues, or in situations where network connectivity is unavailable. 
	- #### SSH and Telnet
		- Telnet is basically insecure SSH
			- Everything is in plain text
		- In-Band SSH
			- Establishes connection over the same network path that carries other network traffic. 
				- Typically uses TCP/IP
				- Most common method
			- Used for general remote access to servers and devices
				- Potential security risk
		- Out-of-Band SSH
			- AKA: Management SSH
			- Involves establishing an SSH connection throughs a separate and dedicated network path
				- Used for remote management and administrative purposes. 
			- Out of band network path
				- Typically a separate network or a dedicated management network
					- Physically or logically isolated from the main production network. 
			- Used for secure management of critical systems and infrastructure. 
	- #### Management Port
		- Used for remote management and configuration of the switch
			- Utilizes Ethernet connectivity for remote access
		- Used for data to day remote management, configuration changes, monitoring, and integrations. 