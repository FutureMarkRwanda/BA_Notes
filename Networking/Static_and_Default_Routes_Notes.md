# Configuring Static and Default Routes

## Summary

This topic covers the configuration of static and default routes on Cisco routers, essential for directing network traffic in small or stable networks. It includes:

* **Initial Router Configuration**: Setting up basic router parameters like hostname, passwords, and interfaces.
* **Static and Default Route Configuration**: Configuring static routes for specific networks or hosts, default routes for unknown destinations, and floating static routes for backup paths.

---

## Initial Router Configuration

Configuring a router’s initial settings establishes its identity and connectivity. The **setup command facility** guides users through configuring a hostname, passwords, and interfaces for network management. This process creates an initial configuration file, which can be modified later using the Command Line Interface (CLI).

The setup process prompts for:
- **Hostname**: A unique name for the router.
- **Enable Secret Password**: An encrypted password for privileged EXEC mode.
- **Enable Password**: A less secure, unencrypted password for older systems.
- **Virtual Terminal Password**: Secures remote access (e.g., via Telnet).
- **Interface Settings**: Configures an interface (e.g., FastEthernet) with an IP address and subnet mask.

Example configuration using the setup facility:
```bash
--- System Configuration Dialog ---
Would you like to enter the initial configuration dialog? [yes/no]: yes
Would you like to enter basic management setup? [yes/no]: yes
Enter host name [Router]: Router
Enter enable secret: xxxxxx
Enter enable password: xxxxxx
Enter virtual terminal password: xxxxxx
Configure SNMP Network Management? [yes]: yes
Community string [public]: public
Enter interface name used to connect to the management network: FastEthernet0
Use the 100 Base-TX (RJ-45) connector? [yes]: yes
Operate in full-duplex mode? [no]: no
Configure IP on this interface? [yes]: yes
IP address for this interface: 172.1.2.3
Subnet mask for this interface [255.255.0.0]: 255.255.0.0
[0] Go to the IOS command prompt without saving this config.
[1] Return back to the setup without saving this config.
[2] Save this configuration to nvram and exit.
Enter your selection [2]: 2
```

Verification commands:
- `show interfaces`: Checks interface status (up/down).
- `show ip interface brief`: Displays IP configuration summary.
- `show configuration`: Verifies hostname and passwords.
- `show version`: Shows router details (e.g., IOS version, uptime).

A network admin configures a new router for a branch office, setting the hostname to "Branch1" and assigning 172.1.2.3/16 to FastEthernet0 for management.

---

## Static and Default Route Configuration

Static routes are manually configured paths for packets to reach specific networks or hosts, ideal for small, stable networks. A **default route** directs traffic to unknown destinations, acting as a gateway of last resort. Types include:
- **Static Network Route**: Targets a specific network.
- **Static Host Route**: Targets a single IP address (32-bit mask).
- **Default Route**: Uses 0.0.0.0/0 for unmatched destinations.
- **Floating Static Route**: A backup route with a higher administrative distance (AD), used if the primary route fails.

**Floating Static Route**: This is a static route configured with a higher AD (default AD for static routes is 1) to serve as a backup. If the primary route (with a lower AD, e.g., from a dynamic protocol or another static route) is removed from the routing table, the floating static route is installed. For example, a floating static route with AD 125 is less preferred than a primary route with AD 1.

![Static  Route](https://media.geeksforgeeks.org/wp-content/uploads/20220617220604/rou1.jpg)
Example: Configure static routes on two routers (R5 and R6) to connect networks 192.168.1.0/24 and 192.168.2.0/24 via 192.168.3.0/24:
```bash
! On R5
Router> enable
Router# configure terminal
Router(config)# hostname R5
R5(config)# interface fa0/1
R5(config-if)# ip address 192.168.1.3 255.255.255.0
R5(config-if)# no shutdown
R5(config-if)# exit
R5(config)# interface fa0/0
R5(config-if)# ip address 192.168.3.1 255.255.255.0
R5(config-if)# no shutdown
R5(config-if)# exit
R5(config)# ip route 192.168.2.0 255.255.255.0 fa0/0
R5(config)# exit
R5# copy running-config startup-config

! On R6
Router> enable
Router# configure terminal
Router(config)# hostname R6
R6(config)# interface fa0/0
R6(config-if)# ip address 192.168.3.2 255.255.255.0
R6(config-if)# no shutdown
R6(config-if)# exit
R6(config)# interface fa0/1
R6(config-if)# ip address 192.168.2.1 255.255.255.0
R6(config-if)# no shutdown
R6(config-if)# exit
R6(config)# ip route 192.168.1.0 255.255.255.0 192.168.3.1
R6(config)# exit
R6# copy running-config startup-config
```

Default route example on R3 and R4:
```bash
! On R3
R3(config)# interface s0/2/0
R3(config-if)# ip address 192.168.20.1 255.255.255.0
R3(config-if)# clock rate 1280000
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# interface g0/0
R3(config-if)# ip address 192.168.10.1 255.255.255.0
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# ip route 0.0.0.0 0.0.0.0 192.168.20.2
R3(config)# exit
R3# copy running-config startup-config

! On R4
R4(config)# interface s0/2/0
R4(config-if)# ip address 192.168.20.2 255.255.255.0
R4(config-if)# no shutdown
R4(config-if)# exit
R4(config)# interface g0/0
R4(config-if)# ip address 192.168.30.1 255.255.255.0
R4(config-if)# no shutdown
R4(config-if)# exit
R4(config)# ip route 0.0.0.0 0.0.0.0 192.168.20.1
R4(config)# exit
R4# copy running-config startup-config
```

Static host route example:
```bash
R1(config)# ip route 203.0.113.100 255.255.255.255 10.0.0.2
```

Floating static route example:
```bash
! On R1
R1(config)# ip route 203.0.113.0 255.255.255.0 10.0.0.2 125
R1(config)# ip route 203.0.113.0 255.255.255.0 10.0.0.6 1
```
In this example, the route via 10.0.0.6 (AD 1) is preferred. If it fails, the route via 10.0.0.2 (AD 125) is installed.

A company configures a floating static route on R1 to reach 203.0.113.0/24 via a backup link (10.0.0.2) with AD 125, ensuring connectivity if the primary link (10.0.0.6, AD 1) fails.