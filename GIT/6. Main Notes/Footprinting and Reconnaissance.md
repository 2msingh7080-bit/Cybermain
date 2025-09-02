
2025-03-22 00:24

Status:

Tags:

# Footprinting and Reconnaissance

21/03/25

FootPrinting

1. Passive FootPrinting  
    involves gathering information about the target without direct interaction. Collecting archived or stored information about the target using search engines, social networking sites and son on.
2. Active FootPrinting  
    involves gathering information about the target direct interaction about the targeyt with direct

Information obtained in footprinting  
Network information- whois database analysis, trace routing, etc  
system information- web server OS, location of web  
Organization information- Employee details, address, mobile/telephone numbers, web technologies, etc.  

Techniques of footprinting

1. ping - ping ipadress / ping website (works on icmp )  
    64 bytes from maa03s46-in-f14.1e100.net (142.250.196.78): icmp_seq=3 ttl=118 time=14.8 ms  
    ttl= time to leave value

traceroute (how many nodes it crossed)  
traceroute google.com  
traceroute to google.com (142.250.196.78), 30 hops max, 60 byte packets  
1 10.0.0.1 (10.0.0.1) 1.608 ms 1.519 ms 2.648 ms  
2 * * *  
3 broadband.actcorp.in (183.83.251.124) 10.827 ms !X 10.803 ms !X 10.776 ms !X

## **Default TTL Values for Operating System**

|Operating System|Default TTL Value|
|---|---|
|**Windows**|128 seconds|
|**Linux**|64 seconds|
|**macOS**|64 seconds|
|**Cisco Routers**|255 seconds|
|**Android**|64 seconds|
|**FreeBSD**|64 seconds|

States that it has firewall and  
To know about the OS

1. wapplyzar
2. ping  
    php and Apache server is uses in Linux

To whois

1. website whois (to obtain information related for website)
    
2. whois terminal
    
3. netcraft  
    To know about ipaddrss
    
4. whatismyip  
    checking the ipaddrss  
    changing the ipaddrss like  
    ping -c 5 erpsmec.in  
    PING erpsmec.in (119.235.48.131) 56(84) bytes of data.  
    [http://119.235.48.12/](http://119.235.48.12/)  
    [http://119.235.48.20/](http://119.235.48.20/)  
    [http://119.235.48.21/](http://119.235.48.21/)  
    To get location use ip  
    whatsmyip- 119.235.48.131
    
    ```
    Latitude:17.3753 (17° 22′ 31.04″ N)
    Longitude:78.4744 (78° 28′ 27.80″ E)
    ```
    
    Netcraft  
    site report netcraft  
    For automation all this things we use Dmitry  
	    Dmitry  
    To know what target is using OS  
    using metadata (manually)  
    google dorking (directly)
    

Google dorking  
for watching movies  
index of /.movies/  
site:tata.com  
allinurl:googel career  
inurl:jos site:www.indosys  
allintitle: detect malware

filetype:pdf hacking 101  
anti-virus inanchor:norton  
allinanchor:best cloud service provider  
intext:"cyber crime"  
define:eterpreneur

Exploit database for dork  
create dork and upload in Exploit database and show you did it

tips for jobs is  
budling networking  
make connection for jobs by connecting who is working for cyber security  
ask what skills required for job  
what kind of certifiaction they are looking for  
what kind of tools there use  
and make cv and linked

To extract the metadata from file  
exiftool

To view old contains of website use  
waybackmachine -  
[http://web.archive.org/web/20111108174704/http://www.cbit.ac.in/?q=node/58](http://web.archive.org/web/20111108174704/http://www.cbit.ac.in/?q=node/58)

# 24/03/25

Proxy servers 
 20 % of module 30


NAT 
public ip assign by router 
	Port forwarding 
	using port to accessing the internet
manicous request identifying using 
	user-Agent: 
	%% Mozilla %%/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
	curl https://www.hackerschool.in/  -v (-v responds header request header)
	User-Agent: curl/8.11.0
curl -I https://www.iare.ac.in/ (I)
	HTTP/1.1 200 OK
	Date: Mon, 24 Mar 2025 04:28:39 GMT
	Server: Apache
	Expires: Sun, 19 Nov 1978 05:00:00 GMT
	Cache-Control: no-cache, must-revalidate
	X-Content-Type-Options: nosniff
	Content-Language: en
	X-Frame-Options: SAMEORIGIN
	Vary: User-Agent
	Content-Type: text/html; charset=utf-8
responds header
user agent is part of  request header




To identify ipaddress nslookup 

nslookup 
	 set type=a
 > example.com
 > Server:                9.9.9.11
 > Address:        9.9.9.11#53

	Non-authoritative answer:
	Name:   example.com
	Address: 23.215.0.138
	Name:   example.com
	Address: 96.7.128.198
	Name:   example.com
	Address: 96.7.128.175
	Name:   example.com
	Address: 23.215.0.136
	Name:   example.com
	Address: 23.192.228.84
	Name:   example.com
	Address: 23.192.228.80
To obtain meta data automatically using tool 
	metagoofil
	metagoofil -d iare.ac.in -l100 -t pdf 

To collecting email 
	theHarvester ( d- = domain, -b= sources )
	theHarvester -d tata.com -b brave 
OSINT Framework 

To verfie email address 
	mailbox validator
	mx toolbox 
	 email dossier 
	 emkei.cz
### Spoofing 
What is Spoofing ?
	Spoofing is fraudulent or malicious practice in which communication sent from an unknown source disguised as a source know to the receiver .

IP Spoofing:
	is technique to gain unauthorized access to computer by sending messages to a computer with false IP address.

MAC Spoofing: 
	is technique  for changing a factory-assigned media Access Control (MAC) address of network interface on a networked device 
	The MAC address that is hard-coded on a network interface controller (NIC) can not be changed.
MAC 
	ether = 08:00:27:6e:13:6e
	changing MAC address using macchnager 
	Usage: macchanger options device

IP address Spoofing 
changing IP address using 
1. Proxy 
2. VPN

Proxy 
using free proxy list 
using browser proxy settings (manually)
	uses  HTTPS and HTTPS only 

VPN 
	VPNBOOK 
	openvpn vpnbook-pl140-tcp80.ovpn ( save username and password )

TOR
The internet is 3 web 
1. surface web 
2. Deep web 
3. Dark web 
search engin for tor 
ahmia
thehiddenwiki=[-](https://inthehiddenwiki.net/index.php/Main_Page)
forword proxy and 


### References

