# **Task #33: Detect High Number of 404 Errors (Reconnaissance Attempts) Using Splunk**  

## **Objective**  
The goal of this task is to help students **detect reconnaissance attempts** where attackers probe a web server for non-existent resources, often leading to **multiple 404 errors**. By analyzing Apache access logs in Splunk, students will identify **potential attackers scanning for vulnerabilities**.

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

**Ensure Apache Logs Are Ingested into Splunk**  
1. If logs are stored locally, upload them manually:  
   ```splunk
   | inputlookup apache_logs.csv
   ```
2. If logs are forwarded via Splunk Universal Forwarder, ensure they are indexed correctly:
   ```splunk
   index=web sourcetype=apache_access
   ```

## Attack Simulation & Detection Using Splunk
We will now detect high-frequency 404 errors, which may indicate reconnaissance activity.

### Step 1: Detect IPs Generating Multiple 404 Errors
Run this query to identify IPs that repeatedly request non-existent pages:
```
index=web sourcetype=apache_access status=404
| stats count by client_ip
| sort -count
```
🚨 Attackers often scan for missing pages (e.g., /admin, /login, /backup.zip).

### Step 2: Identify Scanning Behavior Over Time
Run this query to analyze 404 errors by time to detect aggressive scanning patterns:
```
index=web sourcetype=apache_access status=404
| timechart span=5m count by client_ip
```
🚨 A sudden spike in 404 errors may indicate an automated scanner or bot performing reconnaissance.

### Step 3: Identify the Most Requested Non-Existent Pages
Run this query to list the most frequently requested URLs that returned a 404 error:

```
index=web sourcetype=apache_access status=404
| stats count by request
| sort -count
```
🚨 If many requests are targeting sensitive directories like /wp-admin/ or /config.php, attackers may be scanning for vulnerabilities.

## Conclusion
✅ Successfully detected reconnaissance activity using Apache logs in Splunk.    
✅ Identified top attacking IPs repeatedly triggering 404 errors.    
✅ Analyzed common scanning patterns and targeted pages.    
✅ Learned how SOC analysts monitor for reconnaissance attempts using Splunk.    

## Submission
- Share a screenshot of the Splunk query results showing frequent 404 errors.   
- Share a screenshot of the time-based trend analysis for 404 errors.   
- Write a short observation on how reconnaissance detection helps prevent attacks.   






