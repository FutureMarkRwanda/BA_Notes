# Documenting Network Addressing

Effective network documentation is essential for designing, managing, and troubleshooting computer networks. Whether you're planning a new network or auditing an existing one, creating accurate and clear documentation ensures operational efficiency and easy maintenance.

## Summary

This topic covers:

* The key details to record when documenting a network.
* The two essential documents: a **Topology Diagram** and an **Addressing Table**.
* The purpose of each document and how to use them effectively.

---

## Importance of Network Documentation

Proper network documentation helps administrators:

* Understand the network structure.
* Track device configurations and IP allocations.
* Troubleshoot connectivity issues.
* Communicate designs and plans with teams and stakeholders.

At a minimum, your documentation should include:

* **Device Names**: Unique identifiers for routers, switches, PCs, etc.
* **Interfaces**: Specific ports or interfaces used (e.g., GigabitEthernet0/1).
* **IP Addresses and Subnet Masks**: Assigned IPv4 addresses and their corresponding subnet masks.
* **Default Gateway Addresses**: Routers’ IP addresses used for external communication.

---

## Topology Diagram

A **Topology Diagram** is a **visual representation** of the network's layout. It displays both the **physical connections** (how devices are wired together) and **logical addressing** (how IP addresses are assigned across the network).

Key features of a topology diagram:

* Shows routers, switches, and end devices.
* Includes interface labels (e.g., Fa0/0, G0/1).
* Indicates IP subnets or VLANs in use.
* Highlights routing paths and inter-network connections.

**Tools commonly used**:

* Microsoft Visio
* Cisco Packet Tracer (for simulation and design)
* draw\.io (free and web-based)
* Lucidchart (cloud-based diagramming)

A well-crafted topology diagram provides an at-a-glance understanding of how the network operates.

---

## Addressing Table

An **Addressing Table** records the IP-related configurations of network devices. It includes:

* Device name
* Interface name
* IPv4 address
* Subnet mask
* Default gateway

This table ensures that no IP address is reused, makes troubleshooting easier, and supports consistent IP planning.

### Sample Addressing Table:

| **Device** | **Interface** | **IPv4 Address** | **Subnet Mask** | **Default Gateway** |
| ---------- | ------------- | ---------------- | --------------- | ------------------- |
| PC-A       | NIC           | 192.168.1.10     | 255.255.255.0   | 192.168.1.1         |
| Router-1   | G0/0          | 192.168.1.1      | 255.255.255.0   | —                   |
| Router-1   | G0/1          | 192.168.2.1      | 255.255.255.0   | —                   |
| PC-B       | NIC           | 192.168.2.10     | 255.255.255.0   | 192.168.2.1         |
| Server-1   | NIC           | 192.168.1.100    | 255.255.255.0   | 192.168.1.1         |

> Note: NIC stands for Network Interface Card. Interfaces on routers/switches are often labeled as G0/0 (GigabitEthernet), Fa0/1 (FastEthernet), etc.

---

## Final Notes

* Both documents — the **topology diagram** and the **addressing table** — are essential in any professional network setup.
* Keeping these updated after changes (e.g., adding a new router or changing IP assignments) ensures accuracy and prevents misconfiguration.
* These documents also serve as helpful guides for onboarding new IT staff or troubleshooting complex issues.

