# Computer Network Architecture

## Definition
- Physical and logical design of software, hardware, protocols, and media for data transmission.
- Organizes computers and allocates tasks for efficient communication.

## Network Architecture Types
- Two main types: Peer-to-Peer (P2P) and Client/Server.

### Peer-to-Peer (P2P) Network
- **Description**: Computers share equal privileges and responsibilities.
- **Features**:
  - Ideal for small setups (up to 10 computers).
  - No dedicated server; resources shared via permissions.
  - Issue: Resource access fails if hosting computer is down.
- **Advantages**:
  - Low cost (no server needed).
  - Resilient (other devices work if one fails).
  - Easy setup and self-managed.
- **Disadvantages**:
  - No centralized backup; data scattered.
  - Security risks (self-managed devices).
  - Limited scalability.

### Client/Server Network
- **Description**: Clients access resources from a central server.
- **Features**:
  - Server handles security, files, and network management.
  - Clients communicate via server (e.g., Client1 needs server permission to reach Client2).
- **Advantages**:
  - Centralized backup simplifies data management.
  - Better performance with dedicated server.
  - Enhanced security via server control.
  - Faster resource sharing.
- **Disadvantages**:
  - Expensive (high-memory server, NOS costs).
  - Needs dedicated administrator.
  - Server failure disrupts network.

---
## Computer Network Types
- Categorized by size, users, services, and area.

### LAN (Local Area Network)
- **Description**: Connects devices in small areas (e.g., office).
- **Features**:
  - Uses affordable hardware (hubs, Ethernet cables).
  - Fast data transfer and high security.
- **Examples**: Office or school networks.

### PAN (Personal Area Network)
- **Description**: Connects personal devices within ~10 meters.
- **Features**:
  - Wired (USB) or wireless (WiFi, Bluetooth).
  - Covers laptops, phones, media players.
- **Examples**:
  - Body Area Network (mobile with person).
  - Home Network (offline home devices).
  - Small Home Office (VPN-connected devices).

### MAN (Metropolitan Area Network)
- **Description**: Links LANs across a city.
- **Features**:
  - Uses protocols like RS-232, ATM, ADSL.
  - Connects via telephone lines.
- **Uses**: Banks, airlines, colleges, military.

### WAN (Wide Area Network)
- **Description**: Spans large areas (states, countries).
- **Features**:
  - Uses telephone lines, fiber, or satellites.
  - Internet is the largest WAN.
- **Examples**:
  - Mobile Broadband (4G/5G).
  - Last Mile (telecom Internet).
  - Private Network (bank offices).
- **Advantages**:
  - Global connectivity.
  - Centralized data.
  - Fast updates and messaging.
  - High bandwidth with leased lines.
- **Disadvantages**:
  - Security risks (needs firewalls, antivirus).
  - High setup costs.
  - Hard to troubleshoot.

---

## Internetworking
- **Description**: Connects multiple networks using devices and addressing schemes.
- **Purpose**: Unifies public, private, or government networks.
- **Protocol**: Internet Protocol (IP).
- **Model**: OSI (Open System Interconnection).

### Extranet
- **Description**: TCP/IP-based network for restricted sharing.
- **Features**:
  - Requires login credentials.
  - Can be MAN, WAN, or others (not single LAN).
- **Example**: Secure partner data sharing.

### Intranet
- **Description**: Private TCP/IP network for an organization’s employees.
- **Features**:
  - Supports resource sharing, group work, teleconferencing.
- **Advantages**:
  - Cheap, easy communication.
  - Real-time, time-saving sharing.
  - Enhances collaboration.
  - Platform-independent.
  - Cost-effective (reduces physical copies).

## Internet
- **Description**: Global WAN of millions of networks.
- **Features**:
  - Uses TCP/IP for global communication.
- **Example**: Kigali and Nairobi networks linked via Internet.