Secure Campus Network Using Cisco Packet Tracer
Project Overview
This mini project demonstrates the design and implementation of a small secure campus network using Cisco Packet Tracer. The network connects two separate LANs through one router and two switches. Basic security mechanisms are configured to protect network devices and restrict unauthorized access.
Objectives
- Design and simulate a campus network using Cisco routers, switches, and PCs.
- Configure IP addressing and communication between two LAN networks.
- Protect router and switch access using console and privileged EXEC passwords.
- Enable SSH for secure remote administration.
- Apply password encryption to locally configured passwords.
- Configure switch port security with sticky MAC address learning.
- Disable unused switch ports and verify network connectivity and security.
Network Topology
The simulated network contains:
- 1 Cisco 2911 Router — R1
- 2 Cisco 2960 Switches — S1 and S2
- 6 PCs — PC1 to PC6
- Copper straight-through cables
The router connects the two LANs:
- Network 1: 192.168.10.0/24 — connected to S1 and PC1–PC3
- Network 2: 192.168.20.0/24 — connected to S2 and PC4–PC6
IP Addressing Plan
Device	Interface	IP address	Subnet mask	Default gateway
R1	G0/0	192.168.10.1	255.255.255.0	—
R1	G0/1	192.168.20.1	255.255.255.0	—
S1	VLAN 1	192.168.10.2	255.255.255.0	192.168.10.1
S2	VLAN 1	192.168.20.2	255.255.255.0	192.168.20.1
PC1	NIC	192.168.10.10	255.255.255.0	192.168.10.1
PC2	NIC	192.168.10.11	255.255.255.0	192.168.10.1
PC3	NIC	192.168.10.12	255.255.255.0	192.168.10.1
PC4	NIC	192.168.20.10	255.255.255.0	192.168.20.1
PC5	NIC	192.168.20.11	255.255.255.0	192.168.20.1
PC6	NIC	192.168.20.12	255.255.255.0	192.168.20.1


Main Security Features
1. Console security: Password protection is configured for console access to the router and switches.
2. Privileged EXEC security: The enable secret command protects privileged EXEC mode.
3. Password encryption: service password-encryption obfuscates line passwords in the device configuration. It is not strong cryptographic protection; use enable secret for privileged access.
4. SSH remote access: SSH version 2 is configured for secure remote administration using a local username.
5. Switch port security: Access ports are configured to allow one secure MAC address, use sticky MAC learning, and shut down the port when a security violation occurs.
6. Unused ports: Unused switch ports (Fa0/4–Fa0/24) are shut down to reduce the risk of unauthorized connections.
Configuration and Setup
1. Open Cisco Packet Tracer and create the topology with one Cisco 2911 router, two Cisco 2960 switches, and six PCs.
2. Connect R1 G0/0 to S1 G0/1 and R1 G0/1 to S2 G0/1.
3. Connect PC1–PC3 to S1 Fa0/1–Fa0/3 and PC4–PC6 to S2 Fa0/1–Fa0/3.
4. Configure the router interfaces with the IP addresses in the addressing table and enable the interfaces using no shutdown.
5. Configure the switch management addresses on VLAN 1 and set each switch's default gateway.
6. Configure console passwords, enable secret, password encryption, and SSH on R1, S1, and S2.
7. Apply port security to the PC-facing access ports. Set the maximum secure MAC address count to 1, enable sticky MAC learning, and use shutdown as the violation action.
8. Configure the IP address, subnet mask, and default gateway on each PC under Desktop → IP Configuration.
9. Shut down unused switch ports and save the configurations on R1, S1, and S2 using:
copy running-config startup-config
For the complete device-specific Cisco IOS commands, follow the configuration steps in the project document.
Testing and Verification
Network connectivity
From PC1, use the Command Prompt to test the router and devices on the other LAN:
ping 192.168.10.1
ping 192.168.20.10
ping 192.168.20.11
ping 192.168.20.12
Successful replies confirm connectivity after ARP and MAC address learning have completed.
SSH access
Test SSH access from the PCs to the router and switches. For example:
ssh -l admin 192.168.10.2
ssh -l admin 192.168.10.1
From PC4, test access to S2:
ssh -l admin 192.168.20.2
Port security
Use the following commands on the switch to verify port security:
show port-security
show port-security address
show port-security interface fastEthernet 0/1
show mac address-table
To demonstrate a violation, first connect PC1 to S1 Fa0/1 and generate traffic so the switch learns its MAC address. Then connect a different PC to that port. The switch should detect a violation because the port permits only one secure MAC address.

To recover a port placed in the shutdown state, enter interface configuration mode and run:
interface fastEthernet 0/1
shutdown
no shutdown
Expected Results
- PCs in both LANs can communicate through the router.
- Console and privileged EXEC access are password-protected.
- SSH remote login is available on the router and switches.
- Port security learns the permitted MAC address and detects an unauthorized replacement device.
- Unused switch ports remain disabled.
Project Deliverables
- Cisco Packet Tracer (.pkt) project file
- Network topology screenshot
- IP addressing table
- Router and switch configuration screenshots
- SSH login screenshot
- Port security verification and violation screenshots
- Network connectivity test screenshots
- Short project report with observations and conclusion
Conclusion
This project provides practical experience in configuring and securing Cisco routers and switches. It demonstrates how IP addressing, inter-network communication, console and privileged EXEC protection, SSH, password obfuscation, and switch port security can be combined to improve the security of a small campus network. The Packet Tracer simulation also provides a foundation for understanding network administration and basic network security in larger organizational environments.
Tools and Technologies
- Cisco Packet Tracer
- Cisco IOS CLI
- Cisco 2911 Router
- Cisco 2960 Switches
- SSH version 2
- IPv4 addressing
Security Note
The passwords used in a classroom simulation should be treated as examples only. Change all credentials before using similar configurations in a real network, and do not publish real passwords or private keys in a public repository.
