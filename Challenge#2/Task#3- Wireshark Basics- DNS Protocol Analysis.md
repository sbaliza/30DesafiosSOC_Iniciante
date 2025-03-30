# **Lab#8: Wireshark Basics – DNS Protocol Analysis**

---

## 🎯 **Objective**  
The objective of this lab is to introduce students to analyzing **DNS (Domain Name System)** traffic using **Wireshark**. Students will learn how DNS queries and responses look, understand DNS packet structure, and use filters to identify domain resolution activities.

---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Operating System:** Windows 10/11 (or Linux/macOS)
- **Software:** Wireshark (latest version)

### **Files Needed**
- [Download Sample PCAP file](https://github.com/0xrajneesh/90-Days-SOC-Challenge-Beginner/raw/refs/heads/main/Protocol_Analysis_pcap.pcapng)

---

## 📘 **DNS Packet Structure and Fields**

DNS is an **application-layer protocol** used to resolve domain names to IP addresses (and vice versa). DNS runs over UDP/53 or TCP/53 (for large responses or zone transfers).

### **Key DNS Fields:**

| Field Name        | Description                             |
|-------------------|-----------------------------------------|
| **Transaction ID**| Unique ID to match query/response       |
| **Flags**         | Indicates type (query/response), recursion, etc. |
| **Questions**     | Number of domain name queries            |
| **Answer RRs**    | Number of resource records in answer     |
| **Authority RRs** | Number of authority records              |
| **Additional RRs**| Number of additional records             |
| **Queries**       | Domain names being queried               |
| **Answers**       | Resolved IP addresses or records         |

---

## 🔍 **Most Common DNS Display Filters**

Use these filters in Wireshark’s **Display Filter** bar:

| Filter                  | Description                              |
|--------------------------|------------------------------------------|
| `dns`                   | Show all DNS traffic                     |
| `udp.port == 53`        | Show all UDP-based DNS packets           |
| `dns.qry.name == "example.com"` | Filter DNS query for specific domain |
| `dns.flags.response == 1` | Show DNS responses                     |
| `dns.flags.rcode != 0`   | Show failed DNS queries (errors)        |

---

## ✅ Conclusion
- DNS logs are critical for tracking domain resolution and detecting malicious domains.
- Wireshark provides a clear view of DNS queries and responses, helping analysts investigate suspicious traffic.
- DNS traffic analysis can help detect:
 - Command and control domains
 - DNS tunneling
 - Unexpected domain lookups from endpoints

## 📸 Submission
Submit a screenshot showing:
- DNS traffic
- Show DNS responses
- Show failed DNS queries (errors)  
