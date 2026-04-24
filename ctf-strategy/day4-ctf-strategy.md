# Day 4 — CTF Strategy & Competition Day 🏆

**Workshop:** GDG on Campus AUM · CTF Challenge Bootcamp  
**Date:** April 14, 2026  
**Category:** General Skills · CTF Methodology

---

## What is a CTF?

A **Capture The Flag** competition is a cybersecurity challenge where you solve puzzles to find hidden strings called "flags."

- **Format:** Jeopardy-style — pick any challenge, any order
- **Flag format:** Always looks like `picoCTF{some_text_here}`
- **Scoring:** Each solved challenge earns points based on difficulty

---

## CTF Categories

### Web Exploitation
Apply Days 1 & 2 skills:
- View page source for hidden comments
- Inspect and manipulate cookies
- Try XSS payloads in input fields
- Attempt SQL injection on login forms
- Check robots.txt and sitemap.xml

### Cryptography
Apply Day 3 skills:
- Identify encoding type (Base64? Hex? ROT13?)
- Use CyberChef for decoding
- Try CrackStation for hash cracking
- Use dCode.fr for cipher identification

### General Skills
- Basic Linux commands
- Reading and manipulating files
- Format conversion
- Use the picoCTF webshell for command-line access

### Forensics
- Analyze files for hidden data
- Check file metadata
- Look for steganography (data hidden in images)
- Examine file headers

---

## My CTF Strategy

### 1. Read Everything
The challenge title, description, and hints all contain clues:
- "Mod 26" → ROT13 (26 letters in the alphabet)
- "Inspector" → Use DevTools
- "where are the robots" → Check robots.txt

### 2. Start Easy, Score Fast
- Do all Tier 1 (25pts) and Tier 2 (50pts) challenges first
- Quick wins build momentum and secure a good rank
- Don't get stuck on hard challenges when easy points are available

### 3. Time-Box Attempts
- Stuck for 15+ minutes? Move on
- Come back later with fresh eyes
- More challenges = more opportunities

### 4. Team Division of Work
```
Team Role Assignment:
  Person 1 → Web Exploitation challenges
  Person 2 → Cryptography challenges  
  Person 3 → General Skills challenges
  Regroup → Help each other on stuck challenges
```

---

## The "I'm Stuck" Flowchart

```
1. Re-read the challenge — title, description, hints
   ↓ (still stuck)
2. Check the basics — source? robots.txt? cookies? DevTools?
   ↓ (still stuck)
3. Try CyberChef "Magic" — paste any suspicious text
   ↓ (still stuck)
4. Search the internet — "[technique] tutorial" or "[challenge name] hint"
   ↓ (still stuck)
5. Ask teammate or AI — describe the challenge for a fresh perspective
   ↓ (still stuck)
6. Skip it — move on, come back later. No shame in this.
```

---

## Competition Day Tools Reference

| Tool | URL | Use Case |
|------|-----|----------|
| DevTools | F12 | Web exploitation, cookie manipulation |
| CyberChef | gchq.github.io/CyberChef | Encoding, decoding, hashing |
| CrackStation | crackstation.net | Hash cracking |
| dCode.fr | dcode.fr | Cipher identification |
| Webhook.site | webhook.site | Capture HTTP requests |
| picoCTF Webshell | picoctf.org | Browser-based terminal |

---

## Competition Results — April 16, 2026

**Event:** GDG on Campus AUM · NexClique CTF Competition  
**Format:** 2 rounds · 4.5 hours total

### Scoring Breakdown
| Tier | Points | Difficulty |
|------|--------|-----------|
| Tier 1 | 25 pts | Warm-Up |
| Tier 2 | 50 pts | Easy |
| Tier 3 | 100 pts | Medium |
| Tier 4 | 150 pts | Hard |
| First Blood Bonus | +25 pts | First team to solve Tier 3/4 |

---

## Reflections

### What I Did Well
- Applied web exploitation techniques from Days 1 & 2 effectively
- Used CyberChef confidently for crypto challenges
- Stayed methodical — followed the "I'm stuck" flowchart

### What I Want to Improve
- More practice with SQL injection edge cases
- Explore forensics category (file metadata, steganography)
- Get faster at identifying encoding types at a glance

### Next Steps
- Continue practicing on picoCTF picoGym
- Work toward completing Google Cloud Cybersecurity Certificate
- Apply web security knowledge to cloud security context

---

## Key Takeaway
> CTF competitions aren't just games — they build the muscle memory of a security mindset. Every challenge teaches you to think like an attacker so you can defend like a professional.
