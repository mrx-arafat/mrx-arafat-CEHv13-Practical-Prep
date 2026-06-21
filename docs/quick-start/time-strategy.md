---
layout: default
title: Time Management Strategy
parent: Quick Start
nav_order: 1
description: "Hour-by-hour breakdown of the 6-hour CEH v13 practical exam."
---

# 6-Hour Time Allocation Strategy

## Timeline Overview

```
HOUR 1 (0:00-1:00) - RECONNAISSANCE
├─ Start NMAP comprehensive scan: nmap -A -T4 -p- TARGET
├─ Identify live hosts
├─ Look for open ports: 22, 80, 443, 3306, 3389, 445
└─ Continue scanning while working other tasks

HOUR 2 (1:00-2:00) - ENUMERATION + QUICK WINS
├─ Enumerate SMB: enum4linux -a TARGET
├─ Enumerate SNMP if port 161 open
├─ Try default credentials on discovered services
├─ Extract easy files/data
└─ Scans should be complete by now

HOUR 3 (2:00-3:00) - CREDENTIAL CRACKING (START)
├─ Start Hydra for RDP/SSH if needed
├─ Start Hashcat for hash cracking
├─ Begin web vulnerability testing
├─ Run SQLMAP on identified targets
└─ BREAK around 2:30

HOUR 4 (3:00-4:00) - EXPLOITATION + CRYPTO
├─ Finish web testing (SQL injection, parameter tampering)
├─ Hash cracking should complete
├─ Steganography extraction
├─ PE file analysis with DIE
└─ Directory enumeration (Nikto/Robuster)

HOUR 5 (4:00-5:00) - ADVANCED ANALYSIS
├─ Android ADB extraction if challenge present
├─ WiFi cracking if needed
├─ PCAP analysis (Wireshark/tshark)
├─ RAT detection in traffic
└─ TTL fingerprinting analysis

HOUR 6 (5:00-6:00) - FINAL REVIEW + CLEANUP
├─ Review all answers
├─ Fix format issues
├─ Verify exact answer format
├─ Submit any last-minute answers
└─ Submit exam
```

## Strategy by Challenge Type

### Network Scanning Challenges (Domains 1)
- **Time:** 15-20 min per challenge
- **Difficulty:** Easy to Medium
- **Approach:** Start first, let NMAP run while you work others
- **Key Tools:** nmap, enum4linux, SMB/SNMP enumeration

### Credential Cracking Challenges (Domain 2, 4)
- **Time:** 20-40 min (can run in background)
- **Difficulty:** Medium
- **Approach:** Start early, let Hydra/Hashcat run, return for results
- **Key Tools:** Hydra, Hashcat, John the Ripper

### Web Exploitation Challenges (Domain 3)
- **Time:** 15-25 min per challenge
- **Difficulty:** Medium to Hard
- **Approach:** Quick SQLMAP tests, then manual testing if needed
- **Key Tools:** SQLMAP, Burp Suite, Nikto

### Cryptography Challenges (Domain 4)
- **Time:** 15-35 min per challenge
- **Difficulty:** Medium to Hard
- **Approach:** Run hash cracking in background, parallel steganography
- **Key Tools:** Hashcat, Steghide, DIE, exiftool

### Mobile/IoT Challenges (Domain 5)
- **Time:** 20-30 min per challenge
- **Difficulty:** Medium
- **Approach:** Requires ADB connectivity, sequential
- **Key Tools:** adb, sqlite3, exiftool

### Traffic Analysis Challenges (Domain 6)
- **Time:** 10-20 min per challenge
- **Difficulty:** Easy to Medium
- **Approach:** Quick wins, use Wireshark filters
- **Key Tools:** Wireshark, tshark, tcpdump

### Wireless Challenges (Domain 7)
- **Time:** 20-30 min per challenge
- **Difficulty:** Medium to Hard
- **Approach:** Time-intensive, start early if present
- **Key Tools:** Aircrack-ng, airmon-ng

## Optimal Challenge Order

1. **First:** Domain 1 (Network Scanning) - builds target list
2. **Second:** Domain 6 (Traffic Analysis) - quick wins with PCAP
3. **Third:** Domain 2 (System Hacking) - start cracking tools early
4. **Fourth:** Domain 3 (Web Hacking) - SQL injection/directory enum
5. **Fifth:** Domain 4 (Cryptography) - parallel with cracking tools
6. **Sixth:** Domain 5 (Mobile/IoT) - requires ADB setup
7. **Last:** Domain 7 (Wireless) - most time-intensive

## Time Allocation by Score %

| Challenge Count | Estimated Time | Buffer |
|-----------------|-----------------|--------|
| 4 challenges | 60 min | 60 min |
| 8 challenges | 120 min | 60 min |
| 12 challenges | 180 min | 60 min |
| 16 challenges | 240 min | 60 min |
| 20 challenges | 300 min | 60 min |

**Key Insight:** You need 70% (14 out of 20) to pass. Don't waste time trying to solve all 20. Focus on getting 14 solid answers.

## When to Skip a Challenge

Skip if:
- You've spent 20+ minutes with no progress
- Tool keeps failing (Hydra, Hashcat, etc.)
- Challenge requires specific tool not installed
- You already have 14+ answers correct

Come back if:
- You have time in the final 30 minutes
- You've completed other easier challenges
- You can make an educated guess on format

## Time-Saving Tactics

### Quick Wins (5-10 min each)
- Traffic analysis with basic filters
- SMB enumeration with enum4linux
- Default credentials on discovered services
- Quick NMAP service detection

### Medium Effort (15-20 min each)
- SQL injection with SQLMAP
- Hash cracking (if fast)
- Web directory enumeration
- Basic steganography extraction

### Long-Term (30+ min each)
- Password cracking from network capture
- Android ADB extraction + database analysis
- WiFi WPA2 cracking
- Complex PE file analysis

## What NOT to Do

- ❌ Spend 1+ hour on single challenge
- ❌ Try all 20 challenges (aim for 14-15)
- ❌ Work sequentially (use parallel tools)
- ❌ Manually test when tools can automate
- ❌ Wait for one tool to finish before starting next

## Emergency Time Management

**If you have only 60 minutes left:**

1. Count correct answers so far
2. If 14+, submit and optimize existing answers
3. If <14, focus on quick wins only:
   - Traffic analysis (Wireshark filters)
   - Network scanning results
   - SMB shares/default credentials
   - Make educated guesses on format
