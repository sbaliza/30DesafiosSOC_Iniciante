# **Lab#15: Wireshark Basics – FTP Protocol Analysis**

---

## 🎯 **Objective**  
The objective of this lab is to help students analyze **FTP (File Transfer Protocol)** traffic using **Wireshark**. Students will explore how FTP works over the network, identify login credentials and file transfer commands, and understand how insecure protocols can expose sensitive data.

---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Operating System:** Windows 10/11 (or Linux/macOS)
- **Software:** Wireshark (latest version)

### **Files Needed**
- **FTP Sample PCAP File:** [Download FTP pcap](https://wiki.wireshark.org/SampleCaptures#FTP)  
  *(Example: `ftp.cap` or `ftp.pcap` from Wireshark sample captures)*

---

## 📘 **FTP Packet Structure and Fields**

FTP is an **application-layer protocol** used for transferring files over a network. It runs over **TCP ports 21** (control) and **20** (data). FTP transmits data and credentials in **plaintext**, making it vulnerable to interception.

### **Common FTP Commands and Responses:**

| FTP Command / Response | Description                              |
|-------------------------|------------------------------------------|
| `USER`                 | Username sent by client                  |
| `PASS`                 | Password sent by client (in plaintext)   |
| `RETR`                 | Retrieve a file from the server          |
| `STOR`                 | Upload a file to the server              |
| `LIST`                 | List files in the directory              |
| `230 Login successful` | Successful login                         |
| `530 Login incorrect`  | Failed login                             |

---

## 🔍 **Most Common FTP Display Filters**

Use these filters in Wireshark’s **Display Filter** bar:

| Filter                     | Description                              |
|----------------------------|------------------------------------------|
| `ftp`                     | Show all FTP commands and responses      |
| `ftp.request.command == "USER"` | Show username requests            |
| `ftp.request.command == "PASS"` | Show password submissions          |
| `tcp.port == 21`          | FTP control traffic                      |
| `ftp.response.code == 530`| Show failed logins                      |

---

## ✅ Conclusion
- FTP is an insecure protocol; credentials and files are sent in plaintext.
- Wireshark can easily extract:
 - Usernames, Passwords
 - Transferred filenames
- Use of FTP should be avoided on production networks in favor of FTPS or SFTP.

## 📸 Submission
Submit a screenshot showing:
- Show all FTP commands and responses
- Show username requests
- Show password submissions 
