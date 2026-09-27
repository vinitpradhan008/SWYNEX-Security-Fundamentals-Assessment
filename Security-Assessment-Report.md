Security Fundamentals Assessment

 1. Assessment Overview

Target:
OWASP Juice Shop

Environment:
Local authorized lab environment

Target URL:
http://localhost:3000

Testing Scope:
Authentication and client-side input handling.

 2. Test 1 — Invalid Login Handling

Affected Component:
User Login

Endpoint:
POST /rest/user/login

Test:
Invalid credentials were submitted.

Observed Result:
HTTP 401 Unauthorized was returned.

Assessment:
The application rejected the invalid authentication attempt.
No vulnerability was established from this test.
Evidence:
evidence/01-invalid-login-401.png

 3. Finding 1 — SQL Injection Authentication Bypass

Affected Component:
User Login

Endpoint:
POST /rest/user/login

Risk:
A crafted input was accepted in a way that resulted in successful
authentication without valid credentials. This demonstrates an
authentication bypass caused by SQL injection.

Impact:
An attacker could potentially gain unauthorized access to an account
without knowing the legitimate password.

Evidence:
evidence/02-sql-injection-auth-bypass.png

Severity:
High

Recommended Mitigation:
- Use parameterized queries/prepared statements.
- Never concatenate user-controlled input into SQL queries.
- Validate input on the server side.
- Use secure database access patterns.
- Add authentication bypass tests to the security test suite.

- 
 4. Finding 2 — DOM-Based Cross-Site Scripting

Affected Component:
Search functionality

Risk:
Attacker-controlled input was interpreted as executable JavaScript in
the browser.

Impact:
Successful exploitation of DOM XSS can allow malicious JavaScript to
execute in a victim's browser in the context of the application.

Evidence:
evidence/03-dom-xss.png

Severity:
High

Recommended Mitigation:
- Treat all client-side input as untrusted.
- Avoid unsafe HTML/DOM insertion of user-controlled data.
- Prefer safe DOM APIs such as textContent where appropriate.
- Apply context-appropriate output encoding.
- Implement a restrictive Content Security Policy.

- 
 5. Summary

The assessment was performed exclusively against the locally hosted
OWASP Juice Shop training environment.

Two security findings were successfully demonstrated:

1. SQL Injection leading to authentication bypass.
2. DOM-Based Cross-Site Scripting.

The invalid-login test also confirmed that the application returned
HTTP 401 Unauthorized for the tested invalid credentials.

Evidence:
evidence/01-invalid-login-401.png
