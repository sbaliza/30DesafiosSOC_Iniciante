# **Day#2: Log Analysis Basics: Windows Security Logs**

## **Objective:**
The objective of this lab is to introduce students to **Windows Security Logs** and help them understand how to analyze logs for security-related events. Students will learn how to explore and analyze various security logs such as login attempts, user account changes, and other critical system events that could indicate potential security threats.

---

## **Lab Setup**
### **Requirements:**
- **System:** Windows 10/11 or Windows Server 2019/2022
- **Tools:**
  - **Windows Event Viewer** (pre-installed)
  - **Notepad** (to create custom events, if needed)
  - **Administrative Privileges** (to access certain security logs)

---

## **Preparation:**
In this lab, you will explore and analyze the **Security Logs** in the **Windows Event Viewer**, which records security events like login attempts, account lockouts, and more. To get started:

### **On Windows:**
1. Press `Win + R` and type `eventvwr.msc` to open the **Event Viewer**.
2. In the **Event Viewer**, expand the **Windows Logs** section and click on **Security**.
3. You will now see various security-related events like **Login attempts**, **Account lockouts**, **Privilege escalations**, etc.

---

## **What are Windows Security Logs?**
Windows Security Logs contain records of security-related events on the system, such as:
- **Successful and Failed Login Attempts:** Track users who log in or fail to log in.
- **Account Lockouts:** Occurs when a user exceeds the maximum allowed number of incorrect login attempts.
- **Audit Policies:** Logs related to changes in system audit settings and configurations.
- **Group Membership Changes:** Tracks changes in group memberships and user privileges.
- **Privilege Escalation:** Logs events when a user gains elevated privileges.

These logs are valuable for monitoring security incidents, detecting unauthorized access, and auditing system changes.

---

## **Understanding Event IDs in Security Logs:**
Some common **Event IDs** in **Windows Security Logs** that you will encounter include:
- **Event ID 4624**: Successful Logon.
- **Event ID 4625**: Failed Logon.
- **Event ID 4740**: Account Lockout.
- **Event ID 4732**: A user was added to a security-enabled local group.
- **Event ID 4672**: Special privileges assigned to a new logon (Privilege escalation).

---

## **Lab Task: Explore and Analyze Windows Security Logs**

### **Step 1: Generate a Sample Logon Event**
1. Log into the Windows system with your credentials.
2. In the **Event Viewer**, navigate to:  
   `Windows Logs → Security`
3. Look for **Event ID 4624** (Successful Logon). This event will show you the successful logins to the system.
4. Take a screenshot of the event details, including:
   - User Name
   - Logon Type
   - Source Network Address
   - Logon Time

### **Step 2: Simulate a Failed Login Attempt**
1. Open **Command Prompt** and enter an invalid username and password. You can do this by using the following command:
   ```cmd
   net user invaliduser invalidpassword
   ```
2.  After the failed login, go back to Event Viewer.
3. Filter the Security Logs for Event ID 4625 (Failed Logon).
4.. Look for entries that correspond to the failed login attempt.
5. Take a screenshot of the event details, including:
   - Failed Login Attempt Details
   - User Name
   - Logon Type
   - Source Network Address

### Step 3: Check for Account Lockouts
1. Attempt a few additional failed logins to intentionally lock out the account (e.g., 5 failed login attempts).
2. After the account is locked, look for Event ID 4740 (Account Lockout).
3. Analyze the event details:
 - Locked User Account
 - Lockout Time
 - Source IP Address
4. Take a screenshot of the account lockout event.


## Conclusion:
- Understanding Windows Security Logs: Windows Security Logs are essential for identifying suspicious behavior such as unauthorized login attempts, privilege escalation, and system configuration changes.
- SOC Analyst Role: As a SOC Analyst, reviewing and analyzing these logs regularly is critical to detecting and responding to security incidents in real-time.
- Threat Detection: By monitoring for multiple failed logins, account lockouts, and privilege escalations, SOC Analysts can quickly detect malicious activities on a network.

## Submission:
- Event ID 4624 (Successful Login): Submit a screenshot showing a successful login event from the Security logs.
- Event ID 4625 (Failed Login): Submit a screenshot showing a failed login attempt event from the Security logs.
- Event ID 4740 (Account Lockout): Submit a screenshot showing an account lockout event from the Security logs.

