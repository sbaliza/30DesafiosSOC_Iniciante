🧪 Lab 1: SSH Brute Force Attack Detection on Ubuntu
🎯 Objective
Detect, investigate, and respond to an SSH brute-force attack on an Ubuntu server using log analysis.

🛠️ Lab Setup with Requirements
Ubuntu 22.04 machine
Attacker machine (Kali Linux or another Ubuntu)
SSH service enabled
fail2ban, auditd, or use /var/log/auth.log
Tools: Hydra (on attacker), Splunk or ELK (for log analysis)
🔧 Preparation
Enable and start SSH on the Ubuntu server:
bash
Copy
Edit
sudo systemctl enable ssh
sudo systemctl start ssh
Create a weak user (e.g., testuser with password 1234)
Set up Splunk Forwarder or Filebeat to forward /var/log/auth.log
⚔️ Attack Simulation
From attacker machine:

bash
Copy
Edit
hydra -l testuser -P /usr/share/wordlists/rockyou.txt ssh://<Ubuntu-IP>
🔍 Detection and Analysis
Check /var/log/auth.log for multiple failed attempts:
bash
Copy
Edit
grep "Failed password" /var/log/auth.log
Query in ELK/Splunk:
bash
Copy
Edit
index=linux_logs "Failed password" | stats count by src_ip
🛡️ Response and Containment
Block the attacking IP:
bash
Copy
Edit
sudo ufw deny from <attacker-IP>
Enable rate-limiting:
bash
Copy
Edit
sudo apt install fail2ban
sudo systemctl enable fail2ban
📝 Reporting and Documentation
Include IP of attacker, username targeted, timestamps
Screenshot of logs, detection method, and command output
✅ Conclusion and Submission
Summarize how brute-force detection was done
Submit analysis notes, screenshots, and mitigation steps
