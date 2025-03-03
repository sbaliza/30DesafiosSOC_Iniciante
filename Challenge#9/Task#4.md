# **Task #4: Osquery Basics - Detecting Unusual Network Connections**  

## **Objective**  
The objective of this task is to help students **detect unusual or unauthorized network connections on an Ubuntu system using Osquery**. Attackers often establish **reverse shells, persistence backdoors, or data exfiltration channels**, which can be identified by monitoring network activity. This task will teach students how to **query and investigate active network connections for security monitoring**.

---

## **Preparation**  

### **Requirements**  
- **System:** Ubuntu 22.04/20.04 (Target Machine)  
- **Tools Required:**  
  - **Osquery (Installed and running - Refer to Task #1)**  
  - **Terminal (Command-line access to Ubuntu machine)**  

### **Step 1: Ensure Osquery Is Installed and Running**  
1. Verify Osquery installation:  
   ```bash
   osqueryi --version

2. Start Osquery interactive shell:
```
osqueryi
```


## Attack Simulation and Investigation

### Step 1: Simulate an Unauthorized Network Connection
1. Open a terminal and start a dummy network listener (simulating a backdoor connection):
```
nc -lvp 4444
```
2. From another machine or terminal, connect to this port:
```
nc <target-ip> 4444
```
3. This simulates a malicious remote access session.

### Step 2: List Active Network Connections
Run this Osquery query to retrieve all active network connections:

```
SELECT pid, local_address, local_port, remote_address, remote_port, protocol FROM process_open_sockets;
```
🚨 Look for unexpected external IP connections and unusual port numbers.

## Conclusion
✅ Successfully collected and analyzed network connections using Osquery.    
✅ Simulated an unauthorized network connection and detected it using Osquery queries .   
✅ Identified suspicious connections to untrusted IPs and unexpected listening services.    
✅ Learned how SOC analysts monitor network activity to detect security threats.   

## Submission
- Share a screenshot of Osquery running the query to list active network connections.
- Share a screenshot of a query detecting unauthorized external connections.
- Write a short observation on how Osquery helps detect unusual network activity.
