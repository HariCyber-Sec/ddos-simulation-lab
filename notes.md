# 📝 DDoS Simulation Lab Notes

## 🧠 Objective

Simulate a simple DDoS (SYN flood) attack on a Metasploitable 2 VM from Kali Linux and analyze the packet traffic using Wireshark.

---

## 🖥️ Lab Setup

* **Attacker**: Kali Linux (running `hping3`)
* **Target**: Metasploitable 2
* **Monitor**: Wireshark running on attacker machine
* **Virtualization**: VirtualBox with Host-Only Adapter

---

## 🔧 Network Configuration

* **Kali IP**: 192.168.56.101
* **Metasploitable IP**: 192.168.56.102
* **Interface monitored in Wireshark**: `eth0`

---

## 🚀 Attack Command

Using `hping3` to flood SYN packets:

```bash
hping3 -S --flood -V 192.168.56.102
```

* `-S`: SYN flag
* `--flood`: send packets as fast as possible
* `-V`: verbose mode

> 📌 Tip: Run as root for full functionality

---

## 🧪 Observations During Attack

* CPU usage on Metasploitable 2 spiked
* Network became unresponsive to ping after sustained SYN flooding
* Wireshark captured a high volume of duplicate SYN packets

---

## 🔍 Wireshark Filters Used

To analyze SYN flood pattern:

```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

To monitor TCP connections:

```wireshark
tcp.analysis.flags
```

---

## 📂 Files

* `wireshark-captures/ddos-attack.pcapng`: Full capture of SYN flood
* `scripts/hping3_ddos.sh`: Simple bash script to run attack

---

## 📸 Screenshots Collected

* Kali terminal running `hping3`
* Wireshark graph showing spike in traffic
* `top` command output from Metasploitable 2

---

## ✅ Summary

This simulation demonstrates how SYN flood attacks generate abnormal TCP traffic that can be identified using packet inspection tools like Wireshark. All actions were performed in an ethical, isolated test lab.

---

## ⚠️ Disclaimer

This project is for **educational purposes only** and was performed in a controlled lab environment. Never use these techniques on systems you do not own or have explicit permission to test.
