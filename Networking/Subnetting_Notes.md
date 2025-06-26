# Subnetting

## Summary

This topic covers subnetting, the process of dividing a single network into smaller subnetworks (subnets) to optimize IP address allocation, enhance security, and improve network performance. It includes:

* **Subnetting Concepts**: Understanding subnetting, its purpose, and key terms like block size, borrowed bits, and host addresses.
* **Subnetting Techniques**: Exploring Fixed-Length Subnet Masking (FLSM), Variable-Length Subnet Masking (VLSM), CIDR, and other methods.
* **Advantages and Disadvantages**: Benefits and challenges of subnetting.
* **Implementation and Troubleshooting**: Step-by-step subnetting example, configuration, and resolving common issues.

---

## Subnetting Concepts

Subnetting divides a network into smaller subnets, each with its own network address and IP range. It uses bits from the host portion of an IP address to create subnet identifiers, allowing efficient IP allocation without requiring new network numbers from ISPs. Subnetting reduces network traffic, enhances security, and simplifies management by segmenting a large network into logical units.

**Key Terms**:
- **Subnet Mask**: Defines network and host portions (e.g., 255.255.255.0 or /24).
- **Block Size**: Number of addresses per subnet (e.g., 2^(32-prefix) = 256 for /24).
- **Borrowed Bits**: Host bits used for subnetting, increasing subnets but reducing hosts per subnet.
- **Network Address**: First address in a subnet (e.g., 192.168.10.0).
- **Broadcast Address**: Last address in a subnet (e.g., 192.168.10.255).
- **First/Last Valid Host**: Usable addresses between network and broadcast (e.g., 192.168.10.1–254 for /24).
- **Customized Subnet Mask (CSM)**: Non-default mask tailored to subnet needs (e.g., /26).

**Purpose**:
- Efficient IP address use.
- Reduced broadcast traffic.
- Improved security and management.

Scenario: A company subnets 192.168.10.0/24 to create separate networks for departments, reducing congestion and isolating sensitive data.

---

## Subnetting Techniques

Subnetting techniques vary in flexibility and efficiency, including Fixed-Length Subnet Masking (FLSM), Variable-Length Subnet Masking (VLSM), Classless Inter-Domain Routing (CIDR), borrowed bits, and supernetting.

**Techniques**:
- **FLSM**: Uses a single mask for all subnets, creating equal-sized subnets. Simple but wasteful for varied host needs.
- **VLSM**: Uses different masks within the same network, optimizing for varied subnet sizes (e.g., /30 for links, /24 for LANs).
- **CIDR**: Replaces classful addressing with flexible prefix lengths (e.g., /24, /27), supporting route summarization.
- **Borrowed Bits**: Takes host bits to create subnets, balancing subnet count and host addresses.
- **Supernetting**: Combines smaller networks into a larger one for efficient routing (opposite of subnetting).

**Step-by-Step Subnetting Example** (FLSM with 192.168.10.0/24, 4 subnets):
- **Goal**: Divide 192.168.10.0/24 into 4 equal subnets for departments (Sales, IT, HR, Admin).
- **Step 1: Determine Subnet Requirements**:
  - Need 4 subnets.
  - Each department requires ~50 hosts (including network/broadcast).
- **Step 2: Calculate Borrowed Bits**:
  - Subnets = 2^n, where n is borrowed bits. For 4 subnets, n = 2 (2^2 = 4).
  - New mask: /24 + 2 = /26 (255.255.255.192).
- **Step 3: Calculate Block Size**:
  - Block size = 2^(32-26) = 2^6 = 64 addresses per subnet.
  - Usable hosts = 64 - 2 = 62 per subnet.
- **Step 4: Allocate Subnets**:
  - Subnet 1 (Sales): 192.168.10.0–63
    - Network: 192.168.10.0
    - First Host: 192.168.10.1
    - Last Host: 192.168.10.62
    - Broadcast: 192.168.10.63
  - Subnet 2 (IT): 192.168.10.64–127
    - Network: 192.168.10.64
    - First Host: 192.168.10.65
    - Last Host: 192.168.10.126
    - Broadcast: 192.168.10.127
  - Subnet 3 (HR): 192.168.10.128–191
    - Network: 192.168.10.128
    - First Host: 192.168.10.129
    - Last Host: 192.168.10.190
    - Broadcast: 192.168.10.191
  - Subnet 4 (Admin): 192.168.10.192–255
    - Network: 192.168.10.192
    - First Host: 192.168.10.193
    - Last Host: 192.168.10.254
    - Broadcast: 192.168.10.255
- **Step 5: Verify CIDR Notation**:
  - Each subnet is 192.168.10.x/26, where x is 0, 64, 128, 192.

**Example Configuration** (Cisco Router for Subnet 1 and 2):
```bash
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.10.1 255.255.255.192
R1(config-if)# description Sales-LAN
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/1
R1(config-if)# ip address 192.168.10.65 255.255.255.192
R1(config-if)# description IT-LAN
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# ip dhcp pool SALES
R1(config-dhcp)# network 192.168.10.0 255.255.255.192
R1(config-dhcp)# default-router 192.168.10.1
R1(config-dhcp)# dns-server 8.8.8.8
R1(config-dhcp)# exit
R1(config)# ip dhcp pool IT
R1(config-dhcp)# network 192.168.10.64 255.255.255.192
R1(config-dhcp)# default-router 192.168.10.65
R1(config-dhcp)# dns-server 8.8.8.8
R1(config-dhcp)# exit
R1# copy running-config startup-config
```

**Client Configuration**:
- Sales PC: IP 192.168.10.10/26, Gateway 192.168.10.1.
- IT PC: IP 192.168.10.70/26, Gateway 192.168.10.65.

**Notes**:
- FLSM is used here for simplicity; VLSM would optimize further for varied host needs.
- CIDR notation (e.g., /26) simplifies mask representation.
- Borrowed bits (2) create 4 subnets, reducing hosts from 254 (/24) to 62 (/26).

Scenario: A small business subnets 192.168.10.0/24 into 4 /26 subnets for departments, using FLSM to ensure equal-sized networks with DHCP for client IPs.

---

## Advantages and Disadvantages

Subnetting offers significant benefits but introduces challenges that require careful planning and management.

**Advantages**:
- **Efficient IP Use**: Allocates addresses based on need, minimizing waste.
- **Improved Performance**: Reduces broadcast domains, lowering congestion.
- **Enhanced Security**: Isolates subnets for granular access control.
- **Simplified Management**: Divides networks into manageable segments.
- **Scalability**: Supports network growth via flexible designs (e.g., VLSM, CIDR).
- **Segmentation**: Dedicates subnets to specific services (e.g., VoIP, servers).

**Disadvantages**:
- **Increased Complexity**: Requires understanding of masks and calculations.
- **Administrative Overhead**: Managing multiple subnets increases workload.
- **Potential Congestion**: Poorly designed subnets may cause bottlenecks.
- **Troubleshooting Difficulty**: Complex networks complicate issue resolution.
- **Reduced Flexibility**: Reconfiguring subnets can disrupt operations.
- **Scalability Limits**: Initial designs may not accommodate future growth.

Scenario: A university subnets its network to separate student and faculty traffic, improving security but requiring more administrative effort to manage subnets.

---

## Implementation and Troubleshooting

Implementing subnetting involves configuring devices with correct IPs, masks, and gateways, often using DHCP for clients. Troubleshooting ensures connectivity and proper subnet allocation.

**Verification Commands** (Cisco):
- `show ip interface brief`: Checks interface IPs and masks.
- `show ip dhcp binding`: Lists DHCP-assigned IPs.
- `show ip route`: Verifies routing between subnets.
- `ping <destination>`: Tests connectivity.

Example output for `show ip interface brief` on R1:
```bash
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.1    YES manual up                    up
GigabitEthernet0/1     192.168.10.65   YES manual up                    up
```

**Troubleshooting Common Issues**:
- **Incorrect Mask**: Devices cannot communicate across subnets. Verify with `show ip interface brief` and correct mask (e.g., /26 vs. /24).
- **Duplicate IPs**: Conflicts within a subnet. Check with `arp -a` or `show arp` and reassign IPs.
- **DHCP Failure**: Clients get APIPA (169.254.x.x). Verify `show ip dhcp pool` and ensure pool matches subnet.
- **Routing Issues**: Subnets unreachable. Confirm `show ip route` and add routes if needed.
- **Broadcast Overlap**: Subnets misconfigured. Recalculate ranges to avoid overlap.

**Troubleshooting Scenario**: IT PCs (192.168.10.70/26) cannot reach Sales (192.168.10.10/26). `show ip interface brief` reveals g0/1 on R1 has /24 mask. Correcting to /26 (255.255.255.192) resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Incorrect Mask       | No inter-subnet communication | Correct mask (e.g., /26)             |
| Duplicate IPs        | Connectivity conflicts        | Reassign unique IPs                  |
| DHCP Failure         | APIPA addresses               | Verify DHCP pool and subnet match    |
| Routing Issues       | Subnets unreachable           | Add static routes or routing protocol|

**Example Verification**:
```bash
R1# ping 192.168.10.70
Sending 5, 100-byte ICMP Echos to 192.168.10.70, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5)
R1# show ip dhcp binding
IP address       Client-ID/Hardware address  Lease expiration
192.168.10.10    00:1A:2B:3C:4D:5E          Jun 23 2025 10:00 AM
192.168.10.70    00:1A:2B:3C:4D:5F          Jun 23 2025 10:00 AM
```

Scenario: An admin configures subnets for departments, verifies connectivity with pings, and fixes a DHCP misconfiguration to ensure all clients receive correct IPs.