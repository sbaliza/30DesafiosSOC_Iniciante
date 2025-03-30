# **Lab#1: Introduction to Wireshark – Packet Analysis for SOC Analysts**

---

## 🎯 **Objective**  
The objective of this lab is to introduce students to **Wireshark**, a powerful packet analysis tool used by SOC analysts to investigate network traffic. Students will learn the interface, how to capture packets, apply filters, and identify suspicious communication patterns.

---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Operating System:** Windows, Linux, or macOS
- **Network Adapter:** Required for packet capture

### **Software Required**
- [Wireshark](https://www.wireshark.org/download.html) (latest stable version)
- [Download Sample PCAP file](https://github.com/0xrajneesh/90-Days-SOC-Challenge-Beginner/raw/refs/heads/main/Protocol_Analysis_pcap.pcapng)

---

## 🎥 **YouTube Tutorial Video**
📺 Watch: **[Wireshark for Beginners – Hands-On Walkthrough](https://youtu.be/nmLH0c5YUJk)**  
Duration: 15 minutes

---

## 📘 **What is Wireshark?**

**Wireshark** is an open-source network protocol analyzer that lets you capture and interactively browse network traffic. It allows analysts to view data packets flowing in and out of a system in real time or from saved PCAP files.

---

## 🛡️ **Wireshark Use Cases for SOC Analysts**

- 🔍 **Incident Investigation:** Analyze malicious traffic patterns (e.g., C2 communication, lateral movement)
- 🕵️ **Malware Analysis:** Extract indicators like domains, IPs, and payloads from suspicious network behavior
- 🚨 **Threat Hunting:** Detect anomalies like DNS tunneling, beaconing, or unauthorized FTP/SSH usage
- 🛠️ **Protocol Troubleshooting:** Identify service failures, misconfigurations, or latency issues

---

## ✅ **Task Checklist**

| Task | Description |
|------|-------------|
| ✅ Install Wireshark | Download and install from the official website |
| ✅ Capture Live Traffic | Start a capture on your main interface |
| ✅ Apply Filters | Use filters like `http`, `tcp.port==80`, `ip.addr==192.168.1.1` |
| ✅ Analyze a PCAP File | Download a malware traffic PCAP and examine sessions |
| ✅ Identify Suspicious Traffic | Locate large POST requests, unknown IPs, or DNS anomalies |

---

## 📸 **Submission**
Submit screenshots showing:
- Wireshark interface with live traffic or loaded PCAP
- Filter applied in the display filter bar
- One packet expanded with layer-by-layer details
- Optional: any suspicious IP or payload pattern identified

