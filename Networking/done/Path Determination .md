# Path Determination

Routers are essential for directing packets across networks. One of their key functions is **path determination**—deciding the best route a packet should take to reach its destination. This process involves examining routing information, choosing the optimal path, and possibly balancing traffic across multiple paths.

## Summary

This topic includes:

* Routing decision sources and logic
* How routers select the **best path**
* Load balancing techniques
* The concept of **administrative distance** for resolving route conflicts

---

## 1. Routing Decisions

Routers make decisions by **matching the destination IP** in a packet with entries in their **routing table**. The source of this routing information can be:

* **Directly Connected Networks**: Interfaces with active IP addresses.
* **Static Routes**: Manually configured routes by the administrator.
* **Dynamic Routing**: Routes learned from routing protocols.
* **Default Routes**: Used when no specific route exists.

### Routing Outcomes

| **Scenario**           | **Router Action**                                                                                                      |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Directly connected** | Forward packet to destination host directly.                                                                           |
| **Remote network**     | Forward to another router toward destination.                                                                          |
| **No matching route**  | Check for **default route** (Gateway of Last Resort); otherwise, drop the packet and send an ICMP unreachable message. |

### Router Decision Flowchart

If a flowchart were visualized:

1. Is destination in directly connected network? → Yes → Send directly
2. Is destination reachable via known route? → Yes → Forward to next hop
3. Is default route configured? → Yes → Forward to default gateway
4. No matching route? → Drop packet and notify sender via ICMP

---

## 2. Best Path Selection

When **multiple routes exist to the same destination**, routers must select the **best one**. The **metric** is the value used to rank paths.

Each dynamic routing protocol has its own way of calculating metrics:

| **Routing Protocol** | **Metric Used**                                 |
| -------------------- | ----------------------------------------------- |
| RIP                  | Hop Count                                       |
| OSPF                 | Cost (based on bandwidth)                       |
| EIGRP                | Composite (Bandwidth, Delay, Reliability, Load) |

https://www.youtube.com/watch?v=ZMSYx7HRlXs&ab_channel=NetworkingwithRich

### EIGRP Metric Example

To compute an EIGRP metric:

$$
\text{Metric} = 256 \times \left( \frac{10^7}{\text{Minimum Bandwidth}} + \frac{\text{Sum of Delays}}{10} \right)
$$

This composite metric allows for more intelligent path selection compared to simpler protocols like RIP.

---

## 3. Load Balancing

When a router has **multiple equal-cost paths** to the same destination, it can perform **load balancing**, forwarding packets over all paths in rotation or proportionally.

### Types of Load Balancing

| **Type**                      | **Description**                                                         |
| ----------------------------- | ----------------------------------------------------------------------- |
| **Equal-cost**                | Uses multiple paths with the **same metric**.                           |
| **Unequal-cost** (EIGRP only) | Uses paths with **different metrics**, based on the `variance` setting. |

Cisco routers support up to **4 equal-cost paths** by default (configurable). Load balancing improves **redundancy** and **bandwidth utilization**.

---

## 4. Administrative Distance (AD)

When the same destination is reachable via **multiple sources** (e.g., static route and EIGRP), the router chooses the route with the **lowest AD**, which measures **trustworthiness**.

### AD Priority Table

| **Route Source**    | **AD Value** |
| ------------------- | ------------ |
| Connected           | 0            |
| Static              | 1            |
| EIGRP Summary       | 5            |
| External BGP        | 20           |
| Internal EIGRP      | 90           |
| IGRP                | 100          |
| OSPF                | 110          |
| IS-IS               | 115          |
| RIP                 | 120          |
| External EIGRP      | 170          |
| Internal BGP        | 200          |
| Unknown (Untrusted) | 255          |

### Example Scenario

If a router learns about network `192.168.5.0/24` from:

* A **static route** (AD 1), and
* An **OSPF update** (AD 110),

The router **installs the static route** into the routing table because it has a **lower AD**.

---

## Notes

* **Routing decisions** depend on destination IP lookup in the routing table.
* The **best path** is the one with the **lowest metric** based on the routing protocol.
* **Load balancing** spreads traffic across multiple valid paths to optimize bandwidth.
* **Administrative distance** resolves conflicts between different routing sources.

Understanding these concepts helps in designing resilient, efficient, and scalable networks.
