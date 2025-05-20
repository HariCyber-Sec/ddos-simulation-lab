# 📝 DDoS Simulation Lab Notes

## 🧠 Objective

Simulate a DoS/DDoS (SYN flood) attack on a Metasploitable 2 VM from Kali Linux and analyze the packet traffic using Wireshark.

---

## 💽 Lab Setup

* **Attacker**: Kali Linux (running `hping3`)
* **Target**: Metasploitable 2
* **Monitor**: Wireshark running on attacker machine
* **Virtualization**: VirtualBox with Host-Only Adapter
* **Tool Used**: hping3, Wireshark

---

## Detailed Methodology

### Attack 1: Spoofed SYN Flood:
This command sends a flood of TCP SYN packets to the victim (192.168.56.101) using a spoofed source IP address.
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

### Attack 2: Random Source SYN Flood:
This version of the SYN flood sends randomized TCP SYN packets with random fake source IPs and custom payload size to simulate a large-scale DDoS attack.
### 1.
As with the previous test, packet capture was initiated using Wireshark on the victim machine, maintaining identical network and service conditions to observe the traffic pattern during this attack.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/18.jpg)
### 2.
We initiated a simulated DDoS attack using hping3 with the following command:
`hping3 -S 192.168.56.101 -d 100 -p 80 --flood --rand-source`
This command launches a high-volume SYN flood attack targeting port 80 of the victim machine, sending packets with random spoofed source IPs and a custom payload size, effectively mimicking traffic from multiple attackers.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/19.jpg)
This simulates a Distributed Denial of Service (DDoS) scenario, where thousands of spoofed clients (simulated by --rand-source) bombard a server with TCP connection attempts, eventually overwhelming its resources and making it unavailable for legitimate users.
### 3.
While observing the packets in Wireshark, you can observe that while the destination IP remains constant (192.168.56.101), the source IP addresses vary with each packet. This effectively mimics a Distributed Denial of Service (DDoS) attack, where the target is overwhelmed by traffic seemingly coming from multiple different machines.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/20.jpg)
### 4.
This screenshot shows a **successful SYN flood attack** using `hping3` with randomized source IPs. Over **133,000 spoofed SYN packets** were sent to the target `192.168.56.101` on port 80, with **100% packet loss**—indicating the target server was overwhelmed and unable to respond. This confirms that the attack effectively simulated a **DoS condition**, potentially making the service unresponsive.
![Ddos lab](https://github.com/HariCyber-Sec/ddos-simulation-lab/blob/main/screenshots/23.jpg)

 
---

## 🧪 Observations During Attack

* CPU usage on Metasploitable 2 spiked
* Network became unresponsive to ping after sustained SYN flooding
* Wireshark captured high volume of SYN packets, some with spoofed or random IPs
* The victim machine experienced 100% packet loss
* DVWA became unresponsive due to the flood

 
---

## 📂 Files

* `wireshark-captures/ddos-packets.zip`: Full capture of SYN flood
* `wireshark-captures/ddos-rand.zip`:  Full capture of randomized TCP SYN flood


---


## ✅ Summary

The SYN flood attacks using hping3 were successfully executed and validated through network monitoring. This simulation demonstrated the impact of DoS/DDoS in a controlled lab setup and reinforced core principles of network security monitoring and threat simulation.All actions were performed in an ethical, isolated test lab.

---
### Takeaways

- Denial-of-Service (DoS) attacks can be effectively simulated using tools like hping3, helping security professionals understand network 
  vulnerabilities.

- IP spoofing and randomized packet flooding can mimic Distributed DoS (DDoS) scenarios in controlled lab environments.

- Wireshark plays a critical role in visualizing and analyzing traffic anomalies during such simulations.

- These attacks highlight the importance of rate limiting, SYN cookies, and firewall rules in defending against real-world threats.

- Proactive testing helps organizations validate their incident detection and response strategies before facing actual attacks.
  
---
## ⚠️ Disclaimer

This project is for **educational purposes only** and was performed in a controlled lab environment. Never use these techniques on systems you do not own or have explicit permission to test.


---
## 🧪 Attack Command Used
```bash
hping3 -S <TARGET_IP> -a <Spoof_IP> -p <port no> --flood
hping3 -S <TARGET_IP> -d <data size> -p <port no> --flood --rand-source
