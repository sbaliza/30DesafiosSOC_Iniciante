# **Task #38: Extract Top Attacking IPs Using Splunk**  

## **Objective**  
The goal of this task is to help students **identify the top source IPs involved in suspicious activities** using Apache logs in Splunk. Attackers generating **multiple failed login attempts, directory traversal, SQL injection attempts, or reconnaissance scans** can be identified based on frequent access patterns. By analyzing web server logs, students will extract **the top attacking IPs for further investigation and mitigation**.

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
If logs are forwarded via Splunk Universal Forwarder, ensure they are indexed correctly:
splunk
Copy
Edit
index=web sourcetype=apache_access
Attack Simulation & Detection Using Splunk
We will now detect top attacking IPs based on multiple suspicious access attempts.

Step 1: Identify IPs Generating High Numbers of Unauthorized Requests
Run this query to list top IPs making failed authentication, blocked access, or error requests:

splunk
Copy
Edit
index=web sourcetype=apache_access status=403 OR status=401 OR status=404
| stats count by client_ip
| sort -count
🚨 Frequent unauthorized requests from an IP may indicate malicious intent.

Step 2: Detect IPs with High Request Volume
Run this query to track IPs making an unusually high number of requests:

splunk
Copy
Edit
index=web sourcetype=apache_access
| stats count by client_ip
| sort -count
🚨 A high request rate from a single IP could indicate scanning, brute-force attempts, or an automated attack.

Step 3: Identify the Most Active IPs Over Time
Run this query to analyze how attacking IPs behave over time:

splunk
Copy
Edit
index=web sourcetype=apache_access
| timechart span=5m count by client_ip
🚨 Sudden spikes in activity from an IP may indicate an ongoing attack.

Step 4: Correlate IPs with Other Suspicious Activity
Run this query to find IPs involved in multiple types of attacks (SQL injection, brute-force, scanning, etc.):

splunk
Copy
Edit
index=web sourcetype=apache_access (request="*../*" OR request="*UNION*" OR request="/login")
| stats count by client_ip
| sort -count
🚨 If an IP appears in multiple attack categories, it is likely a serious threat.

Conclusion
✅ Successfully extracted top attacking IPs based on Apache logs in Splunk.
✅ Identified IP addresses involved in brute-force, directory traversal, and scanning.
✅ Correlated IP activity with attack frequency and patterns.
✅ Learned how SOC analysts monitor attack sources and take mitigation actions.

Submission
Share a screenshot of the Splunk query results listing the top attacking IPs.
Share a screenshot of the attack frequency analysis over time.
Write a short observation on how identifying attacker IPs helps in blocking malicious traffic.
