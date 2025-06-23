# Configuring Switch Security

## Summary

This topic covers essential security configurations for Cisco switches to protect against unauthorized access and common network attacks. It includes:

* **Switch Access Security**: Configuring console, VTY, Telnet, SSH, and management access.
* **Password and Port Security**: Enabling encryption, setting password policies, and securing unused ports.
* **Common Security Attacks and Countermeasures**: Addressing MAC, VLAN, ARP, DHCP, and other attacks.
* **Verification and Troubleshooting**: Checking configurations and resolving security issues.

---

## Switch Access Security

Securing switch access prevents unauthorized management and ensures only trusted devices can interact with the switch. Key methods include configuring console and virtual terminal (VTY) access, enabling Telnet or SSH, assigning a management IP, and setting a Message of the Day (MOTD) banner.

**Console Access**: Provides direct physical access for initial configuration or troubleshooting.
**VTY Access**: Enables remote management via Telnet or SSH.
**Telnet**: Insecure, uses clear-text passwords; restrict with access lists.
**SSH**: Secure, encrypted; preferred for remote access.
**Management IP**: Assigned to VLAN 1 by default for switch management.
**MOTD Banner**: Displays warnings to deter unauthorized access.

**Example Configuration**:
```
! On Switch
switch> enable
switch# configure terminal
switch(config)# hostname switch1
switch1(config)# line console 0
switch1(config-line)# password strongconsolepass
switch1(config-line)# login
switch1(config-line)# exit
switch1(config)# line vty 0 15
switch1(config-line)# password strongtelnetpass
switch1(config-line)# login
switch1(config-line)# transport input telnet
switch1(config-line)# access-class TELNET-ACCESS in
switch1(config-line)# exit
switch1(config)# ip access-list standard TELNET-ACCESS
switch1(config-std-nacl)# permit 10.1.1.100
switch1(config-std-nacl)# permit 10.1.1.101
switch1(config-std-nacl)# exit
switch1(config)# username rca privilege 15 secret rca123
switch1(config)# ip domain-name rca
switch1(config)# crypto key generate rsa general-keys modulus 1024
switch1(config)# line vty 0 15
switch1(config-line)# login local
switch1(config-line)# transport input ssh
switch1(config-line)# exit
switch1(config)# interface vlan 1
switch1(config-if)# ip address 10.1.1.200 255.255.255.0
switch1(config-if)# no shutdown
switch1(config-if)# exit
switch1(config)# banner motd $Only Authorized People Are Allowed$
switch1(config)# exit
switch1# copy running-config startup-config
```

Scenario: A corporate network configures a switch with SSH for secure remote management, restricts Telnet to specific IPs, and sets a management IP for monitoring.

---

## Password and Port Security

Strong password policies and port security protect the switch from unauthorized access and limit physical vulnerabilities. Password encryption, minimum length requirements, privileged EXEC mode passwords, disabling unused ports, and port security features enhance protection.

**Password Security**:
- **Enable Secret**: Protects privileged EXEC mode with a strong password.
- **Password Encryption**: Encrypts all passwords in the configuration.
- **Minimum Length**: Enforces stronger passwords.

**Port Security**:
- Limits MAC addresses allowed on a port to prevent MAC flooding attacks.
- Configurable actions: shutdown, restrict, or protect.

**Example Configuration**:
```
! Password Security
switch1# configure terminal
switch1(config)# enable secret somestrongpass
switch1(config)# security passwords min-length 9
switch1(config)# service password-encryption
switch1(config)# exit

! Disable Unused Ports (e.g., ports 25–48 on a 48-port switch)
switch1(config)# interface range fa0/25-48
switch1(config-if-range)# shutdown
switch1(config-if-range)# exit

! Port Security (e.g., on fa0/1 for a single device)
switch1(config)# interface fa0/1
switch1(config-if)# switchport mode access
switch1(config-if)# switchport port-security
switch1(config-if)# switchport port-security maximum 1
switch1(config-if)# switchport port-security violation shutdown
switch1(config-if)# switchport port-security mac-address sticky
switch1(config-if)# no shutdown
switch1(config-if)# exit
switch1# copy running-config startup-config
```

Scenario: A small office switch enforces a 9-character password policy, encrypts passwords, disables unused ports, and restricts fa0/1 to one device to prevent unauthorized connections.

---

## Common Security Attacks and Countermeasures

Switches are vulnerable to various attacks targeting Layer 2 operations. Understanding and mitigating these threats is critical for network security.

**Attacks and Countermeasures**:
- **MAC Address Attacks (MAC Flooding)**:
  - **Description**: Attackers flood the switch’s MAC address table, causing it to act like a hub, forwarding frames to all ports.
  - **Countermeasure**: Enable port security to limit MAC addresses per port.
- **VLAN Hopping**:
  - **Description**: Attackers send double-tagged frames or spoof trunk ports to access other VLANs.
  - **Countermeasure**: Disable Dynamic Trunking Protocol (DTP) with `switchport nonegotiate` and explicitly set `switchport mode access` or `trunk`.
- **ARP Attacks (ARP Spoofing)**:
  - **Description**: Attackers send fake ARP replies to redirect traffic through their device.
  - **Countermeasure**: Use Dynamic ARP Inspection (DAI) to validate ARP packets.
- **DHCP Attacks (DHCP Spoofing/Starvation)**:
  - **Description**: Attackers pose as DHCP servers or exhaust IP addresses.
  - **Countermeasure**: Enable DHCP Snooping to filter untrusted DHCP messages.
- **General Attacks (e.g., CDP/LLDP Spoofing)**:
  - **Description**: Attackers use discovery protocols to gather network information.
  - **Countermeasure**: Disable CDP/LLDP on untrusted ports with `no cdp enable`.
- **Port Security Violations**:
  - **Description**: Unauthorized devices connect to secure ports.
  - **Countermeasure**: Configure violation actions (shutdown, restrict, protect) and monitor logs.

**Example Countermeasure Configuration** (for VLAN hopping and DHCP snooping):
```
switch1# configure terminal
switch1(config)# interface fa0/1
switch1(config-if)# switchport mode access
switch1(config-if)# switchport nonegotiate
switch1(config-if)# exit
switch1(config)# ip dhcp snooping
switch1(config)# ip dhcp snooping vlan 1
switch1(config)# interface fa0/24
switch1(config-if)# ip dhcp snooping trust
switch1(config-if)# exit
switch1# copy running-config startup-config
```

Scenario: A university switch mitigates VLAN hopping by disabling DTP and enables DHCP snooping to block rogue DHCP servers, ensuring secure VLAN and IP assignments.

---

## Verification and Troubleshooting

Verifying switch security confirms access controls, port security, and countermeasures are functioning. Troubleshooting resolves issues like locked ports or access failures.

**Verification Commands**:
- `show running-config`: Displays current configuration (passwords, ACLs, etc.).
- `show interfaces`: Checks interface status and configurations.
- `show vlan brief`: Verifies VLAN assignments.
- `show interface status`: Shows port status, speed, and duplex.
- `show mac address-table`: Confirms learned MAC addresses.
- `show port-security`: Displays port security settings and violations.
- `show ip dhcp snooping`: Verifies DHCP snooping status.
- `show access-lists`: Checks Telnet access lists.

Example output for `show port-security` on switch1:
```
Secure Port  MaxSecureAddr  CurrentAddr  SecurityViolation  Security Action
              (Count)       (Count)      (Count)
------------------------------------------------------------------------
Fa0/1        1             1            0                  Shutdown
```

**Troubleshooting Common Issues**:
- **Console/VTY Access Failure**: Incorrect password or login settings. Verify with `show running-config | section line` and correct with `password` or `login`.
- **SSH Connection Refused**: Missing crypto keys or domain name. Check with `show ip ssh` and generate keys with `crypto key generate rsa`.
- **Port Security Violation**: Unauthorized device triggers shutdown. Verify with `show port-security` and clear with `interface fa0/1; no shutdown`.
- **Telnet Denied**: ACL misconfiguration. Check `show access-lists` and adjust `ip access-list standard TELNET-ACCESS`.
- **DHCP Snooping Drops**: Untrusted port blocks DHCP. Verify with `show ip dhcp snooping` and set trusted ports with `ip dhcp snooping trust`.
- **VLAN Hopping Detected**: DTP enabled. Confirm with `show interfaces switchport` and disable with `switchport nonegotiate`.

Example troubleshooting scenario: Users cannot access switch1 via SSH. `show ip ssh` shows no RSA keys. Generating keys with `crypto key generate rsa general-keys modulus 1024` resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Console/VTY Failure  | Cannot log in                 | Correct `password` or `login`         |
| SSH Refused          | Connection fails              | Set `ip domain-name` and generate keys|
| Port Security Violation | Port shut down             | Clear with `no shutdown`             |
| Telnet Denied        | Access blocked                | Adjust `ip access-list`               |

Scenario: An admin finds fa0/1 shut down due to a port security violation. `show port-security` confirms an unauthorized MAC. Clearing the port with `no shutdown` after removing the device restores connectivity.