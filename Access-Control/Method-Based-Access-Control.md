# Method-Based Access Control Can Be Circumvented

**Platform:** PortSwigger Web Security Academy  
**Category:** Access Control / Broken Access Control  
**Difficulty:** Apprentice  
**Tool:** Burp Suite Community Edition  
**Status:** Solved  

## 1. Objective
Bypass access control restrictions on administrative functions by changing the HTTP request method.

## 2. Vulnerability Overview
Some access control implementations rely heavily on the HTTP method (e.g., enforcing access controls on `POST` requests while failing to secure `GET` requests to the same administrative endpoint). 

## 3. Testing Methodology
1. **Identify Admin Action:** Log in as an administrator to observe how administrative functions (e.g., promoting a user) are requested (typically via `POST`).
2. **Replay as Standard User:** Log in as a standard user, attempt the action, and intercept the request in Burp Suite.
3. **Change HTTP Method:** Send the request to Repeater and switch the method (e.g., from `POST` to `GET`, or vice versa).
4. **Verify Access:** Check if the backend processes the request due to missing method-specific access controls.

## 4. Remediation
- Ensure access control frameworks enforce security rules uniformly across all HTTP methods for a given endpoint unless explicitly intended otherwise.
