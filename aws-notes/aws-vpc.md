## VPC
- Scope: Regional
- SIDR - IP Address range
	- 10.0.0.0/16
### Subnet
- Scope: Availibility zone
- Internet facing / Private subnet
	- SIDR
		Subnet AZ1			Subnet AZ1
		- 10.0.1.0/24		- 10.0.3.0/24
		- 10.0.2.0/24		- 10.0.4.0/24

### Routing
- Main Route table
Network | Target
10.0.0.0/16 | Local

### Internet Gateway
- Scope: Regional
- Used by public subnet for internet traffic
- Public Route table
Network | Target
10.0.0.0/16 | Local
0.0.0.0/0 | IGW	

### NAT - Network Address Translation
- convert private address to public adress on internet
- Private Route table
Network | Target
10.0.0.0/16 | Local
0.0.0.0/0 | NAT	

### Virtual private gateway 
- conection to on-premis
- VPN 

### Network Access Control List 
- One subnet to another subnet
- default allow all

---

VPC - 10.0.0.0/16
		- Subnet AZ1
			- 10.0.1.0/24 - public - Internet gate		
			- 10.0.4.0/24 - private - NAT	
		- Subnet AZ1
			- 10.0.3.0/24
			- 10.0.2.0/24	
