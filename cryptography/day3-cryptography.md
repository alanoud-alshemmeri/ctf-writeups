# Day 3 — Cryptography & Ciphers 🔐

**Workshop:** GDG on Campus AUM · CTF Challenge Bootcamp  
**Date:** April 12, 2026  
**Category:** Cryptography

---

## The Most Important Distinction: Encoding vs Encryption vs Hashing

This question solves 50% of CTF crypto challenges:
> *"Is this encoded, encrypted, or hashed?"*

| | Encoding | Encryption | Hashing |
|--|---------|-----------|---------|
| **Analogy** | Language translation | Locked box with a key | A fingerprint |
| **Reversible?** | Yes — anyone can | Yes — only with the key | No — one-way |
| **Purpose** | Data format conversion | Keeping secrets | Verifying integrity |
| **Security** | None | Strong | Partial |
| **Examples** | Base64, Hex, URL | AES, RSA | MD5, SHA-256 |

---

## Recognizing Encodings at a Glance

```
Base64:  SGVsbG8gV29ybGQ=
         → Letters + numbers + / and + → Often ends with = or ==

Hex:     48656c6c6f
         → Only 0-9 and a-f → Even number of characters

URL:     Hello%20World
         → % followed by two hex digits

Binary:  01001000 01101001
         → Only 0s and 1s → Groups of 8

ROT13:   Uryyb Jbeyq
         → Looks like text but nonsensical → Only letters are shifted
```

---

## Caesar Cipher & ROT13

ROT13 is a Caesar cipher with a shift of 13. Since the alphabet has 26 letters, applying ROT13 **twice** returns the original text.

```
Plain:   A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
ROT13:   N O P Q R S T U V W X Y Z A B C D E F G H I J K L M

Example:
  "Hello" → ROT13 → "Uryyb"
  "Uryyb" → ROT13 → "Hello"  ✓ (applying twice = original)
```

### How to Decode Quickly
In **CyberChef**: drag "ROT13" into the recipe → instant decode.

---

## Symmetric vs Asymmetric Encryption

### Symmetric (AES)
- One key for both encrypting and decrypting
- Like a house key — both parties need the same copy
- **Fast** — used for large data (files, HTTPS data transfer, disk encryption)
- **Problem:** How do you securely share the key in the first place?

### Asymmetric (RSA)
- Two keys: **public key** (share openly) + **private key** (keep secret)
- Like a mailbox: anyone can drop in a letter, only you can open it
- **Slower** — used for key exchange and digital signatures
- **Solves** the key-sharing problem

### How HTTPS Uses Both
```
1. Your browser connects to a website
2. Asymmetric (RSA) → securely exchanges a temporary AES key
3. Symmetric (AES) → encrypts the rest of the session
   ↑ Fast + secure = best of both worlds
```

---

## Hash Identification Quick Guide

```
Count the characters:
  32 chars  → MD5    (broken — don't use for security)
  40 chars  → SHA-1  (weak — being phased out)
  64 chars  → SHA-256 (secure — current standard)

Example:
  5d41402abc4b2a76b9719d911017c592  → 32 chars = MD5
```

To crack a hash: paste it into **crackstation.net** — if it's a common password, you'll get it instantly.

---

## CyberChef Workflow

CyberChef (gchq.github.io/CyberChef) is the Swiss Army knife of CTF crypto.

```
My standard approach for an unknown string:
1. Paste into CyberChef input
2. Try "Magic" operation — auto-detects encoding
3. If Base64 suspected → "From Base64"
4. If hex → "From Hex"
5. If looks like shifted text → "ROT13"
6. Chain operations if needed: "From Hex" → "From Base64"
```

---

## Challenges Practiced

### Mod 26 / 13 (picoCTF)
**Category:** Cryptography  
**Approach:** Pasted cipher text into CyberChef → applied ROT13  
**Key Takeaway:** ROT13 is the most common simple cipher in CTFs — always try it first

### caesar (picoCTF)
**Category:** Cryptography  
**Approach:** Used dCode.fr's auto-solver to try all 26 Caesar shifts  
**Key Takeaway:** When shift is unknown, brute force all 26 options — it's fast

### The Numbers (picoCTF)
**Category:** Cryptography  
**Approach:** Converted numbers to letters (1=A, 2=B, etc.) using CyberChef  
**Key Takeaway:** Simple substitution ciphers are common warm-up challenges

---

## Tools Used
- **CyberChef** (gchq.github.io/CyberChef) — encoding/decoding/hashing
- **CrackStation** (crackstation.net) — hash cracking
- **dCode.fr** — cipher identification and solving
- **picoCTF** — practice challenges

## Key Takeaway
> Before trying to "break" any crypto, first identify what you're looking at. Encoding is not encryption — Base64 has zero security.
