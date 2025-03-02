# **Task #36: Detect SQL Injection Attempts in Apache Logs Using Splunk**  

## **Objective**  
The goal of this task is to help students **identify SQL injection attempts** in Apache logs using Splunk. SQL injection is a web attack technique where malicious SQL statements are injected into input fields to manipulate a database. By analyzing web server logs, students will detect **unauthorized database query attempts**.

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
We will now detect malicious SQL queries embedded in HTTP requests.

Step 1: Detect Common SQL Injection Payloads in URLs
Run this query to find requests containing SQL keywords that indicate injection attempts:

splunk
Copy
Edit
index=web sourcetype=apache_access request="*UNION*" OR request="*SELECT*" OR request="*DROP*" OR request="*INSERT*" OR request="*UPDATE*" OR request="*DELETE*"
🚨 Attackers may be trying to execute unauthorized SQL queries, bypass authentication, or dump database tables.

Step 2: Identify the Most Frequent SQL Injection Attempts
Run this query to analyze which SQL-based attack patterns appear most often:

splunk
Copy
Edit
index=web sourcetype=apache_access request="*UNION*" OR request="*SELECT*"
| stats count by request
| sort -count
🚨 Frequent SQL queries in URLs indicate a possible automated SQL injection attack.

Step 3: Extract IP Addresses Involved in SQL Injection Attempts
Run this query to list IPs making suspicious SQL queries:

splunk
Copy
Edit
index=web sourcetype=apache_access request="*UNION*" OR request="*SELECT*" OR request="*DROP*"
| stats count by client_ip
| sort -count
🚨 Repeated SQL injection attempts from the same IP suggest an attacker or botnet is targeting the web application.

Conclusion
✅ Successfully detected SQL injection attempts using Apache logs in Splunk.
✅ Identified malicious SQL queries and potential exploitation attempts.
✅ Extracted top offending IPs executing SQL-based payloads.
✅ Learned how SOC analysts monitor and prevent SQL injection-based attacks.

Submission
Share a screenshot of the Splunk query results showing SQL injection attempts.
Share a screenshot of the IP analysis related to SQL injection attacks.
Write a short observation on how SQL injection detection helps in securing databases.
