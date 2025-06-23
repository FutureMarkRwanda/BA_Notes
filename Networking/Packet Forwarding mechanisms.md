# Packet Forwarding Mechanisms

Routers use specific techniques to determine how to forward packets from one interface to another. Cisco routers support three main packet-forwarding mechanisms, each varying in speed and efficiency: Process Switching, Fast Switching, and Cisco Express Forwarding (CEF).

## Summary

This topic explores how routers handle packet forwarding through:

* **Process Switching (Process Forwarding)**: The oldest and least efficient method, where each packet is processed individually.
* **Fast Switching (Fast Forwarding)**: Improves performance by caching forwarding information after the first packet.
* **Cisco Express Forwarding (CEF)**: The most efficient and modern method, using pre-built tables that update based on network changes.

---

## Process Switching

Process switching is the most basic and CPU-intensive method. When a packet arrives at a router, it is handed off to the **control plane**, where the router’s **CPU** looks up the destination address in the **routing table** and determines how to forward the packet.

In this mechanism, **each packet**, even those going to the same destination, is processed separately by the CPU.

For example, if five packets arrive for the same destination, the CPU will process each one individually, repeating the same lookup and decision process five times.

This method is mostly used for specific cases like debugging or exception handling due to its high overhead.

[//]: # (![Visuals]&#40;https://interpolados.wordpress.com/wp-content/uploads/2017/04/12.png&#41;)
![Visuals](https://usercontent.one/wp/administration-utrustning.diginto.se/wp-content/uploads/2018/07/pic398-ccna2-process-switching.png)

---

## Fast Switching

Fast switching introduces the use of a **fast-switching cache** (also called a **route cache**) to reduce the workload on the CPU.

When a new packet arrives:

* The CPU first checks the fast-switching cache for a match.
* If a match is not found, the CPU performs the forwarding decision using process switching.
* The information is then **stored** in the cache for future packets.

This way, only the **first packet** in a flow is CPU-processed, while subsequent packets use the cache for faster handling.

For example, in a flow of five packets going to the same destination:

* The first packet is process-switched and its info stored in the cache.
* The remaining four packets are forwarded using the cached data, **bypassing the CPU**.


Fast switching improves performance significantly compared to process switching, but still relies on packet-triggered entries.

![Visuals](https://usercontent.one/wp/administration-utrustning.diginto.se/wp-content/uploads/2018/07/pic399-ccna2-process-switching.png)
---

## Cisco Express Forwarding (CEF)

Cisco Express Forwarding is the most advanced and preferred method for packet forwarding in Cisco routers. Unlike fast switching, CEF builds and maintains forwarding data **proactively**, not based on incoming packets.

It uses two main components:

* **FIB (Forwarding Information Base)**: Contains Layer 3 routing data derived from the IP routing table.
* **Adjacency Table**: Contains Layer 2 information (e.g., MAC addresses) needed to build complete outgoing frames.

CEF updates these tables **whenever the network topology changes**, ensuring they always contain the latest forwarding data.

Once the network has converged, forwarding decisions are **instant**, since the router doesn’t need to wait for packets to trigger lookups or cache-building.

This makes CEF:

* The **fastest** forwarding method.
* Ideal for high-performance and large-scale networks.

![Visuals](https://usercontent.one/wp/administration-utrustning.diginto.se/wp-content/uploads/2018/07/pic400-ccna2-cef-switching.png)
---

## Analogy Comparison

To help visualize the difference between these three mechanisms:

| Mechanism             | Analogy Description                                                               |
| --------------------- | --------------------------------------------------------------------------------- |
| **Process Switching** | Like solving a math problem by hand every time, even if the problem is identical. |
| **Fast Switching**    | Like solving a problem by hand once, then writing down the answer for reuse.      |
| **CEF**               | Like preparing a spreadsheet with all possible answers in advance.                |


Links\
https://administration-utrustning.diginto.se/router/routers-funktioner/