2025-09-02 22:12

Status:

Tags:

# CEH short

- start E to view machine using 
1. `` sudo arp-scan -local or netdiscover -i 10.10.1.0 or nmap -sn ip/24  ``


- command for searching file in 
	- ``find / -name filename -type f 2>/dev/null  ``
	- ``find / -name acsa.txt -type f 2>/dev/null > cat 5sa.txt ``

- extract data from  image 
	- using OpenStego
	- ``steghide extract -sf stealth.jpeg -p azerty@123``

- vulnerability scan host with IP address
	- ``nmap -Pn  --script vuln <IP> ``

- chat gpt setup 
	- ``cd /home/attacker ``
	- `` bash sgpt.sh ``
	- enter the api

- to analyze log file IDE
	- Tail cowrie.log
- share files using smb 
	- ``Smbclient //ip/CEH-Tools -U Admin``
### References
- ports and protocol

| **Port Number** | **Service**                                    | **Protocol** |     |
| --------------- | ---------------------------------------------- | ------------ | --- |
| 20, 21          | FTP (File Transfer Protocol)                   | TCP          |     |
| 22              | SSH (Secure Shell)                             | TCP          |     |
| 23              | Telnet                                         | TCP          |     |
| 25              | SMTP (Simple Mail Transfer Protocol)           | TCP          |     |
| 53              | DNS (Domain Name System)                       | TCP/UDP      |     |
| 67, 68          | DHCP (Dynamic Host Configuration Protocol)     | UDP          |     |
| 80              | HTTP (HyperText Transfer Protocol)             | TCP          |     |
| 88              | Kerberos / AS-REP Roasting                     |              |     |
| 110             | POP3 (Post Office Protocol)                    | TCP          |     |
| 123             | NTP (Network Time Protocol)                    | UDP          |     |
| 143             | IMAP (Internet Message Access Protocol)        | TCP          |     |
| 161, 162        | SNMP (Simple Network Management Protocol)      | UDP          |     |
| 389             | LDAP (Lightweight Directory Access Protocol)   |              |     |
| 443             | HTTPS (HyperText Transfer Protocol Secure)     | TCP          |     |
| 455             | SMB, Active Directory, Windows shares          |              |     |
| 465             | SMTPS (SMTP Secure)                            | TCP          |     |
| 993             | IMAPS (IMAP Secure)                            | TCP          |     |
| 995             | POP3S (POP3 Secure)                            | TCP          |     |
| 1433            | SQL server                                     |              |     |
| 3389            | RDP (Remote Desktop Protocol) / domain control | TCP          |     |
| 5555            | Android Debug Bridge (ADB)                     |              |     |
| 6703            | e-design-web (RAT)                             |              |     |
| 9871            | Hadoop HDFS NameNode HTTPS (RAT)               |              |     |
