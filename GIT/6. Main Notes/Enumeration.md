2025-03-31 16:35

Status:

Tags:
# Enumeration

## 28/03/25

# Enumeration

* Enumeration extends the amount of information you have about a target network - it gives you even more information at a deeper level of detail.
* Enumeration involves making active connection to the target and run built-in OS commands and utilities with no credentials.
* Trying to get information in the form of error messages fromtarget host.

## Services running 

Running Scripts 

Step1: 
 * locate *.nse | grep ftp
  
 To identify  which script  is used for FTP  Anonymous  

	  ftp-anon.nse

 Step2: 
* nmap 10.10.10.6  --script script name or script location

	  sudo nmap 10.10.10.6 -Pn -p21 -n --script ftp-anon.nse  
Next
### port 21 - FTP   services
- check Anonymous login
- sudo nmap 10.10.10.6 -Pn -p21 -n --script ftp-anon.nse( anonymous : ftp <IP>)

- Login using Anonymous login

ftp ``<IP>``

``login : anonymous or ftp``

``password :``

- We can upload or download files or change directories 

- check file upload or download 

	- ``put`` command to upload  the file 
	
		- put test.xt
	
	- ``get``  Command to download file
		- get tikiwiki-1.9.11.zip
* Checking vulnerabilities

	* locate *.nse | grep ftp 

	- nmap --script-help=<scriptname>

	- nmap --script  ftp-vsftpd-backdoor.nse
		- nmap --script  ftp-vsftpd-backdoor.nse -p21 10.10.10.6
- Brute forec the password 
	- sudo nmap <IP> -Pn -n -p21 --script  ftp-brute.nse
### Port 22 - SSH
Locate scripts for ssh

	locate *.nse | grep ssh

-  Execute namp scripts
	- sudo nmap 10.10.10.6 -Pn -n -p22 --script ssh-hostkey.nse 
- If we know user name and password then login 
 
	 * ssh <username>@<IP/domain name >
- Brute forec the password 

	 - sudo nmap 10.10.10.6 -Pn -n -p22 --script ssh-brute.nse

### port 445 - SMB

 check for anonyms  share 

	 smbmap -H <IP>
	 smbmap -H 10.10.10.6
If we know user name and password then login 

     smbmap -H  <IP> -u username -p password 
     smbmap -H  10.10.10.6 -u  -p   ( for windows )
To connect with Metaspoiable2 

	 smbclient //10.10.10.6/tmp 
- Check file upload or download 
	
	- using put
	
	- unsing get

If there is an error and fix config file 

	 sudo nano /etc/samba/smb.conf 
- To idendefiy username  in linux 
	
	- enum4linux


 Net buyers score 
- on windows 
	-  nbstat
		
		- ``sudo nbtsat -r 10.0.0.1/24``
	
- on linux 
	- nbtscan 
		
		- ``sudo nbtscan  -r 10.0.0..1/24``

Linux utility 
- for getting specific thing 
- using cut 
- grep 

``enum4linux -U 10.10.10.6| grep user: |cut -d [ -f 2 | cut -d ] -f 1 ``


#### extra 
Locate scripts for SMB

```
locate *.nse | grep smb
```

- Execute namp scripts
    
    - sudo nmap 10.10.10.6 -Pn -n -p22 --script smb-os-discovery.nse




if there is an error and fix config file 
sudo nano /etc/samba/smb.conf 
* on windows - nbstat
* on linux -nbtscan <IP> Iidentify host names 
*check for anonymos share 
	list sahres -smbmap  -H <IP>
	   
## Password Cracking 

- **Dictionary Based Attack -** 
	- All words in the dictionary are tried as the victim's password.

- **Brute Force Attack -**
	- All possible permutations & combinations of the keyboard are tried as the victim's password. Obviously all passwords have to be some kind of permutation or combination of victim's keyboard.
	- Brute Force Attack Tools 
		1. Hydra 
		2. Medusa 
- **Syllable attack -**
	- Combination of both, brute force attack and a dictionary attack. This is often used when the password is a nonexistent word.


 ### Hydra

Syntax 
- ``hydra -l <username> -p <password> <service name>//<IP>``

		   hydra -l msfadmin -p msfadmin ftp://10.10.10.6 

If you don't know username and password 

- ``hydra -L users. txt -ensr ftp://10.10.10.6``  
		(L-FILE  login) (-e nsr    try "n" null password, "s" login as pass and/or "r" reversed login)

SSH

hydra -L users. txt -P passwword.txt ssh://10.10.10.6

SMB

hydra -L users. txt -P passwword.txt smb://10.10.10.6

### Built word list and password list 
Tools used for creating wordlist and password list, we use the following tools  
1. cewl 
2. cupp
3. curnch 
#### cewl
cewl  -m 5 -d2 https://adc.edu.in

To save the word list in file 
- use -w
- cewl  -m 5 -d2 https://adc.edu.in -w user.txt

#### cupp
cupp is automatic tools which creates username and password.
- Install cupp using git 
- cd to cupp
- to run cupp 
	- ./cuppy.py
	- ./cuppy.py -i (interactive)

 #### crunch
 crunch is tool which uses permutation and combinations  

``crunch <min> <max> [options]``
To know the user manual we use 
- man crunch 

Examples 

- crunch 8 8 -t admin%%%
	- admin000
	- admin123
	- admin456

- crunch 9 9 -t admin@%%% -l aaaaa@aaa
	- admin@123
	- admin@456
	- admin@469

- crunch 30 30 -p varun vamshi pasha mohansai mayank
	- mayankmohansaipashavamshivarun
	- mayankmohansaipashavarunvamshi
	- mayankmohansaivamshipashavarun
	- mayankmohansaivamshivarunpasha
	- mayankmohansaivarunpashavamshi
	- mayankmohansaivarunvamshipasha
	- mayankpashamohansaivamshivarun
To check is your password is how strong 
	ismy password strong 

 


## 01/04/25

#### Medusa 
Syntax for medusa 

	 medusa -U user.txt -P password.txt   -h <IP> or -H <list of IPs > -M ssh
	 medusa -U user.txt -P password.txt   -h <IP> -n  -M ftp (-n = port number )  

medusa -u jack -p Cyberspace -M ftp -h 10.10.10.7 

To check help menu for namp script, we use this command 

	nmap --script-help  ''<scriptt name >

To use namp script along with username and password 

	nmap  --script <scriptt name >  --script -args userdb= <file name> ,passdb= <file name> <IP> -p 

What if there is no nmap in you machine then how to use by 

	https://github.com/andrew-d/static-binaries/tree/master/nmap
ssh login 

if you are getting error while connectig the shh to fix 

sudo  nano /etc/ssh/ssh_config 

	HostKeyAlogorithms  +ss-rs
	PubKeyAcceptedKeyTypes +ssh-rsa
 How to  start ssh service in your kali 

	 sudo service ssh start 
To check the status of ssh

	sudo service ssh status 
checking through ports 

	netstat -antp | grep  22

### **DNS - Domain Name System**
- Internet equivalent of the phone book. They maintain the directory of domain names & translate them to internet protocol address. 

**DNS Records** 

- The list of DNS records provide an overview of types of resource records stored in the zone files of the domain name system. 

- The DNS implements a distributed, hierarchical and redundant database for information associated with internet domain names & addresses.

	![[DNS .png]]

To check which DNS is running in your system 

	cat /etc/resolv.conf

To start apache service 

	sudo service apache2 start

- you can change ISP using public DNS 
	- google DNS - 8.8.8.8
	
	- Cloudflare - 1.1.1.1 

#### DNS Zone Transfer 

Non-Authoritative Response
		![](https://miro.medium.com/v2/resize:fit:700/1*20lOJctutX1PTdWzYUbbZQ.png)






- Used to replicate DNS data across a number of DNS servers or to backup DNS files. A user or server.
  - DNS servers should not permit transfer towards any Ip address from internet 
  - since zone file contain complete information about domain n names, subdomains and IP address configured on the target name server, finding this information is useful for incresing you attack surface and for better understanding the internet structure of the target company.




#### DNS enumeration 

To collect inforamation about DNS 

dnsenum

  dnsenum --enum  tata.com 

/

#### DNS Records types and  uses 

[![Understanding Different Types of Record in DNS Server - 2 (1)](https://www.cloudtechadmin.com/wp-content/uploads/2019/03/Understanding-Different-Types-of-Record-in-DNS-Server-2-1.png)](https://www.cloudtechadmin.com/wp-content/uploads/2019/03/Understanding-Different-Types-of-Record-in-DNS-Server-2-1.png)

	 dnsenum  --enum zonetransfer.me



#### dig 
- dig is usec for DNS enumeration for domain or dns 
- Syntax
	
	``dig  <records > @<nameserver> <domin name >``
	 
	 ``dig ns @nsztm1.digi.ninja. zonetransfer.me``
	
	``dig axfr  @nsztm1.digi.ninja. zonetransfer.me``

done 



challenges
1. Identity the IP address of macnine running windows 7 in 10.0.0.1/24 network




### References
