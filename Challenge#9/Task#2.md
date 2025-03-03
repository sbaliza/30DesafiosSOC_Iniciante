# **Task #2: Query Running Processes to Detect Unauthorized Applications Using Osquery**  

## **Objective**  
The objective of this task is to help students **detect unauthorized or suspicious applications running on an Ubuntu server** using Osquery. By querying system processes, students will learn how to **identify rogue applications, detect unauthorized privilege escalations, and monitor unusual command executions**.

---

## **Preparation**  

### **Requirements**  
- **System:** Ubuntu 22.04/20.04 (Target Machine)  
- **Tools Required:**  
  - **Osquery (Installed and running - Refer to Task #1)**  
  - **Terminal (Command-line access to Ubuntu machine)**  

### Ensure Osquery Is Installed and Running**  
1. Verify Osquery installation:  
   ```bash
   osqueryi --version
   ```
2. Start Osquery interactive shell:
```
osqueryi
```

## Attack Simulation and Investigation

### Step 1: Simulate an Unauthorized Process Execution
1. Run a simulated unauthorized process in the background:
```
nohup bash -c 'sleep 600' &
```
2. This will create a long-running hidden process, which attackers often use for persistence.

### Step 2: Detect All Running Processes
Run this query to list all active processes on the system:

```
SELECT pid, name, path, cmdline, start_time FROM processes;
```
🚨 Look for unknown or suspicious applications running on the system.

### Step 3: Detect Non-Standard Applications
Run this query to find processes executing from unusual locations:

```
SELECT pid, name, path FROM processes WHERE path NOT LIKE "/usr/bin/%" AND path NOT LIKE "/bin/%";
```
🚨 Processes running from /tmp, /dev/shm, or user directories may indicate malware or unauthorized software.


### Conclusion
✅ Successfully queried running processes using Osquery.    
✅ Simulated an unauthorized process execution and detected it using Osquery.    
✅ Identified suspicious applications, unauthorized root processes, and risky command executions.    
✅ Learned how SOC analysts use process monitoring to detect unauthorized activity.   


## Submission
- Share a screenshot of Osquery running the query to list all running processes.
- Share a screenshot of a query detecting unauthorized applications.
- Write a short observation on how Osquery helps detect unauthorized software and security threats.

Submission
Share a screenshot of Osquery running the query to list all running processes.
Share a screenshot of a query detecting unauthorized applications.
Write a short observation on how Osquery helps detect unauthorized software and security threats.
