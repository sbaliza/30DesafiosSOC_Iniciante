# **Day#4: Log Analysis Basics – Network-Based Attack Detection Using Syslog**

---

## 🎯 **Objective**  
The objective of this lab is to simulate a **network-based port scan attack** and demonstrate how to detect it using **Syslog** logs on a Linux system. Students will learn how to analyze network-related log entries to identify reconnaissance activity from attackers.

---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Attacker Machine:**: Kali Linux
- **Target Machine**: Ubuntu Linux

### **Tools Needed**
- `nmap` (on attacker machine)
- `ufw` or `iptables` (on target machine)
- `rsyslog` (default logging service)

### **Log Files**
- `/var/log/syslog` – Captures system and network-related messages

---

## 📘 **Preparation**

Network-related events such as blocked connections, failed service access, or unexpected traffic can appear in syslog. When using tools like `ufw` or `iptables`, their logs also integrate with syslog, providing visibility into rejected packets and scan attempts.

---

## 🧠 **What is a Network Port Scan?**

A **port scan** is a technique used by attackers to probe a system for open ports and active services. Tools like `nmap` are commonly used to map a system’s network surface.

### **Why It’s Dangerous**
- Port scans are often a **precursor to exploitation**
- They help attackers identify vulnerable services like open SSH, FTP, or outdated web servers

---

## 🛡️ **Types of Network Attacks Detectable via Syslog**
- Port scans (e.g., Nmap, Masscan)
- Failed service connections
- Suspicious outbound connections
- Firewall rule violations
- Repeated connection attempts on closed ports

---

## 🧪 **Lab Task: Explore and Analyze Linux Syslog for Network Scans**

---

### ⚔️ **Step 1: Attack Simulation – Perform a Port Scan**

> ⚠️ *Only scan systems you own or are authorized to test.*

**On the Attacker Machine:**
```bash
nmap -sS TARGET-IP
```
Or for more aggressive scan:
```
nmap -T4 -A -v TARGET-IP
```
On the Target Machine: Enable and configure UFW firewall:

```
sudo ufw enable
sudo ufw default deny incoming
sudo ufw allow ssh
```

### 🔍 Step 2: Detection and Analysis – Analyze Syslog
Check for UFW blocked messages:

```
sudo grep "UFW BLOCK" /var/log/syslog
```
Check for connection attempts on closed ports:

```
sudo grep -i "connection attempt" /var/log/syslog
```
Optional – Real-time monitoring:

```
sudo tail -f /var/log/syslog
```
Look for patterns such as:
- Multiple blocked attempts from the same IP address
- Scans targeting non-standard ports (e.g., 8080, 3306, 21)
- Frequent hits within a short timeframe (burst activity)

## ✅ Conclusion
- Syslog, combined with firewall logs, is powerful for detecting early-stage reconnaissance
- Port scanning is often the first indicator of an attacker mapping your system
- Detecting and blocking IPs performing scans is a crucial step in proactive defense

## 📸 Submission
Submit a screenshot of a syslog entry showing blocked network traffic due to a port scan. Include:
- Source IP of scan
- Targeted port
- Timestamp


