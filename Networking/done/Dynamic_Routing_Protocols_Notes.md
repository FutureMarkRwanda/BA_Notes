# Dynamic Routing Protocols Configuration

## Summary

This topic explores dynamic routing protocols, which enable routers to automatically learn and update routes, adapting to network changes. It covers:

* **Routing Protocol Classification**: Categorizing protocols by purpose, operation, and behavior.
* **Configuring Key Protocols**: Setting up RIP, OSPF, EIGRP, and BGP on Cisco routers.

---

## Routing Protocol Classification

Dynamic routing protocols allow routers to share routing information, building and maintaining routing tables automatically. They are classified by:
- **Purpose**:
  - **Interior Gateway Protocols (IGP)**: Operate within a single autonomous system (AS), e.g., RIP, OSPF, EIGRP.
  - **Exterior Gateway Protocols (EGP)**: Operate between autonomous systems, e.g., BGP.
- **Operation**:
  - **Distance Vector**: Share entire routing tables based on hop count or metrics, e.g., RIP, EIGRP.
  - **Link-State**: Share link status to build a topology map, e.g., OSPF.
  - **Path-Vector**: Share paths with attributes, e.g., BGP.
- **Behavior**:
  - **Classful (Legacy)**: Ignore subnet masks (e.g., RIPv1, IGRP), used in older networks.
  - **Classless**: Support subnet masks and CIDR (e.g., RIPv2, OSPF, EIGRP, BGP).

The following table summarizes key routing protocols:

| Protocol | Distance-Vector | Link-State | Path-Vector | Purpose | Behavior |
|----------|-----------------|------------|-------------|---------|----------|
| RIP (v1) | Yes             | No         | No          | IGP     | Classful |
| RIP (v2) | Yes             | No         | No          | IGP     | Classless |
| OSPF     | No              | Yes        | No          | IGP     | Classless |
| EIGRP    | Yes             | No         | No          | IGP     | Classless |
| BGP      | No              | No         | Yes         | EGP     | Classless |
| IGRP     | Yes             | No         | No          | IGP     | Classful |

A company uses OSPF within its internal network (IGP) for efficient routing and BGP to connect to its ISP (EGP) for external routing.

---

## Configuring Key Protocols

Configuring dynamic routing protocols involves enabling the protocol on a router, specifying participating networks, and tuning parameters for optimization. Below are configurations for RIP, OSPF, EIGRP, and BGP on Cisco routers.

**RIP (Routing Information Protocol)**:
- Simple distance-vector protocol using hop count (max 15 hops).
- RIPv2 supports classless routing and authentication.

Configuration example for RIPv2:
```
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# no auto-summary
Router(config-router)# network 192.168.1.0
Router(config-router)# network 192.168.2.0
Router(config-router)# exit
Router# copy running-config startup-config
```
Verification:
```
Router# show ip route
Router# show ip protocols
```

**OSPF (Open Shortest Path First)**:
- Link-state protocol using Dijkstra’s algorithm for shortest path.
- Supports areas for scalability.

Configuration example for OSPF:
```
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
Router(config-router)# exit
Router# copy running-config startup-config
```
Verification:
```
Router# show ip ospf neighbor
Router# show ip route ospf
```

**EIGRP (Enhanced Interior Gateway Routing Protocol)**:
- Advanced distance-vector protocol using bandwidth and delay metrics.
- Cisco-proprietary, supports fast convergence.

Configuration example for EIGRP:
```
Router> enable
Router# configure terminal
Router(config)# router eigrp 100
Router(config-router)# network 192.168.1.0 0.0.0.255
Router(config-router)# network 192.168.2.0 0.0.0.255
Router(config-router)# no auto-summary
Router(config-router)# exit
Router# copy running-config startup-config
```
Verification:
```
Router# show ip eigrp neighbors
Router# show ip route eigrp
```

**BGP (Border Gateway Protocol)**:
- Path-vector protocol for inter-AS routing, using attributes like AS paths.
- Used for Internet routing.

Configuration example for BGP:
```
Router> enable
Router# configure terminal
Router(config)# router bgp 65001
Router(config-router)# neighbor 192.168.1.2 remote-as 65002
Router(config-router)# network 10.0.0.0 mask 255.255.255.0
Router(config-router)# exit
Router# copy running-config startup-config
```
Verification:
```
Router# show ip bgp
Router# show ip bgp neighbors
```

A network admin configures OSPF for internal routing across 192.168.1.0/24 and 192.168.2.0/24 networks in area 0, and BGP to advertise 10.0.0.0/24 to an ISP router in AS 65002.