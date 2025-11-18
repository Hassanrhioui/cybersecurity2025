# Booking System Phase 1 – Penetration Test Report

## 1. Scope
**Target:** Registration page of Booking System  
**Goal:** Identify functionality and security flaws using OWASP ZAP testing.

## 2. Methodology
- **Environment:** Local Booking System running at localhost:8000  
- **Tools:** OWASP ZAP (passive scan, active scan, fuzzing), browser manual tests  
- **Approach:**  
  1. Functional testing (valid/invalid inputs, duplicates, weak passwords)  
  2. Passive scanning (headers, CSRF, clickjacking)  
  3. Active scanning (SQLi, Path Traversal, fuzzing)  
  4. Evidence collection (screenshots, ZAP alerts)

## 3. Detailed Evidence

### Path Traversal
- **Request:** POST /register with crafted `username` parameter  
- **Impact:** Potential access to files outside web root  
- **Fix:** Strict input validation, allow-list filenames, block directory traversal sequences

### SQL Injection
- **Request:** POST /register with payload `'` in `username`  
- **Evidence:** Server returned `HTTP/1.1 500 Internal Server Error`  
- **Impact:** Possible bypass of authentication or data manipulation  
- **Fix:** Parameterized queries, ORM usage, input sanitization

### Absence of Anti-CSRF Tokens
- **Observation:** Registration form lacks CSRF protection  
- **Evidence:** `<form action="/register" method="POST">` with no CSRF token field  
- **Impact:** Attacker could trick users into unwanted registrations  
- **Fix:** Implement CSRF tokens in all forms, use frameworks with built-in CSRF protection

### CSP Header Not Set
- **Observation:** No CSP header in responses for `/` and `/register`  
- **Impact:** Increased risk of XSS and content injection  
- **Fix:** Add strict CSP header (e.g., `default-src 'self'`)

### Format String Error
- **Request:** POST /register with payload `ZAP%n%s...` in `username`  
- **Observation:** Connection closed, potential format string vulnerability  
- **Impact:** Could allow arbitrary code execution or crashes  
- **Fix:** Sanitize input, avoid unsafe string formatting, recompile with safe libraries

### Missing Anti-clickjacking Header
- **Observation:** No `X-Frame-Options` or CSP `frame-ancestors` directive in responses  
- **Impact:** Vulnerable to clickjacking attacks  
- **Fix:** Add `X-Frame-Options: DENY` or CSP `frame-ancestors 'none'`

### X-Content-Type-Options Header Missing
- **Observation:** No `X-Content-Type-Options` header in responses for `/`, `/register`, and static files  
- **Impact:** Browser may misinterpret MIME types, leading to attacks  
- **Fix:** Add `X-Content-Type-Options: nosniff`

### User Agent Fuzzer
- **Observation:** Application responded differently to multiple User-Agent strings (IE, Chrome, Firefox, bots)  
- **Impact:** Could reveal inconsistencies or hidden functionality exploitable by attackers  
- **Fix:** Standardize responses, monitor logs for unusual User-Agent activity

## 4. Conclusion
The Booking System registration page contains multiple high-risk vulnerabilities (SQL Injection, Path Traversal) and several medium-risk issues (missing headers, CSRF). Immediate remediation should prioritize **input validation, secure coding practices, and proper security headers**.  

## 5. Reflection
As a beginner using OWASP ZAP, I learned how automated scanning highlights common web application flaws. The most challenging part was interpreting alerts and understanding their real-world impact. For example, SQL Injection and Path Traversal are critical because they can directly compromise data, while missing headers like CSP or X-Frame-Options are more subtle but still important for defense in depth.  

This exercise taught me:
- How to set up a penetration testing environment with ZAP and a local app  
- The importance of combining manual functional tests with automated scans  
- That security is layered: fixing input validation alone is not enough without proper headers and CSRF protection  

Overall, the assignment showed me how penetration testing is both technical and analytical, requiring evidence collection and clear reporting.

## 6. Attachments
- **ZAP_Report.html** (full scan output)  
- **Screenshots** (optional, stored in Evidence folder)
