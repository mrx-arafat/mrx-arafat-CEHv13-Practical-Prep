---
layout: default
title: Tools Cheat Sheet
parent: Quick Start
nav_order: 5
description: "Quick reference for all 85+ tools used in CEH v13 practical exam."
---

# Tools Cheat Sheet

Quick one-liner reference for the most common tools. For detailed examples, see the Domain sections.

## Network Scanning Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **nmap** | Port/service scanning | `nmap -A -T4 -p- 192.168.1.5` |
| **netdiscover** | ARP host discovery | `netdiscover -i eth0 -r 192.168.1.0/24` |
| **enum4linux** | SMB enumeration | `enum4linux -a 192.168.1.5` |
| **snmpwalk** | SNMP enumeration | `snmpwalk -c public 192.168.1.5` |
| **dig** | DNS queries | `dig @192.168.1.5 domain.com axfr` |
| **nslookup** | DNS reverse lookup | `nslookup -type=PTR 192.168.1.5` |
| **smbclient** | SMB share access | `smbclient -L //192.168.1.5 -U admin` |
| **rpcclient** | RPC enumeration | `rpcclient -U "" 192.168.1.5` |

## Credential Cracking Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **Hydra** | Brute force credentials | `hydra -l admin -P rockyou.txt rdp://IP` |
| **hashcat** | Hash cracking | `hashcat -m 0 -a 0 hash.txt rockyou.txt` |
| **John** | Hash cracking (alt) | `john --wordlist=rockyou.txt hashfile` |
| **hashid** | Hash type identifier | `hashid HASHVALUE` |
| **rockyou.txt** | Common password list | Located: `/usr/share/wordlists/rockyou.txt` |
| **crunch** | Custom wordlist generation | `crunch 8 10 -o list.txt` |

## Web Exploitation Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **sqlmap** | SQL injection | `sqlmap -u "http://IP/page.php?id=1" --dbs` |
| **nikto** | Web vulnerability scan | `nikto -h http://192.168.1.5` |
| **Burp Suite** | Web proxy/testing | Open GUI, set proxy to localhost:8080 |
| **robuster** | Directory enumeration | `robuster dir -u http://IP -w wordlist.txt` |
| **wpscan** | WordPress scanner | `wpscan --url http://target.com --enumerate u` |
| **curl** | HTTP requests (CLI) | `curl -u admin:pass http://192.168.1.5` |
| **wget** | Download files | `wget http://192.168.1.5/file.txt` |

## Cryptography & Steganography Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **steghide** | Steganography extract | `steghide extract -sf image.jpg -p ""` |
| **stegdetect** | Detect steganography | `stegdetect image.jpg` |
| **DIE** | PE file analyzer | Launch GUI, open .exe file |
| **strings** | Extract text from binary | `strings file.exe \| grep -i version` |
| **exiftool** | Image metadata extract | `exiftool image.jpg` |
| **VeraCrypt** | Encrypted volume mount | `veracrypt --mount /dev/X /mnt/point --password=PASS` |
| **binwalk** | Firmware/binary analysis | `binwalk file.bin` |
| **xxd** | Hex dump viewer | `xxd file.bin` |

## Packet Analysis Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **Wireshark** | GUI packet analyzer | Open .pcap file, apply filters |
| **tshark** | CLI packet analyzer | `tshark -r file.pcapng -Y "http" -T fields` |
| **tcpdump** | Packet capture | `tcpdump -i eth0 -w capture.pcap` |
| **tcpflow** | TCP stream extraction | `tcpflow -r capture.pcap -C` |
| **Scapy** | Packet manipulation | Python: `from scapy.all import *` |

## Wireless Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **aircrack-ng** | WPA password cracker | `aircrack-ng -w rockyou.txt -b BSSID cap.cap` |
| **airmon-ng** | Monitor mode | `airmon-ng start wlan0` |
| **airodump-ng** | Capture handshake | `airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w cap wlan0mon` |
| **aireplay-ng** | Deauth/replay | `aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF wlan0mon` |
| **kismet** | Wireless discovery | GUI: `kismet` |

## Mobile & IoT Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **adb** | Android Debug Bridge | `adb connect 192.168.1.100:5555` |
| **sqlite3** | Database query | `sqlite3 app.db ".tables"` |
| **exiftool** | Image metadata | `exiftool image.jpg` |
| **apktool** | APK decompiler | `apktool d app.apk` |
| **androguard** | Android analysis | Python tool for APK analysis |

## System Analysis Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **file** | File type detection | `file filename` |
| **strings** | Extract readable strings | `strings executable` |
| **binwalk** | Binary analysis | `binwalk file.bin` |
| **objdump** | Binary disassembler | `objdump -d executable` |
| **nm** | Symbol listing | `nm executable` |

## Utility Tools

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| **grep** | Text search | `grep -r "pattern" /path` |
| **find** | File search | `find / -name "*.db" 2>/dev/null` |
| **sed** | Text manipulation | `sed 's/old/new/g' file.txt` |
| **awk** | Data processing | `awk '{print $1}' file.txt` |
| **cut** | Column extraction | `cut -d: -f1 file.txt` |
| **sort** | Sort lines | `sort -u file.txt` |
| **uniq** | Remove duplicates | `sort file.txt \| uniq` |
| **wc** | Word/line count | `wc -l file.txt` |

## Wordlists & Resources

| Name | Location | Size | Use Case |
|------|----------|------|----------|
| **rockyou.txt** | `/usr/share/wordlists/rockyou.txt` | 139 MB | General passwords |
| **dirb/common.txt** | `/usr/share/wordlists/dirb/common.txt` | ~5 KB | Web directories |
| **dirb/big.txt** | `/usr/share/wordlists/dirb/big.txt` | ~200 KB | Larger dir enum |
| **seclists** | `/usr/share/wordlists/seclists/` | Large | All types |
| **fasttrack.txt** | Common passwords | Small | Quick brute-force |

## One-Liners by Task

### Network Reconnaissance
```bash
# Discover all open ports
nmap -p- --open 192.168.1.5

# Service enumeration
nmap -sV -sC 192.168.1.5

# SMB shares
smbclient -L //192.168.1.5 -N

# DNS zone transfer
dig @192.168.1.5 domain.com axfr
```

### Credential Cracking
```bash
# RDP brute force
hydra -l Admin -P rockyou.txt rdp://192.168.1.5

# SSH brute force
hydra -l root -P rockyou.txt ssh://192.168.1.5

# Hash cracking
hashcat -m 0 -a 0 hash.txt rockyou.txt

# Identify hash type
hashid HASHVALUE
```

### Web Testing
```bash
# SQL injection test
sqlmap -u "http://192.168.1.5/page.php?id=1" --dbs

# Directory enumeration
nikto -h http://192.168.1.5

# WordPress enumeration
wpscan --url http://target.com --enumerate u
```

### File Analysis
```bash
# Extract from image
steghide extract -sf image.jpg -p ""

# PE file analysis
strings file.exe | grep -i version

# Image metadata
exiftool image.jpg

# Database query
sqlite3 app.db "SELECT * FROM table;"
```

### Packet Analysis
```bash
# Filter HTTP traffic
tshark -r file.pcapng -Y "http" -T fields -e ip.src -e http.uri

# Find DDoS source
tshark -r file.pcapng -Y "ip.dst == TARGET_IP" -T fields -e ip.src | sort | uniq -c | sort -rn

# Extract MQTT topics
tshark -r file.pcapng -Y mqtt -T fields -e mqtt.topic | sort -u

# TTL analysis
tshark -r file.pcapng -T fields -e ip.ttl | sort -u
```

### Wireless Cracking
```bash
# Find BSSID
aircrack-ng capture.cap

# Crack WPA2
aircrack-ng -w rockyou.txt -b AA:BB:CC:DD:EE:FF capture.cap

# Monitor mode
airmon-ng start wlan0

# Capture handshake
airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon
```

### Mobile Analysis
```bash
# Connect ADB
adb connect 192.168.1.100:5555

# Pull files
adb pull /sdcard/DCIM/Camera/ ./

# Extract database
adb pull /data/data/com.app.name/databases/app.db ./

# Query database
sqlite3 app.db ".dump"
```

## Tool Availability Check

Before exam starts, verify these are installed:

```bash
# Core tools
which nmap hashcat hydra sqlmap nikto

# Analysis tools
which Wireshark tshark tcpdump adb

# Optional tools
which aircrack-ng steghide exiftool
```

## Troubleshooting Tools

| Problem | Command | Result |
|---------|---------|--------|
| "Command not found" | `which COMMAND` | Shows full path if installed |
| Check tool version | `COMMAND --version` | Verifies it's available |
| Tool documentation | `man COMMAND` | Shows manual pages |
| Locate wordlist | `find / -name "rockyou.txt"` | Finds file location |
| Check running jobs | `ps aux \| grep TOOL` | See if tool is running |
| Kill stuck tool | `pkill TOOL` | Forcefully stop |

---

**Pro Tip:** During exam, bookmark this page and use Ctrl+F to search for specific tools!
