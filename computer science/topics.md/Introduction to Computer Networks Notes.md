# Unit 3: Introduction to Computer Networks

## 3.1 Fundamentals of Computer Networks
A computer network is a system of interconnected devices that communicate to share resources and data.

- **Definition**: A collection of computers and devices connected to exchange information.
- **Purpose**:
  - Share resources (e.g., files, printers).
  - Enable communication (e.g., email, messaging).
  - Provide centralized data storage and access.
- **Key Components**:
  - **Nodes**: Devices like computers, smartphones, or printers.
  - **Links**: Connections (wired or wireless) between nodes.
  - **Protocols**: Rules for data communication (e.g., TCP/IP).
- **Example**: A home Wi-Fi network connecting laptops, phones, and smart TVs.

## 3.2 Computer Network Concepts and Technology
Network concepts and technologies define how devices communicate and operate.

- **Concepts**:
  - **Client-Server Model**: Clients request services; servers provide them (e.g., web browser and web server).
  - **Peer-to-Peer (P2P)**: Devices act as both clients and servers (e.g., file-sharing networks).
  - **Bandwidth**: Data transfer rate (e.g., Mbps, Gbps).
  - **Latency**: Time taken for data to travel between nodes.
- **Technologies**:
  - **Ethernet**: Standard for wired LANs.
  - **Wi-Fi**: Wireless networking using IEEE 802.11 standards.
  - **TCP/IP**: Protocols for reliable data transfer and addressing.
- **Example**: Accessing a website uses TCP/IP over Wi-Fi or Ethernet.

## 3.3 Local Area Networks (LANs)
LANs connect devices within a limited geographic area, such as a home or office.

- **Characteristics**:
  - Small geographic scope (e.g., single building).
  - High-speed connections (e.g., 100 Mbps to 1 Gbps).
  - Privately owned and managed.
- **Components**:
  - Computers, switches, routers, and access points.
- **Example**: An office LAN connecting employee computers to a shared printer and server.
- **Advantages**:
  - Fast data transfer.
  - Easy resource sharing.
- **Disadvantages**:
  - Limited range.
  - Setup costs for hardware.

## 3.4 Physical Components
Physical components are the hardware used to build a network.

- **Cables**:
  - **Ethernet Cables**: Twisted pair (e.g., Cat5e, Cat6) for wired connections.
  - **Fiber Optic**: High-speed, long-distance data transmission.
- **Connectors**:
  - **RJ45**: Used for Ethernet cables.
  - **Fiber Connectors**: LC, SC for fiber optic cables.
- **Network Interface Cards (NICs)**:
  - Hardware enabling devices to connect to a network (wired or wireless).
- **Access Points**: Devices providing wireless connectivity (e.g., Wi-Fi routers).
- **Example**: A laptop with a wireless NIC connects to a Wi-Fi access point.

## 3.5 Network Devices
Network devices manage data flow and connectivity.

- **Hub**: Connects multiple devices, broadcasting data to all ports (inefficient).
- **Switch**: Connects devices, sending data only to the intended recipient.
  - Example: A switch connects computers in a LAN.
- **Router**: Directs data between networks (e.g., LAN to Internet).
  - Example: A home router connects a LAN to an ISP.
- **Access Point**: Extends Wi-Fi coverage.
- **Modem**: Converts digital signals to analog (and vice versa) for Internet access.
- **Example**: A router connects a home LAN to the Internet via a modem.

## 3.6 Network Transmission Medium
Transmission media carry data between devices.

- **Wired Media**:
  - **Twisted Pair**: Copper cables (e.g., Cat5e, Cat6) for Ethernet.
  - **Coaxial Cable**: Used in cable Internet.
  - **Fiber Optic**: Glass fibers for high-speed, long-distance transmission.
- **Wireless Media**:
  - **Radio Waves**: Used in Wi-Fi and Bluetooth.
  - **Microwaves**: Used in long-range wireless (e.g., cellular networks).
  - **Infrared**: Short-range communication (e.g., remote controls).
- **Comparison**:
  - Wired: Reliable, faster, but less flexible.
  - Wireless: Flexible, but susceptible to interference.
- **Example**: A LAN using Cat6 cables for wired connections and Wi-Fi for wireless devices.

## 3.7 IP Address
An IP address uniquely identifies a device on a network.

- **Definition**: A numerical label (e.g., 192.168.1.1) assigned to devices for communication.
- **Types**:
  - **IPv4**: 32-bit address (e.g., 192.168.0.1), limited to ~4.3 billion addresses.
  - **IPv6**: 128-bit address (e.g., 2001:0db8::1), supports more devices.
- **Assignment**:
  - **Static**: Fixed IP assigned manually.
  - **Dynamic**: Assigned by a DHCP server (e.g., router).
- **Example**: A laptop with IP 192.168.1.10 communicates with a server at 192.168.1.100.
- **Subnet Mask**: Defines network and host portions (e.g., 255.255.255.0).

## 3.8 Data and Device Sharing
Networks enable sharing of data and devices among users.

- **Data Sharing**:
  - File sharing via network drives or cloud services (e.g., Google Drive).
  - Real-time collaboration (e.g., shared documents).
- **Device Sharing**:
  - Printers: Multiple devices print to a single networked printer.
  - Servers: Centralized storage or application hosting.
- **Protocols**:
  - **SMB (Server Message Block)**: File and printer sharing.
  - **FTP (File Transfer Protocol)**: File transfers.
- **Example**: A LAN allows employees to access a shared folder on a server.

## 3.9 Network Topology
Topology describes the physical or logical arrangement of devices in a network.

- **Types**:
  - **Bus**: All devices share a single cable.
    - Pros: Simple, low cost.
    - Cons: Single point of failure.
  - **Star**: Devices connect to a central switch or hub.
    - Pros: Easy to manage, scalable.
    - Cons: Central device failure affects all.
  - **Ring**: Each device connects to the next, forming a loop.
    - Pros: Equal access to network.
    - Cons: Failure of one device disrupts the network.
  - **Mesh**: Devices are interconnected.
    - Pros: Highly reliable.
    - Cons: Expensive, complex.
- **Example**: A home network often uses a star topology with a router as the central device.