---
layout: default
title: Answer Formatting Guide
parent: Quick Start
nav_order: 3
description: "Critical answer format guidelines - the #1 reason people fail the CEH exam."
---

# Answer Format - CRITICAL!

**This is the #1 reason people fail. Format MUST match exactly.**

Your answer can be technically correct but marked wrong if:
- Case doesn't match (Admin vs admin)
- Padding is wrong (3306 vs 03306)
- Extra spaces (admin vs "admin ")
- Wrong symbols or no symbols (IP:PORT vs IP)

## Format Legend

| Symbol | Meaning | Example |
|--------|---------|---------|
| `A` | Uppercase letter | `PQRS` |
| `a` | Lowercase letter | `pqrs` |
| `N` | Digit | `1234` |
| `*` | Any characters | `Pass*123` (password followed by 123) |
| `.` | Literal period | `192.168.1.5` |
| `:` | Literal colon | `1234:AB:CD` |
| `/` | Literal slash | `/home/admin` |

## Common Format Examples

### IP Addresses

```
Format: NN.NN.NN.NN
CORRECT:   "192.168.1.5"
WRONG:     "192.168.1.5:3306"  (don't include port)
WRONG:     "192.168.001.005"   (don't pad octets)
```

### Passwords & Usernames

```
Format: AaaAaa*aaaa
CORRECT:   "MyPassword123"    (capitals at specific positions, match case)
WRONG:     "mypassword123"    (wrong case)
WRONG:     "MYPASSWORD123"    (all caps - doesn't match format)
WRONG:     " MyPassword123"   (no leading spaces)
WRONG:     "MyPassword123 "   (no trailing spaces)
```

### Port Numbers

```
Format: NNNNN (5 digits)
Answer: 3306

CORRECT:   "03306"    (padded with leading zero)
WRONG:     "3306"     (only 4 digits)
WRONG:     "3306:mysql" (don't include service name)
```

### File Paths

```
Format: /aaa/aaaaa
CORRECT:   "/home/admin"
WRONG:     "home/admin"       (missing leading slash)
WRONG:     "/home/admin/"     (don't include trailing slash)
WRONG:     "C:\home\admin"    (wrong separators)
```

### Hash Values

```
Format: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa (32 char - MD5)
CORRECT:   "5d41402abc4b2a76b9719d911017c592"
WRONG:     "5D41402ABC4B2A76B9719D911017C592" (uppercase)
WRONG:     "5d41402abc4b2a76b9719d911017c592 " (trailing space)
```

### MAC Addresses

```
Format: NN:NN:NN:NN:NN:NN
CORRECT:   "AA:BB:CC:DD:EE:FF"
WRONG:     "AA-BB-CC-DD-EE-FF" (dashes instead of colons)
WRONG:     "AABBCCDDEEFF"      (no separators)
```

### Service Versions

```
Format: N.N.N
CORRECT:   "5.7.17"
WRONG:     "5.7.17-ubuntu" (don't include OS designation)
WRONG:     "v5.7.17"       (don't include 'v' prefix)
```

## Domain-Specific Formats

### Domain 1: Network Scanning

| Item | Format | Example |
|------|--------|---------|
| IP Address | NN.NN.NN.NN | `192.168.1.5` |
| Computer Name | Mixed case | `WORKSTATION1` or `domain-controller` |
| Port Number | NNNNN | `03306` (padded) |
| Service Version | N.N.N | `5.7.17` |
| Service Name | Exact name | `MySQL` not `mysql` |

**Common Mistakes:**
```
WRONG:  "192.168.1.5:3306"  CORRECT: "192.168.1.5"
WRONG:  "mysql"              CORRECT: "MySQL"
WRONG:  "5.7.17-ubuntu"      CORRECT: "5.7.17"
WRONG:  "3306"               CORRECT: "03306"
```

### Domain 2: System Hacking

| Item | Format | Example |
|------|--------|---------|
| Password | Mixed case/numbers | `MyPassword123` |
| Username | Exact case | `Administrator` or `admin` |
| Registry Path | Windows format | `HKLM\Software\Microsoft\Windows\Run` |
| TTL Value | Digits only | `128` (Windows), `64` (Linux) |
| File Path | Windows format | `C:\Windows\System32\config\sam` |

**Common Mistakes:**
```
WRONG:  "admin"              CORRECT: "Administrator"
WRONG:  "mypassword"         CORRECT: "MyPassword123"
WRONG:  "C:/Windows/System32"  CORRECT: "C:\Windows\System32"
```

### Domain 3: Web Hacking

| Item | Format | Example |
|------|--------|---------|
| URL Path | Leading slash | `/admin/dashboard` |
| Full URL | http/https | `http://target.com/login` |
| SQL Data | Exact value | `admin` (if that's in DB) |
| Directory | Forward slashes | `/uploads`, `/admin`, `/config` |
| Parameter Name | Exact name | `user`, `password`, `id` |

**Common Mistakes:**
```
WRONG:  "admin/dashboard"    CORRECT: "/admin/dashboard"
WRONG:  "target.com/login"   CORRECT: "http://target.com/login"
WRONG:  "users"              CORRECT: "users" (must match DB exactly)
```

### Domain 4: Cryptography

| Item | Format | Example |
|------|--------|---------|
| Hash (MD5) | 32 lowercase hex | `5d41402abc4b2a76b9719d911017c592` |
| Hash (SHA1) | 40 lowercase hex | `356a192b7913b04c54574d18c28d46e6395428ab` |
| Hash (SHA256) | 64 lowercase hex | `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855` |
| Cracked Password | Mixed case/numbers | `SecurePassword99` |
| File Version | N.N.N.N | `2.3.4.5` |
| Compiler | Full name | `Microsoft Visual C++` |

**Common Mistakes:**
```
WRONG:  "5D41402ABC4B2A76B9719D911017C592"  CORRECT: "5d41402abc4b2a76b9719d911017c592"
WRONG:  "SecurePassword99 "                   CORRECT: "SecurePassword99"
WRONG:  "2.3.4"                               CORRECT: "2.3.4.5"
```

### Domain 5: Mobile & IoT

| Item | Format | Example |
|------|--------|---------|
| File Path | Full Linux path | `/sdcard/DCIM/Camera/IMG_001.jpg` |
| Database File | With extension | `app.db` |
| SQL Query Result | Exact value | `password123` |
| Hidden Message | Exact text | The steganography message |
| Device Model | Exact model | `SM-G920F` |

**Common Mistakes:**
```
WRONG:  "/sdcard/DCIM/Camera/IMG_001.jpg/"  CORRECT: "/sdcard/DCIM/Camera/IMG_001.jpg"
WRONG:  "IMG_001"                            CORRECT: "IMG_001.jpg"
WRONG:  "application.db"                     CORRECT: "app.db" (exact name)
```

### Domain 6: Traffic Analysis

| Item | Format | Example |
|------|--------|---------|
| Attacker IP | NN.NN.NN.NN | `203.0.113.45` |
| Victim IP | NN.NN.NN.NN | `192.168.1.50` |
| Port Number | NNNNN | `04444` |
| MQTT Topic | With slashes | `home/temperature` |
| Domain Name | Full domain | `malware-c2.com` |
| Protocol | Exact name | `HTTP`, `FTP`, `SSH` |

**Common Mistakes:**
```
WRONG:  "203.0.113.45:4444"  CORRECT: "203.0.113.45"
WRONG:  "4444"                CORRECT: "04444"
WRONG:  "home\temperature"   CORRECT: "home/temperature"
```

### Domain 7: Wireless

| Item | Format | Example |
|------|--------|---------|
| WiFi Password | Mixed case/numbers | `MyWiFiPass123` |
| Last 4 Chars | Exact characters | `Pass1` (from "MyWiFiPass1") |
| BSSID | Uppercase hex | `AA:BB:CC:DD:EE:FF` |
| Channel | Digits | `6` or `11` |
| Security | Exact format | `WPA2-PSK` |

**Common Mistakes:**
```
WRONG:  "mywifipass123"      CORRECT: "MyWiFiPass123"
WRONG:  "AAB:BBB:CCC:DD:EEE:FF"  CORRECT: "AA:BB:CC:DD:EE:FF"
WRONG:  "Pass"                CORRECT: "Pass1" (full answer, not just part)
```

## Testing Your Answer

Before submitting, check:

1. **Case Sensitivity**
   - [ ] Does it match the format exactly?
   - [ ] Are capitals in right places?

2. **Padding**
   - [ ] Are leading zeros included if format shows?
   - [ ] Did you not add extra zeros?

3. **Symbols**
   - [ ] Are colons, periods, slashes correct?
   - [ ] No extra spaces at start/end?

4. **Length**
   - [ ] Does it match the format length?
   - [ ] Count character by character if unsure

## Real Examples from Past Exams

### Example 1: IP Address with Port Confusion
```
Question: What is the MySQL server IP?
Format: NN.NN.NN.NN

❌ WRONG: "192.168.1.5:3306"  (included port)
✅ CORRECT: "192.168.1.5"
```

### Example 2: Hash Capitalization
```
Question: What is the MD5 hash of the file?
Format: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa

❌ WRONG: "5D41402ABC4B2A76B9719D911017C592"  (uppercase)
✅ CORRECT: "5d41402abc4b2a76b9719d911017c592"  (lowercase)
```

### Example 3: Port Padding
```
Question: What port is the web server on?
Format: NNNNN

❌ WRONG: "80"      (only 2 digits)
❌ WRONG: "00080"   (wrong padding)
✅ CORRECT: "00080"  OR depends on format shown
```

### Example 4: Path Slashes
```
Question: Where is the config file located?
Format: /aaa/aaaaa/aaa

❌ WRONG: "home/admin/config"     (missing leading slash)
❌ WRONG: "/home/admin/config/"   (trailing slash)
✅ CORRECT: "/home/admin/config"
```

### Example 5: Password Case
```
Question: Find the database password
Format: AaaAaa*aaaa

Question answer: MyDatabase123

❌ WRONG: "mydatabase123"      (wrong case)
❌ WRONG: "MYDATABASE123"      (all caps)
✅ CORRECT: "MyDatabase123"     (matches format exactly)
```

## If You Copied from Output

Tools often output data in different formats. Convert before answering:

```bash
# Tool outputs uppercase hash
echo "5D41402ABC4B2A76B9719D911017C592"

# Convert to lowercase for MD5
tr '[:upper:]' '[:lower:]' <<< "5D41402ABC4B2A76B9719D911017C592"
# Output: 5d41402abc4b2a76b9719d911017c592
```

---

## Summary Checklist

Before answering ANY question:

- [ ] Format matches exactly (including case)
- [ ] No extra spaces at beginning or end
- [ ] Padding matches (zeros where needed)
- [ ] Symbols are correct (: vs - vs /)
- [ ] Length matches format requirements
- [ ] Not including extra information (port, service name, etc)
