# Classful, Classless Routing, and IP Addressing

## Summary

This topic covers IP addressing concepts, including classful and classless addressing, subnetting, Variable Length Subnet Mask (VLSM), and route summarization, essential for efficient network design. It includes:

* **Classful IP Addressing**: Traditional IP address classes and their limitations.
* **IPv6 Addressing**: Structure and benefits of IPv6 over IPv4.
* **Subnetting and VLSM**: Dividing networks into subnets and optimizing IP allocation.
* **Route Summarization**: Combining subnets to reduce routing table size.

---

## Classful IP Addressing

Classful IP addressing divides IPv4 addresses into five classes (A, B, C, D, E) based on the first octet, each with a default subnet mask. It was used historically but is less common today due to inefficiencies.

- **Class A**: Large networks, 1–126 (e.g., 10.1.1.1, 255.0.0.0, /8).
- **Class B**: Medium networks, 128–191 (e.g., 128.1.1.1, 255.255.0.0, /16).
- **Class C**: Small networks, 192–223 (e.g., 192.168.1.1, 255.255.255.0, /24).
- **Class D**: Multicast, 224–239.
- **Class E**: Reserved, 240–254.

Limitations include inefficient address allocation and risk of address exhaustion. Private IP ranges (e.g., 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) are used for internal networks, while public IPs are ISP-assigned.

| Class | Range         | Default Mask       | Max Networks | Use Case            |
|-------|---------------|--------------------|--------------|---------------------|
| A     | 1–126         | 255.0.0.0 (/8)     | 128          | Large networks      |
| B     | 128–191       | 255.255.0.0 (/16)  | 16,384       | Medium networks     |
| C     | 192–223       | 255.255.255.0 (/24)| 2,097,157    | Small networks      |

Scenario: A company uses 192.168.1.0/24 (Class C) for its internal network, reserving 10.0.0.0/8 for future expansion.

---

## IPv6 Addressing

IPv6 uses 128-bit addresses (e.g., 2003:DB0:AAAA:A::1/64), providing a vast address space (2^128) compared to IPv4. Represented in colon-hexadecimal notation, it simplifies headers, eliminates broadcasts, and supports mobility and security.

Address types:
- **Unicast**: For a single interface (e.g., global: 2000::/3, unique local: FD00::/8, link-local: FE80::/10).
- **Multicast**: For groups (e.g., ff02::1 for all IPv6 devices).
- **Anycast**: For the nearest interface in a group.

Example configuration on a Cisco router:
```
Router(config)# ipv6 unicast-routing
Router(config)# interface g0/0
Router(config-if)# ipv6 enable
Router(config-if)# ipv6 address 2003:DB0:AAAA:A::1/64
Router(config-if)# exit
Router(config)# interface g0/1
Router(config-if)# ipv6 enable
Router(config-if)# ipv6 address 2003:DB0:AAAA:B::1/64
```

Verification:
```
Router# show ipv6 interface brief
Router# ping 2003:DB0:AAAA:B::2
```

Scenario: A network admin configures IPv6 on a router to enable communication between PCs in subnets 2003:DB0:AAAA:A::/64 and 2003:DB0:AAAA:B::/64.

---

## Subnetting and VLSM

Subnetting divides a network into smaller subnets to improve efficiency, security, and speed. Variable Length Subnet Mask (VLSM) allows different subnet masks within the same network, optimizing IP usage.

For example, subnet 192.168.1.0/24 into four subnets:
- New mask: /26 (255.255.255.192).
- Subnets: 2^2 = 4.
- Hosts per subnet: 2^6 − 2 = 62.
- Block size: 256 − 192 = 64.

| Subnet | Network Address | Host Range              | Broadcast Address |
|--------|-----------------|-------------------------|-------------------|
| 1      | 192.168.1.0     | 192.168.1.1–192.168.1.62 | 192.168.1.63      |
| 2      | 192.168.1.64    | 192.168.1.65–192.168.1.126 | 192.168.1.127    |
| 3      | 192.168.1.128   | 192.168.1.129–192.168.1.190 | 192.168.1.191   |
| 4      | 192.168.1.192   | 192.168.1.193–192.168.1.254 | 192.168.1.255   |

VLSM example: Allocate IPs for departments from 192.168.1.0/24:
- Sales (120 hosts): /25 (126 hosts, 192.168.1.0–192.168.1.127).
- Development (50 hosts): /26 (62 hosts, 192.168.1.128–192.168.1.191).
- Accounts (26 hosts): /27 (30 hosts, 192.168.1.192–192.168.1.223).
- Management (5 hosts): /29 (6 hosts, 192.168.1.224–192.168.1.231).

| Department | Network         | Host Range              | Mask            |
|------------|-----------------|-------------------------|-----------------|
| Sales      | 192.168.1.0/25  | 192.168.1.1–192.168.1.126 | 255.255.255.128 |
| Development| 192.168.1.128/26| 192.168.1.129–192.168.1.190 | 255.255.255.192 |
| Accounts   | 192.168.1.192/27| 192.168.1.193–192.168.1.222 | 255.255.255.224 |
| Management | 192.168.1.224/29| 192.168.1.225–192.168.1.230 | 255.255.255.248 |

Scenario: A company uses VLSM to allocate IPs from 192.168.1.0/24, assigning larger subnets to departments with more devices to minimize IP waste.

---

## Route Summarization

Route summarization (supernetting) combines multiple subnets into a single route, reducing routing table size and improving router performance. It uses a shorter subnet mask to aggregate contiguous networks.

Example: Summarize 192.168.0.0/24, 192.168.1.0/24, 192.168.2.0/24, 192.168.3.0/24:
- Convert to binary and find common bits (22 bits).
- Result: 192.168.0.0/22.

| Network        | Binary Representation                     |
|----------------|-------------------------------------------|
| 192.168.0.0    | 11000000.10101000.00000000.00000000      |
| 192.168.1.0    | 11000000.10101000.00000001.00000000      |
| 192.168.2.0    | 11000000.10101000.00000010.00000000      |
| 192.168.3.0    | 11000000.10101000.00000011.00000000      |

Configuration on R3:
```
R3(config)# ip route 192.168.0.0 255.255.252.0 192.168.20.2
```

Scenario: An ISP summarizes customer networks (192.168.0.0/24 to 192.168.3.0/24) into 192.168.0.0/22 to reduce routing table size on its core router.