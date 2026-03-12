## 🔐 Enterprise Web Application VAPT (DVWA & OWASP Juice Shop)
## Enterprise Web Application Penetration Testing | DVWA | OWASP Juice Shop | Burp Suite | SQLMap | Hydra | Kali Linux

## 📌 Project Overview

This project demonstrates a **Web Application Vulnerability Assessment and Penetration Testing (VAPT)** conducted on intentionally vulnerable applications:

* **DVWA (Damn Vulnerable Web Application)**
* **OWASP Juice Shop**

The assessment was performed in a **controlled lab environment** using **Kali Linux as the attacker machine** and **Ubuntu Server as the target host**.
Testing methodology follows the **OWASP Top 10 Web Security Risks** and **OWASP Web Security Testing Guide**.

---

## 🎯 Objectives

* Identify vulnerabilities in web applications
* Demonstrate real-world exploitation techniques
* Understand the impact of security flaws
* Provide mitigation and remediation recommendations
* Build a practical web penetration testing lab

---

## 🧪 Lab Environment

| Component           | Technology             |
| ------------------- | ---------------------- |
| Attacker Machine    | Kali Linux             |
| Target Server       | Ubuntu Server          |
| Target Applications | DVWA, OWASP Juice Shop |
| Testing Methodology | OWASP Top 10           |
| Testing Type        | Black Box Testing      |

---

## 🌐 Lab Network Architecture

Attacker Machine: Kali Linux
IP Address: **10.0.1.50**

Target Server: Ubuntu Server
IP Address: **10.0.1.142**

Applications Hosted:

* DVWA (Port 80)
* OWASP Juice Shop (Port 3000)

---

## 🛠 Tools Used

| Tool       | Purpose                                |
| ---------- | -------------------------------------- |
| Nmap       | Network scanning and service detection |
| Burp Suite | HTTP request interception              |
| SQLMap     | Automated SQL injection testing        |
| FFUF       | Directory brute forcing                |
| Hydra      | Password brute force testing           |
| Curl       | HTTP header inspection                 |
| Firefox    | Manual web testing                     |

---

## 🔍 Testing Methodology

The penetration test followed a structured methodology:

1. Reconnaissance
2. Vulnerability Identification
3. Exploitation
4. Validation
5. Reporting

---

## ⚡ Reconnaissance Phase

**Command**

nmap -sC -sV -A 10.0.1.142

**Purpose**

* Identify open ports
* Detect running services
* Discover software versions

**Example Result**

PORT      STATE SERVICE VERSION
80/tcp    open  http    Apache
3000/tcp  open  http    Node.js

---

## 📂 Directory Discovery

**Command**

ffuf -u http://10.0.1.142/FUZZ -w /usr/share/wordlists/dirb/common.txt

**Purpose**

* Discover hidden directories
* Identify admin panels and backup folders

Example results discovered:

* admin
* uploads
* backup

---

## 💉 SQL Injection Testing

**Target**
DVWA SQL Injection Module

**Payload**

1' OR '1'='1

**Impact**

* Authentication bypass
* Database data extraction
* Unauthorized access

**Automated Exploitation**

sqlmap -u "http://10.0.1.142/DVWA/vulnerabilities/sqli/?id=1" --dbs

Example output databases:

* information_schema
* dvwa
* mysql

---

## 🧠 Cross-Site Scripting (XSS)

**Payload**

<script>alert('XSS')</script>

**Impact**

* Session hijacking
* Credential theft
* Malicious script execution in victim browser

---

## 📤 File Upload Vulnerability

**Test File**

shell.php

**Attack Method**

1. Upload malicious PHP file
2. Access uploaded file through browser

**Impact**

* Remote code execution
* Full server compromise

---

## 🔓 Authentication Brute Force

**Tool**

Hydra

**Command**

hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.0.1.142 http-get-form

**Result**

Username: admin
Password: password

**Impact**

* Weak authentication
* Unauthorized access to system

---

## ⚠ Security Misconfiguration

**Command**

curl -I http://10.0.1.142

**Missing Security Headers**

* X-Frame-Options
* Content-Security-Policy
* X-XSS-Protection

**Impact**

* Increased risk of clickjacking
* Increased risk of XSS exploitation

---

## 📊 Vulnerability Summary

| Vulnerability              | Risk Level |
| -------------------------- | ---------- |
| SQL Injection              | Critical   |
| File Upload Vulnerability  | Critical   |
| Weak Authentication        | High       |
| Cross Site Scripting (XSS) | Medium     |
| Directory Discovery        | Medium     |
| Security Misconfiguration  | Low        |

---

## 🛡 Security Recommendations

### Immediate Fix

* Implement parameterized queries to prevent SQL injection
* Validate and restrict file uploads
* Enforce strong password policies

### Short-Term Fix

* Enable security headers
* Implement a Web Application Firewall (WAF)

### Long-Term Fix

* Adopt secure coding practices
* Implement Secure Software Development Lifecycle (SSDLC)
* Conduct regular penetration testing

---

## 📄 Full Report

The complete penetration testing report is available in the repository:

/REPORT/Enterprise_Web_Application_VAPT_Report.pdf

---

## 👨‍💻 Author

**Parakh Shinde**

Cybersecurity Enthusiast
Web Application Security
Vulnerability Assessment & Penetration Testing

---

## ⭐ Project Purpose

This project demonstrates practical cybersecurity skills including **reconnaissance, vulnerability assessment, exploitation, and reporting** using industry-standard tools and OWASP testing methodology.
