# Unprotected Admin Functionality

**Platform:** PortSwigger Web Security Academy  
**Category:** Access Control / Vertical Privilege Escalation  
**Difficulty:** Apprentice  
**Tool:** Burp Suite Community Edition / Browser  
**Status:** Solved  

## 1. Objective
Gain access to a hidden administrative panel that is not linked in the application's user interface, and delete a user account (`carlos`).

## 2. Vulnerability Overview
Unprotected admin functionality occurs when sensitive administrative endpoints exist on a web server without proper authentication or authorization checks. Attackers can discover these hidden paths through information disclosure leaks in `robots.txt`, sitemaps, HTML source code comments, or directory fuzzing.

## 3. Testing Methodology
1. **Analyze Information Disclosure:** Check `/robots.txt` or view the page source of the home page to look for hidden directory paths (e.g., `/admin`).
2. **Navigate to the Endpoint:** Directly browse to the discovered administrative path in the browser.
3. **Perform Administrative Action:** Locate the user management interface and execute the required action (deleting user `carlos`).
4. **Verify:** Confirm that the application processes the action successfully and marks the lab as solved.

## 4. Impact
Exposing administrative functionality without authorization allows unauthorized users to perform privileged actions, leading to complete system compromise or data loss.

## 5. Remediation
- Implement strict server-side authentication and session validation checks on all administrative endpoints.
- Ensure sensitive paths are not leaked publicly through `robots.txt` or client-side code.
