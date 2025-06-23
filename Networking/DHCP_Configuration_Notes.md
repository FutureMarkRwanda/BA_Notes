# DHCP Configuration

## Summary

This topic covers configuring DHCP (Dynamic Host Configuration Protocol) on Cisco routers to dynamically assign IP addresses to devices, streamlining network management. It includes:

* **DHCP Basics**: Understanding DHCP’s role in IP address allocation.
* **Configuring DHCP on Cisco Routers**: Setting up DHCP pools for network subnets.

---

## DHCP Basics

DHCP automatically assigns IP addresses, subnet masks, default gateways, and other network parameters to devices, reducing manual configuration. A DHCP server maintains pools of IP addresses for specific networks, leasing them to clients (e.g., computers, phones) as they join the network.

Key components:
- **DHCP Pool**: A range of IP addresses for a network.
- **Excluded Addresses**: Reserved IPs (e.g., for servers or gateways) not assigned by DHCP.
- **Default Gateway**: The router’s IP address for client traffic to exit the network.

For example, a DHCP server can assign IPs to devices in a school’s network, ensuring each device gets a unique address within the correct subnet.

| Network         | Purpose                     | Example IP Range          |
|-----------------|-----------------------------|---------------------------|
| 192.168.1.0/24  | Staff devices               | 192.168.1.10–192.168.1.254 |
| 192.168.8.0/24  | Student devices             | 192.168.8.5–192.168.8.254  |

Scenario: A school uses DHCP to assign IPs to student laptops, reserving specific addresses for servers to avoid conflicts.

---

## Configuring DHCP on Cisco Routers

Cisco routers can act as DHCP servers, assigning IPs to devices in configured subnets. The process involves setting up router interfaces as gateways, excluding reserved IPs, and defining DHCP pools with network ranges and default gateways.

For two subnets (Student-block and Teacher-block), the configuration assigns IPs and ensures reserved addresses are excluded.

| Block           | Network Range          | Usable IPs                | Subnet Mask   | Default Gateway |
|-----------------|------------------------|---------------------------|---------------|-----------------|
| Student-block   | 192.168.8.0–192.168.8.255 | 192.168.8.5–192.168.8.254 | 255.255.255.0 | 192.168.8.1     |
| Teacher-block   | 192.168.1.0–192.168.1.255 | 192.168.1.10–192.168.1.254 | 255.255.255.0 | 192.168.1.1     |

Configuration commands:
```
Router> enable
Router# configure terminal
! Configure Student-block interface
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.8.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
! Configure Teacher-block interface
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
! Configure DHCP for Student-block
Router(config)# ip dhcp excluded-address 192.168.8.0 192.168.8.5
Router(config)# ip dhcp pool Student-block
Router(dhcp-config)# network 192.168.8.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.8.1
Router(dhcp-config)# exit
! Configure DHCP for Teacher-block
Router(config)# ip dhcp excluded-address 192.168.1.0 192.168.1.10
Router(config)# ip dhcp pool Teacher-block
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# exit
! Save configuration
Router# copy running-config startup-config
! Verify DHCP pools
Router# show ip dhcp pool Student-block
Router# show ip dhcp pool Teacher-block
```

Scenario: A school configures DHCP on a Cisco router for two subnets. The Student-block serves student devices, and the Teacher-block serves staff, with reserved IPs for servers and gateways excluded to prevent conflicts.