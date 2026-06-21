---
layout: default
title: Decision Tree - When Stuck
parent: Quick Start
nav_order: 4
description: "Troubleshooting guide for when you're stuck on a challenge."
---

# When You're Stuck (Decision Tree)

Use this flowchart when you can't find the answer to a challenge.

## Master Decision Tree

```
I can't find the answer
│
├─ Is it a NETWORK/IP question?
│  ├─ Is it asking for IP address?
│  │  └─ Open PCAP in Wireshark
│  │     ├─ Filter: ip.src == X or ip.dst == Y
│  │     └─ Look at Conversations (Statistics menu)
│  │
│  ├─ Is it asking for PORT number?
│  │  └─ Use tshark: tshark -r file.pcapng -T fields -e tcp.port | sort -u
│  │
│  ├─ Is it asking for TTL?
│  │  └─ Wireshark: filter by "ip.ttl == 128" (Windows) or "ip.ttl == 64" (Linux)
│  │
│  └─ Is it asking for domain/hostname?
│     └─ Look for DNS queries: filter "dns" in Wireshark
│        └─ Or use nmap: nmap -sV -O IP
│
├─ Is it a CREDENTIAL question?
│  ├─ Do you already have a username?
│  │  └─ Try Hydra: hydra -l USERNAME -P rockyou.txt SERVICE://IP
│  │
│  ├─ Do you need to find the username first?
│  │  ├─ Check SMB shares: enum4linux -a IP
│  │  └─ Check web enumeration: nikto -h http://IP
│  │
│  ├─ Is it a default credential?
│  │  └─ Try these first:
│  │     ├─ admin:admin
│  │     ├─ root:root
│  │     ├─ admin:password
│  │     └─ Check service documentation
│  │
│  └─ Still can't crack it?
│     ├─ Check if Hydra is still running (it may not be visible)
│     └─ Try different service: rdp, ssh, ftp, mysql, smb
│
├─ Is it a HASH question?
│  ├─ First, identify hash type
│  │  └─ Use: hashid HASHVALUE
│  │
│  ├─ Then crack it
│  │  ├─ MD5 (32 chars): hashcat -m 0 -a 0 hash.txt rockyou.txt
│  │  ├─ SHA1 (40 chars): hashcat -m 100 -a 0 hash.txt rockyou.txt
│  │  ├─ SHA256 (64 chars): hashcat -m 1400 -a 0 hash.txt rockyou.txt
│  │  └─ Windows NTLM: hashcat -m 1000 -a 0 hash.txt rockyou.txt
│  │
│  ├─ Is it running slow?
│  │  └─ Let it run in background, move to next challenge
│  │     └─ Check status with: hashcat --session=SESSION_NAME --status
│  │
│  └─ Can't identify type?
│     └─ Check online: https://hash-identifier.online
│
├─ Is it a FILE/DATA question?
│  ├─ Is it hidden (steganography)?
│  │  └─ Try: steghide extract -sf FILE -p "" (empty password first)
│  │
│  ├─ Is it encrypted (VeraCrypt/CryptoForge)?
│  │  └─ Try: veracrypt --mount /dev/DEVICE /mnt/point --password=PASSWORD
│  │
│  ├─ Is it a binary/executable file?
│  │  ├─ Check type: file FILENAME
│  │  ├─ Extract strings: strings FILENAME | grep -i "flag\|password\|secret"
│  │  └─ Analyze with DIE: DIE FILENAME (GUI tool)
│  │
│  ├─ Is it metadata in an image?
│  │  └─ Try: exiftool IMAGEFILE
│  │
│  └─ Can't find it at all?
│     └─ Search filesystem: find / -name "*.db" 2>/dev/null
│        └─ Or: find / -type f -name "*password*" 2>/dev/null
│
├─ Is it from a PCAP/network capture?
│  ├─ Open in Wireshark
│  │  ├─ Filter by protocol: http, ftp, ssh, mqtt
│  │  └─ Follow stream: right-click → Follow TCP/UDP Stream
│  │
│  ├─ Is it HTTP traffic?
│  │  └─ Look for POST requests with credentials
│  │     └─ Wireshark: filter "http.request.method == 'POST'"
│  │
│  ├─ Is it FTP traffic?
│  │  └─ Look for USER/PASS commands
│  │     └─ Wireshark: filter "ftp.request.command"
│  │
│  ├─ Is it a DDoS attack?
│  │  └─ Find destination IP with most packets
│  │     └─ Statistics → IPv4 Statistics → Destination/Source Addresses
│  │
│  ├─ Is it MQTT (IoT)?
│  │  └─ Filter: mqtt
│  │     └─ Look at: Statistics → Protocol Hierarchy → MQTT
│  │
│  └─ Can't find the right protocol?
│     └─ Export all: File → Export Objects → HTTP/FTP/etc
│
├─ Is it from ANDROID/MOBILE?
│  ├─ First, connect with ADB
│  │  └─ adb connect IP:5555
│  │  └─ If fails: adb root
│  │
│  ├─ Is it a file/photo?
│  │  ├─ List files: adb shell ls /sdcard/DCIM/Camera/
│  │  ├─ Pull file: adb pull /sdcard/path/to/file ./
│  │  └─ Check metadata: exiftool file
│  │
│  ├─ Is it a database?
│  │  ├─ Pull database: adb pull /data/data/com.app.name/databases/app.db ./
│  │  ├─ Query database: sqlite3 app.db
│  │  └─ List tables: .tables
│  │
│  ├─ Is it hidden data?
│  │  ├─ List all files: adb shell ls -la /sdcard/
│  │  └─ Look for hidden: adb shell find /sdcard -name ".*"
│  │
│  └─ Can't connect ADB?
│     └─ Check if USB debugging enabled on device
│        └─ Or check IP/port is correct
│
├─ Is it a WIFI/WIRELESS question?
│  ├─ Do you have a .cap file?
│  │  └─ Try: aircrack-ng -w rockyou.txt -b BSSID capture.cap
│  │
│  ├─ Do you need to capture handshake?
│  │  └─ airmon-ng start wlan0
│  │     └─ airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon
│  │     └─ aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF wlan0mon
│  │
│  ├─ Is the password cracking slow?
│  │  └─ Let it run in background
│  │     └─ Can take 15-30 minutes for strong passwords
│  │
│  └─ Can't find BSSID?
│     └─ List all: airmon-ng
│        └─ Or open capture: aircrack-ng capture.cap
│
├─ Is it a WEB EXPLOITATION question?
│  ├─ Is it SQL injection?
│  │  ├─ Try: sqlmap -u "http://IP/page.php?id=1" --dbs
│  │  └─ Extract database: sqlmap -u URL -D database -T table --dump
│  │
│  ├─ Is it directory enumeration?
│  │  ├─ Try: nikto -h http://IP
│  │  └─ Or: robuster dir -u http://IP -w /usr/share/wordlists/dirb/common.txt
│  │
│  ├─ Is it a wordpress site?
│  │  └─ Try: wpscan --url http://IP --enumerate u,p,t
│  │
│  ├─ Is it parameter tampering?
│  │  └─ Test each parameter in URL/POST with different values
│  │
│  └─ Is it still not working?
│     └─ Try manual testing in Burp Suite
│        └─ Or try different endpoints
│
└─ NONE OF THE ABOVE?
   ├─ Re-read the challenge description carefully
   ├─ Check if it's asking for something specific:
   │  ├─ Exact filename?
   │  ├─ Directory path?
   │  ├─ Service version?
   │  ├─ Username (not password)?
   │  └─ Or something else?
   │
   ├─ If you've spent 20+ minutes:
   │  └─ MARK FOR LATER and move to next challenge
   │
   └─ Return in final 30 minutes if time permits
```

## Quick Decision Tables

### By Challenge Type

| Type | Tools to Try | Order |
|------|--------------|-------|
| Network Scan | nmap, enum4linux, SNMP | 1st |
| Enumeration | enum4linux, smbclient, snmpwalk | 2nd |
| Credential | Hydra, rockyou.txt | 3rd |
| Hash Cracking | hashcat, John, hashid | 4th |
| Web | SQLMAP, nikto, Burp | 5th |
| Crypto | steghide, DIE, exiftool | 6th |
| PCAP | Wireshark, tshark, tcpdump | 7th |
| Mobile | adb, sqlite3, exiftool | 8th |
| Wireless | aircrack-ng, airodump | 9th |

### By Symptom

**"I found the IP but not the credentials"**
- [ ] Try Hydra with discovered username
- [ ] Check for default credentials
- [ ] Try SMB enumeration (enum4linux)
- [ ] Check if credentials are in PCAP

**"Hydra keeps failing"**
- [ ] Verify IP address is correct
- [ ] Verify port is open: `nmap IP`
- [ ] Try different username/password list
- [ ] Check if service is actually running
- [ ] Try manual connection to verify it works

**"Hash cracking is too slow"**
- [ ] Let it run in background (check every 5 min)
- [ ] Try John the Ripper instead
- [ ] Try smaller wordlist first (rockyou-top100.txt)
- [ ] Move on to other challenges, come back later

**"Can't find the file"**
- [ ] Check if it's in a PCAP: extract with Wireshark
- [ ] Check if it's hidden: steghide extract
- [ ] Check if it's in a compressed archive: unzip/tar
- [ ] Check if it's in a database: sqlite3
- [ ] Check Android filesystem: adb shell find

**"PCAP won't open"**
- [ ] Make sure it's .pcap or .pcapng format
- [ ] Try in Wireshark (File → Open)
- [ ] If corrupted, try tshark: `tshark -r file.pcapng`
- [ ] If still fails, move to next challenge

**"ADB won't connect"**
- [ ] Check IP/port is correct: `adb connect IP:5555`
- [ ] Check if USB debugging enabled on device
- [ ] Try: `adb root`
- [ ] Restart adb: `adb kill-server && adb start-server`

**"Can't identify hash type"**
- [ ] Use: `hashid HASHVALUE`
- [ ] Check hash length:
  - 32 chars = MD5 (-m 0)
  - 40 chars = SHA1 (-m 100)
  - 64 chars = SHA256 (-m 1400)
  - 128 chars = SHA512 (-m 1700)

## When to Skip & Come Back

Skip if:
- More than 20 minutes with no progress
- Tool keeps crashing/failing
- Missing required tool/data
- Dependent on another unsolved challenge

Come back if:
- You need the answer for another challenge
- You've solved easier challenges
- Have 30+ minutes remaining
- Can make educated guess on format

## Emergency Mode (< 30 minutes left)

1. Count correct answers
2. If 14+, review and format-check existing answers
3. If <14, focus ONLY on:
   - Traffic analysis (quick Wireshark filters)
   - Network scanning (already done?)
   - Default credentials
   - Make educated guesses based on format

## Tools Status Checks

```bash
# Check Hydra progress (if running)
ps aux | grep hydra

# Check Hashcat progress
hashcat --status

# Check if Aircrack is still running
ps aux | grep aircrack

# List background jobs
jobs

# Bring job to foreground
fg %1
```

---

**Remember:** You don't need to solve all 20. You need 14 correct. Focus on getting those 14 solid answers rather than struggling with 20 mediocre attempts.
