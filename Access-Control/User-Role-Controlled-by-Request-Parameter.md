# User Role Controlled by Request Parameter

**Platform:** PortSwigger Web Security Academy  
**Category:** Access Control / Vertical Privilege Escalation  
**Difficulty:** Apprentice  
**Tool:** Burp Suite Community Edition  
**Status:** Solved  

## 1. Objective
Bypass access controls by manipulating client-controlled parameters to elevate account privileges to administrator.

## 2. Vulnerability Overview
Some applications rely on user-controlled parameters (such as hidden form fields, cookies, or JSON parameters like `role=0` or `admin=false`) to determine a user's authorization level, trusting the client-side data without server-side re-validation.

## 3. Testing Methodology
1. **Intercept Traffic:** Log into the application with Burp Suite running and observe requests made during login or profile updates.
2. **Identify Role Indicators:** Look for parameters or cookies indicating user privileges (e.g., `role=1` or `admin=false`).
3. **Modify Request:** Send the request to Repeater, change the parameter value to represent an administrator (e.g., `role=2` or `admin=true`), and forward it.
4. **Verify Escalation:** Refresh the browser or check the response to confirm administrative access and solve the lab.

## 4. Impact
An attacker can easily grant themselves administrative rights, gaining full control over application features and other user accounts.

## 5. Remediation
- Never trust user-supplied parameters or cookies to determine authorization levels.
- Retrieve role and permission assignments securely from a trusted server-side session store or database.
