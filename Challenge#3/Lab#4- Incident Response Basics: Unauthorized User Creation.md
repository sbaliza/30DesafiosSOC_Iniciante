# 🧪 Lab 3: Unauthorized User Creation (Persistence)

## 🎯 Objective
Detect unauthorized user account creation and respond to persistent backdoor access.

## 🛠️ Lab Setup with Requirements
- Ubuntu 22.04 machine
- Logging enabled (auditd, /var/log/auth.log)

## 🔧 Preparation
1. Enable auditing:

```bash
sudo apt install auditd
sudo systemctl start auditd
```

2. Watch /etc/passwd and /etc/shadow for changes:

```bash
auditctl -w /etc/passwd -p wa -k passwd_changes
```

## ⚔️ Attack Simulation
1. Simulate attacker adding a new user:

```bash
sudo useradd hacker -m -s /bin/bash
echo "hacker:password123" | sudo chpasswd
```

## 🔍 Detection and Analysis
1. Audit log:

```bash
ausearch -k passwd_changes
```
2. Auth log:

```bash
grep 'useradd' /var/log/auth.log
```

## 🛡️ Response and Containment
1. Delete the unauthorized user:
```bash
sudo userdel -r hacker
```
2. Rotate credentials of all users
3. Enable stricter sudo policies

## 📝 Reporting and Documentation
- Timestamp and source of user creation
- User created, detection method, response actions

## ✅ Conclusion and Submission
- Summarize unauthorized access and persistence detection
- Submit report with screenshots and queries used
