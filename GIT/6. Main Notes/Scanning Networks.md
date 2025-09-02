2025-03-25 23:45

Status:

Tags:

# Scanning Networks
### 25/03/25

#### Scanning:
Scanning is performed to collect network related information about the target. To identify IP/Host name, Ports, Services, Live Hosts, Vulnerable services running on the target network.
* Types of Scanning
	1. Network Scanning
	2. Port Scanning
	3. Vulnerability Scanning

#### OSI Model 
	Layers

   [![OSI 7 layers](https://www.imperva.com/learn/wp-content/uploads/sites/13/2020/02/OSI-7-layers.jpg.webp)](https://www.imperva.com/learn/wp-content/uploads/sites/13/2020/02/OSI-7-layers.jpg.webp)

TCP/ IP Model 

 ![OSI MODEL vs TCP/IP MODEL](https://media.licdn.com/dms/image/v2/D4E22AQHT7n28jhbGeg/feedshare-shrink_2048_1536/feedshare-shrink_2048_1536/0/1694076569075?e=2147483647&v=beta&t=XqEVbVHYIkTu0lb8nQ4Zudfon0ICVOlfvoOMhQtkimE)


#### IPv4 Address Format /classes
IPv4 Address format 
				![IPv4 Address Format](https://www.cloudns.net/blog/wp-content/uploads/2023/03/IPv4-Address-Format.png)
IPv4 Address classes 
				![What are the classes of IPv4 Addresses | Blog | Adroit Information Technology Academy (AITA)](https://www.adroitacademy.com/web-portal/img/blog/43892065.jpg)
IPv4 Address classification
				![IPv4 Address (Internet Protocol Address) | Range of IPv4 Address](https://media.licdn.com/dms/image/v2/D5612AQGW8pEmr7LIXA/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1692180202486?e=2147483647&v=beta&t=8JiUUmukmNrAihOZMrSVld7z4QM_JTMWoYFbxoicbOs)

To identify on which of these classes we are in
	using ifconfig 
		eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        ==(IP) === inet 10.0.0.197  netmask 255.255.255.0  broadcast 10.0.0.255
		 netmask 255.255.255.0
			First three are network identifications bits (255.255.255) and Last one is for Host (0) 
		broadcast (range) 10.0.0.255
			from 10.0.0.0 to 10.0.0.255
			10.0.0.1 is for gateway (router) and 10.0.0.255 is for broadcast's IP
			Starting from
				10.0.0.0 
				10.0.0.1
				10.0.0.2
				.
				.
				10.0.0.255

network and host identification
IP address classification 
TO identification of public or   ip 

#### Network Scanning 
Network Scanning is a procedure for identifying active hosts on a network, either for the purpose of attacking them or for network security assessment.
Network Scanning tools 
1. Anger IP Scanner
2. Nmap
3. Advanced IP Scanner (for windows)
Basic one 
		To check device is active or not using ping(public and private IP)
		ping -c2 10.0.0.4
	using fping 
		fping -aqg 10.0.0.1/24
			10.0.0.1
			10.0.0.111
			10.0.0.119
			10.0.0.130
			10.0.0.132
			10.0.0.145
			10.0.0.144
			10.0.0.146
			10.0.0.148
			10.0.0.155
			10.0.0.157
			10.0.0.156
			10.0.0.168

   ARP Porto call (use case if fping fails then uses and it works on  private ) 
	   sudo arping  10.0.0.235
using arp-scan
	sudo arp-scan  10.0.0.1/24
Netdiscover 
sudo netdiscover -r 10.0.0.1/24 -p
	or 
 sudo netdiscover -p -i eth0
 Angry ip Scanner (GUI) 


Wireshark 
add filter arp 
add filter icmp

Nmap 
Host Discovery - using -sn option 
* when performed as normal user will sent TCP SYN packet to port 80 and TCP SNY packet to port 443. If we receive repones for any one of the packet then, Nmap will display host is up.
* When performed as root user will send ARP packet. If we receive a response then Nmap will display hot is up.  
* when performed as root user when ARP is blocked then Nmap will sent 4 packet - 
  TCP SYN to port 443, ACK to port 80, ICMP echo request and ICMP time stamp request.

		 nmap -sn 10.0.0.1/24  (-sn disable port )
Open wire shark 
set filter 
	ip.addr == 10.0.0.197

### 26/03/25
#### Port Scanning 
Ports are doors through which data is exchanged between two different  devices. Port Scanning is used to find out active ports (65536 virtual ports), applications running on ports and OS running on target computer.
	Number of ports 
		0   - 1023 - Well known ports 
		1024 - 49135 - Random ports 
		49136 - 65535 -Experimental ports 

#### NAT setting 
Network Address Translation (NAT)
		* Under NAT settings from host machine router is created for every virtual machine  
		* While Host machine cannot connect default using NAT.  but port forwarding can be configured to enable communication.
				![virtualbox nat mode](https://sp-ao.shortpixel.ai/client/to_webp,q_glossy,ret_img,w_825,h_464/https://cysecon.com/wp-content/uploads/2021/09/Din-Img-3-1024x576.png)

 
NAT Network :
	Creates only one router for all the VM's 
	All VM's  can connect with each other, but host machine can not connect with VM's
			![virtualbox nat network mode](https://sp-ao.shortpixel.ai/client/to_webp,q_glossy,ret_img,w_825,h_464/https://cysecon.com/wp-content/uploads/2021/09/Din-Img-4-1024x576.png)
 Creating NAT Network in Virtual Box
	1. **Open VirtualBox Preferences**:
	    
	    - Launch Oracle VM VirtualBox Manager.
	        
	    - Go to **Tools** > **Network**.
	        
	2. **Navigate to the Network Tab**:
	        
	    - Select the **NAT Networks** sub-tab.
	        
	3. **Add a New NAT Network**:
	    
	    - Click on the **Create** (plus) icon on the right side to add a new NAT Network.
	        
	4. **Configure the NAT Network**:
	    
	    - After adding, select the new NAT Network entry and click on the **Edit** button (wrench icon).
	        
	    - Set parameters such as:
	        
	        - **Network Name**: Assign a name for easy identification.
	            
	        - **Network CIDR**: Define the network address and subnet mask (e.g., `192.168.10.0/24`).
	            
	        - **Supports DHCP**: Enable this option if you want the NAT Network to provide DHCP services to connected VMs.
	
	5. **Save Configuration**:
	    
	    - Click **OK** to save your settings.
	        
	    - The newly created NAT Network will now appear in the list.
	        
	6. **Assigning NAT Network to a VM**:
	    
	    - Select a VM from the main window and click on **Settings**.
	        
	    - Go to the **Network** tab, enable one of the adapters, and set it to attach to the NAT Network you created.
	        
	    - Choose your NAT Network from the dropdown menu and click **OK**.
Connected using NAT Network 
	IP (kali Linux) =10.10.10.4
	IP (windows 10) =10.10.10.5
	IP (meta2) =10.10.10.6
Port Scanning
Most network applications run on top of TCP or UDP. These protocols are the transport mechanism used by many applications like FTP, Simple Mail Transfer Protocol (SMTP), Dynamic Host Configuration Protocol (DHCP), and HTTP. TCP - connection-oriented protocol UDP - connectionless protocol 

##### Port Numbers / List

| **Application** | **Port Number** | **Full forms**                                         |
| --------------- | --------------- | ------------------------------------------------------ |
| FTP             | 20/21           | File Transfer Protocol - (Data Transfer) / (Control)   |
| SSH             | 22              | Secure Shell                                           |
| Telnet          | 23              | Telnet                                                 |
| SMTP            | 25              | Simple Mail Transfer Protocol                          |
| DNS             | 53              | Domain Name System                                     |
| DHCP            | 67/68           | Dynamic Host Configuration Protocol (Server)/ (Client) |
| HTTP            | 80              | Hypertext Transfer Protocol                            |
| POP3            | 110             | Post Office Protocol version 3                         |
| NTP             | 123             | Network Time Protocol                                  |
| IMAP            | 143             | Internet Message Access Protocol                       |
| SNMP            | 161             | Simple Network Management Protocol                     |
| SNMP Trap       | 162             | SNMP Trap                                              |
| HTTPS           | 443             | HTTP Secure - Encrypted Web Communication              |
TCP
	Connecting port through TCP
		The TCP performs three-way handshake to established connection with the target host. An established connection is one that has completed the three-way handshake that occurs when two hosts initiate communication with each other.
			![TCP/IP 3 Way handshake for client-server communication on Internet](https://lh7-us.googleusercontent.com/0f9ILAa6xCmdJre8rmlopHCX_aclNQmIlq1IPbmCL4YESypVnr6QuKhawMHGySNBlyD2sw9kRcYJ9IIByRywyM0lThXAj_QPrfLOmSP0Yk4hfa_zWvR4_8f-ChpBeDAwQs5_eJoUoskMeHaVSZIi3Fk)



TCP Flags 
	 Each TCP data packet has a particular purpose or function, which is specified with the help of TCP Flag options. A value of 1 usually means that particular flag has been turned ON
		![[1Screenshot 2025-03-26 224512.png]]

Wireshark 
	open Wireshark 
	visit : example.com
	add http as filter  in Wireshark 
				To covert IP > domain 
					view->name resolution->resolve Network addresses  
We will see four layer information 
	Psyhical layer
		* Frame 863: 394 bytes on wire (3152 bits), 394 bytes captured (3152 bits) on interface enpos3, id 0
	Datalink layer 
			* Ethernet II, Src: PcsCompu_7f: 75:e6 (08:00:27:7f:75:e6), Dst: 40:ed:00:55:6a:61 (40:ed:00:55:6a:61)
	Internet /Network layer 
			* Internet Protocol Version 4, Src: 10.0.0.134, Dst: 23.215.0.136
	Transport layer
			* Transmission Control Protocol, Src Port: 38848, Dst Port: 80, Seq: 1, Ack: 1, Len: 328
	Application layer 
			* Hypertext Transfer Protocol


TCP
![[aScreenshot 2025-03-27 005929.png]]
The TCP performs three-way handshake to established connection with the target host.

#### TCP Connect Scan / Full Open Scan 

![[Screenshot 2025-03-27 014624.png]]
Syntax
`namp -sT <IP/domain name>`


nmap -sT 10.0.0.177 
	Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:06 EDT
	Nmap scan report for 10.0.0.177
	Host is up (0.017s latency).
	Not shown: 980 filtered tcp ports (no-response)
	PORT     STATE SERVICE
	21/tcp   open  ftp
	22/tcp   open  ssh
	23/tcp   open  telnet
	25/tcp   open  smtp
	53/tcp   open  domain
	80/tcp   open  http
	111/tcp  open  rpcbind
	139/tcp  open  netbios-ssn
	445/tcp  open  microsoft-ds
	512/tcp  open  exec
	514/tcp  open  shell
	1099/tcp open  rmiregistry
	1524/tcp open  ingreslock
	2049/tcp open  nfs
	2121/tcp open  ccproxy-ftp
	3306/tcp open  mysql
	5432/tcp open  postgresql
	5900/tcp open  vnc
	6000/tcp open  X11
	8009/tcp open  ajp13
	
	Nmap done: 1 IP address (1 host up) scanned in 50.00 seconds

Default things that nmap does 
1. nmap will perfrom host discovery before port scan 
2. namp will perform port scan on common 1000 ports 

-sn (ping scan) (host discovery )
As user - TCP SYN 80 & SYN 443
As root - ARP
    - TCP SYN 443, ACK 80, ICMP echo request, ICMP timestamp request 

To know why nmap told we use 
--reason 
	PORT     STATE SERVICE      REASON
	21/tcp   open  ftp          syn-ack
	22/tcp   open  ssh          syn-ack
	23/tcp   open  telnet       syn-ack``
To get more detailed output (verbose)
	``nmap <IP>  -vv`` 
	Nmap port info (status)
* Open - Application on the target machine is listening for connections/packets.
* Filtered - A firewall, filter, or other network obstacle is blocking the port so that Nmap cannot tell whether it is open or closed.
* Closed - No application is listening on these ports (though they could open up at any time).
* Unfiltered - Responding to Nmap's probes, but Nmap cannot determine whether they are open or closed.
* open filtered and closed filtered when nmap cannot determine which of the two states describe a port.


Nmap extensions list  


| Nmap extensions list | use case           |
| -------------------- | ------------------ |
| --resson             | gives reasons for  |
| --vv (verbose)       | deta               |
| -Pn                  | skips host machine |
| -n                   | skips DNS          |
| -p                   | specifies port     |
| -F                   | fast Scan          |


To see what are the TCP connections that are open 
-  `sudo netstat -antp`
 - Active Internet connections (servers and established) 
 - Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 10.10.10.4:51638        49.205.171.9:80         ESTABLISHED 15822/firefox-esr   
tcp        0      0 10.10.10.4:50532        44.227.3.195:443        TIME_WAIT   -                   
tcp        0      0 10.10.10.4:53368        142.250.193.150:443     ESTABLISHED 15822/firefox-esr   
tcp        0      0 10.10.10.4:41878        34.107.243.93:443       ESTABLISHED 15822/firefox-esr   
tcp        0      0 10.10.10.4:50452        142.250.207.68:443      TIME_WAIT   -                   
tcp        0      0 10.10.10.4:56328        142.250.195.46:443      ESTABLISHED 15822/firefox-esr   
tcp        0      0 10.10.10.4:41872        34.107.243.93:443       ESTABLISHED 15822/firefox-esr   


TO starting ssh service
sudo service ssh start 

Nmap port info (status)
* Open - Application on the target machine is listening for connections/packets.
* Filtered - A firewall, filter, or other network obstacle is blocking the port so that Nmap cannot tell whether it is open or closed.
* Closed - No application is listening on these ports (though they could open up at any time).
* Unfiltered - Responding to Nmap's probes, but Nmap cannot determine whether they are open or closed.
* open filtered and closed filtered when nmap cannot determine which of the two states describe a port.
* slow scan means it can be firewall 


nmap  10.10.10.5 -sT 
-host discovery - 80 & 443 
-Common 1000 ports 

#### SYN Scan / Half Open Scan /Stealth Scan 

![800](https://ptgmedia.pearsoncmg.com/images/chap5_1587052083/elementLinks/05fig17.gif)


Figure 5-17 SYN Scan

* Source does not respond with an ACK packet, which is the expected response in the three way handshake. Instead, source responds with an RST packet, dropping the connection. 
* SYN Scan can go unnoticed  by some firewalls. However, many intrusion detection systems detect SYN scans.
* Syntax 
	 sudo nmap -sS<IP/domain name>
`` sudo namp -sS 10.0.0.5(window10)``
``sudo nmap  -sS 10.10.10.6( meta2)``


### Inverse Scan
Inverse Scaning 
1. NULL Scan 
2. FIN Scan 
3. Xmas

#### NULL Scan 

 ![1001](https://ptgmedia.pearsoncmg.com/images/chap5_1587052083/elementLinks/05fig18.gif)


* A packet is sent to a TCP port with no flags set (In normal TCP communication, at least one bit or flag is set). In TCP connect / SYN scans, a response indicate an open port, but in a NULL scan, a response indicates a closed port.
* This is why a NULL scan is called an inverse scan.
* Inverse scans are stealthier than the TCP Connect and SYN scans, but not accurate.
* Syntax 
	sudo nmap -sN <IP address/ domain name>
sudo nmap  -sN 10.10.10.6

The inverse scan will not work on windows 
	sudo nmap -sN  10.10.10.5 -Pn --reason
	Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-28 15:55 EDT
	Nmap scan report for 10.10.10.5
	Host is up, received arp-response (0.00080s latency).
	All 1000 scanned ports on 10.10.10.5 are in ignored states.
	Not shown: 1000 closed tcp ports (reset)
	MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)
Reason
	
	* **RFC 793** states that if a TCP segment arrives with no flags with no flags set, the receiving host should drop the segment and send an RST if port is closed.  
	* In reality, windows host do not comply with this RFS, so we can not use a Null scan against a  Windows machine to determine ports are active.
	* When  a Windows  machine receives a packet that has no flags set, it sends an RST packet in response, regardless of whwther the port is open or closed. with all NULL packet recivving an RST packet in respose, you cannot open and closed ports. 
	* UNIX-based system do not comply with RFC 793; therefor, they send RST packet backs when the port is closed and no packet, when port is open.

#### FIN Scan
![11](https://ptgmedia.pearsoncmg.com/images/chap5_1587052083/elementLinks/05fig19.gif)

*  A packet is sent to each TCP port with the -FIN bit set to ON. The FIN bit indicates the ending of a TCP session.
*  Like all inverse scans, a RST response indicates the port being closed, and no response indicates that the port is listening.
* Syntax
	nmap -SF <IP address/domain name>

	`sudo nmap -sF <IP/doain name>

#### Xmas Scan (faster than other 3)
![11](https://ptgmedia.pearsoncmg.com/images/chap5_1587052083/elementLinks/05fig20.gif)

The Xmas-Tree scan sends a TCP packet with the following flags:
**URG** — Indicates that the data is urgent and should be processed immediately
**PSH** - Forces data to a buffer
**FIN** - Used when finishing a TCP session
* Syntax
	nmap -sx <IP address/domain name>

	`sudo nmap -sX <IP/domain name >`

We use inverse scan to guess the operating system 
	sudo nmap -sX smec.ac.in -p0443
		Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-28 16:13 EDT
		Nmap scan report for smec.ac.in (119.235.48.133)
		Host is up (0.031s latency).
		
		PORT    STATE         SERVICE
		443/tcp open|filtered https
	as port is open in this machine, so it is linux and why not windows as in windows inverse scan does not work and port is closed.

 

| Scans        | SYNTAX | OPEN    | ClOSED |
| ------------ | ------ | ------- | ------ |
| connect scan | -sT    | SYN/ACK | RST    |
| SYN Scan     | -sS    | SYN/ACK | RST    |
| NULL sacn    | -sN    | -       | RST    |
| FIN Scan     | -sF    | -       | RST    |
| Xmas scan    | -sX    | -       | RST    |


Common nmap commands 
``sudo nmap -sS -Pn - p80 <IP>`` (SYN Scan)
``nmap -Pn -n <IP> ``(Connect Scan)
``sudo map -Pn -n <IP> ``(SYN Scan)
``nmap - Pn -n -p21,22,80 <I>`` (Connect Scan)
``nmap - p10-100 <IP>`` (range)
``sudo nmap -p--sT ``example.com
``nmap <publicip>`` (no ARP)
 
 
Cheatsheet NMAP 
	
	Default 
	1. nmap will perfrom host discovery before port scan 
	2. namp will perform port scan on common 1000 ports 
	
	-sn 
	As user - TCP SYN 80 & SYN 443(connect scan )
	As root - ARP (local network <privete IP>)
	    - TCP SYN 433, ACK 80, ICMO echo request, ICMP timestamp request 
	To see service runnig
		netstat -antp
	s csc


| Flag              | Description                                |
|-------------------|------------------------------------------|
| `--reason`       | Provides reasons for host state          |
| `-vv` (verbose)  | Enables detailed output                  |
| `-Pn`            | Skips host discovery (assumes hosts are up) |
| `-n`             | Skips DNS resolution                      |
| `-p <port>`      | Specifies a single port or range         |
| `-p-` or `-p0-`  | Scans all ports (1-65535)                |
| `-F`             | Performs a fast scan (fewer ports)       |
| `--top-ports <N>`| Scans the top N most common ports        |
| `-T<0-5>`        | Sets scan speed: T0 (slow) to T5 (fast)  |




|Scans|SYNTAX|OPEN|ClOSED|
|---|---|---|---|
|connect scan|-sT|SYN/ACK|RST|
|SYN Scan|-sS|SYN/ACK|RST|
|NULL sacn|-sN|-|RST|
|FIN Scan|-sF|-|RST|
|Xmas scan|-sX|-|RST|

Common nmap commands 
sudo nmap -sS -Pn - p80 <IP> (SYN Scan)
nmap -Pn -n <IP> (Connect Scan)
sudo map -Pn -n <IP> (SYN Scan)
nmap - Pn -n -p21,22,80 <I> (Connect Scan)
nmap - p10-100 <IP> (range)
sudo nmap -p--sT example.com
nmap <publicip>(no ARP)
sudo nmap -Pn -sV 10.10.10.6 (-sV service version detection )




### 27/03/25 

To know which services is running 
	-sV
		sudo nmap -Pn -sV 10.10.10.6

To connect using FTP
	ftp <IP/domain name>
	password 

To connect using SSH
	ssh <username>@<IP/domainname>

To rest fingerprint 
	ssh-keygen -R <ip>
		ssh-keygen -R 
To connect using HTTP services 
	<ip/domainname>:port number 
	10.10.10.6:8180
To locate nmap scripts w
	locate *nse
Default script Scan
	 sudo nmap -sC -Pn -n 10.10.10.6

Aggressive Scan 
	namp -A <IP>
	nmap -A 10.10.10.6

ACK Scan Or Firewall detection scan 

	sudo namp -sA <IP>
	REST (there is some connection)
	unfiltered means no firewall
	filtered means firewall  

	sudo namp -sA<IP>

checking in windows 10
sudo nmap -sA 10.10.10.5

OS detection scan 
	sudo nmap -O 10.10.10.5 (windows 10)
	locate *nse | grep smb 
		sudo nmap 10.10.10.6 -p445 -sC

	sudo nmap -O 10.10.10.6 (met2)
	
	sudo nmap -O 10.10.10.5 -p21 (only one port for OS )
	
	
	sudo nmap -O 10.10.10.5 -p445 ()

Q & N Section
1. Identify the number of machines running port 3389
nmap -p3389 10.10.10.1/24 --open 

2. How many ports are open on target 10.0.032
nmap 10.0.0.32
namp -PN -p- 10.0.0.32
3. what is the operating system running on 10.0.0.10
pin -c 2 10.0.0.10
nmap -O 10.0.010 
4. what is the IP address of machine running port 1515
nmap -p1515 10.0.0.1/24 --open 
5.   what is the version of the software running on the port 1515
nmap -sV --open -p1515 10.0.0.1/24 
sudo nmap 10.0.0.109 -021. 1515.3535 -SV


Add to spoofing 
Proxy Chains (to use in terminal )
	Setp1: Edit proxychains config 
				-Eable dynamic chains 
				-add line in the end of the file 
					sock4 127.0.0.1 9050
					sock 127.0.0.1 9050
	
	Step2: (if you  do not have tor service)
		sudo apt install tor 
		 sudo service tor start 
	
	Step3: Use proxy 
		proxyxhains firefox <domainname>
	
	To use proxyxhains  for namp 
		proxyxhains namp <IP>
To see service is  running
	1. sudo service tor status
	2. netstat -antp

-oN-save as text file 
-oN/-oX/-oS/-oG <file>: Output scan in normal, XML, s|<rIpt kIddi3,
     and Grepable format, respectively, to the given filename.
  -oA <basename>: Output in the three major formats at once
 
 
 




[[Terminal]]- file commands 

### References
