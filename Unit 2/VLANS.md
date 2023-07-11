[Reading Material](Network-Lessons/Unit-2/Private-VLANs.md)

### Trunk
- Lets us tag frames as they're leaving a switch, in order for the next switch(es) to know where to send things.
- ### Two Main Trunk Encapsulations
	- ISL (Cisco Proprietary)
		- Usually try to negotiate trunking protocols automatically using **Dynamic Trunking Protocol (DTP)**
			- AKA - it will try to figure out if a port should be an **access port** or a **trunk port**.
	- 802.1Q (IEEE Open Standard)
		- If we need to trunk between a Cisco and Juniper switch. 

**![](https://lh5.googleusercontent.com/C-cznvgP8Dj9BK3WC_Tbwlo8qEGKgiwnul0xkM-GNn95DgJ5q8fBNHAXlC9WRxk6TyZdn2NhHY5c1G5PGWWsR8G7FaHlZ6YpZ7v5BozgZvnDmooU7EaVMlRkYHEWz4MZ_TSIdPR33CkwGMCaOCjdH3I)**

### VLAN Cisco Commands to Note
    Switch# show run | begin interface G
    interface GigabitEthernet0/1
	    switchport access vlan 10
	    switchport trunk allowed vlan 10
	    switchport mode trunk

- switchport access vlan 10 
	- This is **NOT** an access port on VLAN 10. 

#### Making or Breaking Jobs
Let us say we want to add VLAN 20 to the allowed list above

       Switch(config-if)# switchport trunk allowed vlan add 20
       Switch(config-if)# end
       Switch# show run | begin interface G
	    interface GigabitEthernet0/1
		    switchport access vlan 10
		    switchport trunk allowed vlan 10,20
		    switchport mode trunk

Note the **Proper** command is '*switchport trunk allowed vlan **add** 20*'
Let us see what happens when you forget that **add** part

           Switch(config-if)# switchport trunk allowed vlan 30
           Switch(config-if)# end
           Switch# show run | begin interface G
           interface GigabitEthernet0/1
			    switchport access vlan 10
			    switchport trunk allowed vlan 30
			    switchport mode trunk

VLANs 10 and 20 just got removed. **ONLY** leaving 30
