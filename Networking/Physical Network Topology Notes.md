# Network Topology

## Overview
- **Definition**: The arrangement or layout of nodes (computers, devices) and connections in a network.
- **Purpose**: Determines how devices communicate and share resources efficiently.
- **Types**:
  - **Physical Topology**: Physical layout of cables and devices.
  - **Logical Topology**: How data flows within the network, regardless of physical connections.
- **Importance**: Affects network performance, scalability, reliability, and ease of maintenance.

## Physical Network Topologies

### Bus Topology
- **Description**: All devices connect to a single backbone cable.
- **Characteristics**:
  - Data broadcasts to all devices; only the intended recipient processes it.
  - Uses CSMA/CD (collision detection) or CSMA/CA (collision avoidance).
  - Common in Ethernet (802.3) networks.
  - ![Image](https://educatecomputer.com/wp-content/uploads/2024/03/Bus-topology-diagram.webp)
- **Advantages**:
  - Low-cost cabling; no hub needed.
  - Easy to implement and extend.
  - Failure of one node does not affect others.
- **Disadvantages**:
  - Extensive cabling; difficult to troubleshoot.
  - Signal interference from simultaneous transmissions.
  - Backbone failure disrupts entire network.
  - Limited cable length and number of devices.

### Ring Topology
- **Description**: Nodes form a closed loop, each connected to the next.
- ![Ring topology](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhpVEzGD5PM6qDeIgjAYpobf2hmRPbsdS26eeIngEFEPOAFfOKT-t8oH1Hvg0Xrw0i0PzBce-cbxxVVZF0P6AgmP-TvbqCWU0UL3kxxLjOO2HKom9UOu2XUPtDVKp74HJ9FnIetBgT65BaT/s533/Ring+Topology.png)
- **Characteristics**:
  - Unidirectional data flow (usually clockwise).
  - Uses token passing to control access.
  - No termination points; continuous loop.
- **Advantages**:
  - Easy to manage; faulty devices can be bypassed.
  - Reliable; not dependent on a single host.
  - Inexpensive twisted pair cabling.
- **Disadvantages**:
  - Single node failure can disrupt the network.
  - Adding devices increases delay.
  - Troubleshooting cable faults is complex.

### Star Topology
- **Description**: All nodes connect to a central hub or switch (server).
- ![Start Topology image](https://www.researchgate.net/publication/327897159/figure/fig1/AS:675274681221120@1538009438453/Some-Networks-Implement-a-Local-Ring-Topology-A-star-topology-is-a-LAN-architecture-in.jpg)
- **Characteristics**:
  - Uses coaxial or RJ-45 cables.
  - Popular in modern networks for efficiency.
- **Advantages**:
  - Efficient troubleshooting; issues isolated to nodes.
  - Easy to expand and manage.
  - High speeds (up to 100 Mbps).
  - Single node failure does not affect others.
- **Disadvantages**:
  - Central hub failure disrupts the network.
  - Complex cable routing increases costs.

### Tree Topology (Hierarchical Topology)
- **Description**: Combines bus and star topologies in a hierarchical structure with a root node.
- ![Tree Topology Image](https://www.researchgate.net/publication/261043184/figure/fig1/AS:392423676104708@1470572503177/Binary-Tree-Network-Topology.png)
- **Characteristics**:
  - Root node connects star-configured subnetworks.
  - Single path between any two nodes.
- **Advantages**:
  - Supports broadband transmission.
  - Easily expandable and manageable.
  - Error detection is simple.
  - Segment failure does not affect the entire network.
- **Disadvantages**:
  - Expensive broadband devices.
  - Main bus cable failure disrupts the network.
  - Complex troubleshooting and reconfiguration.

### Mesh Topology
- **Description**: Nodes interconnect with multiple paths, no central hub.
- ![Mesh Topology Image](https://miro.medium.com/v2/resize:fit:1400/0*dMmsACWrglsYZz_-)
- **Characteristics**:
  - **Fully Connected**: Every node connects to all others.
  - **Partially Connected**: Some nodes have multiple connections.
  - Cable formula (full mesh): `(n*(n-1))/2`, where `n` is number of nodes.
  - Uses routing algorithms for shortest paths.
- **Advantages**:
  - Highly reliable; link failure does not disrupt communication.
  - Fast communication via direct connections.
  - Secure and robust with redundancy.
- **Disadvantages**:
  - High cost due to extensive cabling.
  - Complex to manage and maintain.
  - Redundant connections reduce efficiency.

### Hybrid Topology
- **Description**: Combines different topologies (e.g., star + bus).
- ![Hybrid Topology Image](https://theinstrumentguru.com/wp-content/uploads/2022/04/Capture6.jpg)
- **Characteristics**:
  - Formed only by combining different topologies.
  - Customizable to organizational needs.
- **Advantages**:
  - Reliable; partial failures do not affect the entire network.
  - Scalable and flexible.
  - Maximizes strengths, minimizes weaknesses.
- **Disadvantages**:
  - Complex design and architecture.
  - Expensive hubs and cabling.
  - High infrastructure costs.