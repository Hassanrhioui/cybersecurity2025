# 📘 Logbook

| Date       | Used hours | Subject(s)             | Outcome(s)        |
|-------------|-------------|------------------------|-------------------|
| 28.10.2025  | 2           |-Preparing the course   |-clear instructions   |
| 29.10.2025  | 2           |-started cisco course   |-module 1 of cyber security and data privacy|     |
| 2.11.2025  | 2            |-cisco course   |-module 2    |
| 2.11.2025  | 1            |-indepandent search   |-deep dive into CS & DP   |
| 4.11.2025  | 2            |-cisco course   |-module 3    |
| 4.11.2025  | 3             |-cisco course   |-module 4, 5 and final exam    |
| 4.11.2025  |4             |-dive into burp suite <br>- dive into portSwingger<br>-Authentification    |-clear idea about burp suite <br> -**Lab1**: Username enumeration via different responses <br> -**Lab2**: 2FA simple bypass  |
| 7.11.2025  | 2           | SQL injections   |-SQL injections<br>-**Lab3**: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data<br>-**Lab4**: SQL injection vulnerability allowing login bypass    |
| 13.11.2025  | 4            |-Access control<br>-reflections  |-**Lab5**: unprotected admin functionality<br>-**Lab6**: unprotected admin functionality with unpredictable URL<br>-Reflections   |
| 16.11.2025  | 2             |-Access control labs   |-**Lab7**: User role controlled by request parameter <br>-**Lab8**: User role can be modified in user profile    |
| 18.11.2025  | 6            |-Penetration testing of Booking System -Phase 1  |-Set up a local testing environment |
| 19.11.2025  | 6            |-Penetration testing of Booking System -Phase 1  |-used OWASP ZAP to analyze the registration page, identified multiple vulnerabilities, documented findings in a structured report, and some reflections  |

| 26.11.2025  |  6           |-going through some recorings, documentations and practice  |-practice in docker, Linux    |
| 27.11.2025  | 5             |-pen testing of part2<br>-reports: part1 and part2    |-Deployed Phase 1 Part 2 application. Performed OWASP ZAP scan (Round 2). |
| 28.11.2025  | 5             |-pen testing of part2<br>-reports: part1 and part2    |-Analyzed results comparing Part 1 and Part 2. Verified fixes manually. Wrote functionality test report and discussion forum post.    |
| 28.11.2025| 3    |-dicussion report|-report about what was fixed from part 1|
| 05.12.2025  | 6  |-	Step 1: Application Deployment<br>-Step 2: ZAP Re-Test (Round 3)<br>-Step 3A: Panopto & DB Access<br>-Step 3B: Password Cracking Execution<br>-Report Compilation (Cracking)  |-Docker environment for Phase 2 deployed and accessed on http://localhost:8002. Verified application functionality.<br>-Performed manual browsing to explore Phase 2 changes. Ran OWASP ZAP Baseline Scan on the new URL. Generated zap_report_round3.md.<br>-Watched the required Panopto video.|
| 06.12.2025  | 6 |-	Step 1: Application Deployment<br>-Step 2: ZAP Re-Test (Round 3)<br>-Step 3A: Panopto & DB Access<br>-Step 3B: Password Cracking Execution<br>-Report Compilation (Cracking)  |- Identified the hashing algorithm (MD5) and obtained the password hashes/user list from the database.<br>-Installed Hashcat and prepared the rockyou.txt wordlist. Ran Dictionary Attacks and targeted Mask/Brute-Force attacks. Successfully cracked 5 passwords.<br>-Prepared the detailed written explanation, captured and edited 5 screenshots, and wrote the answers to the three analytical questions.<br>-**Lab9**-for the lab of path traversal:first we look for the http image then we send it to repeater, after trying /etc/passwd it did work because of the path so we have to add different path to access. which is ../../../../ect/password|
|08.12.2025| 5|-Deployment, Testing, & Tool Setup|-Set up the new test app. Checked basic Guest/Reserver web pages. Ran ZAP scan. Found: GDPR Problem (Website shows who booked) and Admin/Reserver functions work as expected.|
|09.12.2025|6|-Advanced Testing & Final Report|-Tried hacking (Gobuster/wfuzz) to find hidden pages. Tested Admin deleting users. Found: Two CRITICAL HACKING FLAWS: 1) A hidden link that lets Guests see all resources (IDOR). 2) RCE/SSTI test code worked on the reservation page. Final report was finished.|


