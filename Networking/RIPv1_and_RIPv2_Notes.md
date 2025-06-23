# Configuring RIPv1 and RIPv2 Routing Protocols

## Summary

This topic covers the configuration and operation of RIPv1 and RIPv2, two distance-vector routing protocols used for dynamic routing in small networks. It includes:

* **RIPv1 Operation and Configuration**: Understanding RIPv1’s classful nature and configuring it on Cisco routers.
* **RIPv2 Operation and Configuration**: Exploring RIPv2’s classless features and its configuration.
* **Verification and Troubleshooting**: Checking RIP functionality and resolving common issues.

---

## RIPv1 Operation and Configuration

RIPv1 (Routing Information Protocol version 1) is a distance-vector protocol that uses hop count as its metric, with a maximum of 15 hops (16 is unreachable). It is classful, meaning it does not include subnet masks in updates, limiting support for Variable Length Subnet Masks (VLSM) and Classless Inter-Domain Routing (CIDR). RIPv1 broadcasts updates every 30 seconds using UDP port 520, making it suitable for small, flat networks. It implements split horizon with poison reverse to prevent routing loops and supports triggered updates for faster convergence.

Key characteristics:
- Classful protocol, no VLSM/CIDR support.
- Metric: Hop count (max 15).
- Updates: Broadcast every 30 seconds, 25 routes per message.
- Administrative distance: 120.
- No authentication support.

Example configuration for a network with two routers (Router0 and Router1) connecting LAN 1 (192.168.1.0/24), LAN 2 (192.168.2.0/24), and a link (10.10.0.0/30):
```
! On Router0
Router> enable
Router# configure terminal
Router(config)# hostname Router0
Router0(config)# interface g0/1
Router0(config-if)# ip address 10.10.0.2 255.255.255.252
Router0(config-if)# no shutdown
Router0(config-if)# exit
Router0(config)# interface g0/0
Router0(config-if)# ip address 192.168.1.1 255.255.255.0
Router0(config-if)# no shutdown
Router0(config-if)# exit
Router0(config)# router rip
Router0(config-router)# network 192.168.1.0
Router0(config-router)# network 10.10.0.0
Router0(config-router)# exit
Router0# copy running-config startup-config

! On Router1
Router> enable
Router# configure terminal
Router(config)# hostname Router1
Router1(config)# interface g0/1
Router1(config-if)# ip address 10.10.0.1 255.255.255.252
Router1(config-if)# no shutdown
Router1(config-if)# exit
Router1(config)# interface g0/0
Router1(config-if)# ip address 192.168.2.1 255.255.255.0
Router1(config-if)# no shutdown
Router1(config-if)# exit
Router1(config)# router rip
Router1(config-router)# network 10.10.0.0
Router1(config-router)# network 192.168.2.0
Router1(config-router)# exit
Router1# copy running-config startup-config
```

Scenario: A small office uses RIPv1 to connect two LANs (192.168.1.0/24 and 192.168.2.0/24) via a point-to-point link (10.10.0.0/30), ensuring routers exchange routing information.

---

## RIPv2 Operation and Configuration

RIPv2 is an enhanced version of RIPv1, functioning as a distance-vector protocol with some link-state characteristics. It is classless, including subnet masks in updates, supporting VLSM and CIDR. RIPv2 uses multicast (224.0.0.9) instead of broadcasts, supports authentication, and retains the 15-hop limit and 30-second update interval.

Key characteristics:
- Classless protocol, supports VLSM/CIDR.
- Metric: Hop count (max 15).
- Updates: Multicast every 30 seconds, 25 routes per message.
- Administrative distance: 120.
- Supports authentication for secure updates.

Example configuration for a network with two routers (R1 and R2) connecting 10.0.0.0/24, 172.16.0.0/16, and 192.168.0.0/24:
```
! On R1
R1> enable
R1# configure terminal
R1(config)# router rip
R1(config-router)# version 2
R1(config-router)# no auto-summary
R1(config-router)# network 10.0.0.0
R1(config-router)# network 172.16.0.0
R1(config-router)# exit
R1# copy running-config startup-config

! On R2
R2> enable
R2# configure terminal
R2(config)# router rip
R2(config-router)# version 2
R2(config-router)# no auto-summary
R2(config-router)# network 192.168.0.0
R2(config-router)# network 172.16.0.0
R2(config-router)# exit
R2# copy running-config startup-config
```

Scenario: A campus network uses RIPv2 to support VLSM, allowing efficient IP allocation across subnets like 10.0.0.0/24 and 192.168.0.0/24, with multicast updates reducing network congestion.

---

## Verification and Troubleshooting

Verifying RIP configurations ensures routes are correctly advertised and learned. Troubleshooting addresses common issues like missing routes or misconfigurations.

**Verification Commands**:
- `show ip route`: Displays the routing table, showing RIP-learned routes (marked with “R”).
- `show ip protocols`: Shows RIP configuration details (e.g., version, networks, timers).
- `show ip rip database`: Displays RIP’s internal database of routes.

Example output for `show ip route` on Router0:
```
R 192.168.2.0/24 [120/1] via 10.10.0.1, 00:00:15, GigabitEthernet0/1
```

**Troubleshooting Common Issues**:
- **Wrong Network Command**: Incorrect or missing `network` statements prevent route advertisement. Ensure all interfaces’ networks are included.
- **Interface Shutdown**: A shut interface (e.g., `shutdown` command) stops route advertisements. Check with `show ip interface brief`.
- **Passive Interface**: A passive interface suppresses RIP updates. Verify with `show ip protocols`.
- **Version Mismatch**: RIPv1 and RIPv2 are incompatible. Ensure `version 2` is set for RIPv2.
- **Max Hop Count**: Routes exceeding 15 hops are marked unreachable (metric 16). Check hop counts with `show ip route`.
- **Route Filtering**: Filters may block updates. Verify with `show running-config`.
- **Auto-Summarization**: RIPv1 auto-summarizes to classful boundaries, causing issues with discontiguous subnets. Use `no auto-summary` in RIPv2.
- **Split Horizon**: Prevents advertising routes back to the interface they were learned from. Disable only if necessary (e.g., hub-and-spoke networks).

Example troubleshooting scenario: If Router0 does not see 192.168.2.0/24 in its routing table:
1. Run `show ip protocols` to confirm RIP is enabled and networks are correct.
2. Check `show ip interface brief` to ensure g0/1 is up.
3. Verify Router1’s configuration for version mismatch or passive interfaces.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Wrong Network        | Missing routes                | Correct `network` statements          |
| Interface Shutdown   | No updates sent               | Use `no shutdown` on interface        |
| Version Mismatch     | Incompatible updates          | Set `version 2` on both routers       |
| Auto-Summarization   | Discontiguous network issues  | Use `no auto-summary` in RIPv2        |

Scenario: A network admin notices Router0 lacks routes to 192.168.2.0/24. After verifying with `show ip protocols`, they find Router1 is using RIPv2 while Router0 uses RIPv1. Setting `version 2` on Router0 resolves the issue.