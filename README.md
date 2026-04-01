# 🔥 pfSense Firewall Lab – Network Segmentation & Traffic Control

![pfSense](https://img.shields.io/badge/pfSense-212121?style=for-the-badge&logo=pfsense&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-FF0000?style=for-the-badge)

pfSense deployed as the network gateway for the SOC home lab — controlling traffic between VMs, enforcing firewall rules, and generating logs that show real blocked connection attempts. Every finding here came from actual lab activity.

---

## 🖥️ Lab Environment

| Machine | Role |
|---|---|
| pfSense | Network gateway, firewall, NAT, DHCP |
| Kali Linux | Attacker machine, traffic source (192.168.1.101) |
| Ubuntu Server | Wazuh manager, internal SOC server |
| Windows 10 | Target endpoint |

All VMs sit behind pfSense on an isolated internal LAN. pfSense controls all inbound and outbound traffic between them.

---

## 📂 What Was Built and Detected

---

### 🔴 Firewall Rule Configuration & Traffic Blocking

Configured LAN firewall rules in pfSense to control which hosts could communicate with external destinations. Applied a block rule targeting a specific internal host and verified the block worked through both ping testing and firewall log analysis.

**pfSense LAN firewall rules – Anti-Lockout Rule, default allow LAN rules, and a custom block rule configured for the attacker host:**

<img width="1702" height="1080" alt="Firewall rules" src="https://github.com/user-attachments/assets/0b21f688-4b2f-4e52-bc8b-87e04570a54d" />

<br>

**Ping test from Kali Linux – first test shows successful connectivity, second test after applying the block rule shows 100% packet loss confirming the firewall rule worked:**

<img width="1596" height="850" alt="network checking" src="https://github.com/user-attachments/assets/dcfe36b1-97e3-44fc-8053-0e03b295569f" />

<br>

- Configured WAN and LAN interfaces with static IP addressing
- Applied a block rule targeting 192.168.1.101 (Kali Linux attacker machine)
- Verified the block by running ping from Kali — went from 0% packet loss to 100% packet loss after rule was applied
- 📌 MITRE: `T1562.004` Disable or Modify System Firewall

---

### 🔴 Firewall Log Analysis

Reviewed pfSense firewall logs after applying the block rule to confirm the traffic was being dropped and to understand what the blocked connection attempts looked like.

**pfSense firewall log showing 170 matched blocked entries — source 192.168.1.101 (Kali) attempting to reach 8.8.8.8 (external DNS) and 192.168.56.103 via TCP and ICMP, all blocked by USER_RULE:**

<img width="1366" height="868" alt="pfsense-firewall log" src="https://github.com/user-attachments/assets/3b1d12d6-df32-4435-ae66-871662150d64" />

<br>

- 170 blocked connection attempts logged between 06:02:34 and 06:02:52 — concentrated burst consistent with automated scanning or brute force attempt
- Source IP 192.168.1.101 (Kali attacker) was attempting both ICMP pings to 8.8.8.8 and TCP connections to 192.168.56.103:1514
- Port 1514 is the Wazuh agent communication port — this shows Kali attempting to reach the Wazuh manager directly
- All attempts blocked by USER_RULE confirming the firewall rule was correctly enforced
- 📌 MITRE: `T1046` Network Service Scanning

---

## 📁 Files in This Repo

```
pfsense-firewall-lab/
└── screenshots/
    ├── firewall-rules.png
    ├── firewall-log.png
    └── ping-test-block-verification.png
```

---

⬅️ [Back to SOC Home Lab](https://github.com/rohithbaggu56-dot/Home-SOC-Lab-Detection-Log-Analysis) · [Back to Portfolio](https://github.com/rohithbaggu56-dot)
