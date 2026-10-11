# Referer-Based Access Control

**Platform:** PortSwigger Web Security Academy  
**Category:** Access Control / Header-Based Access Control  
**Difficulty:** Apprentice  
**Tool:** Burp Suite Community Edition  
**Status:** Solved  

## 1. Objective
Bypass administrative access controls by forging or replaying a valid administrative `Referer` HTTP header.

## 2. Vulnerability Overview
Some applications rely on the HTTP `Referer` header to determine whether a request originated from an administrative context, assuming that users cannot easily spoof this header (which is incorrect).

## 3. Testing Methodology
1. **Analyze Admin Traffic:** Observe how administrative actions include a specific `Referer` header pointing to an admin page.
2. **Perform Action as Regular User:** Send a request as a standard user and notice it gets blocked.
3. **Inject Referer Header:** Add or modify the `Referer` header in Burp Suite Repeater to match the administrative URL structure expected by the application.
4. **Verify Success:** Submit the modified request and verify that the action executes successfully.

## 4. Remediation
- Do not rely on client-supplied headers like `Referer` for security or authorization decisions. Use robust session-based role checks instead.
