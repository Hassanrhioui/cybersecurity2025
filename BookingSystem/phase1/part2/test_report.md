#  Report – 2

## 1️⃣ Introduction

| Field | Value |
|-------|--------|
| **Tester(s):** | Hassan Rhioui |
| **Name:** | round 2 of tests|
| **Purpose:** | Re-test the target application to verify the successful remediation of Critical/High-risk vulnerabilities identified in Round 1 and to assess any remaining or newly introduced issues. |
| **Scope – Tested components:** | http://localhost:8001/, /register endpoint |
| **Scope – Exclusions:** | Underlying Operating System, Network Infrastructure, External Services |
| **Test approach:** | Black-box |
| **Test environment & dates – Start:** | 2025-11-22 (Placeholder) |
| **Test environment & dates – End:** | 2025-11-22 (Placeholder) |
| **Test environment details:** | Target is running on http://localhost:8001/. The target URL has been updated (Port 8001). |
| **Assumptions & constraints:** | Fixes for Round 1 issues (SQLi, Path Traversal) were successfully deployed before this re-test. |


---

## 2️⃣ Executive Summary

| Field | Value |
|--------|--------|
| **Short summary (1–2 sentences):** | Round 2 scan confirms that all previously identified Critical and High-risk vulnerabilities have been successfully remediated, significantly improving the application's security posture. The primary remaining security issue is a Medium-risk vulnerability concerning the absence of Anti-CSRF tokens. |
| **Overall risk level:** | Medium |
| **Top 5 immediate actions:** |  
| **1.** | Immediately implement unique, cryptographically secure Anti-CSRF Tokens in the /register POST form to prevent Cross-Site Request Forgery.  | 
| **2.** | Verify the successful implementation of fixes for SQL Injection and Path Traversal (originally High/Critical issues).   | 
| **3.** | Implement the `X-Frame-Options: DENY` or a `frame-ancestors` directive to prevent the previously identified Clickjacking issue.  | 
| **4.** | Configure the web server to set a robust Content Security Policy (CSP) header to mitigate injection attacks.  | 
| **5.** | Configure the web server to set the `X-Content-Type-Options: nosniff` header for system hardening.  | 


---

## 3️⃣ Severity scale & definitions

| Severity Level | Description | Recommended Action |
|----------------|-------------|--------------------|
| 🔴 **High** | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | Immediate fix required |
| 🟠 **Medium** | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF). | Fix ASAP |
| 🟡 **Low** | A minor issue or configuration weakness (e.g., server version disclosure). | Fix soon |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers). | Monitor and fix in maintenance |


---

## 4️⃣ Findings

| ID | Severity | Finding | Description | Evidence / Proof |
|-----|----------|----------|--------------|---------------------|
| **F-01** | 🟠 Medium | Absence of Anti-CSRF Tokens | The form on http://localhost:8001/register using a POST method still lacks an Anti-CSRF token, making the action vulnerable to Cross-Site Request Forgery (CSRF). | URL: http://localhost:8001/register, Evidence: `<form action="/register" method="POST">` |
| **F-02** | 🔵 Info | User Agent Fuzzer | The scan performed a test to check for differing responses based on various User Agents. No direct risk, but noted for completeness. | URL: http://localhost:8001/register, Instances: 12 |
| **F-03** | 🔴 High (Resolved) | SQL Injection / Path Traversal | These two High-risk findings from Round 1 were not detected in Round 2, indicating successful remediation. | – |
| **F-04** | 🟠 Medium (Likely Unaddressed) | Missing Security Headers | Multiple Medium/Low security header issues (X-Frame-Options, CSP, X-Content-Type-Options) from Round 1 are likely still present but were not explicitly triggered or detected in this Round 2 baseline scan. | – |

5️⃣ OWASP ZAP Test Report (Attachment)
[Open ZAP Report](./zap_report_round2.md)
