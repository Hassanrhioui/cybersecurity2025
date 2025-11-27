# ZAP Scanning Report - Round 1

**Date:** 2025-11-27
**Target:** http://localhost:8000
**Scanner:** OWASP ZAP (via Checkmarx)

## 1. Summary of Alerts

| Risk Level | Number of Alerts |
| :--- | :--- |
| **High** | **2** |
| **Medium** | **4** |
| Low | 1 |
| Informational | 1 |

## 2. Detailed Alerts

### 2.1. High Risk

#### [Path Traversal](https://www.zaproxy.org/docs/alerts/6/)
*   **Description:** The application allows access to files and directories outside the web root via the manipulation of input variables.
*   **URL:** `http://localhost:8000/register`
*   **Method:** `POST`
*   **Parameter:** `username`
*   **Attack:** `register` (Context implies manipulation of file paths)
*   **Evidence:** The scanner was likely able to access or infer access to restricted files.

#### [SQL Injection](https://www.zaproxy.org/docs/alerts/40018/)
*   **Description:** The application appears to concatenate user input directly into database queries, allowing attackers to manipulate the query structure.
*   **URL:** `http://localhost:8000/register`
*   **Method:** `POST`
*   **Parameter:** `username`
*   **Attack:** `'`
*   **Evidence:** `HTTP/1.1 500 Internal Server Error` (Database error triggered by syntax error).

---

### 2.2. Medium Risk

#### [Absence of Anti-CSRF Tokens](https://www.zaproxy.org/docs/alerts/10202/)
*   **Description:** No Anti-CSRF tokens were found in the HTML submission form. This allows attackers to forge requests on behalf of a victim.
*   **URL:** `http://localhost:8000/register`
*   **Evidence:** `<form action="/register" method="POST">`

#### [Content Security Policy (CSP) Header Not Set](https://www.zaproxy.org/docs/alerts/10038/)
*   **Description:** The `Content-Security-Policy` header is missing, making the site harder to defend against XSS and data injection attacks.
*   **Locations:** Root `/` and `/register`.

#### [Format String Error](https://www.zaproxy.org/docs/alerts/30002/)
*   **Description:** The submitted data is evaluated as a command by the application (specifically formatted strings like `%s` or `%n`).
*   **URL:** `http://localhost:8000/register`
*   **Parameter:** `username`
*   **Attack:** `ZAP%n%s%n%s...`
*   **Evidence:** The script closed the connection on a `/%s`, indicating improper string handling in the backend.

#### [Missing Anti-clickjacking Header](https://www.zaproxy.org/docs/alerts/10020/)
*   **Description:** The response does not include `X-Frame-Options` or `Content-Security-Policy` with `frame-ancestors`, allowing the site to be framed by attackers.
*   **Locations:** Root `/` and `/register`.

---

### 2.3. Low & Informational Risk

*   **X-Content-Type-Options Header Missing (Low):** The header `X-Content-Type-Options: nosniff` is missing, allowing MIME-sniffing.
*   **User Agent Fuzzer (Informational):** The server responds differently based on the User-Agent string provided.
