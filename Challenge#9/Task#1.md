# **Task #1: Setting up Osquery on Ubuntu Server**  

## **Objective**  
The goal of this task is to help students **install and configure Osquery on an Ubuntu Server** for system monitoring and security auditing. Osquery allows users to query system information using SQL-like queries, making it a powerful tool for **threat hunting, forensic analysis, and compliance monitoring**.

---

## **Lab Setup**  

### **Requirements**  
- **System:** Ubuntu 22.04/20.04 (Target Machine)  
- **Tools Required:**  
  - **Osquery (To query system logs and security events)**  
  - **Terminal (Command-line access to the Ubuntu machine)**  

---

## **Installation & Configuration**  

We will now install **Osquery** and configure it for system monitoring.

### **Step 1: Add the Osquery Repository**  
Run the following command to add the official **Osquery repository**:  
```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1484120AC4E9F8A1A577AEEE97A80C63C9D8B80B
```
🚨 This imports the Osquery GPG key to verify package authenticity.

### Step 2: Install Osquery
Run these commands to install Osquery on Ubuntu:

```
sudo add-apt-repository 'deb [arch=amd64] https://pkg.osquery.io/deb deb main'
sudo apt update
sudo apt install osquery -y
```
🚨 Osquery is now installed and ready for use.

### Step 3: Start Osquery Interactive Shell
Launch Osquery’s interactive shell to execute commands:

```
osqueryi
```
Run a test query to check logged-in users:

```
SELECT * FROM users;
```
🚨 If the output displays system users, Osquery is working correctly.

### Step 4: Enable and Start Osquery Daemon (osqueryd)
To allow continuous system monitoring, enable and start the Osquery service:
```
sudo systemctl enable osqueryd
sudo systemctl start osqueryd
```
Verify the status of the Osquery daemon:

```
sudo systemctl status osqueryd
```
🚨 The service should be active and running.

### Step 5: Configure Osquery for System Monitoring
- Modify the Osquery configuration file to enable system logging:

```
sudo nano /etc/osquery/osquery.conf
```
- Add the following configuration to log system activity:

```
{
  "options": {
    "config_plugin": "filesystem",
    "logger_plugin": "filesystem",
    "logger_path": "/var/log/osquery/",
    "schedule_splay_percent": 10,
    "events_expiry": 3600,
    "database_path": "/var/osquery/osquery.db",
    "disable_events": false
  }
}
```
Save and exit the file (CTRL + X, then Y, then ENTER).

- Restart Osquery to apply changes:

```
sudo systemctl restart osqueryd
```
🚨 Osquery is now set up for logging system activity.

## Conclusion
✅ Successfully installed Osquery on an Ubuntu Server.   
✅ Configured Osquery daemon for system monitoring.   
✅ Executed basic Osquery commands to query system information.   
✅ Learned how SOC analysts use Osquery for security monitoring and forensic analysis.   

## Submission
- Share a screenshot of Osquery running a test query (SELECT * FROM users;).   
- Share a screenshot of the Osquery configuration file (/etc/osquery/osquery.conf).    
- Write a short observation on how Osquery helps in system security monitoring.    
