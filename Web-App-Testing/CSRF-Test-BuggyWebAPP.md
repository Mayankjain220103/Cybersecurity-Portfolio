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
