# Router Fundamentals

## Summary
A router is a Layer 3 (Network Layer) device that forwards packets between networks using IP addresses and routing tables. It serves as a gateway, connecting local networks to external networks like ISPs, and supports various interfaces (Ethernet, serial, DSL) for LAN and WAN connectivity. Routers feature hardware components such as CPU, RAM, ROM, and Flash, running an operating system like Cisco IOS to manage routing tasks efficiently.
![Router Image](https://www.cisco.com/content/dam/cisco-cdc/site/images/illustrations/products/branch-routers-933x400.png)
## Description
Routers direct data traffic by analyzing packet headers and selecting optimal paths based on routing tables. With at least two IP addresses, they act as default gateways for devices like PCs and servers. Positioned at network edges, routers facilitate connections to external networks via WAN interfaces and manage internal LAN traffic through Ethernet ports. Their internal architecture includes a CPU for processing, memory (RAM, NVRAM, ROM, Flash) for storing configurations and IOS, and a configuration register to control boot behavior, enabling robust network management.

## Router Description and Functions
Routers forward packets across networks using IP addresses and routing tables, operating at the OSI Network Layer (Layer 3). Unlike Layer 2 switches, they enable communication between different networks. As default gateways, their IP addresses are configured on end devices. Located at network perimeters, routers connect to ISPs via WAN interfaces (serial, DSL, SFP) and support features like load balancing, failover, and security policies to ensure reliable and efficient connectivity.

### **Table: Router Functions**:

  | Function | Description |
  |----------|-------------|
  | Packet Forwarding | Routes packets based on IP addresses and routing tables. |
  | Gateway Role | Acts as default gateway for LAN devices. |
  | WAN Connectivity | Connects to external networks via serial, DSL, or fiber. |
  | Traffic Management | Supports load balancing and failover for reliability. |

**Example**: A router in a small office routes packets from the local LAN (192.168.1.0/24) to an ISP’s network, using its routing table to determine the best path.

**Scenario**: A Cisco 891F router connects a business to two ISPs, using its primary WAN port for main internet access and a backup port for failover.

## Router Hardware Components
A router’s hardware is optimized for networking, resembling a computer’s architecture. The CPU processes routing decisions and interrupts. RAM stores the running IOS and configuration, while NVRAM retains the saved configuration. ROM holds boot code (Bootstrap, POST), and Flash (EEPROM) stores the IOS image. The Configuration Register (16-bit) determines boot sources (Flash, TFTP, RXBoot). Interfaces enable network connectivity, and the RXBoot Image in ROM supports maintenance tasks. The IOS is the primary operating system managing all router operations.

### **Table: Cisco Router Components**:

  | Component | Function |
  |-----------|----------|
  | CPU       | Processes routing tasks and interrupts. |
  | IOS       | Main operating system (2-5 MB or larger). |
  | RXBoot    | Minimal IOS in ROM for maintenance. |
  | RAM       | Stores running IOS and configuration. |
  | NVRAM     | Saves configuration. |
  | ROM       | Contains Bootstrap and POST code. |
  | Flash     | Stores IOS image (4 MB or larger). |
  | Config Register | Controls boot source (e.g., 0x2102). |

**Example Device**: Cisco 891F router.
![Cisco 891F Router Image](https://dedicatednetworksinc.com/wp-content/uploads/2020/12/C891F-K9-back.png)

**Scenario**: During startup, the Cisco 891F loads its IOS from Flash (8 MB) into RAM, retrieves the configuration from NVRAM, and checks the Configuration Register (0x2102) for normal boot.

## Router Interfaces (Cisco 891F Example)
The Cisco 891F router’s interfaces enable diverse connectivity. FE and GE WAN ports support Dual WAN for primary/backup ISP links, with failover (switches to backup on failure) or load balancing (distributes traffic) modes. ISDN S/T provides digital voice/data over PSTN. SFP ports support long-distance fiber/copper links and are hot-swappable. USB ports offer security and storage for VPN credentials. V.92 provides dial backup. LAN ports (4 GE, 4 PoE) connect devices, with PoE powering IP phones or cameras. Console/AUX ports enable local (serial) or remote (modem) management. Additional features include a power connector, on/off switch, reset button, earth ground for safety, and a Kensington security slot.

### **Table: Cisco 891F Interfaces**:

  | Interface | Description | Use Case |
  |-----------|-------------|----------|
  | FE WAN    | Fast Ethernet (100 Mbps) for backup/load balancing. | Secondary ISP link. |
  | GE WAN    | Gigabit Ethernet (1 Gbps) for primary WAN. | Primary ISP link. |
  | ISDN S/T  | Digital voice/data over PSTN. | Backup communication. |
  | SFP       | Fiber/copper for long-distance; hot-swappable. | Remote network links. |
  | USB       | Security, storage; VPN credentials. | Configuration storage. |
  | V.92      | Dial backup (56 kbps download, 48 kbps upload). | Fallback WAN link. |
  | LAN Ports | 4 GE + 4 PoE (15.4 W/port) for devices. | Connecting PCs, IP phones. |
  | Console/AUX | Serial (console) or modem (AUX) for management. | Setup, remote access. |

**Example Configuration**: A Cisco 891F uses its GE WAN port for a 1 Gbps primary ISP link and FE WAN port for a 100 Mbps backup, configured for failover to maintain internet access.

**Scenario**: An admin uses the console port with PuTTY for initial Cisco 891F setup, then configures the AUX port with a modem for remote management.
https://www.router-switch.com/pdf2html/pdf/c891f-k9-datasheet.pdf