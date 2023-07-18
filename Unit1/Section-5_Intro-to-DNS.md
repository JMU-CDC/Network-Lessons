### Domain Name System (DNS)
- Lets you translate names into IP addresses
- Critical in things like the internet
	- No one can remember the IPs to all their favorite websites
	- Accessing things like local servers/switches/routers
#### Naming Structure
- Top level domain
	- .edu
	- .com
	- .net
- Second level domains/subdomains 
	- The "jmu" in jmu.edu
- Hostnames
	- Are the thing itself that you're finding the IP for. 
		- Lib.jmu.edu 
			- Lib is the library web server itself that you're looking up the IP for. 
**![](https://lh4.googleusercontent.com/O3wQc2PRboulEihJpDiL9cF7FfiXC8M2P4Z1Lg5tGDsQrBwV85foDbPdrRDP0QAHm6Q3fJ-Yjhf4e8WU5nnMvMvJgRjRHBMRQApXhjJHnoWDlZDKCr-CeTiU0UuBhQQ3dUuwSC6z8JtylOa6UEJyIrk)**
So if we want to find "www-kelloggs-com" 
- We first need to talk to the root servers to translate the ".com" part of things. 
	- They will say, "Sure thing, .com is handled by these DNS servers and here's their IPs"
- Then we will contact those servers and say,
	- "Hey I'm looking for kelloggs.com"
- The servers will say
	- "Yep kelloggs.com has DNS servers of their own and here are those IPs"
- We will **then** send our DNS query to ns1.kelloggs.com 
	- (If that happens to be their DNS server)
		- "Hey I'm looking for www-kelloggs-com", to which they will say "Sure thing, here's the IP"
#### Recursive
- All of the process is handled by the resolver itself
	- We say, "Hey resolver, I want www-kelloggs-com" and 
		- The resolver asks to the root servers for the TLD server
		- The TLD server for the authoritative server
		- Then the authoritative server (ns1.kelloggs.com) for the IP of the url
- Less going back and forth
- Caching
	- They might have already looked that up recently and will already ahve the IP cached. So it would just immediately tell us what it is without going through the whole process.
		- Way faster
#### Iterative
- We send a request to our resolver. (Could be a BIND or talking to Google DNS 8.8.8.8)
- We ask that server for www-kelloggs-com
	- It sends us "hey here's the .com server IPs"
- We then ask the resolver 
	- "Okay how about www-kelloggs-com"
- Then it will respond with the IP of the server itself. 
 **![](https://lh3.googleusercontent.com/LwxZTqvWdn6VtLtGOtLhxpH8qDRifElS3k0PPis5Xj3jPA77rRLbfGV4L1Kkhz8LfgU0QxJLW8aI7CTu_aMt8Q-kJTRnvKqdZVPhbZRkBPEFUDrHyc_Fg5mKkMEtZwRl_8Jf2M7ojH02UMIxKtIbn3Q)**
 ### Forwarders 
 - Any request that isn't a local resource will get forwarded onto a server. (Like 1.1.1.1 or 9.9.9.9)
	 - The local server will still cache that response but it will put the work on that server and not itself. 
#### Records
- A records
	- Name to IP 
- CNAME records
	- Aliases, so we can use different names to point to an existing record
- PTR record
	- Reverse records
		- IP to Name
- MX
	- Email
- SRV
	- Mapping ports to names
- TXT, AAAA, etc.
	- Basic ones are A, CNAME, PTR 
### Few Commands to Know
- host
**![](https://lh4.googleusercontent.com/ioENXvrrzrKbFJwp-H7hb3Aykmc9InZDt00p4iV_AOsKchx1iE_EGCyalT278hjBQP32kr7f1senykTvnC9M0Vd2oW950ogiwTyGPZtUsOV7VKFHg3vOFx9XN7wsMQi94KBvAujW9SMEPZ5DdAL8gBQ)**
- nslookup
**![](https://lh3.googleusercontent.com/HjEz_GU0E5I5Tb_1aDosnRvpS-ntEAbiO6zuv3M07ADDrtuPtDEXY39aaJ0QLx72r-SqqhlvV7FC-TA5mAW_M1rdwoSJYCr_DGH_kVMVxVjEQlPWgY0plaoQQgsHWMawfvzOMa1PfO-tIj9omdBXBIE)**
- dig
**![](https://lh3.googleusercontent.com/4Ix6HOOwo713MyalGvtuo2abCgksSALaes47KDP7xfjJXzXyLbcnmMHA4VxFFZ8pbXXeNbLcitgcmWSlnaJAlPqY1uSKQlk9RjR7E3cnkJTseMvWeVDGBN5W2sBiiJVD5PtYqYRonLpGXX_aT_I_Vck)**
