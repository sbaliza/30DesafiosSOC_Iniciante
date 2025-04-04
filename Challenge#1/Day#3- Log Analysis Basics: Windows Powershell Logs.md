# **Day#3: Log Analysis Basics: Windows PowerShell Logs**

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
Get-Process | Where-Object { $_.CPU -gt 10 }
```
This command will list the local users on your system, which attackers might use to gather information during post-exploitation.

3. After running the command, go back to Event Viewer and navigate to:

`Applications and Services Logs → Microsoft → Windows → PowerShell → Operational`

4. Look for Event ID 4104 in the logs (this will show script block logging for the PowerShell command you executed).
5. Take a screenshot of the event details, including:
 - PowerShell command that was executed
 - User who ran the command
 - Timestamp of the execution
  

### **Step 3: Analyze Suspicious PowerShell Logs**
- Hunt for suspicious script executions from unknown sources or non-standard paths.
- Correlate user activity with system behavior like file downloads or binary execution.
- Inspect Event ID 4104 for odd commands, encoded scripts, or known attack patterns.

## Conclusion:
- PowerShell Logs: Key to spotting malicious command usage.
- SOC Analyst Role: Review logs to detect post-exploitation actions.
- Threat Detection: Flags abnormal activity for faster response.

## Submission:
- Event ID 4104 (PowerShell Script Execution): Submit a screenshot showing a PowerShell script execution event from the logs.
