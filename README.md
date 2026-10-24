# SWYNEX — Web Security Review

## Overview
This project documents a defensive web security review of a local OWASP Juice Shop training application completed as Task 3 of my SWYNEX internship.

## Objective
Review visible web security controls, inspect browser storage and cookies, and document observations with appropriate limitations and remediation recommendations.

## Tools Used
- OWASP Juice Shop
- Browser Developer Tools
- Network panel
- Application panel

## Review Activities
- Inspected HTTP response headers.
- Reviewed the application-configuration response.
- Examined Local Storage and browser cookies.
- Inspected login and registration interfaces.
- Reviewed the password guidance shown by the registration form.

## Key Observations
- `X-Content-Type-Options: nosniff` and `X-Frame-Options: SAMEORIGIN` were observed.
- A Content Security Policy header was not visible in the inspected main document response.
- A wildcard CORS header was observed; its security impact was not established.
- The registration UI displayed inconsistent password-length guidance that requires further validation.

These are preliminary observations, not claims of confirmed exploitable vulnerabilities.

## Report
See [web-security-review-report.md](web-security-review-report.md) for scope, evidence, priority, limitations, and recommendations.

## Evidence
Supporting screenshots are stored in the [`evidence/`](evidence/) directory.

## Disclaimer
Testing was limited to an authorized local training environment. No third-party systems were targeted.

