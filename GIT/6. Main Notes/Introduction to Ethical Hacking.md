
2025-03-17 22:14

Status:

Tags:

# Introduction to Ethical Hacking
## 17/03/25

What is hacking?
hacking refers to exploitering system vulnerabilities and compromising security control to gain unauthorized or inappropriate access to the system resources it involves modifying system or application features to achieve a goal outside of the creator's original purpose.

Attack = Goal + Method + Vulnerability
goal = mind + vuln + methodologies  

Vulnerability?
Existence of a weakness in design, or implementation that can lead to an unexpected event compromising the security of the system.

What is exploit ? 
a breach of system security through vulnerabilities.

Payload?
Payload is the part of an exploit code that performs the intended malicious action on target machine.

Hacker?
Individual who spends plenty of time exploring computer hardware and software for finding
vulnerabilities and exploit them to gain unauthorized access.

Ethical Hacker?
Is a computer security expert, who specialises in penetration testing and in other testing methodologies to ensure the security of an organization's information system.
	Jobs under Ethical Hacker
		Pentester 
		Security Engineer 
		Security Consultant 

Attacks  are of two types 
1. server side 
2. clint side 
Setting up Lab
	1. Kali/Parrot 
	2. Ubuntu
	3. Windows 10/11

## 18/03/25
#### Types of Hackers

*  Black Hat (Crackers): Individuals with extraordinary computing skills, utilised for malicious or destructive activities.
*  White Hat: Individuals utilising hacking skills for defensive purpose (Security Analysts).
*  Gray Hat: Individuals who work both offensively and defensively at various times.
*  Suicide Hackers: Individuals who aim to bring down critical infrastructure for a cause and are not worried about facing punishment.
*  Script Kiddies: Unskilled hacker who compromises system by running scripts, tools, and software developed by real hackers.
* Cyber Terrorists: Individuals with wide range of skills, motivated by religious or political beliefs to create fear by large-scale disruption of computer networks.
*  Hacktivist: Individuals who promote a political agenda by hacking, especially by defacing or disabling websites.
* Government Sponsored: Individuals employed by the government to penetrate and gain top-secret information.

#### Elements of Information Security / policies
 
Information Security is a state of well-being of information and infrastructure in which the possibility of theft, tampering, and disruption of information and services is kept low or tolerable.

The CIA Triad

The foundational principles of information security are encapsulated in the **CIA triad**, which consists of:
1. Confidentiality
2. Integrity
3. Availability
4. Authenticity (Authentication/Authorization)
5. Non-Repudiation

	1. Confidentiality: refers to the protection of information from unauthorized access and disclosure. It ensures that sensitive data is accessible only to those who have the appropriate permissions.
	2. Integrity: ensures that data remains accurate, complete, and unaltered except by authorized users. It protects against unauthorized modifications, ensuring that data can be trusted. 
			Example: SHA-1 or any other SHA- helps ensure data integrity 
	3. Availability: Availability ensures that information and resources are accessible to authorized users when needed. It involves maintaining system uptime and preventing disruptions.
	4. Authenticity (Authentication/Authorization): involves verifying the identity of users or systems before granting access to resources. This includes both authentication (confirming identity) and authorization (granting access rights).
	5. Non-Repudiation: ensures that individuals cannot deny their actions related to data or transactions. It provides proof of the origin and integrity of the information.
	
CIA triad, is a model designed to guide policies for information security within an organisation.

### CEH Hacking methodology
1. Footprinting / Reconnaissance / Information-Gathering 
2. Scanning
3. Enumeration 
4. Vulnerability Analysis 
5. System Hacking 

prexploitation 
	↓
exploitation 
	↓
postexploitation 


cyber kill chain

oxbox.prg 
changing network settings 

ubuntu p-ubu
windows-0147
XEE - root - toor 
apt -cahe search ``<pakagename>``
leafpad 
learn about dpkg 

### References

**Xclip Command-Line Tool**:

- Install Xclip:
    
    bash
    
    `sudo apt-get install xclip`
    
- Copy text to clipboard:
    
    bash
    
    `echo "text" | xclip -selection clipboard`
    ubu
    mayank
network configuration
ifconfig 
eth0: flags=4163``<UP,BROADCAST,RUNNING,MULTICAST>``  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
ip add =10.0.2.15

 ## 19/03/25 
NAT

changing from NAT to bridge adapter 
direct connected to router 
bridge adapter helps to communicate vm to other vms 

uname 
hostname 
cat /etc/passwd
wc -l /etc/passwd
cat /etc/os-release 
sudo cat /etc/shadow
history 
kali㉿kali)-[~]
└─$ ls -la
-rw-------  1 kali kali   963 Mar 18 15:56 .zsh_history
sudo cat ~.zsh_history
creating directory 
	mkdir 
deleting directory 
	 rmdir 
creating balnk files ( does not required  extension )
	touch mayank.tect 
	touch mayank.text 
file for to know about kind of file 
	file mayank.text 
	mayank.text: empty
nano new 
	ctrl +s  =save 
	ctrl +x  = close 
 To kill the process 
	ctrl +c
To pause the process 
	ctrl +z
cat (used for read and crate files)
cat new (read)
hacker school is gg 
cat > file (cat  > name)(cat > (overrides contain))
dog is the main animal 
To end this same line 
	ctrl +d
to add another line use (>>) append
	cat >> file 
	maybxcjclj    

		cat >> file 
		amcshcd
		^C
	cat file    
	this 2 d line 2nd line maybxcjclj
	amcshcd
To enbeded the command into file 
	command > filename   
	iwconfig > note
To exuate all the commands
	&& 
	hostname && uname 
	kali
	Linux
y- forcefully yes    
To create parent directory 
	mkdir -p HS/{CEH,CPEN,SOC}
mkdir -p HS/{CEH,CPEN,SOC} && touch HS/CEH/notes HS/CPEN/practice.text
	tree
	.
	├── file
	├── HS
	│   ├── CEH
	│   │   └── notes
	│   ├── CPEN
	│   │   └── practice.text
	│   └── SOC
To remove directory 
	rm -r ( remove recursive )
	rm -r HS   
To copy file directory and contain of  file 
	cp
	cp mayank.text /home/kali/Desktop/HS/SOC 
		 tree
		.
		├── file
		├── HS
		│   ├── CEH
		│   │   └── notes
		│   ├── CPEN
		│   │   └── practice.text
		│   └── SOC
		│       └── mayank.text
		├── mayank.tect
		├── mayank.text
		├── new
		├── note
		└── SBI
To move file and rename file 
	mv 
	mv "``<exfile> <nonexfile >``" (rename file)
	 mv" ``<exfile> <exdir>``" (copy file to )
	 
to crate 10 file 
touch test{1..10}
rm *(remove all)
rm -rf*(remove all re)

AI-Driven Ethical Hacking 
AI-Driven Ethical Hacking enchases the efficiency, effectiveness  and scope of cybersecurity measures.
 - Automation of repetitive task 
 - predictive Analysis 
 - Advanced Threat Detection 
 - Enhanced Reporting 
 - Continuous Monitoring 

AI Won't replace ethical hacker 
It will chnage how they work 

PentestGPT 
MalicaiousGPT

Deepfake (image randomly) =https://this-person-does-not-exist.com/en
sock pupates account 
sgpt (paid)
tgpt (free)

### 20/03/25

To add user 
	sudo adduser mayank 
	sudo useradd mayank 

To view all the user 
	cat /etc/passwd 
To switching from one user to another 
	sudo su username
To change password of user 
	passwd  
To add group 
	sudo addgroup CEH 
To view all the groups 
	cat /etc/group 
To display last 10 line 
		tail -10 /etc/passwd
	To display top 10 line 
		 head -10 /etc/passwd
To search 
	| grep
	|= (pipe) cat /etc/group | grep sudo 
				or 
	grep ceh cat /etc/group 
To file permissions 
	u     g      o
	(rwr)(r--)(r--)
	r-read-4
	w-write-2
	x-execute-1
	u-owner/user
	g-group
	o-others 
To change permissions 
	chmod 
		chmod g+w notes.text 
		chmod +x note.ext
To add group to
	  sudo adduser username sudo
	usermod -aG ``<groupname > <username>``
	 usermod -aG 
To change ownership in gr
	sudo chown kali:ceh CEH1
		 sudo chown user:ceh CEH

To allow any user to ready any file (edit =use visudo)


To search for a command 
	whereis cat
	cat: /usr/bin/cat /usr/share/man/man1/cat.1.gz


Things to do after you went home learn about
1.  to remove user from sudo group 
2. remove group 
3. sudoers
4. bin 
5. directory tree
To find or search files 
find (live search )or locate (per-database) 
find
sudo find / -name note.ext
To remove error 
sudo find / -name note.ext 2>/dev/null (null-blackhole) 
locate 
To update locate 
sudo updatedb
To archive files
tar 
To compress the file 



### Keytakeaways 
for any query
jayanth.b@cartelsoftware.com

website to practices linux commands 
website - https://linuxsurvival.com/
book - Linux basis for hacker 
for web application
web application hacker's handbook

solve some challenges
over the wire ([h](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://overthewire.org/&ved=2ahUKEwia57WhxZqMAxWFzDgGHT6JHtIQFnoECA0QAQ&usg=AOvVaw2GzzS5s17KISE9-ZlxxohF)) 
	
	ssh (remote login clint id   and password )
	to connect to ssh clint we command 
		ssh <username>@<IP/domainname>
		ssh bandit0@bandit.labs.overthewire.org -p220

 tips for jobs is  
budling networking 
make connection for jobs by connecting who is working for cyber security 
ask what skills required for job 
what kind of certifiaction they are looking for 
what kind of tools there use 
and make cv and linked  


linux harding 
Mindset for learning is to where can i apply 
ask ai for help and not walkthroughs 
Things to do after you went home learn about
1.  to remove user from sudo group 
2. remove group 
3. sudoers
4. bin 
5. directory tree
To find or search files 
find (live search )or locate (per-database) 
find
sudo find / -name note.ext
To remove error 
sudo find / -name note.ext 2>/dev/null (null-blackhole) 
locate 
To update locate 
sudo updatedb
To archive files
tar 
To compress the file
 








