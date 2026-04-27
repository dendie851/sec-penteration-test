# 🛡️ Security Penetration Testing Lab

## 📑 Table of Contents
- [📖 Background: Why is Penetration Testing Important?](#-background-why-is-penetration-testing-important)
- [1. Penetration Testing Technical Concepts](#1-penetration-testing-technical-concepts)
  - [1.1 DAST (Dynamic Application Security Testing)](#11-dast-dynamic-application-security-testing)
  - [1.2 SAST (Static Application Security Testing)](#12-sast-static-application-security-testing)
  - [1.3 Vulnerability Scanning (Container Security)](#13-vulnerability-scanning-container-security)
  - [1.4 Network Security Testing & Anti-DDoS](#14-network-security-testing--anti-ddos)
- [2. Understanding DAST & OWASP Top 10](#2-understanding-dast--owasp-top-10)
- [3. OWASP ZAP: The DAST Powerhouse](#3-owasp-zap-the-dast-powerhouse)
- [4. Lab Implementation Guide](#4-lab-implementation-guide)
- [5. Vulnerability Analysis & Reports](#5-vulnerability-analysis--reports)
- [6. Advanced Features & Exploration](#6-advanced-features--exploration)
- [🛡️ Conclusion](#️-conclusion)

---

### 📖 Background: Why is Penetration Testing Important?

In today's digital era, applications are not just lines of code, but the heart of businesses and sensitive user data. However, as technology becomes more complex, security vulnerabilities (**vulnerabilities**) become a real and growing threat. Often, we focus too much on functionality and speed-to-market, unknowingly leaving a "backdoor" wide open for attackers.

**Penetration Testing** acts as a real attack simulation to test our system's resilience. Imagine building a grand fortress but forgetting to lock one window on the top floor; an attacker only needs one small gap to bring everything down. By proactively testing through **SAST**, **DAST**, and **Network Security** methods, we:
- **Find Vulnerabilities Before Attackers**: Identify weak points before they are exploited by malicious parties.
- **Understand Real Risks**: It's not just theory; we see the actual impact if an attack successfully breaches the system.
- **Build Trust**: Ensuring user data security is the main key to maintaining reputation and integrity.

This repository is designed as a practical lab to understand how security testing works end-to-end. **Specifically, this guide strongly emphasizes DAST using Open-Source DAST tools (such as OWASP ZAP) to find vulnerabilities in running applications.**

---

## 1. Penetration Testing Technical Concepts

Penetration testing is a simulated cyber attack against a computer system to evaluate its security. Here are the tools and methods used in this ecosystem:

### 1.1 DAST (Dynamic Application Security Testing)
**DAST (Dynamic Application Security Testing)** is a security testing method that involves directly interacting with a running application. Unlike SAST, DAST tests the application from the outside (Black Box Testing) to find vulnerabilities that only appear during runtime.

![Open ZAP](ss/7-owaps-zap-alert-list-result-scan.png)

### 1.2 SAST (Static Application Security Testing)
SAST analyzes the application's source code without running it. This helps find security flaws early in the development cycle (Shift Left Security).
- **Main Tool:** SonarQube.
- **Integration:** Integrated into the Automated CI/CD pipeline.
- **Reference:** [CI/CD Best Practice & Security](https://github.com/dendie851/ci-cd-best-practice)

![SonarQube & Trivy Analysis](ss/ss-devoop-sonarcub-trivy.png)

By combining **SAST** at the code level and **DAST** at the running application level, we can minimize attack risks before the application goes to production. This lab proves how crucial security testing is in the Software Development Life Cycle (SDLC): Network,

### 1.3 Vulnerability Scanning (Container Security)
Scans docker images and library dependencies to detect known vulnerabilities (CVEs).
- **Main Tool:** Trivy.
- **Reference:** [Trivy Scanner in CI/CD](https://github.com/dendie851/ci-cd-best-practice)

![SonarQube & Trivy Analysis](ss/ss-devoop-sonarcub-trivy.png)

### 1.4 Network Security Testing & Anti-DDoS
Protects infrastructure from network-level attacks such as Brute Force and DDoS (Distributed Denial of Service).
- **Solution:** Firewall and Anti-DDoS implementation.
- **Reference:** [DIY Anti-DDoS Solution](https://github.com/dendie851/diy-anti-dos)

![Anti-DDoS Implementation](ss/ss-anti-dos.png)

---

## 2. Understanding DAST & OWASP Top 10

**DAST (Dynamic Application Security Testing)** is a security testing method that involves directly interacting with a running application. Unlike SAST, DAST tests the application from the outside (Black Box Testing) to find vulnerabilities that only appear during runtime.

### OWASP Top 10
The testing in this lab refers to the **OWASP Top 10** standard, which is a list of the 10 most critical web application security risks, including:
1. **Broken Access Control**
2. **Cryptographic Failures**
3. **Injection (SQLi, NoSQL, etc.)**
4. **Insecure Design**
5. **Security Misconfiguration**
6. **Vulnerable and Outdated Components**
7. **Identification and Authentication Failures**
8. **Software and Data Integrity Failures**
9. **Security Logging and Monitoring Failures**
10. **Server-Side Request Forgery (SSRF)**

---

## 3. OWASP ZAP: The DAST Powerhouse

**OWASP ZAP (Zed Attack Proxy)** is the world's most popular open-source security tool for performing DAST.

### Main Functions in This Lab:
- **Spidering:** Crawls the entire application URL structure.
- **Active Scanning:** Performs simulated attacks to find SQL Injection, XSS, etc.
- **AJAX Spidering:** Crawls modern applications that use heavy JavaScript/AJAX.
- **Proxying:** Captures traffic between the browser and the server for manual analysis.

---

## 4. Lab Implementation Guide

### 🚀 Step 1: Installation & Deployment
You can install ZAP natively on Windows or use Docker for an isolated environment.

| Method | Guide Screenshot |
|  |  |
| **Windows Native** | ![Install Windows](ss/33-install-openzap-di-windows.png) |
| **Docker Compose** | ![Deploy Docker](ss/1-deploy-tools-docker.png) |

Use the following command if using Docker:
```bash
docker-compose up -d
```

### 🌐 Step 2: Access Dashboard & Target
After deployment, access the ZAP dashboard and ensure the target application is running.
- **Target App:** `http://localhost:3000` ![Target Web](ss/2-target-web-apps-pentest.png)
- **ZAP Web UI:** `http://localhost:8090/zap` ![ZAP UI](ss/3-owaps-zap-first-access.png) ![ZAP UI 2](ss/4-owaps-zap-first-access-2.png)

### 🔎 Step 3: Proxy Configuration (Manual Explore)
Use **FoxyProxy** in Chrome to direct traffic to the ZAP Proxy (Port 8081) so ZAP can "learn" the application while you use it manually.

![FoxyProxy Setup](ss/30-owaps-test-scan-target-manul-show-port-proxy-zap-in-chrome-menggunakan-foxy-proxy.png)
![ZAP Proxy Port](ss/28-owaps-test-scan-target-manul-show-port-proxy-zap.png)
![Chrome Proxy Set](ss/32-owaps-test-scan-target-manul-show-port-proxy-zap-in-chrome-set-proxy.png)

### ⚡ Step 4: Running Security Scans (Automated)
You can run automated scans using the **Automated Scan** or **AJAX Spider** features.

| Automated Scan | AJAX Spider / Vulnerability |
|  |  |
| ![Auto Scan](ss/5-owaps-zap-auto-scan.png) | ![AJAX Scan](ss/5-owaps-zap-auto-scan-ajax-scan.png) |
| ![Scan Launch](ss/27-owaps-test-scan-target-untuk-test-url-sebagai-target-yg-akan-scan-dan-automatic-launch-browser.png) | ![Vulnerability Scan](ss/6-owaps-zap-auto-scan-vurnability.png) |

---

## 5. Vulnerability Analysis & Reports

ZAP will categorize findings based on risk levels.

### 🚩 List of Findings (Alerts)
![Alert List](ss/7-owaps-zap-alert-list-result-scan.png)

### 💡 Vulnerability Details & Solutions
ZAP provides in-depth explanations and how to fix them (Remediation).

| Vulnerability Type | Detail Screenshot |
|  |  |
| **SQL Injection** | ![SQLi](ss/8-owaps-zap-alert-list-result-sample-potensial-sql-injection-diberi-solusinya.png) |
| **Cross Site Scripting (XSS)** | ![XSS](ss/10-owaps-zap-alert-list-result-sample-potensial-pontesial-xss.png) |
| **Cross-Domain Misconfig** | ![Cross Domain](ss/11-owaps-zap-alert-list-result-sample-potensial-cross-domain.png) |
| **Click Jacking** | ![Click Jack](ss/12-owaps-zap-alert-list-result-sample-potensial-click-jack.png) |
| **Content Security Policy** | ![CSP](ss/9-owaps-zap-alert-list-result-sample-potensial--anti-iframe-conten-security-policy.png) |

### 🔍 Additional Information (Info Disclosure)
ZAP also detects information leaks such as application errors or server configurations.
- **Application Error:** ![Error](ss/13-owaps-zap-alert-list-result-show-info-app-error.png) ![Error 2](ss/14-owaps-zap-alert-list-result-show-info-app-error-2.png)
- **Config Disclosure:** ![Config](ss/15-owaps-zap-alert-list-result-show-info-app-show-configuration.png) ![Config 2](ss/16-owaps-zap-alert-list-result-show-info-app-show-configuration-2.png)
- **Sniffing Info:** ![Sniffing](ss/17-owaps-zap-alert-list-result-show-info-sniping.png)

### 📊 Final Report (Reporting)
Generate reports for stakeholders in various formats.

![Report List](ss/18-owaps-zap-report.png)
![Report Download](ss/20-owaps-zap-report--download.png)
![Full Report](ss/21-owaps-zap-report-show.png)
![Report Detail](ss/22-owaps-zap-report-show-2.png)

---

## 6. Advanced Features & Exploration
Some additional features practiced in this lab:

- **Authentication Handling:** Scanning areas that require login manually, using ZAP auth, or specifying the target URL to scan.
  ![Auth Scan](ss/25-owaps-test-scan-target-have_auth-set-manual-explore.png)
- **Active Recording:** Recording user activity for further analysis.
  ![Active Record](ss/31-owaps-test-scan-target-manul-show-port-proxy-zap-in-chrome-active-record.png)

---

## 🛡️ Conclusion
By combining **SAST** at the code level and **DAST** at the running application level, we can minimize attack risks before the application goes to production. This lab proves how crucial security testing is in the Software Development Life Cycle (SDLC).
