SOC Lab Project – Nmap Scan Detection via pfSense

 📌 Project Overview

This is a basic SOC (Security Operations Center) simulation using virtual machines. The goal is to **detect a network scan** launched using Nmap from Kali Linux, and observe the responses from the Ubuntu target via **Wireshark packet capture** through **pfSense**.

---

🏗️ Lab Setup

| Component     | Configuration / Tool         |
|--------------|-------------------------------|
| Attacker     | Kali Linux (192.168.1.100)    |
| Target       | Ubuntu Server (192.168.1.110) |
| Firewall     | pfSense (Monitoring Bridge)   |
| Tools Used   | Nmap, Wireshark, Netplan      |
| Platform     | VMware Workstation            |

 ## 📋 Static IP Configuration on Ubuntu

File: `netplan-config/50-cloud-init.yaml`

```yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.1.110/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1


STEP 1:
1.Configured Ubuntu Server with static IP using Netplan.
2.Verified connectivity from Kali to Ubuntu.
3.Started Nmap SYN Scan from Kali:
           nmap -sS -T4 -Pn 192.168.1.110
                    -sS : Stealth Scan
                    -T4 : Fast Timer
                    -Pn : Skip Ping
4.pfSense was placed between the attacker and target to capture traffic.
5.Packet capture was saved and opened in Wireshark for analysis.

STEP 2 : WIRESHARK ANALYSIS

Filter Used :
            1.tcp.flags.syn == 1 && tcp.flags.ack == 0
            2.tcp.flags.syn == 1 && tcp.flags.ack == 1

The Logs and Screenshots are added in the log and screenshot folders.


Author:
  A Dhanush Raj
  CIT Graduate
  CyberSecurity and SOC Enthusiast  