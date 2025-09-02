# CEH Running Notes

## Table of Contents
- [Introduction to Hacking](#introduction-to-hacking)
- [CEH Hacking Methodology](#ceh-hacking-methodology)
- [Linux Commands and System Management](#linux-commands-and-system-management)
  - [Basic Commands](#basic-commands)
  - [User and Group Management](#user-and-group-management)
  - [File Operations](#file-operations)
  - [File Permissions](#file-permissions)
  - [Search and Locate](#search-and-locate)
  - [Archiving and Compression](#archiving-and-compression)
- [Footprinting and Reconnaissance](#footprinting-and-reconnaissance)
  - [Passive Footprinting](#passive-footprinting)
  - [Active Footprinting](#active-footprinting)
  - [Tools and Techniques](#tools-and-techniques)
- [AI in Ethical Hacking](#ai-in-ethical-hacking)
- [Career Tips](#career-tips)
- [Learning Resources](#learning-resources)
- [Practice Challenges](#practice-challenges)

## Introduction to Hacking

**What is hacking?**  
Hacking refers to exploiting system vulnerabilities and compromising security controls to gain unauthorized or inappropriate access to system resources. It involves modifying system or application features to achieve a goal outside of the creator's original purpose.

**Goal = Mindset + Vulnerabilities + Methodologies**  

**Vulnerabilities:**  
The existence of a weakness in design or implementation that can lead to an unexpected event compromising the security of a system.

Types of vulnerabilities:
- Software vulnerabilities
- Human vulnerabilities

**What is an exploit?**  
A breach of system security through vulnerabilities.

**Types of attacks:**
1. Server-side attacks
2. Client-side attacks

## CEH Hacking Methodology

1. **Footprinting / Reconnaissance**
2. **Scanning**
3. **Enumeration**
4. **Vulnerability Analysis**
5. **System Hacking**
   - Pre-exploitation
   - Exploitation
   - Post-exploitation
   - Cyber kill chain

## Linux Commands and System Management

### Basic Commands

```bash
# System Information
uname                 # Show system information
hostname              # Display hostname
hostname -I           # Display IP address
whoami                # Show current user
id                    # Show user ID and groups
ifconfig              # Show network interface configuration
ip addr               # Alternative to ifconfig
cat /etc/os-release   # Show OS information

# File Viewing
cat /etc/passwd       # View user accounts
wc -l /etc/passwd     # Count lines in a file
cat /etc/shadow       # View password hashes (requires sudo)
history               # View command history
```

### File Operations

```bash
# Directory Operations
mkdir dirname         # Create directory
mkdir -p dir1/dir2    # Create parent directories
rmdir dirname         # Remove empty directory
rm -r dirname         # Remove directory and contents
rm -rf dirname        # Force remove directory and contents
tree                  # Display directory tree

# File Operations
touch filename        # Create empty file
file filename         # Show file type
nano filename         # Edit file with nano
leafpad filename      # Edit file with leafpad
cat filename          # View file contents
cat > filename        # Create new file (Ctrl+D to end)
cat >> filename       # Append to file (Ctrl+D to end)
cp source dest        # Copy file
mv oldname newname    # Rename file
mv file directory     # Move file to directory

# Batch Operations
touch file{1..10}     # Create 10 files named file1 through file10
```

> [!tip] Keyboard Shortcuts
> - **Ctrl+C**: Kill a process
> - **Ctrl+Z**: Pause a process
> - **Ctrl+D**: End input for cat command

### User and Group Management

```bash
# User Management
sudo adduser username         # Create user with home directory
sudo useradd username         # Create user (basic)
passwd username               # Change user password
sudo su username              # Switch to another user

# Group Management
sudo addgroup groupname       # Create a new group
sudo usermod -aG group user   # Add user to group
sudo usermod -rG group user   # Remove user from group
```

**View users and groups:**
```bash
cat /etc/passwd               # List all users
cat /etc/group                # List all groups
groups username               # Show groups for user
head -10 /etc/passwd          # Show first 10 users
tail -10 /etc/passwd          # Show last 10 users
grep username /etc/passwd     # Search for specific user
```

### File Permissions

File permission structure: `(user)(group)(others)`
- Each section has read (r), write (w), execute (x) permissions
- Numeric values: read = 4, write = 2, execute = 1

```bash
# Change permissions
chmod u+x filename            # Add execute permission for user
chmod g+w filename            # Add write permission for group
chmod o-r filename            # Remove read permission for others
chmod 755 filename            # Set rwx for user, r-x for group and others

# Change ownership
sudo chown user:group filename    # Change user and group ownership
```

### Search and Locate

```bash
# Find files
find / -name filename         # Search for file from root
find / -name "*.txt"          # Search for pattern
find / -name filename 2>/dev/null  # Hide errors

# Locate (uses database)
locate filename               # Find file using locate database
sudo updatedb                 # Update locate database
```

### Archiving and Compression

```bash
# Tar archives
tar -cf archive.tar files     # Create tar archive
tar -xf archive.tar           # Extract tar archive
tar -rf archive.tar file      # Append to archive
tar -xvf archive.tar          # Extract verbosely

# Compression
gzip filename                 # Compress with gzip
gunzip filename.gz            # Decompress gzip file
zip archive.zip files         # Create zip archive
unzip archive.zip             # Extract zip archive
```

## Footprinting and Reconnaissance

### Passive Footprinting

Gathering information about the target without direct interaction. Collecting archived or stored information about the target using search engines, social networking sites, etc.

### Active Footprinting

Gathering information about the target with direct interaction.

### Information Obtained in Footprinting

- **Network information**: WHOIS database analysis, tracerouting, etc.
- **System information**: Web server OS, location of web servers
- **Organization information**: Employee details, address, phone numbers, web technologies, etc.

### Tools and Techniques

#### Basic Network Tools
```bash
# Ping to check connectivity (uses ICMP)
ping google.com

# Traceroute to trace network path
traceroute google.com
```

#### OS Detection via TTL Values

| Operating System | Default TTL Value |
|------------------|------------------|
| Windows          | 128 seconds      |
| Linux            | 64 seconds       |
| macOS            | 64 seconds       |
| Cisco Routers    | 255 seconds      |
| Android          | 64 seconds       |
| FreeBSD          | 64 seconds       |

#### WHOIS and IP Intelligence

```bash
# WHOIS lookup
whois domain.com

# Check your public IP
# Use online services like whatismyip.com
```

#### Google Dorking

Advanced search techniques:
- `site:tata.com` - Search within specific site
- `filetype:pdf hacking 101` - Search for specific file types
- `intitle:"index of"` - Search for directory listings
- `inurl:admin` - Search for URLs containing specific words
- `intext:"confidential"` - Search for specific text in pages

Useful dork examples:
- `index of /.movies/` - Find open directories with movies
- `allinurl:google career` - Find URLs containing all words
- `inurl:jobs site:www.infosys.com` - Combine multiple operators
- `allintitle:detect malware` - Title contains all terms
- `filetype:pdf "cyber security"` - Find PDFs about cyber security

#### Metadata Extraction

```bash
# Extract metadata from files
exiftool filename.pdf
```

#### Historical Web Analysis

- Wayback Machine (web.archive.org) - View historical versions of websites

## AI in Ethical Hacking

AI-Driven Ethical Hacking enhances the efficiency, effectiveness, and scope of cybersecurity measures:
- Automation of repetitive tasks
- Predictive analysis
- Advanced threat detection
- Enhanced reporting
- Continuous monitoring

> [!note] 
> AI won't replace ethical hackers - it will change how they work.

AI Tools in Ethical Hacking:
- PentestGPT
- MaliciousGPT
- Deepfake generation: https://this-person-does-not-exist.com/en
- Shell GPT (sgpt) - paid
- Terminal GPT (tgpt) - free

## Career Tips

- Build networking connections for job opportunities
- Connect with professionals working in cybersecurity
- Ask about required skills for specific jobs
- Inquire about desirable certifications
- Learn about tools used in the industry
- Optimize your CV and LinkedIn profile

## Learning Resources

- Linux Survival: https://linuxsurvival.com/
- Book: "Linux Basics for Hackers"
- Book: "Web Application Hacker's Handbook"

## Practice Challenges

- OverTheWire challenges: https://overthewire.org/
- SSH connection example:
  ```bash
  ssh bandit0@bandit.labs.overthewire.org -p 2220
  ```

> [!important] Learning Mindset
> - Focus on practical applications
> - Ask AI for help, not full walkthroughs
> - Practice regularly with hands-on exercises

## To-Do List

1. Learn how to remove users from sudo group
2. Learn how to remove groups
3. Study the sudoers file configuration
4. Understand the /bin directory structure
5. Learn about directory tree organization

## Contact Information

For queries: jayanth.b@cartelsoftware.com
