# Wireshark Network Traffic Analysis

## Project Overview

This project explores network traffic analysis using Wireshark and Nmap. It focuses on understanding common network protocols, observing packet exchanges, and identifying open ports through practical experiments.

The experiments were performed on a Windows host machine and an Ubuntu virtual machine using VirtualBox.

## Objectives

- Understand how DNS queries and responses work.
- Observe ARP requests and replies.
- Analyse the TCP three-way handshake.
- Inspect HTTP request and response packets.
- Perform TCP port scanning using Nmap.
- Understand how network activity appears at packet level.

## Tools and Technologies

- **Wireshark:** Network protocol analyser used to capture and inspect packets.
- **Nmap:** Network scanning tool used to identify open ports.
- **Windows:** Host operating system.
- **Ubuntu Server:** Virtual machine used as the scanning target.
- **VirtualBox:** Virtualisation platform used to create the lab environment.

## Lab Environment

| Component | Configuration |
|---|---|
| Host machine | Windows |
| Virtual machine | Ubuntu Server |
| Virtualisation | VirtualBox |
| Ubuntu NAT IP | 10.0.2.15 |
| Ubuntu Host-only IP | 192.168.56.103 |
| Network capture | Wireshark |
| Port scanning | Nmap |

A Host-only network adapter was configured to allow communication between Windows and Ubuntu without directly exposing the VM to the external network.

## Experiments

### 1. DNS Traffic Analysis

**Objective:** Observe DNS queries and responses.

**Activities:**
- Captured DNS traffic using Wireshark.
- Generated DNS queries using `nslookup example.com`.
- Examined A and AAAA record queries.

**Observations:**
- DNS queries and responses were captured.
- DNS commonly uses UDP port 53.
- A records resolve IPv4 addresses, while AAAA records resolve IPv6 addresses.

### 2. ARP Traffic Analysis

**Objective:** Understand how devices discover MAC addresses on a local network.

**Activities:**
- Cleared the ARP cache.
- Generated traffic using ping.
- Captured ARP requests and replies.

**Observations:**
- ARP requests are broadcast on the local network.
- The device owning the requested IP responds with its MAC address.
- ARP spoofing can exploit the trust devices place in ARP mappings.

### 3. TCP Three-Way Handshake

**Objective:** Observe how TCP connections are established.

**Activities:**
- Generated HTTPS traffic.
- Used Wireshark to inspect TCP flags.

**Observations:**
- SYN: Client requests a connection.
- SYN-ACK: Server acknowledges the request.
- ACK: Client acknowledges the server's response.
- TLS negotiation follows the TCP handshake for HTTPS connections.

### 4. HTTP Traffic Analysis

**Objective:** Inspect HTTP requests and responses.

**Activities:**
- Generated HTTP traffic.
- Examined HTTP request and response packets.

**Observations:**
- HTTP requests contain information such as the requested resource and Host header.
- HTTP responses contain status codes, such as 200 OK.
- Unencrypted HTTP traffic can expose application-layer information to network observers.

### 5. Nmap Port Scanning

**Objective:** Identify open TCP ports and observe the scanning process.

**Activities:**
- Configured a Host-only network between Windows and Ubuntu.
- Started the SSH service on Ubuntu.
- Used Nmap TCP Connect Scan (`-sT`) to scan selected ports.
- Captured the scan traffic using Wireshark.

**Target:** Ubuntu VM — `192.168.56.103`

**Command used:**

`nmap -sT -p 22 192.168.56.103`

**Observations:**
- Port 22 was identified as open.
- Wireshark captured the TCP SYN, SYN-ACK and ACK sequence.
- The SSH server banner was observed.
- A TCP reset followed the connection attempt.

## Security Learnings

- DNS traffic can reveal information about requested domains.
- ARP spoofing can allow attackers to manipulate local network communication.
- TCP flags help identify connection attempts and connection states.
- Unencrypted HTTP traffic can expose information.
- Port scanning helps identify services that may need security monitoring.
- Firewalls and network segmentation help restrict unauthorised access.

## Repository Structure

```text
Wireshark-Network-Traffic-Analysis/
│
├── Screenshots/
├── Reports/
├── Documentation/
└── README.md
```

## Conclusion

This project provided practical experience in capturing and analysing network traffic, understanding common network protocols, and identifying exposed services through port scanning.

It helped develop foundational skills in network analysis and cybersecurity monitoring.