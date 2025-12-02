# Security Scanning

## Overview
This repository implements multiple layers of security scanning to identify vulnerabilities and ensure code and application integrity. The scans include **SAST**, **SCA**, and **DAST**.

---

### SAST (Static Analysis with CodeQL)
- **Purpose:** Scans source code for vulnerabilities and insecure coding patterns.
- **Trigger:** Runs automatically on push to the `main` branch.
- **Checks for:**
  - SQL Injection
  - Cross-Site Scripting (XSS)
  - Hardcoded secrets
  - Command injection
  - Security misconfigurations in code
- **Artifacts:** See the [GitHub Security tab](https://github.com/<your-org>/<your-repo>/security/code-scanning) for detailed reports.

---

### SCA (Dependency Check)
- **Purpose:** Scans dependencies (Python packages) for known CVEs and insecure versions.
- **Trigger:** Runs automatically on push to the `main` branch.
- **Checks for:**
  - Known vulnerabilities in Python packages
  - Outdated or deprecated packages
  - License compliance issues
- **Artifacts:** See `sca-reports` folder in repository or workflow artifacts.

---

### DAST (Live Application with ZAP)
- **Purpose:** Tests running applications for runtime vulnerabilities.
- **Trigger:** Runs on push to the `main` branch or manually via workflow.
- **Checks for:**  
  Based on OWASP ZAP baseline scan findings:
  - **10020 – Missing Anti-clickjacking Header**: Prevents clickjacking attacks.
  - **10021 – X-Content-Type-Options Header Missing**: Prevents MIME-sniffing and XSS.
  - **10036 – Server Leaks Version Info**: Prevents information disclosure of server version.
  - **10038 – Content Security Policy (CSP) Header Not Set**: Prevents XSS & injection attacks.
  - **10049 – Storable and Cacheable Content**: Prevents caching of sensitive data.
  - **10063 – Permissions Policy Header Not Set**: Prevents abuse of powerful browser APIs.
  - **10109 – Modern Web Application**: Tracks missing modern security headers.
  - **90004 – Insufficient Site Isolation Against Spectre Vulnerability**: Prevents Spectre attacks.
  - **90005 – Sec-Fetch-Dest Header Missing**: Protects against request misrouting.
- **Artifacts:** 
  - `zap-baseline-reports`
  - `zap-fullscan-reports`
  - Reports include full URLs scanned and identified vulnerabilities.

---

## Understanding Results
- Each scan produces structured output in HTML, JSON, or Markdown.
- **ZAP Reports**: Include issue code, affected URL, risk level, and remediation guidance.  

Issue Summary:

| Code   | Issue                                               | Risk Level | Affected                                      | Why It Matters |
|--------|-----------------------------------------------------------|------------|------------------------------------------------------|------------------------------------|
| 10020  | Missing Anti-clickjacking Header                          | Medium     | http://localhost:5000                                | Prevents **clickjacking attacks** where attackers embed your site in an iframe and trick users into clicking hidden elements. |
| 10021  | X-Content-Type-Options Header Missing                     | Low        | http://localhost:5000                                | Prevents **MIME-sniffing**, which can cause the browser to interpret files as a different content type, enabling XSS. |
| 10036  | Server Leaks Version Information (Server Header)          | Low        | http://localhost:5000, http://localhost:5000/robots.txt, http://localhost:5000/sitemap.xml | Prevents **information disclosure**—revealing server version helps attackers target known vulnerabilities. |
| 10038  | Content Security Policy (CSP) Header Not Set              | Medium     | http://localhost:5000, http://localhost:5000/robots.txt | Helps prevent **Cross-Site Scripting (XSS)** & injection attacks by limiting what scripts, resources, and domains are allowed. |
| 10049  | Storable and Cacheable Content                            | Informational        | http://localhost:5000, http://localhost:5000/robots.txt, http://localhost:5000/sitemap.xml | Prevents sensitive content being **cached** on shared devices or proxies, reducing info leakage. |
| 10063  | Permissions Policy Header Not Set                         | Low        | http://localhost:5000, http://localhost:5000/robots.txt, http://localhost:5000/sitemap.xml | Prevents misuse of powerful browser APIs (camera, mic, geolocation) by controlling which features the page is allowed to use. |
| 10109  | Modern Web Application                                   | Informational | http://localhost:5000                                | Indicates missing modern security headers; helps track **best-practice hardening gaps**. |
| 90004  | Insufficient Site Isolation Against Spectre Vulnerability | Low        | http://localhost:5000 (x3)                            | Prevents Spectre-class **side-channel attacks** by enforcing process isolation in browsers. |
| 90005  | Sec-Fetch-Dest Header Missing                             | Informational        | http://localhost:5000, http://localhost:5000/robots.txt, http://localhost:5000/sitemap.xml (x12) | Protects against **request smuggling & CSRF-like misrouting** by declaring the request’s intended destination context. |

---

## Reporting Vulnerabilities
- If you discover a potential security issue, please **do not open a public issue**.
- Email your findings to: **security@example.com**
- Include:
  - Description of the issue
  - Steps to reproduce
  - Any relevant logs or screenshots
  - Suggested remediation (if applicable)

---

## Workflow Links
- **SAST:** `.github/workflows/1-sast-only.yml`  
- **SCA:** `.github/workflows/2-sca-only.yml`  
- **DAST:** `.github/workflows/3-dast-only.yml`
