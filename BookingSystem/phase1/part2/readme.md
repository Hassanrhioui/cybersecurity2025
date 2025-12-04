# Booking System Security - Phase 1 Part 2

## Overview
This folder contains the results of the second round of testing for the Booking System application. After reporting the initial vulnerabilities in Part 1, we received an updated version of the application. The goal of this phase was to verify which vulnerabilities were fixed and which ones are still present.

## Testing Process
1.  **Deployment:** Deployed the updated application code (Phase 1 Part 2) locally on port 8001.
2.  **Automated Scanning:** Ran multiple full "Active Scan" using OWASP ZAP to catch any remaining technical flaws.
3.  **Manual Verification:** Manually attempted to exploit the previous "High Risk" findings (specifically SQL Injection) to confirm the fixes were real.
4.  **Comparison:** Compared `zap_report_round1.md` with the new `zap_report_round2.md`.

## Summary of Findings

### 1. What was Fixed? (The Good News)
fixed the most critical issues we found in Part 1.
*   **SQL Injection:** I attempted to bypass the login using the previous exploit (`' OR '1'='1`), but it no longer works. The application now handles the input correctly.
*   **Path Traversal:** ZAP no longer flags the `username` parameter as vulnerable to file system access.
*   **Security Headers:** The missing header alerts (like CSP and Clickjacking protection) have been resolved.

The ZAP report for Round 2 now shows **0 High Risk** alerts.

## Conclusion
The security of the application has improved significantly because the critical "High" risks are gone.
