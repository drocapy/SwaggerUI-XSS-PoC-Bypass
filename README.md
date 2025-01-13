# SwaggerUI XSS PoC Bypass 🚨💻

**SwaggerUI** is a widely used tool for API documentation and testing. However, misconfigurations or unvalidated input handling can lead to **Cross-Site Scripting (XSS)** vulnerabilities. Here's a simple Proof of Concept (PoC) demonstrating an XSS bypass.

---

## 🚀 The Vulnerability

SwaggerUI allows user-supplied input in certain configurations (e.g., query parameters or headers) to be rendered without proper sanitization. If not handled correctly, attackers can inject malicious scripts.

---

## 🎯 PoC Example: XSS Exploit

### Vulnerable SwaggerUI Configuration:
A SwaggerUI endpoint with the following query parameter handling:
```json
"parameters": [
  {
    "name": "search",
    "in": "query",
    "required": false,
    "type": "string"
  }
]

Attack Payload:

Injecting the payload:https://example.com/swagger-ui?search=<script>alert('XSS')</script>
When rendered in the SwaggerUI interface, the payload executes the alert('XSS').

🛠️ Bypass Technique

If the application attempts to block <script> tags, alternative encodings can bypass the filter. For example:https://example.com/swagger-ui?search=%3Cscript%3Ealert('XSS')%3C%2Fscript%3E
🔒 Fixing the Issue

    1. Input Validation: Ensure all input is sanitized and does not allow untrusted HTML or JavaScript.

    2. Content Security Policy (CSP): Implement a strict CSP to prevent the execution of unauthorized scripts.

    3. SwaggerUI Update: Keep SwaggerUI updated to the latest version to avoid known vulnerabilities
