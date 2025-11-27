# ZAP by Checkmarx Scanning Report - Round 2

## Summary of Alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 0 |
| Medium | 1 |
| Low | 0 |
| Informational | 1 |

## Alerts

| Name | Risk Level | Number of Instances |
| --- | --- | --- |
| Absence of Anti-CSRF Tokens | Medium | 1 |
| User Agent Fuzzer | Informational | 12 |

## Alert Detail

### [ Absence of Anti-CSRF Tokens ](https://www.zaproxy.org/docs/alerts/10202/)

*   **Risk Level:** Medium
*   **Description:** No Anti-CSRF tokens were found in a HTML submission form. A cross-site request forgery is an attack that involves forcing a victim to send an HTTP request to a target destination without their knowledge or intent.
*   **URL:** http://localhost:8001/register
*   **Method:** `GET`
*   **Evidence:** `<form action="/register" method="POST">`
*   **Analysis:** The form accepts a POST request to create a user but lacks a hidden randomized token. This allows attackers to forge requests.

### [ User Agent Fuzzer ](https://www.zaproxy.org/docs/alerts/10104/)

*   **Risk Level:** Informational
*   **Description:** Check for differences in response based on fuzzed User Agent.
*   **URL:** http://localhost:8001/register
