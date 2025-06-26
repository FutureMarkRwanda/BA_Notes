# Configuring Wireless Networks

## Summary

This topic covers the systematic implementation of wireless networks for SOHO and enterprise environments, focusing on WLAN standards, technologies, infrastructure, security, and testing. It also briefly introduces network operating systems (NOS) for server management. Key areas include:

* **WLAN Standards and Technologies**: Understanding IEEE 802.11 standards and wireless technologies like Wi-Fi, Bluetooth, and Zigbee.
* **Wireless Infrastructure and Deployment**: Configuring access points, routers, and mesh networks for small-scale deployments.
* **Wireless Security**: Mitigating attacks like eavesdropping, hijacking, and DoS.
* **Testing and Troubleshooting**: Ensuring connectivity, performance, and security.
* **Network Operating Systems**: Overview of NOS features and considerations for server management.

---

## WLAN Standards and Technologies

Wireless Local Area Networks (WLANs) use IEEE 802.11 standards to enable wireless communication between devices. These standards define frequency bands, data rates, and security protocols. Other wireless technologies complement WLANs for various applications.

**IEEE 802.11 Standards**:
- **802.11a**: 5 GHz, up to 54 Mbps, less interference but shorter range.
- **802.11b**: 2.4 GHz, up to 11 Mbps, longer range but prone to interference.
- **802.11g**: 2.4 GHz, up to 54 Mbps, backward compatible with 802.11b.
- **802.11n**: 2.4/5 GHz, up to 600 Mbps, uses MIMO for improved performance.
- **802.11ac**: 5 GHz, up to 7 Gbps, supports wider channels and MU-MIMO.
- **802.11ax (Wi-Fi 6)**: 2.4/5 GHz, up to 9.6 Gbps, enhanced efficiency and capacity.

**Other Wireless Technologies**:
- **Wi-Fi**: Connects devices to the internet or LANs (802.11-based).
- **Bluetooth**: Short-range (2.4 GHz, up to 24 Mbps) for device pairing (e.g., headphones).
- **Zigbee**: Low-power IoT communication (2.4 GHz, up to 250 kbps).
- **NFC**: Short-range (13.56 MHz, up to 424 kbps) for payments and pairing.
- **Cellular**: Long-range voice/data via mobile networks (e.g., 4G/5G).
- **Satellite**: Wide-area communication for remote locations.

**Benefits of Wireless**:
- Mobility, flexibility, cost-effectiveness, improved collaboration, efficiency, and user experience.

A coffee shop deploys 802.11ac Wi-Fi for customers, using 5 GHz to avoid 2.4 GHz interference from nearby Bluetooth devices, ensuring fast and reliable internet access.

---

## Wireless Infrastructure and Deployment

Wireless networks rely on infrastructure components like access points (APs), routers, and antennas. Small-scale deployments (SOHO/small businesses) use solutions like wireless routers, APs, range extenders, mesh networks, or mobile hotspots. Topology modes (ad hoc, infrastructure, mesh) determine how devices connect.

**Infrastructure Components**:
- **Wireless NICs**: Enable devices to connect to WLANs.
- **Wireless Routers**: Provide Wi-Fi and routing for SOHO networks.
- **Access Points (APs)**: Extend wired networks with wireless connectivity.
- **Antennas**: Enhance signal range and strength.

**Deployment Solutions**:
- **Wireless Routers**: All-in-one devices for small networks (e.g., home Wi-Fi).
- **APs**: Add Wi-Fi to existing wired networks (e.g., office expansions).
- **Range Extenders**: Boost signal in weak areas.
- **Mesh Networks**: Multiple APs for seamless coverage in larger spaces.
- **Mobile Hotspots**: Portable cellular-based Wi-Fi for remote work.

**Topology Modes**:
- **Ad Hoc**: Direct device-to-device connections (no AP).
- **Infrastructure**: Devices connect via an AP to a wired network.
- **Mesh**: Devices act as routers, creating resilient networks.

**Example Configuration** (SOHO Wireless Router with WPA3 Security):
```bash
! Access Cisco Wireless Router (e.g., via web interface at 192.168.1.1)
! Step 1: Basic Setup
- Login: Username: admin, Password: Admin@123
- Set Hostname: SOHO-Router
- LAN IP: 192.168.1.1, Subnet Mask: 255.255.255.0
- DHCP: Enabled, Range: 192.168.1.100–200

! Step 2: Wireless Settings
- SSID: SOHO-WiFi
- Frequency Band: 5 GHz (802.11ac)
- Channel: Auto (or select 36, 40, 44, or 48 for minimal interference)
- Wireless Mode: Infrastructure
- Security: WPA3-Personal
- Passphrase: SecurePass@2025

! Step 3: Save and Reboot
- Apply settings and reboot router

! Verification (CLI or Interface)
Router# show running-config | include wireless
Router# show ip interface brief
```

**Notes**:
- Use WPA3 for modern security; fallback to WPA2 if devices are incompatible.
- Select 5 GHz for speed or 2.4 GHz for range, depending on needs.
- Channels 1, 6, or 11 (2.4 GHz) or 36+ (5 GHz) minimize interference.

A small office configures a wireless router with WPA3 and 5 GHz for employee laptops, ensuring secure and fast connectivity across a 50-foot radius.

---

## Wireless Security

WLANs are vulnerable to attacks like eavesdropping, hijacking, and DoS. Implementing robust security measures protects data and network integrity.

**Common WLAN Attacks**:
- **Eavesdropping**: Intercepting unencrypted traffic.
- **Hijacking**: Taking over a session to gain unauthorized access.
- **Man-in-the-Middle (MitM)**: Impersonating an AP to steal data.
- **Denial of Service (DoS)**: Flooding the network to disrupt service.
- **Encryption Cracking**: Breaking weak encryption (e.g., WEP).
- **Authentication Cracking**: Guessing passwords or exploiting weak protocols.
- **MAC Spoofing**: Impersonating a legitimate device.
- **Peer-to-Peer Attacks**: Exploiting ad hoc connections.
- **Social Engineering**: Tricking users into revealing credentials.

**Security Measures**:
- Use **WPA3** or WPA2 with strong passphrases (e.g., 20+ characters).
- Disable SSID broadcasting to hide the network (requires active scanning).
- Enable MAC filtering to restrict device access (though bypassable).
- Use VLANs to segment guest and corporate traffic.
- Deploy intrusion detection systems (IDS) for monitoring.
- Disable WPS (Wi-Fi Protected Setup) to prevent brute-force attacks.

**Example Configuration** (AP with WPA3 and MAC Filtering):
```bash
! Cisco AP Configuration (via CLI or web interface)
AP> enable
AP# configure terminal
AP(config)# hostname AP1
AP(config)# dot11 ssid SOHO-WiFi
AP(config-ssid)# vlan 10
AP(config-ssid)# authentication open
AP(config-ssid)# authentication key-management wpa version 3
AP(config-ssid)# wpa-psk ascii SecurePass@2025
AP(config-ssid)# exit
AP(config)# interface dot11radio 0
AP(config-if)# encryption vlan 10 mode ciphers aes
AP(config-if)# ssid SOHO-WiFi
AP(config-if)# no shutdown
AP(config-if)# exit
AP(config)# mac-address-table static 00:1A:2B:3C:4D:5E vlan 10 interface dot11radio 0
AP# copy running-config startup-config
```

A corporate office deploys an AP with WPA3, hidden SSID, and MAC filtering to secure employee Wi-Fi, preventing unauthorized access and eavesdropping.

---

## Testing and Troubleshooting

Testing ensures WLAN performance, coverage, and security. Troubleshooting resolves connectivity issues between clients and APs.

**Testing Considerations**:
- **Signal Coverage**: Measure signal strength across the area (e.g., using tools like NetSpot).
- **Performance**: Test throughput and latency (e.g., iPerf).
- **In-Motion**: Verify connectivity while moving (e.g., roaming between APs).
- **Security**: Scan for vulnerabilities (e.g., Aircrack-ng for encryption testing).
- **Pilot Testing**: Deploy in a small area before full rollout.

**Troubleshooting Steps**:
- Verify if any clients can connect to the AP (`show dot11 associations`).
- Check for signal interference (e.g., 2.4 GHz overlap; use a spectrum analyzer).
- Confirm correct SSID and security settings on clients.
- Ensure TCP/IP is configured (e.g., DHCP or static IP).
- Perform a site survey to optimize AP placement.
- Check client status (`show station` on AP).

**Example Verification**:
```bash
AP# show dot11 associations
802.11 Client Stations on Dot11Radio0:
SSID [SOHO-WiFi] :
MAC Address    IP address      State
00:1A:2B:3C:4D:5E 192.168.1.100 Assoc
AP# show running-config | include ssid
AP# ping 192.168.1.100
```

**Troubleshooting Scenario**: Clients cannot connect to AP1. `show dot11 associations` shows no clients. Checking the client reveals a mismatched WPA3 passphrase. Correcting the passphrase on the client restores connectivity.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| No Client Connection | No devices associate with AP  | Verify SSID, passphrase, and security |
| Signal Interference  | Weak or unstable connection   | Change channel (e.g., 1, 6, 11)       |
| Incorrect IP Config  | No internet access            | Check DHCP or static IP settings      |
| Hidden SSID          | Network not visible           | Manually enter SSID on client         |

An admin finds weak Wi-Fi in a meeting room. A site survey reveals 2.4 GHz interference. Switching to 5 GHz channel 36 improves performance.

---

## Network Operating Systems (NOS) Overview

A **Network Operating System (NOS)** manages network resources and enables communication between devices on a LAN. It supports multiuser environments, resource sharing, and network services.

**Common Features**:
- User authentication and access control.
- File, printer, and database sharing.
- Directory services (e.g., Active Directory).
- Backup, web, and internetworking services.
- Protocol and hardware support.

**Popular NOS Examples**:
- **Windows Server**: Active Directory, DNS, file/print sharing.
- **Linux (e.g., Ubuntu Server, RHEL)**: Customizable, supports DNS, DHCP, NFS.
- **macOS Server**: File sharing, VPN, device management (limited scope).
- **FreeBSD**: Stable, secure, with robust networking.
- **Solaris**: Enterprise-grade, supports NFS, DNS, IPsec.

**Selection Considerations**:
- Compatibility with hardware/software.
- Security features and support availability.
- Licensing costs and admin expertise required.

A small business deploys Ubuntu Server as a NOS to manage file sharing and DHCP for its wireless network, leveraging its cost-effectiveness and flexibility.