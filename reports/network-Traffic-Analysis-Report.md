# Network Traffic Analysis — Technical Report

## 1. Introduction

The objective of this project was to understand network communication by capturing and analysing packets using Wireshark. Nmap was used to perform TCP port scanning against an Ubuntu virtual machine.

## 2. Experimental Setup

- Host OS: Windows
- Target OS: Ubuntu Server
- Virtualisation: Oracle VirtualBox
- Packet analyser: Wireshark
- Network scanner: Nmap
- Target IP: 192.168.56.103
- Network configuration: NAT and Host-only adapters

## 3. Experiment Details

### Experiment 1: DNS Analysis

**Procedure:** Used `nslookup example.com` to generate DNS queries while capturing traffic in Wireshark.

**Results:** Observed DNS queries and responses, including A and AAAA records. DNS queries commonly use UDP port 53.

**Security relevance:** DNS traffic analysis can help identify unusual domain lookups and suspicious DNS activity.

### Experiment 2: ARP Analysis

**Procedure:** Cleared the ARP cache and generated traffic using ping to observe address resolution.

**Results:** Captured ARP requests and replies. The request was broadcast, and the device owning the requested IP responded with its MAC address.

**Security relevance:** Unexpected changes in IP-to-MAC mappings can indicate possible ARP spoofing.

### Experiment 3: TCP Handshake Analysis

**Procedure:** Generated HTTPS traffic and applied TCP flag filters in Wireshark.

**Results:** Observed the three stages of TCP connection establishment:

1. SYN
2. SYN-ACK
3. ACK

**Security relevance:** TCP flag analysis helps identify connection attempts, unusual connection patterns and potential scanning activity.

### Experiment 4: HTTP Analysis

**Procedure:** Generated HTTP traffic and inspected request and response packets.

**Results:** Observed HTTP GET requests, headers and server responses, including HTTP 200 OK.

**Security relevance:** Unencrypted HTTP communication can expose application data to network observers.

### Experiment 5: Nmap Port Scanning

**Procedure:** Configured a Host-only network between Windows and Ubuntu. Started the SSH service on Ubuntu and scanned the target using:

`nmap -sT -p 22 192.168.56.103`

**Results:**
- Port 22 was identified as open.
- Wireshark captured the TCP connection sequence.
- The SSH server banner was visible.
- The connection was subsequently reset.

**Packet analysis:**

| Packet | Direction | TCP flag / activity |
|---|---|---|
| 4 | Windows → Ubuntu | SYN |
| 5 | Ubuntu → Windows | SYN-ACK |
| 6 | Windows → Ubuntu | ACK |
| 7 | Ubuntu → Windows | SSH banner |
| 8 | Windows → Ubuntu | RST, ACK |

**Security relevance:** Port scanning can identify exposed services. Unnecessary services should be disabled or restricted using firewall rules.

## 4. Key Findings

- DNS uses queries and responses to resolve domain names.
- ARP maps local IP addresses to MAC addresses.
- TCP establishes connections using a three-way handshake.
- HTTP traffic can expose information because it is unencrypted.
- Nmap can identify open TCP ports.
- Wireshark provides packet-level visibility into network activity.

## 5. Conclusion

The experiments provided practical exposure to network protocols, packet inspection and port scanning. The project helped develop foundational skills relevant to network security, traffic analysis and security monitoring.

## 6. Tools Used

- Wireshark
- Nmap
- Ubuntu Server
- Windows
- Oracle VirtualBox