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
### 5.
Launched Wireshark to begin capturing network packets for analysis during the attack.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/8.jpg)
### 6.
Initiated a SYN flood attack from the Kali terminal using the following command:
`hping3 -S 192.168.56.101 -a 192.168.22.11 -p 80 --flood`
This command sends a continuous stream of TCP SYN packets to port 80 on the target IP (192.168.56.101) while spoofing the source IP address as 192.168.22.11. The -S flag sets the SYN bit, initiating half open TCP handshakes that are never completed, overwhelming the target's network stack. The --flood option maximizes the packet send rate, aiming to exhaust the victim's resources and simulate a denial of service condition.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/11.jpg)
### 7.
Wireshark captured a flood of incoming TCP SYN packets resulting from the spoofed SYN flood attack, clearly indicating abnormal traffic patterns aimed at overwhelming the target system's resources.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/12.jpg)
### 8.
As a result of the sustained SYN flood attack, the DVWA application running in the browser became unresponsive and eventually crashed, demonstrating the denial-of-service effect on the target system.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/14.jpg)
### 9.
This command simulates a DDoS SYN flood attack where the attacker overwhelms the target with fake TCP connection attempts, exhausting its resources. The use of spoofed IP (-a) makes it harder to trace the attacker and prevents proper TCP handshakes. This can lead to service disruption, as seen with  DVWA crash.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/15.jpg)

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
