# Network Addressing

## Summary

This topic covers network addressing, the process of assigning unique logical identifiers to devices in a network to enable communication. It includes:

* **Network Addressing Concepts**: Understanding IP and MAC addresses and their roles in device identification and routing.
* **IP Address Types and Classes**: Exploring IPv4, IPv6, classful addressing, and public/private addresses.
* **IP Address Assignment**: Configuring static and dynamic (DHCP) addresses.
* **Advantages and Troubleshooting**: Benefits of addressing and resolving common issues.

---

## Network Addressing Concepts

Network addressing assigns unique logical identifiers to devices, enabling identification, communication, and routing across networks. Addresses are software-based, configurable, and distinct for each network interface (e.g., Wi-Fi vs. LAN). Key address types include **IP addresses** (Layer 3, for routing) and **MAC addresses** (Layer 2, for local communication).

**Key Components**:
- **IP Address**: Identifies a device in an IP network (e.g., 192.168.1.10).
- **MAC Address**: 48-bit hardware address for local communication (e.g., 00:1A:2B:3C:4D:5E).
- **Default Gateway**: Routes traffic to other networks (e.g., router IP).

**Purpose**:
- Uniquely identifies devices/interfaces.
- Facilitates routing and forwarding.
- Supports network management and communication.

**Example**:
- A PC with IP 192.168.1.10 and MAC 00:1A:2B:3C:4D:5E communicates locally via MAC and externally via IP through a gateway (192.168.1.1).

Scenario: A small office assigns IP addresses to PCs and printers, using MAC addresses for local communication and a default gateway for internet access.

---

## IP Address Types and Classes

IP addresses are categorized into **IPv4** and **IPv6**, with historical **classful addressing** dividing IPv4 into classes A–E. Public and private IP ranges support global and local communication, respectively.

**IP Address Types**:
- **IPv4**: 32-bit, dotted decimal (e.g., 192.168.0.1), ~4.3 billion addresses.
- **IPv6**: 128-bit, hexadecimal with colons (e.g., 2001:0db8:85a3::2c1f), ~3.4 × 10^38 addresses.

**Classful Addressing** (IPv4, largely replaced by CIDR):
| Class | First Octet Range | Default Address Range       | Example Address         | Use Case                     |
|-------|-------------------|-----------------------------|-------------------------|------------------------------|
| A     | 1–126             | 1.0.0.0–126.255.255.255     | 10.52.3.11              | Large networks, many hosts   |
| B     | 128–191           | 128.0.0.0–191.255.255.255   | 172.16.52.63            | Medium networks              |
| C     | 192–223           | 192.0.0.0–223.255.255.255   | 192.168.123.45          | Small networks               |
| D     | 224–239           | 224.0.0.0–239.255.255.255   | N/A                     | Multicast                    |
| E     | 240–255           | 240.0.0.0–255.255.255.255   | N/A                     | Reserved (research)          |

**Special Addresses**:
- **Private IP Ranges** (non-routable, used with NAT):
  - Class A: 10.0.0.0–10.255.255.255
  - Class B: 172.16.0.0–172.31.255.255
  - Class C: 192.168.0.0–192.168.255.255
- **Public IP**: Globally unique, assigned by ISPs (e.g., 203.0.113.1).
- **Special IPv4**:
  - 0.0.0.0: Default/unspecified.
  - 127.0.0.1: Loopback (localhost).
  - 255.255.255.255: Broadcast.

**Example**:
- Class A: 10.1.2.3 (private, large network).
- Class B: 172.16.1.100 (private, medium network).
- Class C: 192.168.1.200 (private, small network).
- IPv6: 2001:0db8::1 (global, documentation range).

Scenario: A university uses private 192.168.1.x addresses for its LAN and public IPs for external servers, planning IPv6 adoption for IoT scalability.

---

## IP Address Assignment

IP addresses are assigned either **statically** (manual configuration) or **dynamically** (via DHCP). Each device requires an IP address and default gateway for TCP/IP communication.

**Static Assignment**:
- Manually configured on devices.
- Suitable for servers, printers, or critical devices.
- Example: Assign 192.168.1.10, gateway 192.168.1.1 to a server.

**Dynamic Assignment (DHCP)**:
- DHCP server assigns IPs from a pool.
- Simplifies client configuration (PCs, phones).
- Example: DHCP pool 192.168.1.100–200, lease duration 24 hours.

**Example Configuration** (Cisco Router with DHCP):
```
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# ip dhcp pool LAN
R1(config-dhcp)# network 192.168.1.0 255.255.255.0
R1(config-dhcp)# default-router 192.168.1.1
R1(config-dhcp)# dns-server 8.8.8.8
R1(config-dhcp)# lease 1
R1(config-dhcp)# exit
R1# copy running-config startup-config
```

**Static Client Example** (Windows PC):
- IP: 192.168.1.10, Subnet Mask: 255.255.255.0, Gateway: 192.168.1.1, DNS: 8.8.8.8.

**Verification Commands**:
- `show ip interface brief`: Checks router interface IPs.
- `show ip dhcp binding`: Lists DHCP-assigned IPs.

Example output for `show ip dhcp binding`:
```
IP address       Client-ID/Hardware address  Lease expiration
192.168.1.100    00:1A:2B:3C:4D:5E          Jun 23 2025 10:00 AM
```

Scenario: A small office uses DHCP for employee laptops (192.168.1.100–200) and static IPs for printers (192.168.1.10–20), ensuring reliable access.

---

## Advantages and Troubleshooting

Network addressing provides critical benefits for communication, scalability, and management. Troubleshooting ensures proper address configuration and connectivity.

**Advantages**:
- **Unique Identification**: Differentiates devices via IP/MAC addresses.
- **Routing/Forwarding**: Enables packet delivery across networks.
- **Scalability**: Supports large device counts with IPv4/IPv6.
- **Address Resolution**: Maps IPs to MACs via ARP.
- **Multicast/Broadcast**: Facilitates group communication.
- **Network Management**: Simplifies monitoring and troubleshooting.
- **Internet Integration**: Enables global connectivity via IP.

**Troubleshooting Common Issues**:
- **Duplicate IP**: Devices conflict. Check with `arp -a` or `show arp` and reassign IPs.
- **Incorrect IP Configuration**: Devices cannot communicate. Verify with `ipconfig` (Windows) or `show ip interface brief` and correct IP/gateway.
- **Missing Gateway**: No external access. Confirm gateway matches router IP.
- **DHCP Failure**: Clients get APIPA (169.254.x.x). Check DHCP pool with `show ip dhcp pool` and ensure server is active.
- **Invalid IP Range**: Private IP used publicly. Verify range (e.g., 192.168.x.x) and use NAT for internet access.

**Troubleshooting Scenario**: A PC cannot access the internet. `ipconfig` shows 169.254.1.5 (APIPA). `show ip dhcp pool` on R1 reveals an exhausted pool. Expanding the pool to 192.168.1.100–250 resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Duplicate IP         | Connectivity conflicts        | Reassign unique IPs                  |
| Incorrect IP Config  | Cannot reach other devices    | Correct IP/gateway settings          |
| Missing Gateway      | No internet access            | Set gateway to router IP             |
| DHCP Failure         | APIPA address (169.254.x.x)   | Check/expand DHCP pool               |

**Verification Example**:
```
R1# show ip interface brief
Interface    IP-Address      OK?  Method  Status  Protocol
GigabitEthernet0/0  192.168.1.1  YES  manual  up      up
R1# ping 192.168.1.100
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.100, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5)
```

Scenario: An admin configures static IPs for servers and DHCP for clients, troubleshooting duplicate IPs to ensure seamless communication.