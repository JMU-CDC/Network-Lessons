
### Passwords
    enable password/secret
- Passwords in 'running-config' ARE NOT encrypted by default. 
- Use 'service password-encryption' to hide that password. 

#### Enable secret
- Uses MD5 hashes for the password 

**![](https://lh6.googleusercontent.com/dGn0ysSss-KiT5I63ZN6hdmLSo3U4L7vmVg-2pNwUsEJCs7iKYyv1jn4wr4_Nh1EgMya9bxSBlzPhB-KlT_OfWGR6nCS1emlCMUy1_WL-cXWKtiGUJ7CBKVzxHo74pl5ujlAZfz4pzJk5SpJ_2vHZqk)**
### Password Recovery
- Pre-boot environment 
	- Lets you view/change the start-up config
		- Remember
			- running-config is the config that's being used on the running switch. 
			- startup-config is the config that is actually in memory. 
				- Save the running-config to startup-config. 

### Users
- Create local users on the switch itself to login. 
	- Auditing
- Setting users with different levels of permission. 

**![](https://lh5.googleusercontent.com/8gQpXmjPmOsgveYT60gg0e_anprblm2988CbtHDxc9Ml7aVxrqsopgNpY25ubzixG8AtjZs8PrZ_SUiSTM6d4Wk-uJG-ERXL7MxyOnsUsR34Br-hxNPZr_bbCaX5xYkVknvfhvj3fEuwojLOHbkpft8)**
- 15 would be full blown admin - Do anything you want. 
- 0 cant do much of anything, unless they have the **enable password**
	- You can use the command "**?**" 
	- Usually, there should be a guide or two out there for setting it. 
- You can point a switch at a remote server for user authentication 
	- We don't want to be updating 100 plus different switches with users. 
	- #### AD User authentication
		- Users will NOT exist locally on the switch. 
			- So if you change your AD password, it's not updating something on the switch itself. 
			- It will update the AD. 
		- Though, if the AD is down or the switch cannot talk to the AD. The user cannot login to it. 
- Local users
	- Mainly used for initial configuration --- Or in case of emergency

### Assigning A Management IP address to a switch
    conf t
    interface vlan X (by default its VLAN 1)
	ip address 192.168.1.55 255.255.255.0
Once we assign an IP address to the switch, we can SSH into it, monitor it with pings, etc.. 

### SSH Configuration 
- Domain set
	- ip domain name example.com
- User that you will SSH with
- Generate crypto keys
- Switch SSH to version 2
- Enable that 'line vtx 0 X' is set for SSH auth
	- Use 'login local' to use the local users and then 'transport input ssh'


