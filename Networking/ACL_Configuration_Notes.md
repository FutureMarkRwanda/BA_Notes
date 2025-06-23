# Configuring Access Control Lists (ACLs)

## Summary

This topic covers Access Control Lists (ACLs), which are used to filter network traffic on routers and switches based on defined criteria. It includes:

* **ACL Concepts and Types**: Understanding standard, extended, and named ACLs, their applications, and limitations.
* **ACL Configuration**: Implementing standard, extended, and named ACLs with examples for various scenarios.
* **Verification and Troubleshooting**: Checking ACL configurations and resolving common issues.
* **Best Practices**: Guidelines for effective ACL design and management.

---

## ACL Concepts and Types

ACLs are sets of rules that permit or deny traffic based on criteria like source/destination IP addresses, ports, protocols, or time. They enhance security, control access, and optimize network performance by filtering traffic at Layer 2 (MAC ACLs), Layer 3, or Layer 4 (IP ACLs). ACLs are typically applied on routers or firewalls, with inbound filtering being most common. Each ACL ends with an implicit "deny any" rule, blocking unmatched traffic.

**Types of IP ACLs**:
- **Standard ACLs**: Filter based on source IP address only (range: 1–99, 1300–1999). Applied closest to the destination.
- **Extended ACLs**: Filter based on source/destination IP, protocol, ports, etc. (range: 100–199, 2000–2699). Applied closest to the source.
- **Named ACLs**: Use descriptive names instead of numbers for standard or extended ACLs, improving manageability.

**Advantages**:
- Protects servers from external threats.
- Controls access to and between networks.
- Mitigates spoofing and denial-of-service attacks.
- Enhances network performance and manageability.

**Limitations** (platform-dependent):
- Maximum of 100 ACLs.
- 8–10 rules per ACL.
- Inbound traffic filtering only.
- No simultaneous MAC and IP ACLs on the same interface.
- Limited logging due to hardware constraints.

Scenario: A company uses ACLs to restrict access to a server, allowing only specific hosts to access HTTP services while denying unauthorized traffic, enhancing security.

---

## ACL Configuration

Configuring ACLs involves creating rules to match traffic and applying them to interfaces (inbound or outbound). Standard ACLs are simple but limited, while extended and named ACLs offer granular control. Below are configurations for various scenarios, including standard, extended, and named ACLs.

**Example Configurations**:

1. **Standard ACL**: Allow traffic from 192.168.10.0/24, deny all others.
```
R1> enable
R1# configure terminal
R1(config)# access-list 1 permit 192.168.10.0 0.0.0.255
R1(config)# interface fa0/0
R1(config-if)# ip access-group 1 in
R1(config-if)# exit
R1# copy running-config startup-config
```

2. **Standard ACL**: Deny PC 192.168.10.10, permit PC 192.168.10.5 to access server 192.168.20.50.
```
R1> enable
R1# configure terminal
R1(config)# access-list 10 deny host 192.168.10.10
R1(config)# access-list 10 permit host 192.168.10.5
R1(config)# interface g0/0
R1(config-if)# ip access-group 10 in
R1(config-if)# exit
R1# copy running-config startup-config
```

3. **Extended ACL**: Deny FTP traffic from 192.168.10.0/24 to server 192.168.20.50, permit HTTP traffic.
```
R1> enable
R1# configure terminal
R1(config)# access-list 100 deny tcp 192.168.10.0 0.0.0.255 host 192.168.20.50 eq ftp
R1(config)# access-list 100 deny tcp 192.168.10.0 0.0.0.255 host 192.168.20.50 eq ftp-data
R1(config)# access-list 100 permit tcp 192.168.10.0 0.0.0.255 host 192.168.20.50 eq www
R1(config)# interface fa0/0
R1(config-if)# ip access-group 100 in
R1(config-if)# exit
R1# copy running-config startup-config
```

4. **Extended ACL with Static Routing**: Permit 192.168.2.0/24 to access HTTP/HTTPS on 192.168.1.100 and all services on 192.168.4.0/24.
```
! Router R1 Interfaces and Static Route
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/1
R1(config-if)# ip address 192.168.4.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/2
R1(config-if)# ip address 192.168.3.1 255.255.255.252
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# ip route 192.168.2.0 255.255.255.0 192.168.3.2
R1(config)# exit

! Router R2 Interfaces, Static Routes, and ACL
R2> enable
R2# configure terminal
R2(config)# hostname R2
R2(config)# interface g0/0
R2(config-if)# ip address 192.168.3.2 255.255.255.252
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface g0/1
R2(config-if)# ip address 192.168.2.1 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# ip route 192.168.1.0 255.255.255.0 192.168.3.1
R2(config)# ip route 192.168.4.0 255.255.255.0 192.168.3.1
R2(config)# access-list 100 permit tcp 192.168.2.0 0.0.0.255 host 192.168.1.100 eq 80
R2(config)# access-list 100 permit tcp 192.168.2.0 0.0.0.255 host 192.168.1.100 eq 443
R2(config)# access-list 100 permit ip 192.168.2.0 0.0.0.255 192.168.4.0 0.0.0.255
R2(config)# interface g0/1
R2(config-if)# ip access-group 100 in
R2(config-if)# exit
R2# copy running-config startup-config
```

5. **Extended ACL with Established TCP**: Permit 192.168.3.0/24 to access HTTP/HTTPS/SMTP on 192.168.2.0/24, and 192.168.1.0/24 to access HTTP/HTTPS on 192.168.3.0/24.
```
! Router R1 Interfaces, Static Routes, and ACL
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/1
R1(config-if)# ip address 192.168.2.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/2
R1(config-if)# ip address 200.10.10.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# ip route 192.168.3.0 255.255.255.0 200.10.10.2
R1(config)# access-list 100 permit tcp any 192.168.2.0 0.0.0.255 eq 80
R1(config)# access-list 100 permit tcp any 192.168.2.0 0.0.0.255 eq 443
R1(config)# access-list 100 permit tcp any 192.168.2.0 0.0.0.255 eq 25
R1(config)# access-list 100 permit tcp any eq 80 192.168.1.0 0.0.0.255 established
R1(config)# access-list 100 permit tcp any eq 443 192.168.1.0 0.0.0.255 established
R1(config)# interface g0/2
R1(config-if)# ip access-group 100 in
R1(config-if)# exit
R1# copy running-config startup-config

! Router R2 Interfaces and Static Routes
R2> enable
R2# configure terminal
R2(config)# hostname R2
R2(config)# interface g0/0
R2(config-if)# ip address 200.10.10.2 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface g0/1
R2(config-if)# ip address 192.168.3.1 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# ip route 192.168.1.0 255.168.255.0 200.10.10.1
R2(config)# ip route 192.168.2.0 255.255.255.0 200.10.10.1
R2(config)# exit
R2# copy running-config startup-config
```

6. **Named Extended ACL**: Permit FTP traffic from 192.168.10.0/24, deny all other traffic.
```
R1> enable
R1# configure terminal
R1(config)# ip access-list extended FTP-FILTER
R1(config-ext-nacl)# permit tcp 192.168.10.0 0.0.0.255 any eq ftp
R1(config-ext-nacl)# permit tcp 192.168.10.0 0.0.0.255 any eq ftp-data
R1(config-ext-nacl)# deny ip any any
R1(config-ext-nacl)# exit
R1(config)# interface g0/0
R1(config-if)# ip access-group FTP-FILTER in
R1(config-if)# exit
R1# copy running-config startup-config
```

**Notes**:
- Standard ACLs are applied close to the destination, extended ACLs close to the source.
- More specific rules (e.g., `deny host`) must precede general rules (e.g., `permit any`).
- The `established` keyword allows return traffic for TCP sessions initiated internally.
- Named ACLs use descriptive names (e.g., FTP-FILTER) and support rule insertion/deletion.

Scenario: A university network uses an extended ACL to allow HTTP/HTTPS access to a server while denying FTP, and a named ACL to manage FTP traffic, ensuring precise access control.

---

## Verification and Troubleshooting

Verifying ACLs confirms rule application and traffic filtering. Troubleshooting resolves issues like incorrect filtering or connectivity failures.

**Verification Commands**:
- `show access-lists`: Displays ACL rules and hit counts.
- `show running-config | include access-list`: Shows ACL configurations.
- `show ip interface <interface>`: Verifies ACL application on interfaces.
- `show ip route`: Confirms routing for ACL-related networks.
- `ping <destination>`: Tests connectivity.
- `traceroute <destination>`: Identifies where traffic is blocked.

Example output for `show access-lists` on R2:
```
Extended IP access list 100
    10 permit tcp 192.168.2.0 0.0.0.255 host 192.168.1.100 eq www (match=50)
    20 permit tcp 192.168.2.0 0.0.0.255 host 192.168.1.100 eq 443 (match=10)
    30 permit ip 192.168.2.0 0.0.0.255 192.168.4.0 0.0.0.255 (match=100)
```

**Troubleshooting Common Issues**:
- **Implicit Deny Blocks All Traffic**: Unexpected traffic blocked. Verify with `show access-lists` and add explicit `permit` rules before the implicit deny.
- **All Network Denied**: Overly restrictive ACL. Check rule order with `show access-lists` and reorder with specific rules first.
- **Incorrect Protocol**: Wrong protocol/port (e.g., TFTP uses UDP, not TCP). Verify with `show access-lists` and correct protocol/port (e.g., `eq tftp`).
- **Wrong Interface/Direction**: ACL applied to incorrect interface or direction. Check with `show ip interface` and reapply with `ip access-group <name> in|out`.
- **Missing Routes**: Traffic not reaching destination. Verify with `show ip route` and add static/dynamic routes.
- **Rule Order Issue**: General rule matches before specific rule. Reorder with `no access-list <number>` and reconfigure, or use sequence numbers in named ACLs.

Example troubleshooting scenario: Hosts in 192.168.2.0/24 cannot access HTTP on 192.168.1.100. `show access-lists` shows `permit any` before `deny host 192.168.2.10`. Reordering rules with `no access-list 100` and reconfiguring places specific rules first, resolving the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Implicit Deny        | All traffic blocked           | Add explicit `permit` rules          |
| All Network Denied   | Overly restrictive ACL        | Reorder with specific rules first    |
| Incorrect Protocol   | Traffic not allowed           | Correct protocol/port (e.g., UDP for TFTP) |
| Wrong Interface      | ACL not filtering             | Reapply to correct interface/direction |

Scenario: An admin finds 192.168.3.0/24 cannot access SMTP on 192.168.2.0/24. `show access-lists` reveals `eq 25` is missing. Adding `permit tcp any 192.168.2.0 0.0.0.255 eq 25` fixes the issue.

---

## Best Practices

- **Placement**: Apply standard ACLs near the destination, extended ACLs near the source.
- **Rule Order**: Place specific rules before general ones to avoid premature matching.
- **Naming**: Use descriptive names for named ACLs (e.g., FTP-FILTER) in uppercase, avoiding spaces.
- **Logging**: Add `log` to key rules (e.g., `deny ip any any log`) to monitor hits, but use sparingly due to resource limits.
- **Maintenance**: Regularly review ACLs with `show access-lists` to remove obsolete rules.
- **Testing**: Test ACLs with `ping` or `traceroute` before deployment to verify behavior.
- **Documentation**: Comment ACLs with `remark` (e.g., `access-list 100 remark Allow HTTP`) for clarity.

Scenario: A network admin uses named ACLs with remarks and logging to filter traffic, regularly auditing with `show access-lists` to maintain security and performance.