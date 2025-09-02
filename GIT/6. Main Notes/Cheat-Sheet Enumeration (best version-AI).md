# Enumeration Cheat Sheet: FTP, SSH, SMB

## Short Version

### FTP - Port 21
```
# Version
nmap -sV <IP> -p21

# Check Anonymous Login
nmap -sC <IP> -p21
ftp <IP> (user: anonymous, pass: [blank])

# File Operations
put file.txt (upload)
get file.txt (download)
binary (for non-text files)

# Vulnerability Scanning
locate *nse | grep ftp
nmap --script ftp-vsftpd-backdoor.nse -p21 <IP>
nmap --script "ftp-*" -p21 <IP> (all FTP scripts)

# Brute Force
hydra -L users.txt -P passwords.txt ftp://<IP>
hydra -l username -P passwords.txt ftp://<IP>
nmap --script ftp-brute.nse -p21 <IP>
```

### SSH - Port 22
```
# Version
nmap -sV <IP> -p22

# Check Default Config
nmap -sC <IP> -p22

# Script Execution
locate *nse | grep ssh
nmap --script ssh-hostkey.nse -p22 <IP>
nmap --script "ssh-*" -p22 <IP> (all SSH scripts)

# Connection
ssh <username>@<IP>
ssh -i private_key.pem <username>@<IP>

# Brute Force
hydra -L users.txt -P passwords.txt ssh://<IP>
hydra -l username -P passwords.txt ssh://<IP>
nmap --script ssh-brute.nse -p22 <IP>
```

### SMB - Port 445
```
# Version
nmap -sV <IP> -p445

# Check Anonymous Access
nmap -sC <IP> -p445
nmap --script smb-enum-shares.nse -p445 <IP>

# Shares
smbmap -H <IP>
smbclient -L //<IP>/ -N (list shares anonymously)
smbclient //<IP>/<sharename>

# With Credentials
smbmap -H <IP> -u username -p password
smbclient //<IP>/<sharename> -U username%password

# Host Discovery
nbtscan -r <IPRange> (Linux)
nbtstat -A <IP> (Windows)

# Username Enumeration
enum4linux -U <IP>
enum4linux -a <IP> (all info)
```

## Detailed Version

### Port 21 - FTP Services

#### Identifying FTP Scripts
```bash
# List all available FTP scripts
locate *.nse | grep ftp

# Get details about a specific script
nmap --script-help=<scriptname>
```

#### Quick Assessment Guide
1. Scan for the service: `nmap -sV <IP> -p21`
2. Check for anonymous access: `nmap -sC <IP> -p21`
3. Try connecting: `ftp <IP>` (try anonymous login)
4. List available files: `ls` (after connecting)
5. Check if upload/download is possible: `put test.txt`, `get file.txt`
6. Scan for vulnerabilities: `nmap --script "ftp-*" -p21 <IP>`

#### Scanning for FTP Services
```bash
# Basic FTP scan
nmap <IP> -p21

# Service version detection
nmap -sV <IP> -p21

# Check for anonymous login using default scripts
nmap -sC <IP> -p21

# Specific check for anonymous login
nmap <IP> -Pn -p21 -n --script ftp-anon.nse

# Run all FTP scripts
nmap --script "ftp-*" -p21 <IP>
```

#### FTP Anonymous Login
```bash
# Connect to FTP server
ftp <IP>

# Login credentials for anonymous access
Username: anonymous (or ftp)
Password: (leave blank or enter any email)
```

#### FTP File Operations
```bash
# List files
ls

# Navigate directories
cd directory_name

# Upload a file
put test.txt

# Download a file
get important_file.txt

# Change to binary mode (for non-text files)
binary

# Exit FTP session
bye
```

#### FTP Vulnerability Scanning
```bash
# Check for vsFTPd backdoor
nmap --script ftp-vsftpd-backdoor.nse -p21 <IP>

# Scan for all FTP vulnerabilities
nmap --script "ftp-*" -p21 <IP>

# Check for brute force vulnerabilities
nmap --script ftp-brute.nse -p21 <IP>

# Check server configuration
nmap --script ftp-syst.nse -p21 <IP>
```

#### FTP Password Attacks
```bash
# Using Hydra with known username
hydra -l msfadmin -p msfadmin ftp://<IP>

# Using Hydra with username list and password list
hydra -L users.txt -P passwords.txt ftp://<IP>

# Using special options (-e nsr: try null password, same as login, reversed login)
hydra -L users.txt -e nsr ftp://<IP>

# Using Medusa
medusa -U users.txt -P passwords.txt -h <IP> -n 21 -M ftp

# Using Nmap
nmap --script ftp-brute.nse -p21 <IP>
```

### Port 22 - SSH Services

#### Identifying SSH Scripts
```bash
# List all available SSH scripts
locate *.nse | grep ssh
```

#### Quick Assessment Guide
1. Scan for the service: `nmap -sV <IP> -p22`
2. Check for configuration: `nmap -sC <IP> -p22`
3. Check host keys: `nmap --script ssh-hostkey.nse -p22 <IP>`
4. Attempt connection with credentials: `ssh username@<IP>`
5. Check key-based auth if available: `ssh -i key.pem username@<IP>`
6. Try password attacks if needed: `hydra -l username -P passwords.txt ssh://<IP>`

#### SSH Reconnaissance
```bash
# Basic SSH scan
nmap <IP> -p22

# Service version detection
nmap -sV <IP> -p22

# Check for configuration/vulnerabilities using default scripts
nmap -sC <IP> -p22

# Check SSH host keys
nmap <IP> -Pn -p22 -n --script ssh-hostkey.nse

# Run all SSH scripts
nmap --script "ssh-*" -p22 <IP>

# Check for weak algorithms
nmap --script ssh2-enum-algos -p22 <IP>
```

#### SSH Connection
```bash
# Basic SSH connection
ssh username@<IP>

# If username and password are known
ssh username@<IP>
# (You'll be prompted for password)

# Specify port if non-standard
ssh username@<IP> -p 2222

# Specify identity file (private key)
ssh -i private_key.pem username@<IP>

# Verbose connection (for debugging)
ssh -v username@<IP>
```

#### SSH Configuration Issues
```bash
# If you encounter algorithm negotiation failures
# Edit SSH config file:
sudo nano /etc/ssh/ssh_config

# Add these lines:
HostKeyAlgorithms +ssh-rsa
PubKeyAcceptedKeyTypes +ssh-rsa

# Check ciphers and algorithms supported by server
ssh -Q cipher
ssh -Q key
ssh -Q mac
```

#### SSH Service Management (on your Kali)
```bash
# Start SSH service
sudo service ssh start

# Check SSH service status
sudo service ssh status

# Check if SSH port is open
netstat -antp | grep 22

# Configure SSH server
sudo nano /etc/ssh/sshd_config
```

#### SSH Password Attacks
```bash
# Using Hydra with username list and password list
hydra -L users.txt -P passwords.txt ssh://<IP>

# Using Hydra with single username
hydra -l username -P passwords.txt ssh://<IP>

# Using Nmap
nmap --script ssh-brute.nse -p22 <IP>

# Using Medusa
medusa -U users.txt -P passwords.txt -h <IP> -M ssh
```

### Port 445 - SMB Services

#### Identifying SMB Scripts
```bash
# List all available SMB scripts
locate *.nse | grep smb
```

#### Quick Assessment Guide
1. Scan for the service: `nmap -sV <IP> -p445`
2. Check for anonymous access: `nmap -sC <IP> -p445`
3. List shares: `smbmap -H <IP>` or `smbclient -L //<IP>/ -N`
4. Connect to shares: `smbclient //<IP>/sharename`
5. Check for user enumeration: `enum4linux -U <IP>`
6. Check for all info: `enum4linux -a <IP>`

#### SMB Reconnaissance
```bash
# Basic SMB scan
nmap <IP> -p445

# Service version detection
nmap -sV <IP> -p445

# Check for anonymous access using default scripts
nmap -sC <IP> -p445

# OS discovery
nmap <IP> -p445 --script smb-os-discovery.nse

# Run all SMB scripts
nmap --script "smb-*" -p445 <IP>

# Check for vulnerabilities
nmap --script smb-vuln* -p445 <IP>
```

#### SMB Share Enumeration
```bash
# List available shares (anonymous)
smbmap -H <IP>

# List shares with credentials
smbmap -H <IP> -u username -p password

# List shares anonymously (alternative method)
smbclient -L //<IP>/ -N

# Connect to a specific share
smbclient //<IP>/sharename

# Connect with credentials
smbclient //<IP>/sharename -U username%password

# List all NetBIOS shares
net view \\<IP> (Windows)
```

#### SMB File Operations
```bash
# Within smbclient session:

# List files
ls

# Navigate directories
cd directory_name

# Upload a file
put test.txt

# Download a file
get important_file.txt

# Recursively download a directory
prompt off
recurse on
mget directory_name
```

#### SMB Configuration Issues
```bash
# If you encounter protocol or connectivity issues
# Edit Samba config file:
sudo nano /etc/samba/smb.conf

# Common fixes:
client min protocol = SMB2
client max protocol = SMB3
```

#### Host Name Resolution
```bash
# On Linux - scan NetBIOS names in a network
sudo nbtscan -r 10.0.0.1/24

# On Windows
nbtstat -A <IP>

# Resolve NetBIOS names
nmblookup -A <IP>
```

#### SMB Username Enumeration
```bash
# Basic user enumeration
enum4linux -U <IP>

# Extract just the usernames
enum4linux -U <IP> | grep "user:" | cut -d "[" -f 2 | cut -d "]" -f 1

# Comprehensive enumeration
enum4linux -a <IP>

# Password policy information
enum4linux -P <IP>

# Get usernames and password policy
enum4linux -a <IP>

# Using Nmap for user enumeration
nmap --script smb-enum-users.nse -p445 <IP>
```

#### SMB Password Attacks
```bash
# Using Hydra
hydra -L users.txt -P passwords.txt smb://<IP>

# Using Medusa
medusa -U users.txt -P passwords.txt -h <IP> -M smbnt

# Using CrackMapExec
crackmapexec smb <IP> -u usernames.txt -p passwords.txt
```
#### SMB file locating 

```bash
smbmap -H <ip> -u <username> -p <password> -R | grep -B 5 <filename>

Example:
smbmap -H 192.168.10.101 -u Martin -p qwerty1234 -R | grep -B 5 webpent.txt
 
```
#### SMB login 

```bash
smbclient //<ip>/SHARENAME -U <username> 
```

## Building Wordlists

### CeWL (Custom Word List generator)
```bash
# Basic usage - create wordlist from website
cewl -m 5 -d 2 https://example.com -w wordlist.txt

# Parameters:
# -m 5: minimum word length of 5
# -d 2: crawl 2 levels deep
# -w: output file

# Extract email addresses
cewl -e https://example.com
```

### CUPP (Common User Passwords Profiler)
```bash
# Interactive mode
./cupp.py -i

# Follow prompts to create targeted password list

# Use built-in dictionaries
./cupp.py -l

# Generate from a name with specified configurations
./cupp.py -n John
```

### Crunch (Pattern-based Generator)
```bash
# Generate passwords of length 8
crunch 8 8 -t admin%%%

# Generate passwords with specific pattern and character set
crunch 9 9 -t admin@%%% -l aaaaa@aaa

# Generate permutations of words
crunch 30 30 -p word1 word2 word3 word4

# Use character sets
crunch 6 8 -f /usr/share/crunch/charset.lst mixalpha
```

## Common Exploitation Paths

### FTP Exploitation
- Anonymous login → File access → Sensitive data
- Brute force → Valid credentials → File access
- Version exploits → Remote code execution
- User enumeration → Password attacks on other services

### SSH Exploitation
- Weak credentials → System access
- Key-based authentication bypass → System access
- Version exploits → Remote code execution
- Valid credentials → Lateral movement

### SMB Exploitation
- Anonymous access → File shares → Sensitive data
- User enumeration → Password attacks → System access
- SMB vulnerabilities (e.g., EternalBlue) → Remote code execution
- Pass-the-hash attacks → Lateral movement

---

**References:**
- FTP RFC: https://datatracker.ietf.org/doc/html/rfc959
- SSH RFC: https://datatracker.ietf.org/doc/html/rfc4251
- SMB/CIFS: https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-smb/
- HackTricks FTP: https://book.hacktricks.xyz/network-services-pentesting/pentesting-ftp
- HackTricks SSH: https://book.hacktricks.xyz/network-services-pentesting/pentesting-ssh
- HackTricks SMB: https://book.hacktricks.xyz/network-services-pentesting/pentesting-smb
