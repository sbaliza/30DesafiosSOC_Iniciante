# **Task #34: Detect Brute-Force Login Attempts in Apache Logs Using Splunk**  

## **Objective**  
The goal of this task is to help students **identify brute-force login attempts** in Apache logs using Splunk. Attackers often try multiple login attempts with different passwords, leading to repeated requests to the login page. By analyzing web server logs, students will detect **high-frequency login failures from the same IP address**.

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
We will now detect repeated failed login attempts, which may indicate a brute-force attack.

### Step 1: Detect IPs with Multiple Login Attempts
Run this query to identify IP addresses that attempted logins multiple times:

```
index=web sourcetype=apache_access request="/login"
| stats count by client_ip
| where count > 10
| sort -count
```
🚨 An IP with excessive login attempts may be performing a brute-force attack.

### Step 2: Analyze Brute-Force Patterns Over Time
Run this query to track login attempts over time to detect bursts of brute-force activity:

```
index=web sourcetype=apache_access request="/login"
| timechart span=5m count by client_ip
```
🚨 A sudden surge in login attempts from a single IP suggests an automated attack.

### Step 3: Identify Login Attempts with Suspicious Usernames
Run this query to find unusual or non-existent usernames used in login attempts:

```
index=web sourcetype=apache_access request="/login"
| stats count by client_ip, user
| where count > 5
```
🚨 Attackers may try common usernames like admin, root, or test as part of brute-force attacks.

## Conclusion
✅ Successfully detected brute-force login attempts using Apache logs in Splunk.    
✅ Identified top attacking IPs attempting multiple logins.    
✅ Analyzed brute-force trends and suspicious usernames used in login attempts.   
✅ Learned how SOC analysts monitor and detect brute-force attacks using Splunk.    

## Submission
- Share a screenshot of the Splunk query results showing repeated login attempts.
- Share a screenshot of the time-based analysis of login attempts.
- Write a short observation on how detecting brute-force attacks helps prevent unauthorized access.
