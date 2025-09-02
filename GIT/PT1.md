
2025-05-23 20:32

Status:

Tags:

# PT1
#### 1. Reconnaissance & Enumeration
Evaluate your ability to gather information about a target using both passive and active techniques.
#### Basic Network Recon
Covers key network reconnaissance topics such as identifying IP ranges and subnets, performing subdomain enumeration, and listing publicly exposed services.
#### Active Information Gathering
Engage in interactive scanning using tools like Nmap to discover open ports, detect operating systems, and identify running services across TCP and UDP.
#### Usage of Key Tooling and Commands

Use tools such as Nmap, dig, WHOIS, and others to enumerate infrastructure. Demonstrate practical knowledge in banner grabbing, DNS analysis, and service enumeration (among others) to build a solid attack surface map.
#### 2. Web Application Testing
Assess your knowledge of common web application vulnerabilities and your ability to exploit and report them.
#### Core Web Vulnerability Discovery
Focus on the OWASP Top 10, including practical scenarios involving SQL Injection, Cross-Site Scripting (XSS), IDOR, SSRF, and more.

#### Manual Testing Techniques
Use THM's Attackbox or tools like Burp Suite and browser-based testing to identify and manually exploit input validation flaws, broken access control, and file upload issues.

#### Bypass Techniques
Demonstrate the ability to bypass basic client-side controls, such as JavaScript restrictions or UI-based limitations, to manipulate application behavior or gain unauthorized access.

#### 3. Network Penetration Testing
Evaluate your understanding of internal and external network testing techniques.
#### Service Enumeration and Exploitation
Interact with common protocols like SMB, RDP, FTP, SSH, and SNMP to identify misconfigurations, outdated services, and credentials exposure.
#### Password Attacks and Misconfig Abuse
Perform password attacks where applicable. Identify weak or default credentials and improperly secured systems.
#### Local Privilege Escalation
Demonstrate the ability to locally enumerate the configuration of both a Linux- or Windows-based host to identify and exploit misconfigurations to perform privilege escalation.
#### Traffic Inspection and Network Defense Awareness
Use sniffing and MITM techniques to capture credentials or manipulate traffic. Understand segmentation boundaries and potential firewall evasion strategies.
#### 4. Active Directory Exploitation
Demonstrate your ability to perform enumeration and attacks in an Active Directory environment.
#### Domain and Object Enumeration
Use tools like BloodHound and built-in Windows commands to map out AD structures, user relationships, and permissions.
#### Common AD Attack Paths
Execute basic attacks such as asrep roasting, kerberoasting, credential harvesting or abusing outdated software. Recognize and abuse common privilege escalation paths in Windows environments.
#### Pivoting and Lateral Movement Basics
Demonstrate initial steps toward pivoting inside a compromised network, identifying trust relationships, and moving laterally.
#### 5. Exploitation & Post-Exploitation
Evaluate your ability to exploit vulnerabilities and maintain access to compromised systems.
#### Privilege Escalation Techniques
Apply common privilege escalation tactics on both Windows and Linux platforms, such as SUID abuse, kernel exploits, and service misconfigurations.
#### Post-Exploitation Workflow
Perform host recon, user enumeration, credential dumping, and persistence techniques after gaining access.

#### 6. Reporting & Time Management
Assess your ability to document findings clearly and manage exam time effectively.
#### Clear Technical Reporting
Write concise and actionable vulnerability descriptions, with impact assessments, reproduction steps, and recommended mitigations.
#### Time and Task Prioritization
Demonstrate good time management over a 48-hour window, identifying high-value targets early and allocating time wisely across the engagement.
#### Note-Taking and Communication
Maintain thorough, clear notes throughout the assessment and provide a logical attack path narrative that communicates risk to technical and non-technical stakeholders.

- Prompt - 
	- I want you to make list of things or tools which will learned in this course accordingly for each sections 


## 🔍 **Course Topics, Tools, and Skills Table**

| **Section**                             | **Topics Covered**                                                                                                                                 | **Tools / Skills**                                                                                                                                                       |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **1. Reconnaissance & Enumeration**     | - Passive & active info gathering  <br>- Subdomain enumeration  <br>- Banner grabbing  <br>- DNS, WHOIS, IP range analysis                         | - `Nmap`  <br>- `dig`  <br>- `WHOIS`  <br>- `nslookup`  <br>- `Amass`  <br>- `theHarvester`  <br>- `Traceroute`  <br>- `Netcat`                                          |
| **2. Web Application Testing**          | - OWASP Top 10 (SQLi, XSS, IDOR, SSRF, etc.)  <br>- Manual testing techniques  <br>- Client-side bypasses                                          | - `Burp Suite`  <br>- Browser DevTools  <br>- `cURL` / `wget`  <br>- `Nikto`  <br>- `WFuzz`, `Dirb`  <br>- Manual payloads  <br>- JS tampering                           |
| **3. Network Penetration Testing**      | - Service enumeration (SMB, RDP, FTP, SSH, SNMP)  <br>- Password attacks  <br>- Local privilege escalation  <br>- Sniffing, MITM, firewall evasion | - `Hydra`, `Medusa`  <br>- `CrackMapExec`  <br>- `Impacket tools`  <br>- `Wireshark`  <br>- `Ettercap`, `Bettercap`  <br>- `John`, `Hashcat`  <br>- `LinPEAS`, `WinPEAS` |
| **4. Active Directory Exploitation**    | - Domain/user enumeration  <br>- Kerberoasting & ASREPRoast  <br>- Privilege escalation in AD  <br>- Pivoting, lateral movement                    | - `BloodHound`, `SharpHound`  <br>- `rpcclient`, `smbclient`  <br>- `Rubeus`, `Mimikatz`  <br>- `Evil-WinRM`  <br>- `PowerView`, `net`, `dsquery`                        |
| **5. Exploitation & Post-Exploitation** | - Exploiting vulnerabilities  <br>- Post-exploitation recon  <br>- Credential dumping  <br>- Persistence mechanisms                                | - `Metasploit`  <br>- `Netcat`  <br>- `Mimikatz`  <br>- `PowerShell`  <br>- `Empire`, `Nishang`, `Powersploit`  <br>- `socat`, `chisel`  <br>- `LinEnum`, `postenum`     |
| **6. Reporting & Time Management**      | - Report writing  <br>- Time/task management  <br>- Note-taking & risk communication<br>                                                           | - `CherryTree`, `Obsidian`, `Notion`, `OneNote`  <br>- Markdown, Word, LaTeX  <br>- CVSS Scoring  <br>- Screenshots, Flowcharts, Logs                                    |
|                                         |                                                                                                                                                    |                                                                                                                                                                          |
|                                         |                                                                                                                                                    |                                                                                                                                                                          |



### References
