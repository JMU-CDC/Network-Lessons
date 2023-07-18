### 3 Basic types of cabling: 

1. Coaxial 
2. Twisted-pair 
3. Fiber-Optical


#### Coaxial Cable
- Contains a conductor, insulator, braiding, and sheath. 
- Sheath covers the braiding
- Braiding covers the insulation
- Insulation covers the conductor

![](https://lh3.googleusercontent.com/nytDvlpiFqyBWuv6tqL4yp9wZHvHnb9SATWro_fR5OIfWj0B_8Eiqaa6H3TemnRe87SN4Kqjbj7uCmLO92ADHjiFe3FkojbpeyYio0va0JTCeAxUt6jlk1ts9HRHUvx3iMPnRBS4rVSBp_1pijyKe6M)

- Sheath
	- Protects from physical damage
- Braided shield 
	- Protects signals from external interference and noise
- Insulation
	- Protects the core. If the shielding and core were to touch it would short-circuit the wire. 
- Core 
	- Can be two types…
		- Single-core coaxial cable 
		- Multi-core coaxial cable

Not primarily developed for the computer network. No longer used to build any type of computer network. 

|   |   |   |   |   |
|---|---|---|---|---|
|Type|Ohms|AWG|Conductor|Description|
|RG-6|75|18|Solid Copper|Cable internet service and cable TV (long)|
|RG-8|50|10|Solid Copper|Earliest computer network. Backbone in bus topology. AKA 10base5 Thicknet cable.|
|RG-58|50|24|Thin strands of copper|Thinner, easier to handle and install than the RG-8. 10Base2 Thinnet cable.|
|RG-59|75|20-22|Solid copper|Used in cable networks to provide short-distance service.|

#### RG stands for Radio Guide. 
- Coaxial cable mainly uses radio frequencies in transmission. 

#### Impedance
- Is the resistance that controls the signals. Expressed in Ohms

#### AWG (American Wire Gauge)
- Used to measure the size of the core. 

### Twisted-Pair Cables
- Primarily developed for computer networks
	- Known as the **Ethernet Cable**
- Almost all modern LAN computer networks use this cable. 

Consists of:
- Color-coded pairs of insulated copper wires.
	- Usually four pairs. 
		- Each pair has one solid color wire and one striped color wire. 
	- Solid Colors are..
		- Blue
		- Brown
		- Green
		- Orange
	- Striped Colors are…
		- Above colors are mixed with a white color. 

Two types: 
- ##### UTP
	- Unshielded twisted-pair cable
		- All pairs are wrapped in a single plastic sheath
- ##### STP
	- Shielded twisted-pair cable
		- Each pair is wrapped with an additional metal shield
		- Then, ALL pairs are wrapped in a single outer plastic sheath. 

#### Similarities..
- Both can transmit data at 10 MBps, 1 Gbps, and 10 Gbps
- Use the same RJ-45 modular connectors
- Can accommodate a maximum of 1024 nodes in each segment?
- Maximum segment length for both cables is 100 meters (328 feet)

#### Differences..
- STP cable contains more materials, meaning it is more expensive than UTP
- STP provides more noise and EMI resistance than UTP cable

![](https://lh5.googleusercontent.com/C0yM0E5CwdgvmL9H_x8H7WfQZcMKaA50zUDeFdgIyEa6dmqELYFXtLrhd1uZeqW8pb6fQJRF8sosEIbb41710QLPJuvh6GFomF-jBL-3sgSXjwQrPA50OT-JHfsOf0bcK6MRghnqzl35Agw1Qhvwdqo)

  

|   |   |   |   |   |
|---|---|---|---|---|
|Cat|Max supp. speed|Bandwidth|Ethernet Standard|Description|
|Cat 1|1 Mbps|1 MHz|Not used for data|Contains two pairs (4 wires). Telephone network - voice transmission|
|Cat 2|4 Mbps|10 MHz|Token ring|This and below all have a min of 8 wires (4 pairs)|
|Cat 3|10 Mbps|16 MHz|10Base-T|First ethernet cable|
|Cat 4|20 Mbps|20 MHz|Token ring|Advanced token ring networks|
|Cat 5|100 Mbps|100 MHz|100Base-T|Advances (fast) LAN networks|
|Cat 5e|1000 Mbps|100 MHz|1000Base-T|Minimum requirement for all modern LAN networks|
|Cat 6|10 Gbps|250 MHz|10GBase-T|Plastic core to prevent cross talk. Uses fire-resistant plastic sheath|
|Cat 6a|10 Gbps|500 MHz|10GBase-T|Reduces attenuation and cross-talk. Recommended cable for all modern Ethernet LAN networks|
|Cat 7|10 Gbps|600 MHz|Not drafted|Sets a base for further development.|


Cat 1, 2, 3, 4, 5
- Outdated and not used in any modern LAN network 

Cat 7
- New technology and not commonly used

Cat 5e, 6, 6a
- Most commonly used twisted-pair cables


### Fiber Optic Cable
- Completely immune to EMI and RFI. 
- Can transmit data over a long distance at the highest speed. 
	- Can transmit data up to 40 kilometers at the speed of 100 Gbps 
- Uses light to send data. 
	- Reflects light from one endpoint to another

#### Consists of:
- Core
	- Carries the data signals in the form of light. 
	- Made up of thin strands of glass or plastic. 
		- Is wrapped in the cladding.
- Cladding 
	- Reflects the light back to the core.
		- Wrapped in the buffer
- Buffer
	- Protects the light from leaking 
		- Wrapped in the jacket
- Jacket 
	- Protects the cable from physical damage

![](https://lh6.googleusercontent.com/CiSV3l8_nI6jo6bzzJb-m6ucQjr6cdteKm8QUNbWNGkvR3nFg89keK_oOOwFtfG1Z5hzs8ZwhlilTgMcubhALQT3SbPKCuXjEpoBunMjwNOFS2y1_hJz0XAvEN9L9GMnYX8J7UqHXbIIE5CzG2HNK7Q)

### Single Mode Fiber
- Carries only a single beam of light. 
	- More reliable, supports much higher bandwidth, and longer distances than the MMF cable. 
- Uses a laser as the light source and transmits 1300 or 1550 nano-meter wavelengths of light. 

### Multi-Mode Fiber 
- Carries multiple beams of light
	- Carries more data than the SMF cable. 
- Used for shorter distances. 
- Uses an LED as the light source and transmits 850 or 1300 nano-meter wavelengths of light. 

![](https://lh3.googleusercontent.com/1zjFRpgw5IBuziHpvMGVzY5qolA_YcOjRictDxbMxawTMsYFTQP_PWizIWPKSeFzBvjgNRnRxkwRKSy0Kv09kMxpm-HxsgqczwNsXAI72Ofh34eVwToord1tulissft2PV10W4d8teTsq_Y5iAhQYFg)

![](https://lh4.googleusercontent.com/sn1L9X9-EXhMzWCeuw4eKp3msmRU8tdw08iP-K-VOxl_MJ-iSgNfwimN6OddOJAwh6YQjnEw1DqSwmXN5XKUn57RM7XtRbzYlJ8QXLXiSWsyUY69rONFwGl68RStgALmBoAWIO4dvTop4oOgOZPmHRs)