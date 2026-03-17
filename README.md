# 🏦 TIMB Bank Enterprise Network Project

![Network](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer-blue)
![Status](https://img.shields.io/badge/Status-Complete-green)
![Level](https://img.shields.io/badge/Level-CCNA%2FCCNP-red)

## 📋 Overview
TIMB Bank (Trusted. Innovative. Modern. Banking.) is a 
complete enterprise bank network simulation designed and 
implemented using Cisco Packet Tracer.

The network serves 1 Headquarters and 3 Branch offices 
with full redundancy, security, and enterprise services.

---

## 🗺️ Network Topology
```
INTERNET (8.8.8.x)
      |
 ISP Router (203.0.113.1)
      |
 ASA Firewall (outside/inside/dmz)
      |              |
 DMZ Servers    HQ Router
 Web/Email/     192.168.1.2
 Banking             |
                HQ-MLS (172.31.0.2)
               /    |    \
           VLAN   VLAN   VLAN
           GRP1   GRP2   GRP3-4

Frame Relay Full Mesh WAN:
HQ <-> Branch1 | HQ <-> Branch2 | HQ <-> Branch3
B1 <-> B2      | B1 <-> B3      | B2 <-> B3
```

---

## ✅ Features Implemented

### Core Infrastructure
- 1 HQ + 3 Branch offices
- 10 VLANs per site (Admin, Banking, Tellers, VoIP, ATM, Guest, IT etc.)
- Full mesh Frame Relay WAN (E-LAN topology)
- OSPF dynamic routing across all sites
- DHCP for all VLANs at every site

### Internet & WAN
- HQ internet via Cisco ASA Firewall
- Each branch has independent direct internet link
- NAT/PAT for all internal networks
- GRE VPN tunnels between all sites

### Security
- Cisco ASA 5505 Firewall (3-zone: inside/outside/dmz)
- DMZ with Web Server, Email Server, Online Banking
- SSH v2 on all routers and switches
- RADIUS + AAA centralized authentication
- Guest VLAN restriction (VLAN 90)
- Banner MOTD on all devices

### Voice
- CME (Call Manager Express) at each site
- VoIP inter-site calling between all branches
- Extensions: HQ(1xxx) B1(2xxx) B2(3xxx) B3(4xxx)

### Services
- TIMB Bank corporate website
- Online Banking portal with MFA login page
- Internal email system (SMTP/POP3)
- Google server simulation
- FTP configuration backup

### Management
- NTP time synchronization
- Syslog centralized logging
- FTP config backup to backup server

---

## 🌐 Redundancy Design

### Branch Independent Internet
Each branch has its own direct ISP link:
| Branch | Internet Link | ISP IP |
|--------|--------------|--------|
| Branch 1 | 100.0.1.0/30 | 100.0.1.1 |
| Branch 2 | 100.0.2.0/30 | 100.0.2.1 |
| Branch 3 | 100.0.3.0/30 | 100.0.3.1 |

**If HQ internet fails → Branches stay online!**

---

## 📊 IP Addressing

### HQ VLANs
| VLAN | Name | Network |
|------|------|---------|
| 10 | Admin Management | 192.168.10.0/24 |
| 20 | Core Banking | 192.168.20.0/24 |
| 30 | Clearing/SWIFT | 192.168.30.0/24 |
| 40 | Tellers | 192.168.40.0/24 |
| 50 | Customer Service | 192.168.50.0/24 |
| 60 | CCTV Security | 192.168.60.0/24 |
| 70 | VoIP Phones | 192.168.70.0/24 |
| 80 | ATMs | 192.168.80.0/24 |
| 90 | Guest WiFi | 192.168.90.0/24 |
| 100 | IT Management | 192.168.100.0/24 |
| 200 | HQ Servers | 192.168.200.0/24 |

### WAN Links
| Link | Network | DLCIs |
|------|---------|-------|
| HQ-Branch1 | 10.0.0.0/30 | 102/201 |
| HQ-Branch2 | 10.0.1.0/30 | 103/301 |
| HQ-Branch3 | 10.0.2.0/30 | 104/401 |
| B1-B2 | 10.1.0.0/30 | 123/213 |
| B1-B3 | 10.2.0.0/30 | 132/312 |
| B2-B3 | 10.3.0.0/30 | 231/321 |

---

## 🛠️ Technologies Used

| Technology | Purpose | Standard |
|-----------|---------|---------|
| Cisco IOS 15.1 | Router/Switch OS | Industry |
| OSPF | Dynamic routing | RFC 2328 |
| Frame Relay | WAN connectivity | ITU-T |
| GRE Tunnels | Site-to-site VPN | RFC 2784 |
| 802.1Q VLANs | Segmentation | IEEE |
| Cisco ASA | Firewall | Cisco |
| NAT/PAT | Address translation | RFC 3022 |
| SSH v2 | Secure management | RFC 4253 |
| RADIUS/AAA | Authentication | RFC 2865 |
| NTP | Time sync | RFC 5905 |
| VoIP/CME | Voice | SIP/H.323 |

---

## 🔧 Key Problem Solved

### ASA Firewall Blocking HTTP
**Problem:** Ping worked but web browser showed 
"Request Timeout" even with ACLs configured.

**Root Cause:** INSIDE_OUT ACL had 
`permit ip any any` on line 1 — this matched 
ALL traffic making all subsequent lines 
(HTTP permits) unreachable. ACLs process 
top-down, first match wins!

**Solution:** Removed all ACLs and used ASA 
security levels instead:
- Inside (100) → automatically reaches Outside (0)
- No ACLs needed for basic internet access!

**Lesson:** Sometimes the simplest solution 
is the best solution!

---

## 📁 Repository Contents

| File/Folder | Description |
|------------|-------------|
| README.md | This file |
| TIMB_Bank_Network_Project.pdf | Full documentation |
| configs/ | Device configuration files |
| screenshots/ | Network evidence screenshots |
| demo-video/ | Network walkthrough video |

---

## 🎓 Certification Coverage

| Certification | Topics Covered |
|--------------|---------------|
| CCNA 200-301 | VLANs, OSPF, NAT, ACLs, SSH, DHCP |
| CCNA Security | ASA, DMZ, AAA, RADIUS |
| CCNA Voice | CME, VoIP, Dial-peers |
| CCNP Enterprise | Frame Relay, GRE, WAN design |

---

## 👩‍💻 Author

**Jessica Ugoh**
Electronics and Computer Engineering
Networking Intern

📧 Connect on LinkedIn: https://www.linkedin.com/in/ugoh-chinazaekpere-a5802027b/

---

## 📄 License
This project is for educational purposes.


