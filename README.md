# 🔐 Web Application Vulnerability Assessment Report

**Target App**: Juice Shop 
**Assessment Date**: July 2025  
**Tools Used**: Nikto, Burp Suite, Wget

---

## 📋 Summary of Findings

| # | Vulnerability                      | Severity | Tool Used   | OWASP Mapping                     |
|---|-----------------------------------|----------|-------------|----------------------------------|
| 1 | SQL Injection (Auth Bypass)       | High     | Manual/Burp | A01:2021 - Broken Access Control |
| 2 | Broken Authentication (Default)  | High     | Manual      | A07:2021 - Identification & Auth Failures |
| 3 | Sensitive Data Exposure (Backup) | High     | Nikto/Wget  | CWE-530 - Backup File Exposure   |

---

## 1️⃣ SQL Injection - Authentication Bypass

**📌 Description:**  
The login form is vulnerable to SQL Injection, allowing attackers to bypass authentication.

**🧪 Payload Used:**
```
Email: ' OR 1=1--
Password: anything
```

**💥 Impact:**  
Attacker can login as an admin without valid credentials.

**🔧 Mitigation:**  
- Use prepared statements  
- Input validation  
- Sanitize user inputs  

**📚 OWASP Reference:**  
- A01:2021 - Broken Access Control

---

## 2️⃣ Broken Authentication via Default Credentials

**📌 Description:**  
Login successful using default credentials.

**🔍 Steps to Reproduce:**  

2. Use:
   ```
   Username: admin@juice-sh.op
   Password: admin123
   
3. Login successful.

**💥 Impact:**  
Full access to application functions. Risk of data exposure and further exploitation.

**🔧 Mitigation:**  
- Change default creds before deployment  
- Enforce password change on first login  
- Enable account lockouts after multiple failures  
- Use MFA

**📚 OWASP Reference:**  
- A01:2021 - Broken Access Control  
- A07:2021 - Identification & Authentication Failures

---

## 3️⃣ Sensitive Data Exposure (CWE-530)

**📌 Description:**  
A backup file was found accessible without authentication, exposing critical data.

**🧪 Tool Used:** Nikto  
**🧪 URL Discovered:**  
```
https://cwe.mitre.org/data/definitions/530.html
```

**💻 Downloaded using:**
```bash
wget https://cwe.mitre.org/data/definitions/530.html
```

**💥 Impact:**  
Leaked file may contain:
- Source code  
- Database credentials  
- API keys  
- Sensitive business logic

**🔧 Mitigation:**  
- Remove sensitive files from production  
- Apply strict access control  
- Automate cleanup via CI/CD  
- Audit file uploads and backups regularly

**📚 Reference:**  
- CWE-530: [Backup File Exposure](https://cwe.mitre.org/data/definitions/530.html)



  
