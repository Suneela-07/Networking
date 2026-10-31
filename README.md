# Secure Campus Network Using Cisco Packet Tracer

## Project Overview

This mini project demonstrates the design and implementation of a small secure campus network using **Cisco Packet Tracer**. The network connects two separate LANs through one router and two switches. Basic security mechanisms are configured to protect network devices and restrict unauthorized access.

## Objectives

- Design and simulate a campus network using Cisco routers, switches, and PCs.
- Configure IP addressing and communication between two LAN networks.
- Protect router and switch access using console and privileged EXEC passwords.
- Enable SSH for secure remote administration.
- Apply password encryption to locally configured passwords.
- Configure switch port security with sticky MAC address learning.
- Disable unused switch ports and verify network connectivity and security.

## Network Topology

The simulated network contains:

- **1 Cisco 2911 Router** – R1
- **2 Cisco 2960 Switches** – S1 and S2
- **6 PCs** – PC1 to PC6
- Copper straight-through cables

The router connects two LANs:

- **Network 1:** `192.168.10.0/24` – Connected to S1 and PC1–PC3.
- **Network 2:** `192.168.20.0/24` – Connected to S2 and PC4–PC6.

## IP Addressing Plan

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| R1 | G0/0 | 192.168.10.1 | 255.255.255.0 | — |
| R1 | G0/1 | 192.168.20.1 | 255.255.255.0 | — |
| S1 | VLAN 1 | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 |
| S2 | VLAN 1 | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 |
| PC1 | NIC | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC2 | NIC | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| PC3 | NIC | 192.168.10.12 | 255.255.255.0 | 192.168.10.1 |
| PC4 | NIC | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |
| PC5 | NIC | 192.168.20.11 | 255.255.255.0 | 192.168.20.1 |
| PC6 | NIC | 192.168.20.12 | 255.255.255.0 | 192.168.20.1 |

## Security Features

1. **Console Security:** Protects console access to routers and switches using passwords.
2. **Privileged EXEC Security:** Uses the `enable secret` command to protect privileged EXEC mode.
3. **Password Encryption:** Uses `service password-encryption` to obfuscate configured line passwords.
4. **SSH Configuration:** Enables SSH version 2 for secure remote device administration.
5. **Port Security:** Uses sticky MAC address learning to restrict unauthorized devices.
6. **Unused Port Shutdown:** Disables unused switch ports to reduce unauthorized network connections.

## Configuration Steps

1. Create the network topology using one Cisco 2911 router, two Cisco 2960 switches, and six PCs.
2. Connect the router to both switches.
3. Connect the PCs to their respective switches.
4. Configure router interfaces with the required IP addresses.
5. Configure switch management IP addresses and default gateways.
6. Implement console security and privileged EXEC passwords.
7. Configure password encryption and SSH on the router and switches.
8. Enable port security on the PC-connected switch ports.
9. Configure IP addresses and default gateways on all PCs.
10. Disable unused switch ports.
11. Test network connectivity and verify security configurations.
12. Save the configurations using:

```bash
copy running-config startup-config
```

## Testing and Verification

### 1. Network Connectivity Testing

Use the following commands from PC1:

```bash
ping 192.168.10.1
ping 192.168.20.10
ping 192.168.20.11
ping 192.168.20.12
```

Successful replies confirm communication between the devices.

### 2. SSH Testing

Test secure remote access using:

```bash
ssh -l admin 192.168.10.2
ssh -l admin 192.168.10.1
```

From PC4:

```bash
ssh -l admin 192.168.20.2
```

### 3. Port Security Verification

Use the following Cisco IOS commands:

```bash
show port-security
show port-security address
show port-security interface fastEthernet 0/1
show mac address-table
```

### 4. Port Security Violation Testing

- Connect PC1 to S1 Fa0/1 and generate network traffic.
- The switch learns PC1's MAC address.
- Disconnect PC1 and connect another PC to the same port.
- The switch detects the unauthorized MAC address and shuts down the port.

To recover the interface:

```bash
configure terminal
interface fastEthernet 0/1
shutdown
no shutdown
```

## Expected Results

- Successful communication between both LAN networks.
- Password-protected router and switch access.
- Secure remote administration using SSH.
- Successful sticky MAC address learning.
- Detection of unauthorized device connections.
- Unused switch ports disabled.

## Project Deliverables

- Cisco Packet Tracer (`.pkt`) file.
- Network topology screenshot.
- IP addressing table.
- Router and switch configuration screenshots.
- SSH login screenshot.
- Port security verification screenshot.
- Port security violation demonstration screenshot.
- Network connectivity test screenshots.
- Project documentation.

## Conclusion

This project demonstrates the design and implementation of a secure campus network using Cisco Packet Tracer. It provides practical experience in router and switch configuration, IP addressing, secure remote access, password protection, and switch port security. The successful implementation of these security mechanisms improves access control and helps prevent unauthorized network connections. Overall, the project provides a foundation for understanding network administration and basic network security in organizational environments.

## Tools and Technologies

- Cisco Packet Tracer
- Cisco IOS Command-Line Interface (CLI)
- Cisco 2911 Router
- Cisco 2960 Switches
- SSH Version 2
- IPv4 Addressing

## Security Note

The passwords used in this project are for demonstration purposes only. Replace example credentials with strong passwords before implementing similar configurations in a real network.
