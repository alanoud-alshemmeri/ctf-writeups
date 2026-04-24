# Day 1 — Web Fundamentals & Information Disclosure 🌐

**Workshop:** GDG on Campus AUM · CTF Challenge Bootcamp  
**Date:** April 5, 2026  
**Category:** Web Exploitation · General Skills

---

## What I Learned

### HTTP Methods & Status Codes
Understanding how browsers communicate with servers is the foundation of web security.

| Method | Purpose | Security Relevance |
|--------|---------|-------------------|
| GET | Retrieve data | Parameters visible in URL — never put sensitive data here |
| POST | Send data | Used for logins — credentials in request body |
| PUT | Update data | Can be abused if server doesn't verify permissions |
| DELETE | Remove data | Dangerous if no authentication check |

Key status codes from an attacker's perspective:
- **403 Forbidden** → Resource exists but you're blocked. Worth probing further.
- **404 Not Found** → Resource doesn't exist — but sometimes a misconfigured server reveals this incorrectly.
- **500 Internal Server Error** → Can leak stack traces, file paths, or framework versions.

---

## Skill: Browser DevTools for Security

DevTools is the most important tool for web exploitation. Here's how I use each tab:

### Elements Tab
- Find hidden HTML comments (`<!-- -->`) left by developers
- Discover hidden form fields or disabled buttons that can be re-enabled

### Console Tab
```javascript
// Check what cookies are accessible via JavaScript
document.cookie

// Get the page title (sometimes reveals tech stack)
document.title

// Find all forms on the page
document.forms
```

### Network Tab
- Watch every request the browser makes
- Identify API endpoints that aren't visible in the UI
- Check request headers for authentication tokens

### Application Tab
- View and **edit** cookies directly
- Check Local Storage and Session Storage for sensitive data
- Key targets: `role=user`, `admin=false`, `isLoggedIn=0`

---

## Technique: Information Disclosure

When approaching any CTF web challenge, I follow this checklist:

```
☐ View Page Source → look for HTML comments
☐ Check /robots.txt → reveals hidden directories
☐ Check /sitemap.xml → lists all pages
☐ Try /.git/ → may expose entire source code
☐ Trigger errors → add ' to inputs for verbose error messages
☐ Inspect CSS/JS files → flags sometimes hidden here
```

### Example: robots.txt Discovery
```
# Target: http://challenge.com/robots.txt
# Output:
User-agent: *
Disallow: /secret-admin-panel/
Disallow: /backup/

# Result: Found hidden admin panel path!
```

---

## Challenges Practiced

### Inspect HTML (picoCTF)
**Category:** Web Exploitation  
**Approach:** Opened DevTools → Elements tab → searched for `picoCTF{` in page source  
**Key Takeaway:** Developers sometimes leave flags or sensitive data in HTML comments

### where are the robots (picoCTF)
**Category:** Web Exploitation  
**Approach:** Navigated to `/robots.txt` → found disallowed path → visited it  
**Key Takeaway:** `robots.txt` is public and often reveals paths the owner wants hidden

### Insp3ct0r (picoCTF)
**Category:** Web Exploitation  
**Approach:** Flag was split across HTML, CSS, and JS files — had to check all three  
**Key Takeaway:** Always check ALL linked resources, not just the main page

---

## Tools Used
- **Browser DevTools** (F12) — primary tool for web exploitation
- **picoCTF** — practice platform

## Key Takeaway
> Security isn't about magic — it's about being more thorough than the developer who left something exposed.
