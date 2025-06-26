# Default Gateways

A **default gateway** is a critical component in network communication, enabling devices on one network to communicate with devices on another. It acts as an access point or IP router that a device uses to send data when the destination IP address is not within the same local network.

## Summary

In this topic, we explore:

* The concept and role of a default gateway.
* How it enables inter-network communication.
* How to identify a default gateway in different operating systems.
* The distinction between local and remote communication in a network.

---

## What is a Default Gateway?

A default gateway serves as a bridge between two or more different IP networks. When a computer needs to send data to another device that is **outside its own IP network**, it forwards that data to the default gateway. The gateway then routes the data to the correct destination network.

The default gateway is typically a **router** that has interfaces in multiple IP networks. It understands how to forward packets from one network to another, ensuring that communication is possible even between systems running different protocols or residing on separate subnets.

When two computers are on the **same IP network**, they can communicate directly without needing the default gateway. But for communication **across different IP networks**, a router (default gateway) is required.

![Default Gateway Image 1](https://i.sstatic.net/LzXCv.png)
![Default Gateway Image 2](https://learn.pivitglobal.com/hs-fs/hubfs/CCNA%20Images/Exploring%20Layer%203%20Redundancy%201_V3.jpg?width=1921&height=961&name=Exploring%20Layer%203%20Redundancy%201_V3.jpg)

---

## Identifying the Default Gateway

The default gateway's IP address is usually configured automatically (e.g., via DHCP) or manually by a network administrator. You can identify it through system commands:

* **On Windows**:
  Run the following command in Command Prompt:

  ```bash
  ipconfig
  ```

  Look for the line labeled `Default Gateway`.

* **On Linux**:
  Use the following command:

  ```bash
  ip route | grep default
  ```

* **On both Windows and Linux**:
  You can also use:

  ```bash
  netstat -r
  ```

  This displays the routing table, where the default gateway entry is usually listed under the "Gateway" column for the "0.0.0.0" destination.

---

## Communication Within and Between Networks

When a device (host) has an **IP address** and a **Subnet Mask**, it can directly communicate with other devices in the **same IP network** (i.e., same subnet). In such cases, the device uses **ARP (Address Resolution Protocol)** to find the MAC address of the destination device and sends the data directly without involving the default gateway.

However, if the destination is in a **different subnet**, the device recognizes that the IP is outside its local network. It then:

1. Forwards the packet to the default gateway.
2. The router (default gateway) receives the packet, examines its destination IP, and forwards it to the appropriate network.

![Network Arch image](https://i.sstatic.net/tXBIZ.png)
---

## Example: Two Devices in Different Networks

Consider:

* **Computer A** with IP: `192.168.0.0/24`
* **Computer B** with IP: `192.168.1.0/24`

![Network diagram](https://i.sstatic.net/tXBIZ.png)

These IPs are in different networks:

* `192.168.0.0/24` and `192.168.1.0/24`

Since they are on separate networks, **direct communication isn't possible**. Each computer must send traffic to a router configured as their **default gateway**, which has:

* One interface on `192.168.0.0/24` (e.g., `192.168.0.1`)
* Another on `192.168.1.0/24` (e.g., `192.168.1.1`)

When Computer A wants to send data to Computer B:

* It sends the packet to `192.168.0.1` (its default gateway).
* The router forwards it through its `192.168.1.1` interface to reach Computer B.

---

## Notes

* **Default gateways are only used when communication is across different IP networks.**
* **Local communication (same subnet)** is handled using MAC addresses and does not require a gateway.
* Routers distribute not just IP addresses and subnet masks but also the default gateway address to hosts (typically via DHCP).
* A default gateway ensures that devices can reach destinations **anywhere on the internet** or on external networks, by passing the traffic to the next hop.

