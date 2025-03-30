# **Lab#7: Wireshark Basics – DHCP Protocol Analysis**

---

## 🎯 **Objective**  
The objective of this lab is to help students analyze **DHCP (Dynamic Host Configuration Protocol)** packets using **Wireshark**. Students will understand the DHCP 4-way handshake process, packet fields, and use filters to detect legitimate and potentially rogue DHCP activity.

---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Operating System:** Windows 10/11 (or Linux/macOS)
- **Software:** Wireshark (latest version)

### **Files Needed**
- **DHCP Sample PCAP File:** [Download DHCP pcap](https://wiki.wireshark.org/SampleCaptures#DHCP)  
  *(Example: `dhcp.pcap` from Wireshark sample captures)*

---

## 📘 **DHCP Packet Structure and Fields**

DHCP is an **application-layer protocol** used to dynamically assign IP addresses and other configuration parameters to devices in a network. It uses **UDP ports 67 (server)** and **68 (client)**.

### **Key DHCP Fields:**

| Field Name            | Description                                 |
|------------------------|---------------------------------------------|
| **Message Type**       | Discover, Offer, Request, Acknowledgment    |
| **Transaction ID**     | Unique value to match DHCP messages         |
| **Client IP Address**  | Requested IP by client                      |
| **Your IP Address**    | IP offered by server                        |
| **Server Identifier**  | IP address of DHCP server                   |
| **Options**            | Includes hostname, lease time, DNS, etc.    |

---

## 🔄 **DHCP 4-Way Handshake**

1. **DHCP Discover** → Client broadcasts request  
2. **DHCP Offer** → Server offers IP address  
3. **DHCP Request** → Client accepts offer  
4. **DHCP ACK** → Server confirms and assigns IP  

---

## 🔍 **Most Common DHCP Display Filters**

Use these filters in Wireshark’s **Display Filter** bar:

| Filter                         | Description                          |
|--------------------------------|--------------------------------------|
| `bootp`                        | Show all DHCP/BOOTP traffic          |
| `udp.port == 67 || udp.port == 68` | DHCP traffic by port           |
| `bootp.option.type == 53`      | Show DHCP message types              |
| `bootp.option.type == 53 && bootp.option.value == 1` | DHCP Discover |
| `bootp.option.type == 53 && bootp.option.value == 2` | DHCP Offer    |

---

## ✅ Conclusion
- DHCP is essential for IP address assignment in dynamic networks.
- DHCP analysis helps identify:
 - Rogue DHCP servers
 - IP conflicts or exhaustion
 - Unauthorized or misconfigured hosts

## 📸 Submission
Submit a screenshot showing:
- Show all DHCP/BOOTP traffic
- Show  DHCP Discover
- Show DHCP Offer
