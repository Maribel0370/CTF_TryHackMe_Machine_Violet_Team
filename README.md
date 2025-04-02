# CTF_TryHackMe_Machine_Violet_Team
This repository contains our notes, exploits, and strategies for solving the CTF machine on TryHackMe. Our goal is to document the attack process, share knowledge, and improve our cybersecurity skills as a team. 🚀💀
#First Commands and Initial Questions
Here are the first six questions we encountered and the initial commands we used to begin our enumeration:

┌──(kali㉿kali)-[~]
└─$ nmap -v -A -sC -Pn 10.10.26.176 -p-
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-01 14:01 EDT
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 14:01
Completed NSE at 14:01, 0.00s elapsed
Initiating NSE at 14:01
Completed NSE at 14:01, 0.00s elapsed
Initiating NSE at 14:01
Completed NSE at 14:01, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 14:01
Completed Parallel DNS resolution of 1 host. at 14:01, 0.01s elapsed
Initiating SYN Stealth Scan at 14:01
Scanning 10.10.26.176 [65535 ports]
Discovered open port 22/tcp on 10.10.26.176
Discovered open port 80/tcp on 10.10.26.176
SYN Stealth Scan Timing: About 39.27% done; ETC: 14:03 (0:00:48 remaining)
Discovered open port 1880/tcp on 10.10.26.176
Completed SYN Stealth Scan at 14:03, 73.93s elapsed (65535 total ports)
Initiating Service scan at 14:03
Scanning 3 services on 10.10.26.176
Completed Service scan at 14:03, 12.67s elapsed (3 services on 1 host)
Initiating OS detection (try #1) against 10.10.26.176
Initiating Traceroute at 14:03
Completed Traceroute at 14:03, 0.10s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 14:03
Completed Parallel DNS resolution of 2 hosts. at 14:03, 0.09s elapsed
NSE: Script scanning 10.10.26.176.
Initiating NSE at 14:03
Completed NSE at 14:03, 1.93s elapsed
Initiating NSE at 14:03
Completed NSE at 14:03, 0.21s elapsed
Initiating NSE at 14:03
Completed NSE at 14:03, 0.00s elapsed
Nmap scan report for 10.10.26.176
Host is up (0.054s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey: 
|   3072 f0:e6:24:fb:9e:b0:7a:1a:bd:f7:b1:85:23:7f:b1:6f (RSA)
|   256 99:c8:74:31:45:10:58:b0:ce:cc:63:b4:7a:82:57:3d (ECDSA)
|_  256 60:da:3e:31:38:fa:b5:49:ab:48:c3:43:2c:9f:d1:32 (ED25519)
80/tcp   open  http    Apache httpd 2.4.56 ((Debian))
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-title: Apache2 Debian Default Page: It works
|_http-server-header: Apache/2.4.56 (Debian)
1880/tcp open  http    Node.js Express framework
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-favicon: Unknown favicon MD5: 818DD6AFD0D0F9433B21774F89665EEA
|_http-title: Node-RED
|_http-cors: GET POST PUT DELETE
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
Uptime guess: 6.023 days (since Wed Mar 26 13:30:08 2025)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=265 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 9979/tcp)
HOP RTT      ADDRESS
1   93.27 ms 10.8.0.1
2   93.19 ms 10.10.26.176

NSE: Script Post-scanning.
Initiating NSE at 14:03
Completed NSE at 14:03, 0.00s elapsed
Initiating NSE at 14:03
Completed NSE at 14:03, 0.00s elapsed
Initiating NSE at 14:03

# Nessus Scan and Vulnerability Discovery
# A scan was conducted using Nessus to identify potential vulnerabilities. During the scan, a critical vulnerability with a CVSS score of 9.8 was discovered in Apache. A screenshot of the findings has been generated and included for reference.
# Nessus Scan and Vulnerability Discovery
# A scan was conducted using Nessus to identify potential vulnerabilities. During the scan, a critical vulnerability with a CVSS score of 9.8 was discovered in Apache. A screenshot of the findings has been generated and included for reference. Additionally, a full Nessus report has been created and is available for review.


Completed NSE at 14:03, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 90.95 seconds
           Raw packets sent: 68506 (3.015MB) | Rcvd: 68237 (2.730MB)

