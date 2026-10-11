# File Path Traversal — Simple Case

**Platform:** PortSwigger Web Security Academy  
**Category:** Server-Side Vulnerabilities  
**Difficulty:** Apprentice  
**Tool:** Burp Suite Community Edition  
**Environment:** Kali Linux on VMware Workstation  
**Status:** Solved

## 1. Objective

Exploit a file path traversal vulnerability in the product image functionality to retrieve the contents of the `/etc/passwd` file from the lab server.

## 2. Vulnerability Overview

Path traversal, also known as directory traversal, occurs when an application uses user-controlled input to construct a file path without properly restricting access to the intended directory.

An attacker may manipulate a filename parameter using directory traversal sequences such as `../` to access files outside the permitted directory.

### Example

A legitimate image request might look like:

```http
GET /image?filename=product.jpg HTTP/2
```

The application uses the `filename` parameter to locate an image on the server.

If the application does not adequately validate the path, an attacker may attempt to access a sensitive file instead.

## 3. Testing Methodology

### Step 1 — Identify the image request

1. Open the lab in the browser.
2. Launch Burp Suite and navigate to **Target → Site map**.
3. Browse the application to generate HTTP requests.
4. Locate a product image request containing the `/image` endpoint.
5. Inspect the request to identify the filename parameter.

### Step 2 — Send the request to Repeater

1. Right-click the image request.
2. Select **Send to Repeater**.
3. Open the Repeater tab.
4. Inspect the HTTP request and identify the filename parameter.

### Step 3 — Test for path traversal

Modify the filename parameter to attempt to retrieve `/etc/passwd`:

```http
GET /image?filename=../../../etc/passwd HTTP/2
```

The exact request path and traversal depth may depend on the lab's implementation. Adjust the path as needed and send the request using Repeater.

### Step 4 — Analyze the response

Inspect the server response for evidence that the requested file was retrieved. On a typical Linux system, `/etc/passwd` contains account information, including usernames and associated account metadata.

Successful retrieval of the file demonstrates that the application allows access beyond its intended image directory.

### Step 5 — Verify the lab objective

Return to the lab page and confirm that PortSwigger marks the lab as **Solved**.

## 4. Evidence

Add screenshots demonstrating your own testing process:

- [ ] Product image request identified in Burp Suite
- [ ] Original request sent to Repeater
- [ ] Modified request and successful response
- [ ] Lab marked as Solved

Store screenshots in this folder if you want to keep the evidence alongside the write-up.

## 5. Impact

Depending on the application's privileges and implementation, path traversal can expose sensitive configuration files, application source code, credentials, or operating system information.

The severity depends on which files are accessible, the privileges of the application process, and the sensitivity of the exposed data.

## 6. Remediation

Developers should:

- Avoid using raw user-controlled input to construct filesystem paths.
- Use an allowlist of permitted filenames or server-side file identifiers.
- Canonicalize paths and verify that resolved paths remain inside the intended directory.
- Apply least-privilege filesystem permissions.
- Avoid exposing sensitive files through application functionality.
- Add security tests for path traversal attempts.

## 7. Key Takeaways

- Learned to identify file-related HTTP requests using Burp Suite.
- Practiced modifying HTTP parameters with Repeater.
- Understood how directory traversal sequences can escape an intended directory.
- Learned to verify exploitation using server responses.
- Reviewed practical remediation techniques.

## References

- [PortSwigger — Path Traversal](https://portswigger.net/web-security/file-path-traversal)
- [PortSwigger — File Path Traversal: Simple Case](https://portswigger.net/web-security/file-path-traversal/lab-simple)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)

---

*Lab completed in an authorized PortSwigger Web Security Academy environment for educational purposes.*
