# **Task #1: Identify Suspicious Processes Using Task Manager and Sysmon**

## **Objective**  
The objective of this task is to help students detect **suspicious processes** running on a Windows system by using **Task Manager** and **Sysmon (System Monitor)**. Students will simulate a **malicious process execution**, capture process creation events, and analyze logs to identify potential threats.

---

## **Lab Setup**  
### **Requirements**  
- **System:** Windows 10/11 or Windows Server 2019/2022  
- **Tools Required:**  
  - **Task Manager (Pre-installed on Windows)**  
  - **Sysmon (System Monitor) from Sysinternals**  
  - **PowerShell**  

---

## **Preparation**  
### **Step 1: Install Sysmon (If Not Installed)**  
1. Download **Sysmon** from Microsoft Sysinternals:  
   [https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)  
2. Extract the Sysmon ZIP file.  
3. Open **Command Prompt (Run as Administrator)** and install Sysmon with basic logging:  
   ```powershell
   sysmon -accepteula -i
   ```
4. Verify installation by checking for Sysmon logs in Event Viewer:
```
Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
```

## Attack Simulation & Detection
We will now simulate a suspicious process execution, detect it using Task Manager, and analyze logs with Sysmon.

### Step 1: Simulate a Suspicious Process Execution
1. Open PowerShell (Run as Administrator).
2. Execute the following command to launch a potentially suspicious process:
```
Start-Process -FilePath "cmd.exe" -ArgumentList "/c whoami & ipconfig & tasklist" -WindowStyle Hidden
```
- This command starts cmd.exe with arguments to gather user information, network details, and running processes.
- Attackers often use similar commands during post-exploitation reconnaissance.
### Step 2: Detect the Suspicious Process Using Task Manager
1. Open Task Manager (`Ctrl + Shift + Esc`).
2. Navigate to Processes Tab.
3. Look for:
- Unknown or suspicious processes (e.g., `cmd.exe` running without a visible window).
- Processes consuming high CPU or memory unexpectedly.
- Processes with no description or signed publisher.

### Step 3: Detect the Process Execution Using Sysmon Logs
1. Open Event Viewer (Win + R, type eventvwr.msc, press Enter).
2. Navigate to:
```
Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
```
3. Click Filter Current Log and enter Event ID 1 (Process Creation).
4. Look for:
- Process Name: `cmd.exe`
- Parent Process: `powershell.exe`
- Command Line Arguments: `/c whoami & ipconfig & tasklist`
- Process Path and User Account Details

### Step 4: Response and Containment(For Real-World Environment)
If confirmed malicious:
- Right-click in Task Manager → End Process.
- Isolate the system from the network (for safety).
- Collect the full Sysmon event logs for further investigation.
- Check for persistence mechanisms (e.g., autoruns, scheduled tasks).

###🧾 Step5 5: Reporting & Documentation
Document Findings
- Time of detection.
- Process details.
- User account involved.
- Actions taken.
- Save relevant Sysmon log entries (Event ID 1).

## Conclusion
✅ Successfully simulated a suspicious process execution.      
✅ Detected malicious activity using Task Manager and Sysmon logs.     
✅ Identified process execution patterns attackers use for reconnaissance.    
✅ Learned how SOC analysts detect and investigate unauthorized process activity.    

## Submission
- Share a screenshot of Sysmon logs showing process execution (Event ID 1 for cmd.exe).
- Write a short observation on how process monitoring helps detect malicious activity on endpoints.
