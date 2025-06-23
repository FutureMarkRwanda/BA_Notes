# Logical Network Topology

## Overview
- **Definition**: The virtual representation of how data flows or signals travel between nodes in a network, regardless of physical connections.
- **Purpose**: Defines the path data takes from one device to another, focusing on frame transfer logic.
- **Contrast with Physical Topology**: Physical topology describes the actual wiring layout, while logical topology outlines data transmission patterns.
- **Key Aspect**: Represents how devices communicate using protocols and access methods, not physical cables or hardware placement.

## Common Logical Topologies
- Three primary logical topologies: Ethernet, Token Ring, Fiber Distributed Data Interface (FDDI).

### Ethernet
- **Description**: A protocol-based technology for connecting devices in wired LANs or WANs using a common network language.
- **Characteristics**:
  - Devices format and transmit data using Ethernet standards (e.g., IEEE 802.3).
  - Uses physical media like Ethernet cables (CAT5/CAT6, fiber optic).
  - Employs CSMA/CD (Carrier Sense Multiple Access/Collision Detection) to manage data collisions.
  - Supports baseband signaling: Sends digital signals over a single frequency, using full bandwidth.
- **History**:
  - Developed in the 1970s from ALOHAnet by Xerox, Intel, and DEC.
  - Standardized as IEEE 802.3 in 1983.
  - Evolved with twisted pair and fiber optic support by the 1990s.
- **Types**:
  - **Fast Ethernet (100BASE-T, 802.3u)**:
    - Speed: Up to 100 Mbps.
    - Cables: Twisted pair (CAT5) or fiber optic.
    - Subtypes:
      - **100BASE-TX**: Uses two twisted pairs, supports 100 Mbps.
      - **100BASE-T4**: Uses four twisted pairs for lower-quality cables.
      - **100BASE-FX**: Uses two-strand fiber optic for 100 Mbps.
    - Note: “100” = 100 MHz frequency; “BASE” = baseband; “T” = twisted pair; “F” = fiber.
  - **Gigabit Ethernet (1000BASE-T, 802.3z/ab)**:
    - Speed: Up to 1 Gbps.
    - Cables: CAT5e or higher, fiber optic.
  - **10 Gigabit Ethernet (802.3ae)**:
    - Speed: Up to 10 Gbps.
    - Full-duplex, point-to-point links; no CSMA/CD or hubs.
  - **Switched Ethernet**: Uses switches to direct data, avoiding interruptions to other devices.
- **Advantages**:
  - Cost-effective and backward compatible.
  - Noise-resistant and reliable.
  - High-speed data transfer.
  - Secure with common firewalls.
- **Disadvantages**:
  - Limited to short-distance networks.
  - Reduced mobility due to wired connections.
  - Longer cables cause crosstalk.
  - Poor for real-time applications.
  - Speeds drop with high traffic.
  - No packet acknowledgment; hard to troubleshoot.

### Token Ring
- **Description**: A LAN protocol where devices in a logical ring pass a token to control data transmission.
- **Characteristics**:
  - Token: A 3-byte frame that grants transmission rights.
  - Unidirectional data flow; only token-holding stations transmit.
  - Token is released after successful data delivery and removed after use.
  - Based on IEEE 802.5 standard.
- **Token Passing Mechanism**:
  - Station with token transmits data, then passes token to the next station.
  - If no data to send, token is passed immediately.
  - Prevents infinite token circulation by removing used tokens.
- **Advantages**:
  - Reduced packet collisions due to token control.
  - High-speed data transfer.
  - Easy to maintain; no central server needed.
  - Scalable; adding nodes has minimal impact.
  - Robust for high traffic and long distances.
  - Cost-compatible with other topologies.
- **Disadvantages**:
  - Single node failure can collapse the network.
  - Data must pass through all nodes, slowing transmission.
  - Hardware (hubs, switches) increases costs.
  - Difficult to add nodes to an active network.
  - Slower than Ethernet under heavy loads.

### Fiber Distributed Data Interface (FDDI)
- **Description**: A high-speed LAN standard using fiber optic cables and a token ring protocol.
- **Characteristics**:
  - Dual token rings: Primary (data) and secondary (backup or additional data).
  - Speeds: 100 Mbps (primary) or 200 Mbps (both rings).
  - Range: Up to 200 km (single ring) or 100 km (dual ring).
  - Supports thousands of devices.
  - Uses timed token for predictable latency (synchronous) or flexible timing (asynchronous).
  - Operates at OSI physical and MAC layers.
- **How It Works**:
  - Implemented as dual token-passing rings in ring or star topology.
  - Primary ring carries data; secondary ring acts as backup or doubles capacity.
  - Fault tolerance: Secondary ring activates if primary fails, using beaconing to isolate faults.
  - Connection types:
    - **Single-Attached Stations (Class B)**: Connect to one ring, used for Ethernet LANs or servers.
    - **Dual-Attached Stations (Class A)**: Connect to both rings, used for backbones.
  - Media Interface Connector (MIC) links stations to rings.
- **Cable Types**:
  - **Multimode Fiber**: Up to 2 km, uses LED light source.
  - **Single-Mode Fiber**: Over 10 km, uses laser for higher bandwidth.
  - **Unshielded Twisted Pair (UTP)**: Up to 30 m, eight wires.
  - **Shielded Twisted Pair (STP)**: Up to 30 m, shielded pairs.
- **Traffic Types**:
  - **Synchronous**: Delay-sensitive (e.g., voice, video).
  - **Asynchronous**: Used when token arrives early, less time-critical.
- **Advantages**:
  - Long-distance transmission (up to 200 km).
  - High bandwidth (up to 250 Gbps).
  - Secure; fiber optic is hard to tap.
  - Durable; fiber resists breaking.
  - Fault-tolerant with dual rings.
- **Disadvantages**:
  - Complex to install and maintain.
  - Expensive due to costly fiber optic cables, connectors, and concentrators.