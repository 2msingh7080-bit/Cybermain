# Enumeration Cheat Sheet: FTP, SSH, SMB

## Short Version

### FTP - Port 21
```
# Version
nmap -sV <IP> -p21

# Anonymous Login
nmap -sC <IP> -p21
ftp <IP> (user: anonymous, pass: [blank])

# File Operations
put file.txt (upload)
get file.txt (download)

# Vulnerability Scanning
locate *nse | grep ftp
nmap --script ftp-vsftpd-backdoor.nse -p21 <IP>

# Brute Force
hydra -L users.txt -P passwords.txt ftp://<IP>
nmap --script ftp-brute.nse -p21 <IP>
```

### SSH - Port 22
```
# Version
nmap -sV <IP> -p22

# Script Execution
locate *nse | grep ssh
nmap --script ssh-hostkey.nse -p22 <IP>

# Connection
ssh <username>@<IP>

# Brute Force
hydra -L users.txt -P passwords.txt ssh://<IP>
nmap --script ssh-brute.nse -p22 <IP>
```

### SMB - Port 445
```
# Version
nmap -sV <IP> -p445

# Shares
smbmap -H <IP>
smbclient //<IP>/<sharename>

# With Credentials
smbmap -H <IP> -u username -p password

# File Operations
put file.txt (upload)
get file.txt (download)

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

#### Scanning for FTP Services
```bash
# Basic FTP scan
nmap <IP> -p21

# Service version detection
nmap -sV <IP> -p21

# Check for anonymous login
nmap <IP> -Pn -p21 -n --script ftp-anon.nse
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
```

#### FTP Vulnerability Scanning
```bash
# Check for vsFTPd backdoor
nmap --script ftp-vsftpd-backdoor.nse -p21 <IP>

# Scan for all FTP vulnerabilities
nmap --script "ftp-*" -p21 <IP>

# Check for brute force vulnerabilities
nmap --script ftp-brute.nse -p21 <IP>
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
```

### Port 22 - SSH Services

#### Identifying SSH Scripts
```bash
# List all available SSH scripts
locate *.nse | grep ssh
```

#### SSH Reconnaissance
```bash
# Basic SSH scan
nmap <IP> -p22

# Service version detection
nmap -sV <IP> -p22

# Check SSH host keys
nmap <IP> -Pn -p22 -n --script ssh-hostkey.nse
```

#### SSH Connection
```bash
# Basic SSH connection
ssh username@<IP>

# Specify port if non-standard
ssh username@<IP> -p 2222

# Specify identity file (private key)
ssh -i private_key.pem username@<IP>
```

#### SSH Configuration Issues
```bash
# If you encounter algorithm negotiation failures
# Edit SSH config file:
sudo nano /etc/ssh/ssh_config

# Add these lines:
HostKeyAlgorithms +ssh-rsa
PubKeyAcceptedKeyTypes +ssh-rsa
```

#### SSH Service Management (on your Kali)
```bash
# Start SSH service
sudo service ssh start

# Check SSH service status
sudo service ssh status

# Check if SSH port is open
netstat -antp | grep 22
```

#### SSH Password Attacks
```bash
# Using Hydra with username list and password list
hydra -L users.txt -P passwords.txt ssh://<IP>

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

#### SMB Reconnaissance
```bash
# Basic SMB scan
nmap <IP> -p445

# Service version detection
nmap -sV <IP> -p445

# OS discovery
nmap <IP> -p445 --script smb-os-discovery.nse
```

#### SMB Share Enumeration
```bash
# List available shares (anonymous)
smbmap -H <IP>

# List shares with credentials
smbmap -H <IP> -u username -p password

# Connect to a specific share
smbclient //<IP>/sharename

# Connect with credentials
smbclient //<IP>/sharename -U username%password
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
```

#### SMB Configuration Issues
```bash
# If you encounter protocol or connectivity issues
# Edit Samba config file:
sudo nano /etc/samba/smb.conf

# Add relevant configuration parameters
```

#### Host Name Resolution
```bash
# On Linux - scan NetBIOS names in a network
sudo nbtscan -r 10.0.0.1/24

# On Windows
nbtstat -A <IP>
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
```

#### SMB Password Attacks
```bash
# Using Hydra
hydra -L users.txt -P passwords.txt smb://<IP>

# Using Medusa
medusa -U users.txt -P passwords.txt -h <IP> -M smbnt
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
```

### CUPP (Common User Passwords Profiler)
```bash
# Interactive mode
./cupp.py -i

# Follow prompts to create targeted password list
```

### Crunch (Pattern-based Generator)
```bash
# Generate passwords of length 8
crunch 8 8 -t admin%%%

# Generate passwords with specific pattern and character set
crunch 9 9 -t admin@%%% -l aaaaa@aaa

# Generate permutations of words
crunch 30 30 -p word1 word2 word3 word4
```

---

**References:**
- FTP RFC: https://datatracker.ietf.org/doc/html/rfc959
- SSH RFC: https://datatracker.ietf.org/doc/html/rfc4251
- SMB/CIFS: https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-smb/
