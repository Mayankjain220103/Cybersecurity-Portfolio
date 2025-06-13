Broken-Auth-Test-OWASPJuice.md – Session fixation, weak token, and IDOR test cases

### Broken-Auth-Test-OWASPJuice.md
```markdown
# 🔓 Broken Authentication Testing – OWASP Juice Shop

## 🔧 Environment
- **Application**: OWASP Juice Shop
- **Tools**: Firefox DevTools, Burp Suite, Postman

## 🌟 Objective
Identify broken authentication issues like session fixation, weak tokens, and IDORs.

---

## 🧪 1. Session Fixation

### Steps:
1. Login with a user account.
2. Capture session cookie in Burp.
3. Logout.
4. Manually reuse the same cookie in another session.

### Observation:
- If the session is accepted after logout, session fixation vulnerability exists.

### Mitigation:
- Invalidate session tokens upon logout.
- Regenerate session tokens after login.

---

## 🧪 2. Predictable Token / Weak Session ID

### Steps:
1. Register multiple users.
2. Capture the session tokens.
3. Analyze for predictable patterns (e.g., JWT with base64-decoded email).

### Mitigation:
- Use secure, randomized tokens (UUIDs or cryptographically generated).
- Avoid exposing user data in session tokens.

---

## 🧪 3. Insecure Direct Object Reference (IDOR)

### Scenario:
- Logged in as user A
- URL: `http://localhost:3000/profile/1`
- Change URL to `.../profile/2` → Access user B’s data

### Observation:
- If another user’s data is viewable/alterable, IDOR exists.

### Mitigation:
- Enforce access control at the server level.
- Never rely solely on client-side validation.

---

## ✅ Summary
Authentication flaws can lead to serious user account compromise. Use secure session management, random tokens, and server-side access control.
```
