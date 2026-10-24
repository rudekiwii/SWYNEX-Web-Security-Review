# Web Security Review Report

## 1. Project Overview

- **Internship:** SWYNEX
- **Task:** Task 3 — Web Security Review
- **Application:** OWASP Juice Shop
- **Environment:** Local Windows lab at `http://localhost:3000`
- **Tools:** Browser Developer Tools, Network panel, Application panel

## 2. Objective

Perform a defensive review of a deliberately vulnerable training application, observe common web security controls, and document evidence-based findings and remediation recommendations.

## 3. Scope and Methodology

The review was limited to the local OWASP Juice Shop instance. Activities included inspecting HTTP response headers, a public application-configuration response, browser storage and cookies, and the login and registration interfaces.

No third-party systems were targeted.

## 4. Observations

### 4.1 HTTP Response Headers

The inspected main document response showed:

- `X-Content-Type-Options: nosniff`
- `X-Frame-Options: SAMEORIGIN`
- `Access-Control-Allow-Origin: *`
- No visible `Content-Security-Policy` header
- No visible `Content-Security-Policy-Report-Only` header

**Assessment:** The absence of a visible CSP header is a potential defense-in-depth improvement. The risk depends on application behavior and other controls. The wildcard CORS header requires resource-specific analysis before any security impact can be concluded.

### 4.2 Application Configuration

The `application-configuration` endpoint returned HTTP `200 OK` and displayed general application settings, including the application name and local server configuration.

**Assessment:** The reviewed excerpt did not establish exposure of a password, private key, or other secret. Public configuration data alone is not sufficient evidence of a vulnerability.

### 4.3 Browser Storage

The Local Storage view for `http://localhost:3000` appeared empty during inspection.

**Assessment:** This observation applies only to the inspected Local Storage view and does not establish that all client-side storage mechanisms are empty.

### 4.4 Cookies

The browser displayed the following preference-related cookies:

- `cookieconsent_status`
- `language`
- `welcomebanner_status`

Their displayed values indicated consent, language, and welcome-banner preferences. The screenshot did not establish an authentication-cookie vulnerability.

### 4.5 Login and Registration Interfaces

The login page displayed email and password fields, a password visibility control, a remember-me option, password recovery, and registration links.

The registration interface displayed a password length message of 5–40 characters, while the password advice listed a minimum of eight characters and requirements for lowercase, uppercase, numeric, and special characters.

**Assessment:** This is a UI guidance inconsistency worth validating. Server-side password enforcement was not tested, so it is not reported as a confirmed security vulnerability.

## 5. Findings and Priority

### Finding 1 — Content Security Policy Not Observed

- **Priority:** Informational / Low
- **Evidence:** Main document response headers
- **Impact:** Without a suitable CSP, the application may have fewer browser-enforced protections against certain content-injection attacks.
- **Recommendation:** Design a restrictive policy appropriate to the application. Test it using `Content-Security-Policy-Report-Only` before enforcement and verify that legitimate application features continue to work.
- **Status:** Preliminary observation; further validation required.

### Finding 2 — Wildcard CORS Header

- **Priority:** Informational; impact not established
- **Evidence:** `Access-Control-Allow-Origin: *` was observed on the inspected responses.
- **Impact:** A wildcard origin can be appropriate for public resources but may be unsuitable for sensitive resources.
- **Recommendation:** Review CORS settings per endpoint and restrict origins where cross-origin access is not intended. Verify whether sensitive data or credentialed requests are involved before assigning severity.
- **Status:** No exploitable CORS issue confirmed.

### Finding 3 — Password Guidance Inconsistency

- **Priority:** Informational / Low
- **Evidence:** Registration UI showed a 5–40 character length message and separate advice requiring at least eight characters.
- **Impact:** Inconsistent guidance can confuse users about password requirements.
- **Recommendation:** Align the visible guidance with the actual server-side password policy and test enforcement on the server.
- **Status:** UI observation; backend enforcement not verified.

## 6. Limitations

This review was limited to the local training application and the screenshots captured during inspection. It did not include a full authenticated test, comprehensive API testing, or validation of all server-side security controls. No confirmed exploitable vulnerability is claimed based on the collected evidence.

## 7. Conclusion

The review documented visible HTTP security headers, public configuration information, browser storage, preference cookies, and login and registration UI behavior. The main recommendations are to assess an appropriate CSP, validate CORS behavior for individual resources, and align password guidance with server-side enforcement.

## 8. Evidence

Supporting screenshots should be placed in the `evidence/` directory. Each screenshot should correspond to an observation described in this report.
