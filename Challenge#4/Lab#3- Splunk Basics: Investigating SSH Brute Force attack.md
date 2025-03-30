# 🧪 Lab#3: Investigating SSH Brute Force Attack using Splunk 

---

## 🎯 Objective

To learn how to search and analyze SSH logs using Splunk to identify brute-force login attempts, extract meaningful information from the data, and answer basic investigation questions using fields like user, src_ip, and status.

---

## 🛠️ Lab Setup
- **Ubuntu Server** (22.04 or later)
- [Download linux Auth log sample](https://github.com/0xrajneesh/90-Days-SOC-Challenge-Beginner/blob/main/linux_auth_logs.json)


## Pre-requisite
- [Seting up Splunk Server on Ubuntu Server](https://github.com/0xrajneesh/90-Days-SOC-Challenge-Beginner/blob/main/Challenge%234/Task%231-Setting%20up%20Splunk.md)

---

## Lab Task

📥 Submit the answers below along with screenshots from your Splunk queries.

---

Question 1:  **Which user has attempted the most number of SSH brute-force attempts?**

Question 2:  **What is the IP Address of the user “thor”?**

Question 3:  **How many times user “thor” failed to login?**

## ✅ Conclusion

In this lab, you learned how to perform a basic security investigation using Splunk by analyzing SSH logs for brute-force attack attempts. You practiced using search queries, filtering data by specific fields such as `user`, `src_ip`, and `action`, and interpreting results to answer real-world security questions.
This exercise helped you:
- Understand how attackers attempt brute-force logins.
- Get hands-on experience with Splunk Search Processing Language (SPL).
- Develop analytical thinking to trace and respond to suspicious activities.
