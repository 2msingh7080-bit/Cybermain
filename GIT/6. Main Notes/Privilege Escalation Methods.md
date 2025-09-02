2025-05-29 00:34

Status:

Tags:

# Privilege Escalation Methods


## Privilege Escalation Methods 
- Methods for privilege escalation are 
	1.  Kernel Vuln
	2. Software Vuln
	3. World Writable Files
	4. Cron
	5. SUID
	6. SUDO
### 1. 🧬 **Kernel Vulnerabilities**
 
 🔹 What It Is:
Kernel vulnerabilities exist when the Linux kernel (core of the OS) has bugs or flaws that can be exploited.

 🔹 How Escalation Happens:
- If you find an unpatched kernel vulnerability, you can run exploit code to get **root access**.
    
- This is often possible if the system is running an **outdated kernel**.
    
🔹 How to Check:
```bash
uname -a   # Shows kernel version 
```

Then check for known exploits:
- Use `searchsploit <kernel version>`
    
- Or check online at sites like [exploit-db.com](https://www.exploit-db.com/)
    

🔹 Example:
```bash
uname -r   # 4.4.0-21-generic
searchsploit 4.4.0
 ```

---
### 2. 🛠️ **Software Vulnerabilities**

🔹 What It Is:
Poorly written or outdated software (e.g., web servers, local tools) may have security holes.

 🔹 How Escalation Happens:
- If such software is running as root or a higher privilege user, exploiting it can give you higher access.
    
🔹 How to Check:
- List running services:
    
```bash
ps aux
netstat -tulpn
 ```

- Check versions:
    

```bash
<software-name> --version 
```

- Look up known CVEs (Common Vulnerabilities and Exposures).
    
🔹 Example:
A vulnerable version of `Exim` mail server or `Apache` can be exploited using public exploits.

---

### 3. 📁 **World Writable Files**
🔹 What It Is:
Files or directories that **any user** can write to (permissions: `-rw-rw-rw-` or `drwxrwxrwx`).

🔹 How Escalation Happens:
- If a file/script owned by **root** is world-writable, a low-privileged user can **inject malicious code**.
    
- If root later executes the file → **Privilege Escalation**.
    
🔹 How to Check:

```bash
 find / -writable -type f 2>/dev/null
find / -perm -2 -type f 2>/dev/null   # All world-writable files
```
🔹 Example:
If `/etc/passwd` is writable, you can add a new root user manually.

---
### 4. ⏰ **Cron Jobs**

🔹 What It Is:
**Scheduled tasks** in Linux, run automatically at fixed intervals.
 
 🔹 How Escalation Happens:
- If a **cron job** is executed by **root** but runs a script located in a **writable location**, you can **edit that script**.
    
🔹 How to Check:
```bash
cat /etc/crontab
ls -la /etc/cron.* 
```
- Check script paths — are they writable?
    
- Use `find` to identify write permissions:
    
```bash
find / -writable -type f -name "*.sh" 2>/dev/null 
```

 🔹 Example:
Cron runs `/opt/backup.sh` as root every minute.  
If you can write to `backup.sh`, insert a reverse shell or `chmod +s /bin/bash`.

---
### 5. 🔒 **SUID (Set User ID)**

🔹 What It Is:
A file with the SUID bit runs **as the file’s owner**, not the user executing it.

 🔹 How Escalation Happens:
- If an executable has SUID and belongs to **root**, you may exploit it to run commands **as root**.
    
🔹 How to Check:
```bash
find / -perm -4000 -type f 2>/dev/null 
```
- Look for binaries like `vim`, `nmap`, `bash`, etc.
    
🔹 Example:

```bash
# If /bin/bash has SUID bit
chmod u+s /bin/bash
./bash -p
```
Use GTFOBins (https://gtfobins.github.io) to find SUID exploitation techniques.

---
### 6. 🔑 **SUDO (Without Password)**
🔹 What It Is:
Some users can run commands as **root** using `sudo`.

🔹 How Escalation Happens:
- If `sudo` allows you to run **any command or specific binaries** without a password, you can leverage that for escalation.
    
🔹 How to Check:
```bash
sudo -l 
```

🔹 Example:
```bash
# If output says:
(ALL) NOPASSWD: /bin/less

# Then run:
sudo /bin/less /etc/shadow
# Or escape to shell using `!sh` inside less 
```
---- 
### ✅ **Summary Table**
|Method|What to Check|Escalation Logic|
|---|---|---|
|**Kernel Vuln**|`uname -a`, outdated kernel|Exploit known kernel bugs to get root|
|**Software Vuln**|`ps aux`, `netstat`, versions|Exploit vulnerable software running as root|
|**WorldWritable**|`find / -perm -2`|Modify sensitive files/scripts run by root|
|**Cron Jobs**|`/etc/crontab`, writable scripts|Inject code in scripts run by root|
|**SUID**|`find / -perm -4000`|Abuse root-owned binaries with SUID|
|**SUDO**|`sudo -l`|Abuse misconfigurations like NOPASSWD|





### References
