# Cisco Hierarchical Network Model

## Overview

- **Definition**: A structured approach dividing a network into layers, each with specific functions to optimize design, performance, and management.
- **Purpose**: Enables efficient hardware/software selection, simplifies data management, and ensures local traffic stays within its network segment unless destined elsewhere.
- **Structure**: Comprises three layers: Access, Distribution, and Core.
- **Network Types**:
  - **Tier-2 Network**: No core layer; distribution switches handle core functions.
  - **Tier-3 Network**: Includes a dedicated core layer for large-scale networks.

## Layers of the Hierarchical Model

### Access Layer

- **Role**: Provides user/workgroup access to the LAN, connecting end devices (e.g., PCs, IP phones).
- **Devices**:
  - **Ethernet Switches** (e.g., Cisco 2390XR): Decode packets, forward using MAC addresses, reducing collisions.
  - **Hubs** (Obsolete): Multiport repeaters; broadcast all packets, prone to collisions.
- **Functions**:

  | Function | Description |
  | --- | --- |
  | End Device Connectivity | Links devices like computers, printers to the LAN. |
  | Layer-2 Switching | Implements services like Spanning Tree, QoS, PoE, and VLANs. |
  | Security Enforcement | Applies port security, DHCP snooping, static MAC configurations to block unauthorized devices. |
  | Traffic Forwarding | Forwards traffic between end devices and the distribution layer. |
- **Characteristics**:
  - Access switches connect end devices, not other access switches.
  - Reduces collisions compared to hubs using MAC-based forwarding.

### Distribution Layer

- **Role**: Aggregates multiple access layer networks, connecting them to each other and the core layer.
- **Devices**: Routers and high-performance switches (e.g., Cisco C9300) using IP addresses for routing.
- **Functions**:

  | Function | Description |
  | --- | --- |
  | Access Layer Aggregation | Connects multiple access switches. |
  | Traffic Control | Filters traffic using ACLs; manages broadcasts via VLANs. |
  | Routing Services | Routes between VLANs and routing domains using IP addresses. |
  | Redundancy/Load Balancing | Provides backup paths and distributes traffic load. |
  | Core Layer Intermediation | Links access switches to core switches (if present). |
  | Demarcation Point | Separates LANs and broadcast domains. |
- **Characteristics**:
  - Uses routing tables to navigate traffic between networks.
  - Does not connect end devices directly.
  - Acts as a policy enforcement point.

### Core Layer

- **Role**: Serves as the network backbone, connecting distribution layer devices for high-speed traffic forwarding.
- **Devices**: High-performance switches (e.g., Cisco Catalyst 9600) with optical fiber for speeds ≥10 Gbps.
- **Functions**:

  | Function | Description |
  | --- | --- |
  | High-Speed Forwarding | Transfers traffic between distribution switches at near-wire speed. |
  | Redundancy | Maximizes redundant connections for reliability. |
  | Aggregation | Connects multiple distribution switches. |
- **Characteristics**:
  - Focuses solely on fast traffic forwarding; no additional services (e.g., filtering).
  - Uses high-bandwidth media (e.g., optical fiber).
  - Critical for large-scale Tier-3 networks.

## Key Design Principles

- **Access Switches**: Connect end devices to the LAN; forward traffic to distribution layer.
- **Distribution Switches**: Aggregate access switches; connect to core switches (if present).
- **Core Switches**: Aggregate distribution switches; provide high-speed backbone connectivity.

## Benefits of the Hierarchical Model

| Benefit | Description |
| --- | --- |
| **Design Simplicity** | Aligns with organizational structure; clear separation of units simplifies setup and adjustments. |
| **Better Performance** | Uses high-performance switches at distribution/core layers for near-wire speed data transfer. |
| **Cost-Effectiveness** | Modular design allows purchasing only necessary equipment; reduces overinvestment. |
| **Scalability** | Modular architecture supports easy expansion by replicating design elements (e.g., adding access switches). |
| **Security** | Access layer enforces port security; distribution layer applies complex ACLs for protocol-based filtering. |
| **Fault Isolation** | Small, modular components simplify identifying and resolving issues. |
| **Ease of Management** | Consistent functions per layer allow uniform configuration changes across switches. |
| **Modular Growth** | Changes affect only specific modules, minimizing network-wide impact. |
| **Redundancy** | Multiple paths at distribution/core layers ensure reliability; access layer has minimal redundancy. |
| **Maintainability** | Modular design and clear documentation simplify upgrades and troubleshooting. |
| **Better Policy Application** | Distribution layer supports advanced filtering (e.g., IP/HTTP restrictions) for precise control. |

## Scalability Example

- **Model**: Two distribution switches per ten access switches.
- **Expansion**: Add access switches until ten are connected to two distribution switches; then add more distribution switches and, if needed, core switches to handle increased load.

## Notes

- **Redundancy**: Access switches connect to two distribution switches; distribution switches link to multiple core switches for path availability.
- **Performance**: Aggregated switch-port links and high-performance switches minimize bandwidth contention.
- **Security**: Layer-3 processing at distribution layer enables advanced protocol-based policies, unlike most access switches.CISCO Hierarchical Network model 

  A network is divided into layers by a hierarchical structure, and each layer has a set of functions that specify how it fits into the overall network. This gives a network designer the ability to select the best hardware, software, and features to fulfill a specific purpose for that network layer. Additionally, data management is far more effective. Local traffic in a hierarchical design only goes to a higher tier when it is destined for another network.

  Dividing the network into multiple level/layers

  Each level perform specific functions within the network

  It helps the network designer and architect to optimize and select the right network hardware, software, and features to perform specific roles.

  There are three layers in hierarchical network design

  Access layer – provides workgroup or user access to the network.

  Distribution layer– provides policy-based connectivity.

  Core layer– provides fast transport between distribution switches

  Access Layer:

  The Access Layer is the part of the network which enables the users to connect to the wired Ethernet Network. It enables the users to share data and resources on the local network. The devices used in this layer include Ethernet Switches and Hubs.

  Hubs are basically multiport repeaters. They are devices that cannot decode the data packets received by them because they lack circuitry and logic to decode the data packets. Hubs cannot determine which host must receive the data packet. They simply repeat the electronic signals received on one interface to all other interfaces on the hub, thus all the hosts connected to the hub receive the data packet. Hubs have a fatal issue of collision. if two hosts transmit data packets at the same time, they would “collide” and be rendered useless. The hosts must retransmit the packets again.

  Another device used in the Access Layer is the Ethernet Switch. An Ethernet Switch is far more capable than hubs. They can decode the data packets and determine the interface to which the data packet must be forwarded. they use the MAC address, also known as the Physical Address, assigned to the host to forward the data packets. This reduces the issue of collision faced while using hubs. The development of Switches has rendered Hubs obsolete. Devices like Cisco 2390XR are used at this layer.

  The main functions of this layer are the following.

  Connecting various types of end devices to the LAN network.

  Providing layer-2 switching and implementing various layer-2 switching services such as spanning tree, virtual access control, QOS, POE, and ARP.

  Preventing unauthorized devices from connecting to the LAN by enforcing various security policies such as port security, DHCP snooping, and static mac address configuration.

  Switches connected in this layer are known as access switches. End-devices connect to the LAN network through the access switches. In other words, an access switch forwards traffic between connected devices and the rest of the LAN.

  Distribution Layer:

  When a network grows beyond a certain size, it must be divided into multiple local (Access Layer) networks. the distribution layer connects these networks together. It ensures that local traffic remains confined to local networks and governs traffic control between these networks.

  This layer uses Routers to connect multiple networks together. Routers and other devices on this layer are meant to connect multiple networks together, and not individual hosts. In order to navigate traffic between hosts on different networks, IP Address, also known as Logical Address, is used. The Router maintains a Routing Table to determine the interface on which to forward the received data packet.

  This layer also acts as an intermediary between the Access Layer and the Core Layer. Devices like the Cisco C9300 are used at this layer.

  The main functions of the distribution layer switches are the following.

  Providing connectivity between the access layer switches

  Aggregating LAN and WAN links and traffic

  If a separate core layer exists, providing upstream services for the access layer switches

  Controlling and filtering traffic by implementing ACLs

  Controlling broadcast through VLANs

  Providing redundancy and load balancing

  Providing routing services between different VLANs and routing domains

  Acting as a demarcation point between different LANs and broadcast domains

  If the network contains a separate core layer, the distribution layer connects the access layer to the core layer. The following image shows how the distribution switches work if the separate core layer exists.

  Core Layer:

  This layer is considered the backbone of a network, as it is used to connect multiple Distribution Layer devices together. This layer uses the most powerful devices to manage the traffic between the networks. The speed at which data flows in this layer is upwards of 10 Gigabit Ethernet. This layer has the maximum number of redundant connections (Redundancy is the process of introducing extra connections between the same network points to ensure reliable data transfer even if one of the connections is down) in order to ensure reliable connectivity.

  Devices like Cisco Catalyst 9600 are used at this layer with high-speed and high-bandwidth transmission media like optical fiber cable.

  The core layer is responsible for forwarding traffic between the distribution switches.

  Key points

  An access switch connects end-user devices to the LAN.

  An access switch forwards traffic between end-user devices and the rest of the LAN.

  An access switch does not connect two or more access switches.

  A distribution switch connects the access switches.

  A distribution switch does not connect end-user devices.

  A distribution switch provides an aggregation point for access switches.

  If the core switches exist, the distribution switches connect the access switches to the core switches.

  A core switch aggregates distribution switches.

  Except for forwarding traffic at the fastest possible speed, core switches do not provide any other services.

  If core switches are not used, the network is known as the Tire-2 network.

  If core switches are used, the network is known as the Tire-3 network.

  Design Simplicity: As equipment and connections typically match the logical structure of an organization, hierarchical networks are among the simplest to design and implement. Routers and switches delimit various organizational units starting from a single or numerous points of traffic egress and ingress until the final end-user is left with a single Ethernet adapter or 802.11 Wi-Fi network access point. Segments of the network are clearly separated by organizational boundaries, enabling simple initial setup and logical adjustments should organizational network requirements alter.

  Better Performance:  Data is routed through aggregated switch-port lines at the near-wire rate in a hierarchical network topology as opposed to being delivered through inferior intermediary switches. High-performance switches are used at the distribution and core layers, resulting in faster speeds and fewer network bandwidth problems. Therefore, during the majority of its journey within the network, data should flow at close to wire speed between every device if the network is configured properly.

  Improved cost-effectiveness: The necessary yet pricey IT networking equipment. However, because the business can only purchase the equipment that is actually required based on the logical structure of the enterprise, hierarchical network architecture might result in cost savings. Since the network is modular, it can be expanded without requiring substantial one-time expenses. One access switch and a few Ethernet connections, for instance, can frequently replace the need for a complete set of routers and switches when adding a new department (many of which will sit underused).

  Scalability: Hierarchical networks scale exceptionally well. The architecture’s modularity enables you to reproduce design pieces as the network grows. Because each module instance is constant, expansion is simple to design and implement. For example, if your design model includes two distribution layer switches for every ten access layer switch, you can keep adding access layer switches until you have ten access layer switches cross-connected to the two distribution layer switches before adding more distribution layer switches to the network topology. In addition, as more distribution layer switches are added to address the load from the access layer switches, additional core layer switches can be added to handle the increasing pressure on the core.

  Security: It is enhanced and more easily managed. Different port security settings that allow for control over which devices are permitted to connect to the network can be configured in access layer switches. Additionally, you have the choice to employ more complicated security procedures at the distribution layer. You can implement access control rules that specify the deployment of communication protocols on your network and the areas to which they are allowed to travel. For instance, you may implement a policy that limits HTTP traffic at the distribution layer if you want to restrict HTTP usage to a particular user community connected at the access layer. Your switches must be able to process policies at the upper layers in order to restrict traffic depending on protocols like IP and HTTP. Your switches must be able to handle policies at that layer in order to restrict traffic based on higher-layer protocols like IP and HTTP. Although certain access layer switches enable Layer 3 capability, Layer 3 data processing is often handled by distribution layer switches because of their superior processing capabilities.

  Strengthened fault isolation: Fault isolation is improved by breaking the network down into small, simple components. Network management can quickly comprehend the network’s transition points, which aids in locating potential trouble spots.

  Easier to Manage: A hierarchical network is generally easy to manage. The hierarchical design’s layers each carry out particular tasks that are consistent throughout that layer. Since all access layer switches in the network presumably fulfill the same functions at their layer, if the functionality of an access layer switch needs to be changed, you could duplicate that change across all access layer switches in the network. The ability to copy switch configurations between devices with minimal change facilitates the deployment of new switches. Each layer’s switches must be consistent with one another for quick recovery and straightforward debugging. Device configuration inconsistencies may occur in some unique circumstances, thus you should make sure that settings are clearly documented so that you can compare them before deployment.

  Modular Network Growth: Changes are facilitated by hierarchical architecture. When designing a network, modularity enables you to produce design features that you can duplicate as the network expands. The expense and complexity of upgrading the network are limited to a small portion of the entire network because every component of its architecture needs to be altered. Changes frequently affect a huge number of systems in big, flat network designs. Limited mesh topologies within a layer or component, like the campus core or backbone connecting central sites, retain utility even in hierarchical design models.

  Redundancy: The availability of a network becomes increasingly critical as it grows. Simple redundant implementations of hierarchical networks can greatly boost availability. To achieve path redundancy, access layer switches are linked to two distinct distribution layer switches. If one of the distribution layer switches fails, the access layer switch can switch to the other. Furthermore, distribution layer switches are linked to two or more core layer switches to assure path availability in the event that a core switch fails. The only layer with minimal redundancy is the access layer. End node devices, such as PCs, printers, and IP phones, do not often support multiple access layer switches for redundancy. If an access layer switch fails, just the devices linked to that single switch are affected. The rest of the network would continue to operate normally.

  Maintainability: Hierarchical networks are simple to manage since they are modular in design and scale up quickly. Other network topology choices make manageability more challenging as the network gets bigger. Additionally, there may be a finite size limit to the network’s expansion before it becomes too difficult and expensive to maintain, according to some network design models. The definition of switch functions at each tier in the hierarchical design model facilitates choosing the right switch. Another limitation may still exist at another layer even after adding switches to one layer. All switches must be high-performance switches in order for a full mesh network topology to operate at its peak efficiency since each switch must be able to handle every task on the network. Switch functions vary at each stage in the hierarchical architecture. Instead of spending more money on the distribution and core layer switches to achieve perfect network performance, you can save money by using less expensive access layer switches at the lowest layer.

  performance: by reducing the transmission of data through intermediary switches with poor performance, communication performance is improved. from the access layer to the distribution layer, data is often transmitted at close to wire speed over aggregated switch port links. after that, the traffic is forwarded up to the core and routed there using the distribution layer’s high-performance switching capabilities. there is less competition for network capacity exists because the core and distribution layers operate at extremely fast rates. hierarchical networks that are well-designed can therefore reach near-wire speed between all devices.

  Better filter/policy creation and application: cisco three layer network model allows better filter/policy creation application.