# **Lab#4: Wireshark Basics – ARP Protocol Analysis**

---

## 🎯 **Objective**  
The objective of this lab is to help students analyze **ARP (Address Resolution Protocol)** traffic using **Wireshark**. Students will learn how ARP helps in resolving IP-to-MAC addresses, explore packet structure, and understand how ARP can be used for reconnaissance or spoofing.

---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Operating System:** Windows 10/11 (or Linux/macOS)
- **Software:** Wireshark (latest version)

### **Files Needed**
- **ARP Sample PCAP File:** [Download ARP pcap](https://wiki.wireshark.org/SampleCaptures#ARP)  
  *(Example: `arp.cap` from Wireshark sample captures)*

---

## 📘 **ARP Packet Structure and Fields**

ARP operates at **Layer 2** (Data Link Layer) and is used to map an IP address to a physical MAC address on a local network.

### **Key ARP Fields:**

| Field Name            | Description                                     |
|------------------------|-------------------------------------------------|
| **Hardware Type**      | Usually Ethernet (1)                            |
| **Protocol Type**      | Usually IPv4 (0x0800)                           |
| **Hardware Size**      | MAC address length (6)                          |
| **Protocol Size**      | IP address length (4)                           |
| **Opcode**             | Request (1) or Reply (2)                        |
| **Sender MAC Address** | MAC address of the requester/respondent        |
| **Sender IP Address**  | IP address of the requester/respondent         |
| **Target MAC Address** | MAC address being queried                      |
| **Target IP Address**  | IP address being resolved                      |

---

## 🔍 **Most Common ARP Display Filters**

Use these filters in Wireshark’s **Display Filter** bar:

| Filter                  | Description                             |
|--------------------------|-----------------------------------------|
| `arp`                   | Show all ARP packets                    |
| `arp.opcode == 1`       | Show ARP Requests                       |
| `arp.opcode == 2`       | Show ARP Replies                        |
| `arp.src.proto_ipv4 == 192.168.1.1` | Show ARP packets from specific IP |
| `eth.dst == ff:ff:ff:ff:ff:ff` | Show broadcast ARP packets        |

---
## ✅ Conclusion
- ARP is crucial for local network communication and device discovery.
- ARP requests are broadcast, while replies are unicast.
- ARP analysis helps detect:
 - IP/MAC spoofing
 - ARP poisoning (Man-in-the-Middle setup)
 - Unauthorized devices sending ARP replies

## 📸 Submission
Submit a screenshot showing:
- Show all ARP packets
- Show ARP Requests
- Show ARP Replies   
