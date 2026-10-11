# User ID Controlled by Request Parameter (IDOR)

**Platform:** PortSwigger Web Security Academy  
**Category:** Access Control / Horizontal Privilege Escalation (IDOR)  
**Difficulty:** Apprentice  
**Tool:** Burp Suite Community Edition  
**Status:** Solved  

## 1. Objective
Access another user's account details and API key by exploiting an Insecure Direct Object Reference (IDOR) vulnerability in the user profile endpoint.

## 2. Vulnerability Overview
IDOR occurs when an application exposes a direct reference to an internal implementation object (such as a database primary key or user ID) without validating whether the current user is authorized to access that specific object.

## 3. Testing Methodology
1. **Log In and Capture Request:** Log into your assigned account and navigate to the user account page (`/my-account?id=wiener`).
2. **Send to Repeater:** Intercept the request in Burp Suite and send it to Repeater.
3. **Modify Object Reference:** Change the `id` parameter value from your username/ID to target another user (e.g., `id=carlos`).
4. **Analyze Response:** Inspect the server response to verify whether Carlos's account data and API key are returned.

## 5. Impact
Horizontal privilege escalation allows attackers to read, modify, or delete sensitive data belonging to any other user of the same privilege level.

## 6. Remediation
- Implement robust server-side access control checks that verify whether the authenticated user owns or has permission to access the requested resource identifier.
- Use indirect object references (such as session-managed IDs) where feasible.
