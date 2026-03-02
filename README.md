# 🔥 pfSense Firewall Lab – Network Segmentation & Traffic Monitoring

This project demonstrates the deployment and configuration of a pfSense firewall inside a virtualized SOC home lab environment to simulate real-world network security monitoring and traffic control.

The firewall acts as the central gateway between virtual machines, enabling network visibility, segmentation, and controlled communication.

---

## 🎯 Objective

- Understand firewall operations in a SOC environment
- Implement network segmentation using pfSense
- Monitor internal traffic between lab machines
- Simulate enterprise-style network architecture

---

## 🏗️ Lab Architecture

The pfSense firewall was configured as the network gateway for the home SOC lab.

**Network Flow:**
<img width="1024" height="656" alt="pfsense_firewall_lab_setup" src="https://github.com/user-attachments/assets/a03fc452-96cf-460f-9ff8-337d96e27918" />


## ⚙️ Configuration Performed

- Installed pfSense in VirtualBox
- Configured WAN and LAN interfaces
- Assigned static IP addressing
- Enabled DHCP services
- Configured firewall rules
- Controlled VM-to-VM communication
- Routed traffic through firewall gateway


## 🔍 Security Concepts Practiced

- Network segmentation
- Firewall rule logic
- Traffic inspection basics
- Internal network isolation
- Gateway monitoring


## 🧠 SOC Learning Outcome

This setup helped understand how real organizations control and monitor traffic flow before logs reach SIEM platforms.

pfSense acts as the first defensive layer in the SOC architecture.


## 🛠️ Tools Used

- pfSense
- Oracle VirtualBox
- Windows 10
- Ubuntu Server
- Kali Linux

---

## 📸 Screenshots
<img width="1702" height="1080" alt="Firewall rules" src="https://github.com/user-attachments/assets/0b21f688-4b2f-4e52-bc8b-87e04570a54d" />


<img width="2592" height="1632" alt="pfsense-firewall log" src="https://github.com/user-attachments/assets/3b1d12d6-df32-4435-ae66-871662150d64" />


---

## ✅ Key Takeaways

- Firewalls control visibility and attack surface
- Network architecture is critical for monitoring
- Proper segmentation improves detection capability

  ---
🔗 **Navigation**  
⬅️ [Back to SOC-Home-Lab-BlueTeam](https://github.com/rohithbaggu56-dot/SOC-Home-Lab-BlueTeam))
---
