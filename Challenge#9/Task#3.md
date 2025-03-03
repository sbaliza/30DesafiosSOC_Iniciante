# **Task #3: Osquery Basics - Collecting Scheduled Tasks on Ubuntu**  

## **Objective**  
The objective of this task is to help students **collect and analyze scheduled tasks (cron jobs) on an Ubuntu system using Osquery**. Scheduled tasks can be used for **system automation, but attackers may also leverage them for persistence and malware execution**. This task will teach students how to **query and investigate scheduled tasks for security monitoring**.

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
### Step 1: Simulate an Unauthorized Scheduled Task
1. Create a malicious cron job that executes a hidden script:
```
echo "* * * * * root /tmp/malicious.sh" | sudo tee -a /etc/crontab
```
2. This command adds a scheduled task that runs every minute.

### Step 2: Collect System-Wide Scheduled Tasks
Run this Osquery query to list all scheduled cron jobs:

```
SELECT * FROM crontab;
```
🚨 Look for unexpected or unauthorized entries.

### Step 3: Identify Scheduled Tasks for Specific Users
Run this query to identify scheduled tasks running under a specific user:

```
SELECT user, command FROM crontab WHERE user != 'root';
```
🚨 If non-root users have suspicious scheduled jobs, it could indicate persistence techniques.



## Conclusion
✅ Successfully collected and analyzed scheduled tasks using Osquery.    
✅ Simulated an unauthorized cron job and detected it using Osquery queries.    
✅ Identified suspicious scheduled jobs running from hidden locations.   
✅ Learned how SOC analysts monitor scheduled tasks to detect persistence mechanisms.    

Submission
Share a screenshot of Osquery running the query to list all scheduled tasks.
Share a screenshot of a query detecting unauthorized scheduled jobs.
Write a short observation on how Osquery helps detect persistence techniques via scheduled tasks.
