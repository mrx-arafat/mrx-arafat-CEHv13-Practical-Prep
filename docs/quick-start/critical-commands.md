---
layout: default
title: Critical Commands
parent: Quick Start
nav_order: 2
description: "Essential commands to memorize for CEH v13 practical exam."
---

# Most Critical Commands (Memorize These)

These are the commands you'll use in 80% of challenges. Memorize these or bookmark this page.

## Network Scanning

### NMAP - The Foundation

```bash
# Comprehensive scan (start this first!)
nmap -A -T4 -p- 192.168.1.5

# Service detection and OS fingerprinting
nmap -sV -sC -O 192.168.1.5

# Quick scan for open ports only
nmap --open 192.168.1.5

# UDP scan (for SNMP)
nmap -sU -p161 192.168.1.5

# SMB-specific scan
nmap --script smb-os-discovery.nse -p445 192.168.1.5

# Ping scan only (no port scanning)
nmap -sn 192.168.1.0/24
```

### Enumeration

```bash
# SMB enumeration (windows shares/users)
enum4linux -a 192.168.1.5

# SNMP enumeration
snmpwalk -c public 192.168.1.5

# DNS zone transfer (if AXFR enabled)
dig @192.168.1.5 domain.com axfr

# DNS reverse lookup
nslookup -type=PTR IP

# SMTP user enumeration
smtp-user-enum -M VRFY -U users.txt -t 192.168.1.5
```

## Credential Cracking

### Hydra - Brute Force

```bash
# RDP brute force
hydra -l Admin -P rockyou.txt rdp://192.168.1.50

# SSH cracking
hydra -l root -P rockyou.txt ssh://192.168.1.5

# FTP brute force
hydra -l admin -P wordlist.txt ftp://192.168.1.5

# HTTP POST login
hydra -l admin -P rockyou.txt http-post-form://192.168.1.5:"/login:user=^USER^&pass=^PASS^:F=incorrect"

# SMB brute force
hydra -l Administrator -P rockyou.txt smb://192.168.1.5

# MySQL brute force
hydra -l root -P rockyou.txt mysql://192.168.1.5
```

### Hashcat - Hash Cracking

```bash
# Identify hash type first
hashid hash_value

# MD5 cracking (mode 0)
hashcat -m 0 -a 0 hashfile rockyou.txt

# SHA1 cracking (mode 100)
hashcat -m 100 -a 0 hashfile rockyou.txt

# SHA256 cracking (mode 1400)
hashcat -m 1400 -a 0 hashfile rockyou.txt

# Windows NTLM (mode 1000)
hashcat -m 1000 -a 0 hashfile rockyou.txt

# With rules for better coverage
hashcat -m 0 -a 0 hashfile rockyou.txt -r /usr/share/hashcat/rules/best64.rule
```

### John the Ripper (Alternative)

```bash
# Auto-detect hash type
john --wordlist=rockyou.txt hashfile

# Specific mode
john --format=md5 --wordlist=rockyou.txt hashfile

# Show cracked passwords
john --show hashfile
```

## Web Exploitation

### SQLMAP - SQL Injection

```bash
# Basic test
sqlmap -u "http://192.168.1.5/page.php?id=1"

# Extract databases
sqlmap -u "http://192.168.1.5/page.php?id=1" --dbs

# Extract tables from database
sqlmap -u "http://192.168.1.5/page.php?id=1" -D databasename --tables

# Extract data from table
sqlmap -u "http://192.168.1.5/page.php?id=1" -D databasename -T tablename --dump

# OS shell (if possible)
sqlmap -u "http://192.168.1.5/page.php?id=1" --os-shell
```

### Nikto - Web Vulnerability Scanner

```bash
# Basic scan
nikto -h http://192.168.1.5

# Specify port
nikto -h http://192.168.1.5:8080

# Save to file
nikto -h http://192.168.1.5 -o report.html

# Specify directory
nikto -h http://192.168.1.5 -d /admin
```

### Robuster - Directory Enumeration

```bash
# Basic directory bruteforce
robuster dir -u http://192.168.1.5 -w /usr/share/wordlists/dirb/common.txt

# Specify status codes to show
robuster dir -u http://192.168.1.5 -w common.txt -s 200,301,302,401,403

# Recursive scan
robuster dir -u http://192.168.1.5 -w common.txt -r

# With custom headers
robuster dir -u http://192.168.1.5 -w common.txt -H "User-Agent: Mozilla"
```

### WPScan - WordPress

```bash
# Enumerate users
wpscan --url http://target.com --enumerate u

# Enumerate plugins
wpscan --url http://target.com --enumerate p

# Enumerate themes
wpscan --url http://target.com --enumerate t

# Password attack
wpscan --url http://target.com -U users.txt -P rockyou.txt
```

## Cryptography & Steganography

### Steganography

```bash
# Extract from image
steghide extract -sf image.jpg -p ""

# Extract with password
steghide extract -sf image.jpg -p "password"

# List embedded data
steghide info image.jpg

# Embed data
steghide embed -cf image.jpg -ef secret.txt -p "password"
```

### PE File Analysis (DIE)

```bash
# Open executable in GUI
DIE filename.exe

# Command line analysis
file filename.exe
strings filename.exe | grep -i "version\|company\|productname"

# Get compilation timestamp
exiftool filename.exe
```

### Cryptography Tools

```bash
# VeraCrypt mounting
veracrypt --mount /dev/sdb1 /mnt/encrypted --password=PASSWORD

# OpenSSL hash comparison
echo -n "string" | openssl md5
echo -n "string" | openssl sha1
echo -n "string" | openssl sha256

# Identify hash from length
# 32 chars → MD5
# 40 chars → SHA1
# 64 chars → SHA256
# 128 chars → SHA512
```

## Packet Analysis

### Wireshark Filters

```bash
# Filter by IP
ip.src == 192.168.1.5
ip.dst == 192.168.1.5

# Filter by port
tcp.port == 3306
udp.port == 53

# Filter by protocol
http
ftp
ssh
mqtt

# Combine filters
(ip.src == 192.168.1.5) && (tcp.port == 80)

# Find DDoS sources
ip.dst == 172.22.10.10

# TTL analysis (Windows = 128, Linux = 64)
ip.ttl == 128

# Extract credentials
ftp.request.command == 'USER' or ftp.request.command == 'PASS'
http.request.method == 'POST'
```

### Tcpdump

```bash
# Capture traffic
tcpdump -i eth0 -w capture.pcap

# Filter by IP
tcpdump -i eth0 -w capture.pcap host 192.168.1.5

# Filter by port
tcpdump -i eth0 -w capture.pcap port 80

# Print to screen
tcpdump -i eth0 -A host 192.168.1.5

# Read existing pcap with filter
tcpdump -r capture.pcap tcp port 80
```

### Tshark - CLI Wireshark

```bash
# Read PCAP and apply filter
tshark -r capture.pcapng -Y "http" -T fields -e http.request.uri

# Filter by IP
tshark -r capture.pcapng -Y "ip.src == 192.168.1.5"

# Extract HTTP requests
tshark -r capture.pcapng -Y http -T fields -e http.host -e http.request.uri

# MQTT topics
tshark -r capture.pcapng -Y mqtt -T fields -e mqtt.topic
```

## Mobile/IoT (Android)

### ADB Commands

```bash
# Connect to Android device
adb connect 192.168.1.100:5555

# List connected devices
adb devices

# Access shell
adb shell

# List files
adb shell ls /sdcard/DCIM/Camera/

# Pull files from device
adb pull /sdcard/DCIM/Camera/image.jpg ./

# Gain root access
adb root

# Extract database
adb pull /data/data/com.example.app/databases/app.db ./

# List installed apps
adb shell pm list packages

# Install APK
adb install myapp.apk
```

### Database Analysis

```bash
# SQLite3 analysis
sqlite3 app.db

# List tables
.tables

# Query table
SELECT * FROM tablename;

# Export to CSV
.headers on
.mode csv
.output output.csv
SELECT * FROM tablename;
```

### File Metadata

```bash
# Extract EXIF data
exiftool image.jpg

# Check file type
file image.jpg

# Search for keywords in files
grep -r "password" /sdcard/
```

## Wireless Cracking

### Aircrack-ng Suite

```bash
# Find BSSID in capture file
aircrack-ng Credmapwifi.cap

# Crack WPA2 password
aircrack-ng -w /usr/share/wordlists/rockyou.txt -b AA:BB:CC:DD:EE:FF Credmapwifi.cap

# Put adapter in monitor mode
airmon-ng start wlan0

# Capture handshake
airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w Credmapwifi wlan0mon

# Deauth attack (force re-handshake)
aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF wlan0mon
```

## Quick Reference by Task Type

| Task | Command | Tool |
|------|---------|------|
| Find open ports | `nmap -p- IP` | nmap |
| Enumerate SMB | `enum4linux -a IP` | enum4linux |
| Crack hash | `hashcat -m 0 -a 0 hash rockyou.txt` | hashcat |
| Crack password | `hydra -l user -P pass.txt rdp://IP` | hydra |
| SQL injection | `sqlmap -u URL --dbs` | sqlmap |
| Extract from image | `steghide extract -sf image.jpg -p ""` | steghide |
| Analyze PCAP | Open in Wireshark, filter | Wireshark |
| Connect Android | `adb connect IP:5555` | adb |
| Crack WiFi | `aircrack-ng -w rockyou.txt -b BSSID capture.cap` | aircrack-ng |

---

**Tip:** During exam, use Ctrl+F to search this page for specific tool commands.
