# Ex. No: 9 - Packet Tracer: Subnet an IPv4 Network
# Date: 03-10-2025
________________________________________ <br>
# Objective
Design, configure, and verify an IPv4 subnetting scheme in Cisco Packet Tracer.<br>
•	Subnet the 192.168.0.0/24 network into multiple subnets.<br>
•	Assign addresses to LAN-A, LAN-B, and future networks.<br>
•	Configure IP addressing on routers, switches, and PCs.<br>
•	Verify connectivity using ping and router show commands.<br>
________________________________________
# Apparatus / Tools Required
•	Cisco Packet Tracer<br>
•	CustomerRouter (2911 or equivalent)<br>
•	ISP Router<br>
•	2 Customer Switches (LAN-A Switch, LAN-B Switch)<br>
•	ISP Switch<br>
•	2 PCs (PC-A, PC-B)<br>
•	ISP Workstation and ISP Server<br>
•	Copper straight-through cables for LAN links<br>
•	Serial DCE/DTE cable for WAN link<br>
________________________________________<br>
# Network Topology Diagram
(Insert your Packet Tracer screenshot showing CustomerRouter → LAN-A Switch → PC-A, CustomerRouter → LAN-B Switch → PC-B, and ISP side with Router, Switch, Workstation, Server, and Serial link.)<br>

<img width="1919" height="1015" alt="image" src="https://github.com/user-attachments/assets/821fffb7-517e-4aef-b527-f48c3986fa5d" />

________________________________________<br>
# Addressing Table
Device	Interface	IP Address	Subnet Mask	Default Gateway<br>
CustomerRouter	G0/0	(1st host of LAN-A subnet)	(Subnet mask)	N/A<br>
CustomerRouter	G0/1	(1st host of LAN-B subnet)	(Subnet mask)	N/A<br>
CustomerRouter	S0/1/0	209.165.201.2	255.255.255.252	N/A<br>
LAN-A Switch	VLAN1	(2nd host of LAN-A subnet)	(Subnet mask)	CustomerRouter G0/0<br>
LAN-B Switch	VLAN1	(2nd host of LAN-B subnet)	(Subnet mask)	CustomerRouter G0/1<br>
PC-A	NIC	(Last host of LAN-A subnet)	(Subnet mask)	CustomerRouter G0/0<br>
PC-B	NIC	(Last host of LAN-B subnet)	(Subnet mask)	CustomerRouter G0/1<br>
ISP Router	G0/0	209.165.200.225	255.255.255.224	N/A<br>
ISP Router	S0/1/0	209.165.201.1	255.255.255.252	N/A<br>
ISP Switch	VLAN1	209.165.200.226	255.255.255.224	209.165.200.225<br>
ISP Workstation	NIC	209.165.200.235	255.255.255.224	209.165.200.225<br>
ISP Server	NIC	209.165.200.240	255.255.255.224	209.165.200.225<br>
(LAN-A and LAN-B IPs to be filled in after subnetting calculation.)<br>
________________________________________<br>
# Procedure
# Part 1: Subnet the Assigned Network
1.	Start with 192.168.0.0/24.<br>
2.	Requirements:<br>
o	LAN-A: ≥50 hosts<br>
o	LAN-B: ≥40 hosts<br>
o	At least 2 unused subnets for future expansion.<br>
3.	Choose a subnet mask that supports both host requirements.<br>
o	Example: /26 (255.255.255.192) → 62 hosts per subnet, 4 subnets.
4.	Allocate:<br>
o	Subnet 1 → LAN-A<br>
o	Subnet 2 → LAN-B<br>
o	Subnets 3 & 4 → Reserved<br>
________________________________________<br>
# Part 2: Configure the Devices
CustomerRouter<br>
•	Set hostname: hostname CustomerRouter<br>
•	Passwords:<br>
o	enable secret Class123<br>
o	line console 0 → password Cisco123 → login<br>
•	Configure interfaces:<br>
•	interface g0/0  <br>
•	 ip address <LAN-A first host> <mask>  
•	 no shutdown  
•	interface g0/1  
•	 ip address <LAN-B first host> <mask>  <br>
•	 no shutdown  <br>
•	interface s0/1/0  <br>
•	 ip address 209.165.201.2 255.255.255.252  <br>
•	 clock rate 64000   ← DCE end  <br>
•	 no shutdown  <br>
•	Save: copy running-config startup-configv
Switches (LAN-A, LAN-B)<br>
•	VLAN1 IP: 2nd host of subnet<br>
•	Default gateway: Router G0/0 or G0/1<br>
PCs (PC-A, PC-B)<br>
•	Last host of subnet<br>
•	Subnet mask and gateway configured<br>
________________________________________<br>
# Part 3: Verification & Testing
1.	On routers:<br>
o	show ip interface brief (check status up/up)<br>
o	show ip route (verify connected subnets)<br>
2.	On PCs:<br>
o	Ping default gateway<br>
o	Ping across subnets (PC-A ↔ PC-B)<br>
o	Ping ISP Server<br>
________________________________________<br>
# Commands Used (Summary)
•	Mode/navigation: enable, configure terminal, end<br>
•	Interface config: interface g0/0, ip address, no shutdown<br>
•	Show/verify: show ip interface brief, show ip route<br>
•	Save: copy running-config startup-config<br>
________________________________________<br>
# Output (Attach Screenshots)
•	show ip interface brief on CustomerRouter<br>

<img width="1919" height="1018" alt="image" src="https://github.com/user-attachments/assets/19701286-53cb-4299-ba8c-180b9fd80c39" />

•	show ip route<br>

<img width="1919" height="1018" alt="image" src="https://github.com/user-attachments/assets/c3b9e367-3d01-421b-baeb-aa3249b89e9d" />

•	Successful pings: PC-A → PC-B, PC-A → ISP Server<br>

<img width="1919" height="1012" alt="image" src="https://github.com/user-attachments/assets/50e90e6e-c0b8-4515-af1b-81ab5905fc6f" />

<img width="1916" height="1016" alt="image" src="https://github.com/user-attachments/assets/fb60be4d-270a-42c5-a4a8-8dc7b8c8f293" />

<img width="1919" height="1016" alt="image" src="https://github.com/user-attachments/assets/f3c6c3ba-8893-48df-a11a-d5580ca3eab8" />



________________________________________<br>
# Result
The IPv4 subnetting scheme was successfully designed and implemented. Router, switches, and PCs were configured with correct addressing. Connectivity within LANs, across subnets, and to ISP devices was verified using ping and show commands.<br>

