# **Task #37: Detect Suspicious User Agents in Apache Logs Using Splunk**  

## **Objective**  
The goal of this task is to help students **identify suspicious or malicious user agents** in Apache logs using Splunk. Attackers, web scrapers, and bots often use unusual or forged user agents to evade detection. By analyzing web server logs, students will detect **automated scanning, scraping, and potential attack attempts**.

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
We will now detect unusual user agents that may indicate bot activity, scrapers, or attackers.

Step 1: List the Most Common User Agents
Run this query to identify the most frequently used user agents in Apache logs:

splunk
Copy
Edit
index=web sourcetype=apache_access
| stats count by user_agent
| sort -count
🚨 Legitimate traffic usually comes from browsers like Chrome, Firefox, or Safari. Look for anomalies.

Step 2: Detect Rare or Suspicious User Agents
Run this query to filter non-standard or potentially malicious user agents:

splunk
Copy
Edit
index=web sourcetype=apache_access NOT user_agent="Mozilla*" NOT user_agent="Chrome*" NOT user_agent="Safari*"
| stats count by user_agent
| sort -count
🚨 Requests from curl, wget, python-requests, or empty user agents may indicate automation, scanning, or scraping.

Step 3: Identify Top IPs Using Suspicious User Agents
Run this query to correlate user agents with IP addresses:

splunk
Copy
Edit
index=web sourcetype=apache_access NOT user_agent="Mozilla*" NOT user_agent="Chrome*" NOT user_agent="Safari*"
| stats count by client_ip, user_agent
| sort -count
🚨 If an IP is using multiple suspicious user agents, it may be an attacker or a botnet.

Conclusion
✅ Successfully detected suspicious user agents using Apache logs in Splunk.
✅ Identified bots, scrapers, or automated scanners.
✅ Correlated malicious user agents with specific IP addresses.
✅ Learned how SOC analysts monitor web traffic to detect and prevent automated attacks.

Submission
Share a screenshot of the Splunk query results listing the most common user agents.
Share a screenshot of the suspicious user agent analysis.
Write a short observation on how identifying malicious user agents helps in detecting bot attacks.
