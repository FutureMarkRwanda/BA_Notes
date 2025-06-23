# Configuring OSPFv2 (Single Area) Routing Protocol

## Summary

This topic covers OSPFv2 (Open Shortest Path First version 2), a widely used link-state routing protocol for IPv4. It includes:

* **OSPFv2 Operations**: Understanding OSPF’s features, tables, areas, and metrics.
* **OSPFv2 Configuration**: Setting up OSPFv2 in a single area on Cisco routers.
* **Verification and Troubleshooting**: Checking OSPF functionality and resolving issues.
* **Dynamic Routing Protocol Selection**: Factors for choosing OSPF or other protocols.

---

## OSPFv2 Operations

OSPFv2 is a link-state routing protocol that uses Dijkstra’s algorithm to calculate the shortest path to each destination. It is an open standard, ensuring interoperability across vendors. OSPF is classless, supporting Variable Length Subnet Masks (VLSM) and equal-cost load balancing. It uses cost as its metric, calculated as `100 Mbps / interface bandwidth` by default (configurable). OSPF communicates via multicast addresses 224.0.0.5 (all OSPF routers) and 224.0.0.6 (DR/BDR), with an administrative distance of 110.

OSPF maintains three tables:
- **Neighbor Table**: Tracks OSPF adjacencies (`show ip ospf neighbor`).
- **Topology Table (Link-State Database, LSDB)**: Stores all possible routes (`show ip ospf database`).
- **Routing Table**: Contains best routes (`show ip route`).

OSPF areas group routers and networks to reduce routing table size and updates. All areas connect to the backbone area (Area 0). Routers with interfaces in multiple areas are Area Border Routers (ABRs), while those connecting to external networks are Autonomous System Border Routers (ASBRs).

Key features:
- Supports IPv4 and IPv6.
- Fast convergence via link-state updates.
- Reduces routing updates within areas.
- Uses router IDs (highest loopback IP, or highest physical IP, or manually set) to uniquely identify routers.

Scenario: A campus network uses OSPFv2 in Area 0 to connect three LANs, minimizing routing updates and ensuring fast convergence.

---

## OSPFv2 Configuration

Configuring OSPFv2 in a single area involves enabling OSPF with a process ID, setting a router ID, and advertising networks with their area IDs. The `network` command specifies interfaces to run OSPF and networks to advertise, using wildcard masks.

Example configuration for three routers (R1, R2, R3) connecting LAN1 (192.168.100.0/24), LAN2 (192.168.230.0/24), LAN3 (192.168.200.0/24), and serial links (10.10.10.0/30, 10.10.10.4/30, 10.10.10.8/30):
```
! On R1
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface g0/0/0
R1(config-if)# ip address 192.168.100.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface s0/2/1
R1(config-if)# ip address 10.10.10.1 255.255.255.252
R1(config-if)# clock rate 64000
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface s0/2/0
R1(config-if)# ip address 10.10.10.5 255.255.255.252
R1(config-if)# clock rate 64000
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface loopback 0
R1(config-if)# ip address 1.1.1.1 255.255.255.255
R1(config-if)# exit
R1(config)# router ospf 10
R1(config-router)# router-id 1.1.1.1
R1(config-router)# network 192.168.100.0 0.0.0.255 area 0
R1(config-router)# network 10.10.10.0 0.0.0.3 area 0
R1(config-router)# network 10.10.10.4 0.0.0.3 area 0
R1(config-router)# exit
R1# copy running-config startup-config

! On R2
R2> enable
R2# configure terminal
R2(config)# hostname R2
R2(config)# interface s0/2/1
R2(config-if)# ip address 10.10.10.10 255.255.255.252
R2(config-if)# clock rate 64000
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface s0/2/0
R2(config-if)# ip address 10.10.10.6 255.255.255.252
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface g0/0/0
R2(config-if)# ip address 192.168.230.1 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface loopback 0
R2(config-if)# ip address 2.2.2.2 255.255.255.255
R2(config-if)# exit
R2(config)# router ospf 10
R2(config-router)# router-id 2.2.2.2
R2(config-router)# network 192.168.230.0 0.0.0.255 area 0
R2(config-router)# network 10.10.10.4 0.0.0.3 area 0
R2(config-router)# network 10.10.10.8 0.0.0.3 area 0
R2(config-router)# exit
R2# copy running-config startup-config

! On R3
R3> enable
R3# configure terminal
R3(config)# hostname R3
R3(config)# interface s0/2/1
R3(config-if)# ip address 10.10.10.9 255.255.255.252
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# interface s0/2/0
R3(config-if)# ip address 10.10.10.2 255.255.255.252
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# interface g0/0/0
R3(config-if)# ip address 192.168.200.1 255.255.255.0
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# router ospf 10
R3(config-router)# router-id 3.3.3.3
R3(config-router)# network 192.168.200.0 0.0.0.255 area 0
R3(config-router)# network 10.10.10.0 0.0.0.3 area 0
R3(config-router)# network 10.10.10.8 0.0.0.3 area 0
R3(config-router)# exit
R3# copy running-config startup-config
```

Scenario: A small enterprise configures OSPFv2 in Area 0 to connect three LANs via serial links, using loopback interfaces for stable router IDs.

---

## Verification and Troubleshooting

Verifying OSPFv2 ensures neighbors form adjacencies and routes are correctly advertised. Troubleshooting addresses issues like misconfigurations or network errors.

**Verification Commands**:
- `show ip ospf neighbor`: Lists OSPF neighbors and their states (e.g., FULL).
- `show ip route ospf`: Displays OSPF routes (marked “O”).
- `show ip ospf database`: Shows the LSDB contents.
- `show ip ospf interface`: Details OSPF-enabled interfaces.
- `show ip ospf`: Provides OSPF process details.

Example output for `show ip ospf neighbor` on R1:
```
Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2         1     FULL/BDR        00:00:38    10.10.10.6      Serial0/2/0
3.3.3.3         1     FULL/DR         00:00:39    10.10.10.2      Serial0/2/1
```

**Troubleshooting Common Issues**:
- **Mismatched Area IDs**: All interfaces in a network segment must be in the same area. Verify with `show ip ospf interface` and correct with `network <IP> <wildcard> area 0`.
- **Incorrect Wildcard Masks**: Wrong masks in `network` statements prevent OSPF activation. Check `show running-config` and correct (e.g., 0.0.0.3 for /30).
- **Interface Issues**: Shut or misconfigured interfaces block adjacencies. Use `show ip interface brief` and issue `no shutdown`.
- **Router ID Conflicts**: Duplicate router IDs cause adjacency failures. Verify with `show ip ospf` and set unique IDs with `router-id <ID>`.
- **Network Type Mismatch**: Interfaces must agree on network type (e.g., point-to-point). Check with `show ip ospf interface` and align with `ip ospf network <type>`.
- **MTU Mismatch**: Differing MTUs prevent adjacency. Verify with `show interfaces` and align MTUs.

Example troubleshooting scenario: R1 does not form an adjacency with R2. `show ip ospf interface` shows R1’s s0/2/0 is in Area 1, not Area 0. Reconfiguring with `network 10.10.10.4 0.0.0.3 area 0` resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Mismatched Area IDs  | No adjacencies                | Correct area in `network` command     |
| Incorrect Wildcard   | OSPF not enabled on interface | Fix wildcard mask                     |
| Router ID Conflict   | Adjacency failure             | Set unique `router-id`                |
| Network Type Mismatch| Adjacency stuck in INIT       | Align with `ip ospf network <type>`   |

Scenario: An admin finds missing OSPF routes on R3. `show ip ospf` reveals a duplicate router ID with R2. Setting `router-id 3.3.3.3` on R3 fixes the adjacency.

---

## Dynamic Routing Protocol Selection

Choosing a dynamic routing protocol depends on network requirements and operational factors:
- **Scalability**: OSPF scales well for large networks due to its area-based design, unlike RIP.
- **Vendor Interoperability**: OSPF’s open standard ensures compatibility across vendors, unlike EIGRP (Cisco-proprietary).
- **Familiarity**: Teams experienced with OSPF may prefer it for ease of management.
- **Convergence Time**: OSPF converges faster than RIP or IGRP, critical for networks requiring minimal downtime.
- **Summarization**: OSPF supports route summarization (e.g., 10.0.0.0/24 to 10.0.3.0/24 into 10.0.0.0/22) to reduce routing table size, improving efficiency.

Example summarization:
```
R1(config)# router ospf 10
R1(config-router)# area 0 range 10.0.0.0 255.255.252.0
```

Scenario: A company chooses OSPF over EIGRP for its multi-vendor environment, leveraging summarization to optimize routing tables and fast convergence for reliability.