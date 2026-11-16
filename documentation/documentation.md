# Network Protocols — Quick Reference

## DNS (Domain Name System)

- Purpose: Converts domain names into IP addresses.
- Common port: UDP 53; TCP 53 is also used in certain situations.
- A record: Resolves a domain to an IPv4 address.
- AAAA record: Resolves a domain to an IPv6 address.
- Security concern: DNS spoofing and suspicious DNS queries.

## ARP (Address Resolution Protocol)

- Purpose: Finds the MAC address associated with an IPv4 address on a local network.
- ARP request: Broadcast to the local network.
- ARP reply: Provides the requested MAC address.
- Security concern: ARP spoofing or poisoning.

## TCP (Transmission Control Protocol)

- Purpose: Provides reliable, connection-oriented communication.
- Three-way handshake:
  1. SYN
  2. SYN-ACK
  3. ACK
- Common flags: SYN, ACK, FIN, RST, PSH.
- Security concern: SYN floods and suspicious connection attempts.

## HTTP (Hypertext Transfer Protocol)

- Purpose: Transfers web resources between clients and servers.
- Default port: TCP 80.
- GET: Requests a resource.
- POST: Sends data to a server.
- HTTP 200: Successful request.
- Security concern: HTTP does not encrypt application data.

## HTTPS

- HTTP communication protected using TLS.
- Default port: TCP 443.
- TLS provides encryption and server authentication.

## SSH (Secure Shell)

- Purpose: Secure remote access to another computer.
- Default port: TCP 22.
- Commonly used for remote administration.
- Security concern: Weak passwords, exposed services and compromised credentials.




# Wireshark Display Filters

Useful display filters used during the project.

| Filter | Purpose |
|---|---|
| `dns` | Display DNS packets |
| `arp` | Display ARP packets |
| `tcp` | Display TCP packets |
| `http` | Display HTTP packets |
| `tcp.port == 22` | Display SSH port traffic |
| `tcp.port == 80` | Display port 80 traffic |
| `tcp.port == 443` | Display port 443 traffic |
| `dns.qry.name == "example.com"` | Display DNS queries for example.com |
| `tcp.flags.syn == 1` | Display packets with SYN flag set |
| `tcp.flags.ack == 1` | Display packets with ACK flag set |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Display initial SYN packets |

## Notes

- Display filters only change which captured packets are shown; they do not delete other captured packets.
- TCP flags help identify connection establishment and termination.
- Combining filters helps isolate specific network activity.



# Nmap — Command Reference

## What is Nmap?

Nmap is a network scanning tool used to discover hosts, identify open ports and investigate network services.

## Commands

### 1. Scan a target

`nmap 192.168.56.103`

Scans commonly used ports on the target.

### 2. TCP Connect Scan

`nmap -sT 192.168.56.103`

Uses the operating system's TCP connection mechanism to test ports.

### 3. Scan specific ports

`nmap -sT -p 22,80,443 192.168.56.103`

Scans ports 22, 80 and 443.

### 4. Scan a port range

`nmap -sT -p 1-1000 192.168.56.103`

Scans TCP ports 1 through 1000.

## Understanding Port States

- Open: A service is listening and accepting connections.
- Closed: The target responds, but no service is listening on that port.
- Filtered: A firewall or network filter prevents Nmap from determining whether the port is open.

## Project Result

The Ubuntu VM at 192.168.56.103 had TCP port 22 open because the SSH service was running.

The TCP Connect Scan was observed in Wireshark, showing the SYN, SYN-ACK and ACK sequence, followed by connection termination.