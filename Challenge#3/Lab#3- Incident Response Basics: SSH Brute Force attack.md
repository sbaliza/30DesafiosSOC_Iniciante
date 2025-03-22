# 🧪 Lab 1: SSH Brute Force Attack Detection on Ubuntu   
## 🎯 Objective   
Detect, investigate, and respond to an SSH brute-force attack on an Ubuntu server using log analysis.    
  
## 🛠️ Lab Setup with Requirements
- Ubuntu 22.04 machine
- Attacker machine (Kali Linux or another Ubuntu)
- SSH service enabled
- Tools: Hydra (on attacker), Splunk or ELK (for log analysis)

## 🔧 Preparation
1. Enable and start SSH on the Ubuntu server:   
```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

## ⚔️ Attack Simulation
From attacker machine:

```bash
hydra -l testuser -P /usr/share/wordlists/rockyou.txt ssh://<Ubuntu-IP>
```

## 🔍 Detection and Analysis
Check /var/log/auth.log for multiple failed attempts:
```bash
grep "Failed password" /var/log/auth.log
```

## 🛡️ Response and Containment
1. Block the attacking IP:
```bash
sudo ufw deny from <attacker-IP>
```

## 📝 Reporting and Documentation
- Include IP of attacker, username targeted, timestamps   
- Screenshot of logs, detection method, and command output    

## ✅ Conclusion and Submission
Summarize how brute-force detection was done   
Submit analysis notes, screenshots, and mitigation steps   
