# Routing Tables

## Summary

This topic explores routing tables, essential for directing network traffic in routers and network hosts. It covers:

* **Routing Table Fundamentals**: The structure and purpose of routing tables in packet forwarding.
* **Static and Dynamic Routing**: Methods to populate routing tables manually or automatically.

---

## Routing Table Fundamentals

A routing table, or Routing Information Base (RIB), is a data structure stored in a router or network host that maps network destinations to forwarding instructions. It guides packets by listing routes to directly connected or remote networks, sometimes including metrics like hop count for route selection.

Each entry includes:
- **Network ID**: The destination network or host address.
- **Subnet Mask**: Defines the network portion of the address for matching.
- **Next Hop**: The IP address of the next device to forward the packet to.
- **Outgoing Interface**: The router interface used to send the packet.
- **Metric**: A value (e.g., number of hops) indicating the route’s cost or preference.

A **default route** (0.0.0.0/0) directs packets with no specific match to a default gateway. When a packet arrives, the router matches its destination IP against the table to determine the forwarding path.

| Destination      | Subnet Mask       | Next Hop/Interface | Description                       |
|------------------|-------------------|--------------------|-----------------------------------|
| 128.75.43.0      | 255.255.255.0     | Eth0               | Directly connected network        |
| 128.75.43.0      | 255.255.255.128   | Eth1               | Subnetted network                |
| 192.12.17.5      | 255.255.255.255   | Eth3               | Host route (specific device)     |
| 0.0.0.0          | 0.0.0.0           | Eth2               | Default route to gateway         |

Scenario: A router receives a packet for 128.75.43.10. It matches the 128.75.43.0/24 entry and forwards the packet via Eth0.

---

## Static and Dynamic Routing

Routing tables are populated either manually (static routing) or automatically (dynamic routing).

**Static Routing**: An administrator manually enters routes, which remain fixed until changed. This is ideal for small, stable networks but requires manual updates if the network topology changes.

**Dynamic Routing**: Routers use protocols like OSPF, RIP, or BGP to exchange routing information and update tables automatically, adapting to network changes like failures or congestion. This suits larger, dynamic networks but uses more resources.

For example, a static route might direct traffic to a remote network, while a dynamic protocol learns routes from neighbors.

Example commands:
- On Windows, view the routing table:
```
route print
```
- On Linux:
```
route
```
- On a Cisco router, add a static route:
```
Router(config)# ip route 192.168.2.0 255.255.255.0 192.168.1.2
```
This directs traffic for 192.168.2.0/24 to the next hop 192.168.1.2.

| Method         | Configuration | Use Case                          |
|----------------|---------------|-----------------------------------|
| Static Routing | Manual entry  | Small, stable networks           |
| Dynamic Routing| Protocols     | Large, changing networks         |

Scenario: A small business uses a static route to connect to a partner network (192.168.2.0/24) via a router at 192.168.1.2. If the partner’s router IP changes, the route must be manually updated.