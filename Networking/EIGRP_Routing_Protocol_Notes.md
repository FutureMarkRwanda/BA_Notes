# Configuring the EIGRP Routing Protocol

## Summary

This topic covers the Enhanced Interior Gateway Routing Protocol (EIGRP), a Cisco-proprietary advanced distance-vector protocol with features of both distance-vector and link-state protocols. It includes:

* **EIGRP Operations**: Understanding EIGRP’s characteristics, metrics, and packet types.
* **EIGRP Configuration for IPv4**: Setting up EIGRP for IPv4 networks.
* **EIGRP Configuration for IPv6**: Configuring EIGRP for IPv6 networks.
* **Verification and Troubleshooting**: Checking EIGRP functionality and resolving issues.

---

## EIGRP Operations

EIGRP (Enhanced Interior Gateway Routing Protocol) is an advanced distance-vector protocol, often described as a hybrid due to its incorporation of link-state features. It is classless, supporting Variable Length Subnet Masks (VLSM) and discontiguous networks by including subnet masks in updates. EIGRP uses a composite metric based on bandwidth, delay, reliability, load, and MTU, but defaults to bandwidth and delay only. It employs the Diffusing Update Algorithm (DUAL) for loop-free paths and fast convergence, maintaining backup routes (feasible successors). EIGRP uses the Reliable Transport Protocol (RTP) for reliable delivery of packets and sends partial, triggered updates only to affected routers, unlike traditional distance-vector protocols.

EIGRP maintains three tables:
- **Neighbor Table**: Tracks adjacent routers, viewed with `show ip eigrp neighbors`.
- **Topology Table**: Stores all routes, including successors and feasible successors, viewed with `show ip eigrp topology`.
- **Routing Table**: Contains the best routes, viewed with `show ip route`.

EIGRP uses five packet types:
- **Hello**: Discovers and maintains neighbors (multicast, periodic).
- **Update**: Advertises routes (multicast or unicast, triggered).
- **Ack**: Acknowledges updates (unicast, UDP-based).
- **Query**: Seeks alternate paths when routes fail (multicast).
- **Reply**: Responds to queries with route information (unicast).

Key features:
- Supports IPv4, IPv6, and legacy protocols (e.g., AppleTalk, IPX/SPX).
- Unequal-cost load balancing for traffic distribution.
- Administrative distance: 90 (internal), 170 (external).
- Uses multicast (224.0.0.10) for efficient updates.

A company uses EIGRP to route between three office LANs, leveraging DUAL to ensure loop-free paths and fast failover to backup routes when a link fails.

---

## EIGRP Configuration for IPv4

Configuring EIGRP for IPv4 involves enabling the protocol with an Autonomous System (AS) number, advertising networks, and optionally setting interfaces as passive to suppress unnecessary updates. All routers in the same EIGRP domain must use the same AS number. The `passive-interface` command prevents EIGRP from sending Hellos on specified interfaces, blocking adjacency formation while still advertising the network.
![Example of network diagram](https://res.cloudinary.com/ddsojj7zo/image/upload/v1750948367/EIGRP_mqyugc.png)

Example configuration for three routers (R1, R2, R3) connecting LAN1 (192.168.0.0/24), LAN2 (192.168.1.0/24), LAN3 (192.168.7.0/24), LINK1 (10.10.10.0/30), and LINK2 (172.31.10.0/30):
```bash
! On R1
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.0.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/1
R1(config-if)# ip address 10.10.10.1 255.255.255.252
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# router eigrp 1
R1(config-router)# network 192.168.0.0 0.0.0.255
R1(config-router)# network 10.10.10.0 0.0.0.3
R1(config-router)# passive-interface g0/0
R1(config-router)# exit
R1# copy running-config startup-config

! On R2
R2> enable
R2# configure terminal
R2(config)# hostname R2
R2(config)# interface g0/1
R2(config-if)# ip address 10.10.10.2 255.255.255.252
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface g0/0
R2(config-if)# ip address 192.168.1.1 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface g0/2
R2(config-if)# ip address 172.31.10.2 255.255.255.252
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# router eigrp 1
R2(config-router)# network 10.10.10.0 0.0.0.3
R2(config-router)# network 172.31.10.0 0.0.0.3
R2(config-router)# network 192.168.1.0 0.0.0.255
R2(config-router)# passive-interface g0/0
R2(config-router)# exit
R2# copy running-config startup-config

! On R3
R3> enable
R3# configure terminal
R3(config)# hostname R3
R3(config)# interface g0/1
R3(config-if)# ip address 172.31.10.1 255.255.255.252
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# interface g0/0
R3(config-if)# ip address 192.168.7.1 255.255.255.0
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# router eigrp 1
R3(config-router)# network 172.31.10.0 0.0.0.3
R3(config-router)# network 192.168.7.0 0.0.0.255
R3(config-router)# passive-interface g0/0
R3(config-router)# exit
R3# copy running-config startup-config
```

A campus network configures EIGRP with AS 1 to connect three LANs, using passive interfaces on LAN-facing ports to reduce unnecessary Hello packets.

---

## EIGRP Configuration for IPv6

EIGRP for IPv6 (EIGRPv6) operates similarly to IPv4 but requires IPv6 unicast routing and interface-level EIGRP configuration. It uses the same AS number across routers and assigns a router ID manually (since IPv6 lacks a default 32-bit ID). Unlike IPv4, EIGRPv6 is enabled directly on interfaces rather than via network statements.

Example configuration for three routers (R1, R2, R3) with IPv6 networks 2001::/64, 2002::/64, 2003::/64, and 2004::/64:
```bash
! On R1
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# ipv6 unicast-routing
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/1
R1(config-if)# ipv6 address 2002::1/64
R1(config-if)# ipv6 enable
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# ipv6 router eigrp 10
R1(config-rtr)# eigrp router-id 1.1.1.1
R1(config-rtr)# no shutdown
R1(config-rtr)# exit
R1(config)# interface g0/0
R1(config-if)# ipv6 eigrp 10
R1(config-if)# exit
R1(config)# interface g0/1
R1(config-if)# ipv6 eigrp 10
R1(config-if)# exit
R1# copy running-config startup-config

! On R2
R2> enable
R2# configure terminal
R2(config)# hostname R2
R2(config)# ipv6 unicast-routing
R2(config)# interface g0/0
R2(config-if)# ipv6 address 2002::2/64
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface g0/1
R2(config-if)# ipv6 address 2003::1/64
R2(config-if)# ipv6 enable
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# ipv6 router eigrp 10
R2(config-rtr)# eigrp router-id 2.2.2.2
R2(config-rtr)# no shutdown
R2(config-rtr)# exit
R2(config)# interface g0/0
R2(config-if)# ipv6 eigrp 10
R2(config-if)# exit
R2(config)# interface g0/1
R2(config-if)# ipv6 eigrp 10
R2(config-if)# exit
R2# copy running-config startup-config

! On R3
R3> enable
R3# configure terminal
R3(config)# hostname R3
R3(config)# ipv6 unicast-routing
R3(config)# interface g0/0
R3(config-if)# ipv6 address 2003::2/64
R3(config-if)# ipv6 enable
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# interface g0/1
R3(config-if)# ipv6 address 2004::1/64
R3(config-if)# ipv6 enable
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# ipv6 router eigrp 10
R3(config-rtr)# eigrp router-id 3.3.3.3
R3(config-rtr)# no shutdown
R3(config-rtr)# exit
R3(config)# interface g0/0
R3(config-if)# ipv6 eigrp 10
R3(config-if)# exit
R3(config)# interface g0/1
R3(config-if)# ipv6 eigrp 10
R3(config-if)# exit
R3# copy running-config startup-config
```

A modern enterprise configures EIGRPv6 with AS 10 to support IPv6 routing across four subnets, ensuring efficient route updates and neighbor discovery.

---

## Verification and Troubleshooting

Verifying EIGRP ensures neighbors are formed, and routes are correctly advertised. Troubleshooting addresses common issues like misconfigurations or network errors.

**Verification Commands** (IPv4 and IPv6):
- `show ip route` or `show ipv6 route`: Displays EIGRP routes (marked “D”).
- `show ip eigrp neighbors` or `show ipv6 eigrp neighbors`: Lists neighbor adjacencies.
- `show ip eigrp interfaces` or `show ipv6 eigrp interfaces`: Shows EIGRP-enabled interfaces.
- `show ip protocols` or `show ipv6 protocols`: Displays EIGRP configuration details.
- `show ip eigrp topology`: Shows topology table with successors and feasible successors.

Example output for `show ip eigrp neighbors` on R1:
```bash
IP-EIGRP neighbors for process 1
H   Address         Interface       Hold Uptime   SRTT   RTO  Q  Seq
0   10.10.10.2      Gi0/1           14   00:05:23  40    240  0  10
```

**Troubleshooting Common Issues**:
- **Mismatched AS Numbers**: All routers must use the same AS. Verify with `show ip protocols` or `show ipv6 protocols` and correct with `router eigrp <AS>` or `ipv6 router eigrp <AS>`.
- **Incorrect Wildcard Masks**: Wrong masks in `network` statements prevent route advertisement. Check `show running-config` and correct masks (e.g., 0.0.0.255 for /24).
- **Interface Issues**: Shut or misconfigured interfaces block adjacencies. Use `show ip interface brief` to confirm interfaces are up and issue `no shutdown`.
- **Passive Interfaces**: Prevent Hellos, blocking adjacencies. Verify with `show ip protocols` and remove with `no passive-interface <interface>`.
- **IPv6 Configuration Errors**: Missing `ipv6 unicast-routing` or `ipv6 enable` on interfaces. Enable with `ipv6 unicast-routing` and `ipv6 enable`.
- **Router ID Conflicts**: Duplicate router IDs in EIGRPv6 cause issues. Verify with `show ipv6 eigrp neighbors` and set unique IDs with `eigrp router-id <ID>`.

Example troubleshooting scenario: R1 does not see routes to 192.168.7.0/24. `show ip protocols` reveals R3 uses AS 2 instead of AS 1. Reconfiguring R3 with `router eigrp 1` resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Mismatched AS        | No adjacencies formed         | Set same AS number                    |
| Incorrect Wildcard   | Missing routes                | Correct `network` wildcard mask       |
| Interface Shutdown   | No Hellos sent                | Use `no shutdown` on interface        |
| Missing IPv6 Routing | No IPv6 adjacencies           | Enable `ipv6 unicast-routing`         |

An admin finds no EIGRPv6 neighbors on R2. `show ipv6 protocols` shows `ipv6 unicast-routing` is disabled. Enabling it with `ipv6 unicast-routing` establishes adjacencies.