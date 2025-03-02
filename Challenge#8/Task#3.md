# **Task #35: Detect Directory Traversal Attacks in Apache Logs Using Splunk**  

## **Objective**  
The goal of this task is to help students **identify directory traversal attacks** in Apache logs using Splunk. Attackers use **`../` sequences** in URLs to attempt accessing restricted files outside the web root directory. By analyzing web server logs, students will detect **unauthorized attempts to access system files**.

---

## **Video Tutorial**  
📺 **Watch the video**  

---

## **Lab Setup**  

### **Requirements**  
- **System:** Ubuntu 22.04/20.04 (Splunk Server)  
- **Tools Required:**  
  - **Splunk Enterprise or Splunk Cloud**  
  - **Apache Web Server Logs (`access.log`)**  

### **Preparation**  

**Step 1: Ensure Apache Logs Are Ingested into Splunk**  
1. If logs are stored locally, upload them manually:  
   ```splunk
   | inputlookup apache_logs.csv
   ```
2. If logs are forwarded via Splunk Universal Forwarder, ensure they are indexed correctly:
   ```
   index=web sourcetype=apache_access
   ```

## Attack Simulation & Detection Using Splunk
We will now detect directory traversal attempts, where attackers try to access files outside the web root.

### Step 1: Detect Directory Traversal Attempts in Requests
Run this query to find requests containing ../ sequences:

```
index=web sourcetype=apache_access request="*../*" OR request="*../../*"
```
🚨 Directory traversal attacks attempt to access sensitive files like /etc/passwd or C:\windows\system32\.

### Step 2: Identify the Most Targeted Files
Run this query to analyze which files attackers are trying to access:

```
index=web sourcetype=apache_access request="*../*"
| stats count by request
| sort -count
```
🚨 If requests frequently target /etc/passwd or .htaccess, attackers may be attempting privilege escalation.

### Step 3: Extract IP Addresses Attempting Directory Traversal
Run this query to list IPs making directory traversal attempts:

```
index=web sourcetype=apache_access request="*../*"
| stats count by client_ip
| sort -count
```
🚨 Repeated requests from the same IP indicate an automated attack.

## Conclusion
✅ Successfully detected directory traversal attacks using Apache logs in Splunk.    
✅ Identified top targeted files and source IPs attempting traversal.    
✅ Analyzed attack frequency and common traversal techniques.   
✅ Learned how SOC analysts monitor web logs to prevent unauthorized file access.   

## Submission
- Share a screenshot of the Splunk query results showing directory traversal attempts.
- Share a screenshot of the most targeted files analysis.
- Write a short observation on how detecting directory traversal helps prevent web exploitation.
