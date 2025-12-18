# John the Ripper – Complete Basics & Usage Guide

## 1. Introduction
**John the Ripper (JtR)** is a powerful password cracking tool widely used in:
- SOC Operations
- Penetration Testing
- Digital Forensics

It supports cracking:
- Linux / Windows password hashes
- ZIP / RAR archives
- SSH private keys
- Many common hash formats

---

## 2. Basic Syntax
```bash
john [options] [file_path]
```

**Explanation**
- `john` → invokes John the Ripper
- `options` → cracking mode, wordlist, format, rules
- `file_path` → file containing hashes

---

## 3. Automatic Hash Cracking (Auto-Detect)

### Purpose
Use when:
- Hash type is unknown
- Quick attempt is needed

⚠️ Auto-detection may be unreliable.

### Syntax
```bash
john --wordlist=[path_to_wordlist] [hash_file]
```

### Example
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

---

## 4. Format-Specific Cracking (Recommended)

### Purpose
- Faster and more accurate
- Used when hash type is known

### Syntax
```bash
john --format=[format] --wordlist=[path_to_wordlist] [hash_file]
```

### Examples
```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash3.txt
```

---

## 5. Listing Supported Formats
```bash
john --list=formats
```

Search for a format:
```bash
john --list=formats | grep -iF "md5"
```

---

## 6. Hash Identification (Pre-Step)
Useful online tools:
- CrackStation
- CyberChef

---

## 7. Cracking Linux Passwords (Unshadow)

### Purpose
Combine `/etc/passwd` and `/etc/shadow`

### Syntax
```bash
unshadow passwd shadow > unshadowed.txt
```

### Example
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
```

---

## 8. Single Crack Mode

### Purpose
Uses usernames and personal data patterns.

### Syntax
```bash
john --single --format=[format] [hash_file]
```

### Example
```bash
john --single --format=raw-sha256 hashes.txt
```

### Required File Format
❌ Incorrect
```
1efee03cdcb96d90ad48ccc7b8666033
```

✅ Correct
```
mike:1efee03cdcb96d90ad48ccc7b8666033
```

---

## 9. ZIP File Cracking (zip2john)

```bash
zip2john file.zip > zip_hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

---

## 10. RAR File Cracking (rar2john)

```bash
rar2john file.rar > rar_hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
```

---

## 11. SSH Private Key Cracking (ssh2john)

### Kali Linux
```bash
python /usr/share/john/ssh2john.py id_rsa > id_rsa_hash.txt
```

### AttackBox
```bash
python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
```

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```

---

## 12. When to Use Which Mode

| Scenario | Mode |
|--------|------|
| Unknown hash | Auto-detect |
| Known hash | Format-specific |
| Linux passwords | Unshadow |
| User-based guessing | Single |
| ZIP / RAR | zip2john / rar2john |
| SSH key | ssh2john |

---

## 13. Official Reference
🔗 https://www.openwall.com/john/
