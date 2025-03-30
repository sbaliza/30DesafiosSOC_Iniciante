# **Lab#6: Wireshark Basics – UDP Protocol Analysis**

---

## 🎯 **Objective**  
The objective of this lab is to help students analyze **UDP (User Datagram Protocol)** traffic using **Wireshark**. Students will learn about UDP's stateless nature, explore the structure of UDP packets, and apply filters to identify common UDP-based traffic like DNS, DHCP, or NTP.

---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Operating System:** Windows 10/11 (or Linux/macOS)
- **Software:** Wireshark (latest version)

### **Files Needed**
- [Download Sample PCAP file](https://github.com/0xrajneesh/90-Days-SOC-Challenge-Beginner/raw/refs/heads/main/Protocol_Analysis_pcap.pcapng)

---

## 📘 **UDP Packet Structure and Fields**

UDP is a **Layer 4 (Transport Layer)** protocol that offers a fast, connectionless method of communication. Unlike TCP, it does not guarantee delivery or maintain session state.

### **Key UDP Fields:**

| Field Name         | Description                             |
|--------------------|-----------------------------------------|
| **Source Port**     | Port of the sending application         |
| **Destination Port**| Port of the receiving application       |
| **Length**          | Total length of the UDP segment         |
| **Checksum**        | Error-checking (optional in IPv4)       |
| **Data**            | Application-layer payload               |

---

## 🔍 **Most Common UDP Display Filters**

Use these filters in Wireshark’s **Display Filter** bar:

| Filter                      | Description                              |
|-----------------------------|------------------------------------------|
| `udp`                      | Show all UDP packets                     |
| `udp.port == 53`           | Show DNS queries/responses              |
| `udp.port == 67 || udp.port == 68` | Show DHCP traffic            |
| `udp.port == 123`          | Show NTP (time sync) traffic             |
| `ip.addr == 192.168.1.1`   | UDP traffic to/from specific host        |

---

## ✅ Conclusion
- UDP is a fast, lightweight protocol used in many core network services (DNS, DHCP, NTP).
- Unlike TCP, it does not require connection setup, making it ideal for speed-critical tasks.
- Understanding UDP traffic helps analysts detect:
 - DNS abuse or tunneling
 - DHCP attacks or rogue servers
 - UDP-based malware C2 channels

## 📸 Submission
Submit a screenshot showing:
- Show all UDP packets
- Show DNS queries/responses
- Show NTP (time sync) traffic
