# 🧪 Lab 3: Unauthorized User Creation (Persistence)

## 🎯 Objective
Detect unauthorized user account creation and respond to persistent backdoor access.

🛠️ Lab Setup with Requirements
Ubuntu 22.04 machine
Logging enabled (auditd, /var/log/auth.log)
Splunk or ELK Stack for analysis
🔧 Preparation
Enable auditing:

bash
Copy
Edit
sudo apt install auditd
sudo systemctl start auditd
Watch /etc/passwd and /etc/shadow for changes:

bash
Copy
Edit
auditctl -w /etc/passwd -p wa -k passwd_changes
⚔️ Attack Simulation
Simulate attacker adding a new user:

bash
Copy
Edit
sudo useradd hacker -m -s /bin/bash
echo "hacker:password123" | sudo chpasswd
🔍 Detection and Analysis
Audit log:

bash
Copy
Edit
ausearch -k passwd_changes
Auth log:

bash
Copy
Edit
grep 'useradd' /var/log/auth.log
Splunk/ELK Query:

bash
Copy
Edit
index=linux_logs "useradd" OR "/etc/passwd"
🛡️ Response and Containment
Delete the unauthorized user:
bash
Copy
Edit
sudo userdel -r hacker
Rotate credentials of all users
Enable stricter sudo policies
📝 Reporting and Documentation
Timestamp and source of user creation
User created, detection method, response actions
✅ Conclusion and Submission
Summarize unauthorized access and persistence detection
Submit report with screenshots and queries used
