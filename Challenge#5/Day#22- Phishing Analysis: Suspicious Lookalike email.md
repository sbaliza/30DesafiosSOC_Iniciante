# **Phishing Analysis Lab – Investigating a Suspicious Lookalike Email**

---

## 🎯 **Lab Objective**

The objective of this lab is to analyze a real-world phishing email sample using manual investigation techniques. Students will learn to review email headers, validate the sender's identity, check domain/IP reputation, and extract indicators of compromise (IOCs).

---

## 🛠️ **Lab Setup**

- 📨 Download Email Sample (.eml): [Click to download sample-1.eml](https://github.com/0xrajneesh/30-Days-SOC-Challenge-Beginner/blob/main/BRADESCO%20LIVELO.eml)  
- 💻 Tools Recommended:
  - [MX Toolbox Email Header Analyzer](https://mxtoolbox.com/EmailHeaders.aspx)
  - [EML Analyzer](https://eml-analyzer.herokuapp.com/#/)
  - IP reputation check (e.g., VirusTotal, AbuseIPDB, Cisco Talos)
  - Whois lookup (e.g., whois.domaintools.com)
  - URL and Domain analysis (e.g., urlscan.io, VirusTotal)

---

## 🧪 **Lab Task: Analyze the Suspicious Email**

### 📥 Scenario:  
You received an email from **BANCO DO BRADESCO LIVELO** claiming that your card has **92,990 points expiring today**, sent from `banco.bradesco@atendimento.com.br`. The sender’s domain looks similar to Bradesco’s official domain.

Investigate and answer the following:

---

### 🔍 **Questions:**

1. **Is the sender domain (`atendimento.com.br`) a legitimate domain owned by Bradesco?**  
   → _Use Whois lookup or domain reputation services._

2. **What is the actual IP address that sent this email?**  
   → _Inspect the email headers for `Received:` lines or `X-Sender-IP` field._

3. **Does the IP address have a poor reputation or appear on any blacklist?**  
   → _Use VirusTotal or AbuseIPDB to check for known abuse._

4. **What do the SPF, DKIM, and DMARC authentication results show?**  
   → _Check `Authentication-Results` in the header. Is it aligned properly?_

5. **Is there any suspicious link or domain in the body of the email?**  
   → _Inspect the HTML body or convert the base64 content to readable HTML._

6. **Based on your findings, would you classify this as phishing? Why or why not?**  
   → _Provide your reasoning based on sender reputation, header anomalies, urgency tone, and link behavior._

---

## ✅ **Learning Outcome**

By the end of this lab, students should be able to:
- Trace email origin
- Validate domains and IPs
- Understand spoofing techniques
- Detect phishing attempts using header and body analysis
