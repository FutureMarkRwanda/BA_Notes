# Variable Length Subnet Masking (VLSM)

## Summary

This topic covers Variable Length Subnet Masking (VLSM), a technique for efficiently allocating IP addresses by using different subnet mask lengths within the same network to meet varying host requirements. It includes:

* **VLSM Concepts**: Understanding VLSM, its advantages over fixed-length subnet masking (FLSM), and its role in IP address conservation.
* **VLSM Design and Implementation**: Step-by-step process to design and configure VLSM for a network with four departments.
* **Verification and Troubleshooting**: Checking VLSM configurations and resolving common issues.

---

## VLSM Concepts

VLSM allows subnets within a network to use different subnet mask lengths, optimizing IP address allocation compared to classful addressing or FLSM, where all subnets use the same mask. VLSM, part of Classless Inter-Domain Routing (CIDR), enables tailored subnets for specific host counts, reducing IP waste and supporting hierarchical network design.

**Key Features**:
- **Flexible Mask Lengths**: Subnets use masks like /24, /26, or /30 based on host needs.
- **Address Efficiency**: Allocates only necessary addresses per subnet.
- **Routing Support**: Requires classless routing protocols (e.g., OSPF, EIGRP) or static routes.

**Comparison with FLSM**:
- FLSM uses a uniform mask (e.g., /24 for all subnets), wasting addresses in small subnets.
- VLSM assigns variable masks (e.g., /30 for links, /25 for large LANs), minimizing waste.

**Use Case**: A company with departments of varying sizes (e.g., 100, 50, 20 hosts, and a point-to-point link) uses VLSM to allocate appropriately sized subnets from one IP block, ensuring efficient use.

Scenario: A retail business uses VLSM on 172.16.0.0/16 to create subnets for four departments with different host requirements, optimizing address usage and simplifying routing.

---

## VLSM Design and Implementation

Designing a VLSM scheme involves calculating subnet sizes based on host requirements, sorting them from largest to smallest, and assigning subnets sequentially from a base IP block. Implementation includes configuring IP addresses, masks, and routing on network devices. Below is a detailed, step-by-step example for a network with four departments.

**Step-by-Step VLSM Design Example**:
- **Scenario**: A company has four departments requiring subnets from 172.16.0.0/16:
  - Department A (Sales): 100 hosts.
  - Department B (IT): 50 hosts.
  - Department C (HR): 20 hosts.
  - Department D (Point-to-Point Link): 2 hosts.
- **Goal**: Assign subnets with minimal address waste using VLSM.

**Step 1: Determine Host Requirements**:
- Include network and broadcast addresses in the count.
- Sales: 100 hosts + 2 = 102 addresses.
- IT: 50 hosts + 2 = 52 addresses.
- HR: 20 hosts + 2 = 22 addresses.
- Link: 2 hosts + 2 = 4 addresses.

**Step 2: Calculate Required Subnet Masks**:
- Use the formula: Addresses = 2^(32-N), where N is the mask length. Subtract 2 for usable hosts.
- Sales (102 addresses): Need 2^7 = 128 addresses (/25, 255.255.255.128, 126 usable hosts).
- IT (52 addresses): Need 2^6 = 64 addresses (/26, 255.255.255.192, 62 usable hosts).
- HR (22 addresses): Need 2^5 = 32 addresses (/27, 255.255.255.224, 30 usable hosts).
- Link (4 addresses): Need 2^2 = 4 addresses (/30, 255.255.255.252, 2 usable hosts).

**Step 3: Sort Subnets by Size**:
- Order: Sales (128), IT (64), HR (32), Link (4).

**Step 4: Allocate Subnets from 172.16.0.0/16**:
- Start with the largest subnet to simplify allocation.
- **Subnet A (Sales, /25)**:
  - Range: 172.16.0.0–172.16.0.127
  - Network: 172.16.0.0
  - Gateway: 172.16.0.1
  - Hosts: 172.16.0.2–172.16.0.126
  - Broadcast: 172.16.0.127
- **Subnet B (IT, /26)**:
  - Next available: 172.16.0.128
  - Range: 172.16.0.128–172.16.0.191
  - Network: 172.16.0.128
  - Gateway: 172.16.0.129
  - Hosts: 172.16.0.130–172.16.0.190
  - Broadcast: 172.16.0.191
- **Subnet C (HR, /27)**:
  - Next available: 172.16.0.192
  - Range: 172.16.0.192–172.16.0.223
  - Network: 172.16.0.192
  - Gateway: 172.16.0.193
  - Hosts: 172.16.0.194–172.16.0.222
  - Broadcast: 172.16.0.223
- **Subnet D (Link, /30)**:
  - Next available: 172.16.0.224
  - Range: 172.16.0.224–172.16.0.227
  - Network: 172.16.0.224
  - Gateway (R1): 172.16.0.225
  - Gateway (R2): 172.16.0.226
  - Broadcast: 172.16.0.227
- **Remaining Addresses**: 172.16.0.228–172.16.255.255 for future use.

**Step 5: Network Diagram**:
- R1 connects Sales (/25) and HR (/27) LANs, plus a link to R2 (/30).
- R2 connects IT (/26) LAN and the link to R1 (/30).

**Step 6: Configure Routers**:
```bash
! Router R1 (Sales, HR, and Link to R2)
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface g0/0
R1(config-if)# ip address 172.16.0.1 255.255.255.128
R1(config-if)# description Sales-LAN
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/1
R1(config-if)# ip address 172.16.0.193 255.255.255.224
R1(config-if)# description HR-LAN
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface s0/0/0
R1(config-if)# ip address 172.16.0.225 255.255.255.252
R1(config-if)# description Link-to-R2
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# ip route 172.16.0.128 255.255.255.192 172.16.0.226
R1# copy running-config startup-config

! Router R2 (IT and Link to R1)
R2> enable
R2# configure terminal
R2(config)# hostname R2
R2(config)# interface g0/0
R2(config-if)# ip address 172.16.0.129 255.255.255.192
R2(config-if)# description IT-LAN
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface s0/0/0
R2(config-if)# ip address 172.16.0.226 255.255.255.252
R2(config-if)# description Link-to-R1
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# ip route 172.16.0.0 255.255.255.128 172.16.0.225
R2(config)# ip route 172.16.0.192 255.255.255.224 172.16.0.225
R2# copy running-config startup-config
```

**Step 7: Configure DHCP for LANs** (Optional, for dynamic IP assignment):
```bash
! On R1 for Sales and HR
R1(config)# ip dhcp pool SALES
R1(config-dhcp)# network 172.16.0.0 255.255.255.128
R1(config-dhcp)# default-router 172.16.0.1
R1(config-dhcp)# dns-server 8.8.8.8
R1(config-dhcp)# exit
R1(config)# ip dhcp pool HR
R1(config-dhcp)# network 172.16.0.192 255.255.255.224
R1(config-dhcp)# default-router 172.16.0.193
R1(config-dhcp)# dns-server 8.8.8.8
R1(config-dhcp)# exit

! On R2 for IT
R2(config)# ip dhcp pool IT
R2(config-dhcp)# network 172.16.0.128 255.255.255.192
R2(config-dhcp)# default-router 172.16.0.129
R2(config-dhcp)# dns-server 8.8.8.8
R2(config-dhcp)# exit
```

**Client Configuration Example**:
- Sales PC: IP 172.16.0.10/25, Gateway 172.16.0.1, DNS 8.8.8.8.
- IT PC: IP 172.16.0.130/26, Gateway 172.16.0.129, DNS 8.8.8.8.
- HR PC: IP 172.16.0.194/27, Gateway 172.16.0.193, DNS 8.8.8.8.

**Notes**:
- Allocate largest subnets first to avoid fragmentation.
- Use /30 for point-to-point links (2 usable hosts).
- VLSM requires classless routing protocols (e.g., OSPF, EIGRP) or static routes for inter-subnet communication.
- Verify no overlaps in address ranges.

Scenario: A retail chain uses VLSM to assign subnets for Sales (100 PCs), IT (50 PCs), HR (20 PCs), and a router link, ensuring efficient use of 172.16.0.0/16 with minimal waste.

---

## Verification and Troubleshooting

Verifying VLSM confirms correct IP allocation and connectivity across subnets. Troubleshooting resolves issues like address overlaps, incorrect masks, or routing errors.

**Verification Commands** (Cisco):
- `show ip interface brief`: Displays interface IPs and masks.
- `show ip route`: Verifies routing table for VLSM subnets.
- `ping <destination>`: Tests connectivity between subnets.
- `show ip dhcp binding`: Lists DHCP-assigned IPs.
- `show running-config | include ip address`: Shows configured IPs.

Example output for `show ip route` on R1:
```
C    172.16.0.0/25 is directly connected, GigabitEthernet0/0
C    172.16.0.192/27 is directly connected, GigabitEthernet0/1
C    172.16.0.224/30 is directly connected, Serial0/0/0
S    172.16.0.128/26 [1/0] via 172.16.0.226
```

**Troubleshooting Common Issues**:
- **Address Overlap**: Subnets conflict (e.g., 172.16.0.0/25 overlaps with 172.16.0.128/25). Check ranges with `show running-config` and reassign non-overlapping subnets.
- **Incorrect Mask**: Devices cannot communicate (e.g., /24 instead of /26). Verify with `show ip interface brief` and correct mask.
- **Routing Failure**: Subnets unreachable. Confirm routes with `show ip route` and add missing static routes or enable classless routing protocols.
- **DHCP Misconfiguration**: Clients get incorrect IPs. Check `show ip dhcp pool` and ensure pool matches subnet mask.
- **Client Misconfiguration**: PCs cannot connect. Verify client IP/mask/gateway match VLSM design.

**Troubleshooting Scenario**: HR PCs (172.16.0.194/27) cannot reach Sales (172.16.0.10/25). `show ip route` on R2 lacks a route to 172.16.0.0/25. Adding `ip route 172.16.0.0 255.255.255.128 172.16.0.225` resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Address Overlap      | Connectivity conflicts        | Reassign non-overlapping subnets     |
| Incorrect Mask       | Cannot reach other subnets    | Correct mask (e.g., /25, /26)        |
| Routing Failure      | Subnets unreachable           | Add static routes or use classless protocol |
| DHCP Misconfiguration | Incorrect client IPs          | Match DHCP pool to subnet mask       |

**Verification Example**:
```bash
R1# ping 172.16.0.130
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 172.16.0.130, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5)
R1# show ip dhcp binding
IP address       Client-ID/Hardware address  Lease expiration
172.16.0.10      00:1A:2B:3C:4D:5E          Jun 23 2025 10:00 AM
172.16.0.194     00:1A:2B:3C:4D:5F          Jun 23 2025 10:00 AM
```

Scenario: An admin verifies VLSM by pinging across departments, fixing a routing issue to ensure Sales and HR can communicate, confirming efficient address allocation.