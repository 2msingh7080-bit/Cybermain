
2025-04-01 18:36

Status:

Tags:

# Cheat Sheet Enumeration
(by sir = short )

port 21 - FTP
- Check anonymous login (nmap -sC)
- login using anonymous: , ftp:
- can we upload (put) or download (get) files or change dir
- version of software  (namp  -sV <IP> -p21 )
- Check vulnerabilities
locate *nse | grep ftp
nmap --script-help=<scriptname>

port 22 - SSH
- Execute nmap scripts
- If we know username and password then login
- version of software  (namp  -sV <IP> -p22)
ssh ‹username>@<IP/domainname>
- Brute forcing 
	- wordlist - crunch, cupp
	- brute - hydra, medusa, nmap 


port 445 - SMB
- - version of software  (namp  -sV <IP> -p445)
- Check for anonymos
shares
- List
shares - smbmap -H <IP>
- smbclient //<IP>/‹sharename>
- Net buyers score

- on windows
    - nbstat
- on linux
    - nbtscan
- Identify usernames and password policy - enumlinux -a <IP>
or 

SMB - version? - nmap -p445 - SV <IP>
Anonymous login yes/no?
user names/ password policy? - enumalinux -a <IP>
user names? - enum4linux -U <IP>
Hostname? - nbtscan -r <IPRange>
Check network shares? - smbmap -H <IP>
Connet to share? - smbclinet //<IP>/<sharename>



# Long step by step 

## **FTP Services Cheat Sheet**

---

### **Identify FTP Scripts**

🔹 Locate FTP scripts:

```bash
locate *.nse | grep ftp
```

🔹 Check FTP Anonymous login script:

```bash
ftp-anon.nse
```

---

### **Run FTP Nmap Scan**

🔹 Execute FTP scan:

```bash
sudo nmap <IP> -Pn -p21 -n --script ftp-anon.nse
```

---

### **Port 21 - FTP Services**

✅ **Check Anonymous Login**

```bash
sudo nmap <IP> -Pn -p21 -n --script ftp-anon.nse
ftp <IP>
```

- **Username:** `anonymous` or `ftp`
    
- **Password:** (Leave blank or enter any value)
    

✅ **File Operations** 🔹 Upload file:

```bash
put test.txt
```

🔹 Download file:

```bash
get tikiwiki-1.9.11.zip
```

---

### **Check FTP Vulnerabilities**

🔹 Locate vulnerability scripts:

```bash
locate *.nse | grep ftp
```

🔹 Get script details:

```bash
nmap --script-help=<scriptname>
```

🔹 Run FTP backdoor scan:

```bash
nmap --script ftp-vsftpd-backdoor.nse -p21 <IP>
```

### References






### References
