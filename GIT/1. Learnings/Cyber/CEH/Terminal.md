2025-03-26 11:09

Status:

Tags:

# Terminal
┌──(kali㉿kali)-[~]
└─$ nmap -sT 10.0.0.177 
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
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo s                        
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ nmap -sT 10.0.0.177 --reason 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:12 EDT
Nmap scan report for 10.0.0.177
Host is up, received reset ttl 255 (0.042s latency).
Not shown: 980 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
512/tcp  open  exec         syn-ack
513/tcp  open  login        syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
3306/tcp open  mysql        syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
6667/tcp open  irc          syn-ack
8009/tcp open  ajp13        syn-ack
8180/tcp open  unknown      syn-ack

Nmap done: 1 IP address (1 host up) scanned in 50.55 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ nmap -sT 10.0.0.177 -vv      
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:13 EDT
Initiating Ping Scan at 01:13
Scanning 10.0.0.177 [4 ports]
Completed Ping Scan at 01:13, 0.02s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 01:13
Completed Parallel DNS resolution of 1 host. at 01:13, 0.02s elapsed
Initiating Connect Scan at 01:13
Scanning 10.0.0.177 [1000 ports]
Discovered open port 445/tcp on 10.0.0.177
Discovered open port 3306/tcp on 10.0.0.177
Discovered open port 139/tcp on 10.0.0.177
Discovered open port 5900/tcp on 10.0.0.177
Discovered open port 25/tcp on 10.0.0.177
Discovered open port 53/tcp on 10.0.0.177
Discovered open port 111/tcp on 10.0.0.177
Discovered open port 23/tcp on 10.0.0.177
Discovered open port 21/tcp on 10.0.0.177
Discovered open port 22/tcp on 10.0.0.177
Discovered open port 80/tcp on 10.0.0.177
Discovered open port 514/tcp on 10.0.0.177
Discovered open port 2121/tcp on 10.0.0.177
Discovered open port 1524/tcp on 10.0.0.177
Discovered open port 512/tcp on 10.0.0.177
Discovered open port 513/tcp on 10.0.0.177
Discovered open port 5432/tcp on 10.0.0.177
Discovered open port 6667/tcp on 10.0.0.177
Discovered open port 6000/tcp on 10.0.0.177
Increasing send delay for 10.0.0.177 from 0 to 5 due to max_successful_tryno increase to 4
Discovered open port 8009/tcp on 10.0.0.177
Discovered open port 1099/tcp on 10.0.0.177
Discovered open port 8180/tcp on 10.0.0.177
Discovered open port 2049/tcp on 10.0.0.177
Completed Connect Scan at 01:14, 58.71s elapsed (1000 total ports)
Nmap scan report for 10.0.0.177
Host is up, received reset ttl 255 (0.015s latency).
Scanned at 2025-03-26 01:13:57 EDT for 59s
Not shown: 977 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
512/tcp  open  exec         syn-ack
513/tcp  open  login        syn-ack
514/tcp  open  shell        syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
2121/tcp open  ccproxy-ftp  syn-ack
3306/tcp open  mysql        syn-ack
5432/tcp open  postgresql   syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
6667/tcp open  irc          syn-ack
8009/tcp open  ajp13        syn-ack
8180/tcp open  unknown      syn-ack

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 58.81 seconds
           Raw packets sent: 4 (152B) | Rcvd: 1 (40B)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -vv
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:19 EDT
Initiating Ping Scan at 01:19
Scanning 10.0.0.177 [4 ports]
Completed Ping Scan at 01:19, 0.04s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 01:19
Completed Parallel DNS resolution of 1 host. at 01:19, 0.04s elapsed
Initiating Connect Scan at 01:19
Scanning 10.0.0.177 [1000 ports]
Discovered open port 111/tcp on 10.0.0.177
Discovered open port 139/tcp on 10.0.0.177
Discovered open port 5900/tcp on 10.0.0.177
Discovered open port 445/tcp on 10.0.0.177
Discovered open port 3306/tcp on 10.0.0.177
Discovered open port 53/tcp on 10.0.0.177
Discovered open port 21/tcp on 10.0.0.177
Discovered open port 23/tcp on 10.0.0.177
Discovered open port 22/tcp on 10.0.0.177
Discovered open port 80/tcp on 10.0.0.177
Discovered open port 25/tcp on 10.0.0.177
Discovered open port 1099/tcp on 10.0.0.177
Discovered open port 2121/tcp on 10.0.0.177
Discovered open port 6000/tcp on 10.0.0.177
Discovered open port 8180/tcp on 10.0.0.177
Discovered open port 1524/tcp on 10.0.0.177
Discovered open port 8009/tcp on 10.0.0.177
Discovered open port 6667/tcp on 10.0.0.177
Discovered open port 512/tcp on 10.0.0.177
Discovered open port 5432/tcp on 10.0.0.177
Increasing send delay for 10.0.0.177 from 0 to 5 due to 13 out of 43 dropped probes since last increase.
Discovered open port 2049/tcp on 10.0.0.177
Completed Connect Scan at 01:20, 50.30s elapsed (1000 total ports)
Nmap scan report for 10.0.0.177
Host is up, received reset ttl 255 (0.028s latency).
Scanned at 2025-03-26 01:19:18 EDT for 51s
Not shown: 979 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
512/tcp  open  exec         syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
2121/tcp open  ccproxy-ftp  syn-ack
3306/tcp open  mysql        syn-ack
5432/tcp open  postgresql   syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
6667/tcp open  irc          syn-ack
8009/tcp open  ajp13        syn-ack
8180/tcp open  unknown      syn-ack

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 50.45 seconds
           Raw packets sent: 4 (152B) | Rcvd: 1 (40B)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -n  -vv
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:20 EDT
Initiating Ping Scan at 01:20
Scanning 10.0.0.177 [4 ports]
Completed Ping Scan at 01:20, 0.04s elapsed (1 total hosts)
Initiating Connect Scan at 01:20
Scanning 10.0.0.177 [1000 ports]
Discovered open port 80/tcp on 10.0.0.177
Discovered open port 21/tcp on 10.0.0.177
Discovered open port 5900/tcp on 10.0.0.177
Discovered open port 25/tcp on 10.0.0.177
Discovered open port 111/tcp on 10.0.0.177
Discovered open port 23/tcp on 10.0.0.177
Discovered open port 445/tcp on 10.0.0.177
Discovered open port 53/tcp on 10.0.0.177
Discovered open port 139/tcp on 10.0.0.177
Discovered open port 22/tcp on 10.0.0.177
Discovered open port 3306/tcp on 10.0.0.177
Discovered open port 2121/tcp on 10.0.0.177
Discovered open port 8180/tcp on 10.0.0.177
Discovered open port 1099/tcp on 10.0.0.177
Discovered open port 1524/tcp on 10.0.0.177
Discovered open port 514/tcp on 10.0.0.177
Discovered open port 6000/tcp on 10.0.0.177
Discovered open port 2049/tcp on 10.0.0.177
Increasing send delay for 10.0.0.177 from 0 to 5 due to 11 out of 35 dropped probes since last increase.
Discovered open port 513/tcp on 10.0.0.177
Completed Connect Scan at 01:21, 35.32s elapsed (1000 total ports)
Nmap scan report for 10.0.0.177
Host is up, received reset ttl 255 (0.026s latency).
Scanned at 2025-03-26 01:20:27 EDT for 35s
Not shown: 981 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
513/tcp  open  login        syn-ack
514/tcp  open  shell        syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
2121/tcp open  ccproxy-ftp  syn-ack
3306/tcp open  mysql        syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
8180/tcp open  unknown      syn-ack

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 35.42 seconds
           Raw packets sent: 4 (152B) | Rcvd: 1 (40B)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -Pn -n -vv 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:21 EDT
Initiating Connect Scan at 01:21
Scanning 10.0.0.177 [1000 ports]
Discovered open port 25/tcp on 10.0.0.177
Discovered open port 139/tcp on 10.0.0.177
Discovered open port 21/tcp on 10.0.0.177
Discovered open port 3306/tcp on 10.0.0.177
Discovered open port 111/tcp on 10.0.0.177
Discovered open port 5900/tcp on 10.0.0.177
Discovered open port 53/tcp on 10.0.0.177
Discovered open port 22/tcp on 10.0.0.177
Discovered open port 80/tcp on 10.0.0.177
Discovered open port 23/tcp on 10.0.0.177
Discovered open port 445/tcp on 10.0.0.177
Discovered open port 1524/tcp on 10.0.0.177
Discovered open port 5432/tcp on 10.0.0.177
Discovered open port 513/tcp on 10.0.0.177
Discovered open port 514/tcp on 10.0.0.177
Discovered open port 512/tcp on 10.0.0.177
Discovered open port 2121/tcp on 10.0.0.177
Discovered open port 6667/tcp on 10.0.0.177
Discovered open port 8180/tcp on 10.0.0.177
Discovered open port 8009/tcp on 10.0.0.177
Discovered open port 1099/tcp on 10.0.0.177
Increasing send delay for 10.0.0.177 from 0 to 5 due to max_successful_tryno increase to 4
Discovered open port 6000/tcp on 10.0.0.177
Discovered open port 2049/tcp on 10.0.0.177
Completed Connect Scan at 01:23, 70.41s elapsed (1000 total ports)
Nmap scan report for 10.0.0.177
Host is up, received user-set (0.026s latency).
Scanned at 2025-03-26 01:21:59 EDT for 71s
Not shown: 977 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
512/tcp  open  exec         syn-ack
513/tcp  open  login        syn-ack
514/tcp  open  shell        syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
2121/tcp open  ccproxy-ftp  syn-ack
3306/tcp open  mysql        syn-ack
5432/tcp open  postgresql   syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
6667/tcp open  irc          syn-ack
8009/tcp open  ajp13        syn-ack
8180/tcp open  unknown      syn-ack

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 70.43 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -Pn -n -p-
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:23 EDT

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -Pn -n -p-
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:26 EDT
Stats: 0:00:12 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.41% done; ETC: 01:40 (0:14:00 remaining)
Stats: 0:00:14 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.66% done; ETC: 01:40 (0:13:47 remaining)
Stats: 0:00:14 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.80% done; ETC: 01:39 (0:12:45 remaining)

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -Pn -n --top-ports 5
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:27 EDT
Nmap scan report for 10.0.0.177
Host is up (0.0073s latency).

PORT    STATE    SERVICE
21/tcp  open     ftp
22/tcp  open     ssh
23/tcp  open     telnet
80/tcp  open     http
443/tcp filtered https

Nmap done: 1 IP address (1 host up) scanned in 1.26 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1                      


Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:30 EDT
Stats: 0:00:00 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.00% done; ETC: 01:30 (0:00:00 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000059s latency).
All 1000 scanned ports on localhost (127.0.0.1) are in ignored states.
Not shown: 1000 closed tcp ports (conn-refused)

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:32 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000068s latency).
All 1000 scanned ports on localhost (127.0.0.1) are in ignored states.
Not shown: 1000 closed tcp ports (conn-refused)

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ netstat -antp          
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 10.10.10.4:48386        34.149.100.209:443      TIME_WAIT   -                   
tcp        0      0 10.10.10.4:38376        34.107.243.93:443       ESTABLISHED 55087/firefox-esr   
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ netstat -antp
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 10.10.10.4:37778        23.215.0.136:80         ESTABLISHED 55087/firefox-esr   
tcp        0      0 10.10.10.4:37764        23.215.0.136:80         ESTABLISHED 55087/firefox-esr   
tcp        0      0 10.10.10.4:38376        34.107.243.93:443       ESTABLISHED 55087/firefox-esr   
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo service ssh start  
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ netstat -antp          
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp        0      0 10.10.10.4:37764        23.215.0.136:80         TIME_WAIT   -                   
tcp        0      0 10.10.10.4:47276        34.117.188.166:443      ESTABLISHED 55087/firefox-esr   
tcp        0      0 10.10.10.4:38376        34.107.243.93:443       ESTABLISHED 55087/firefox-esr   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1                      
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:36 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00012s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo service apache2 start 
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1    
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:37 EDT
Stats: 0:00:00 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.00% done; ETC: 01:37 (0:00:00 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000083s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ netstat -antp              
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp        0      0 10.10.10.4:38376        34.107.243.93:443       ESTABLISHED 55087/firefox-esr   
tcp6       0      0 :::80                   :::*                    LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo service ssh stop      
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo service apache2 stop  
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:41 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000057s latency).
All 1000 scanned ports on localhost (127.0.0.1) are in ignored states.
Not shown: 1000 closed tcp ports (conn-refused)

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds


# todays terminal commands 
┌──(kali㉿kali)-[~]
└─$ nmap -sT 10.0.0.177 
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
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo s                        
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ nmap -sT 10.0.0.177 --reason 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:12 EDT
Nmap scan report for 10.0.0.177
Host is up, received reset ttl 255 (0.042s latency).
Not shown: 980 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
512/tcp  open  exec         syn-ack
513/tcp  open  login        syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
3306/tcp open  mysql        syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
6667/tcp open  irc          syn-ack
8009/tcp open  ajp13        syn-ack
8180/tcp open  unknown      syn-ack

Nmap done: 1 IP address (1 host up) scanned in 50.55 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ nmap -sT 10.0.0.177 -vv      
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:13 EDT
Initiating Ping Scan at 01:13
Scanning 10.0.0.177 [4 ports]
Completed Ping Scan at 01:13, 0.02s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 01:13
Completed Parallel DNS resolution of 1 host. at 01:13, 0.02s elapsed
Initiating Connect Scan at 01:13
Scanning 10.0.0.177 [1000 ports]
Discovered open port 445/tcp on 10.0.0.177
Discovered open port 3306/tcp on 10.0.0.177
Discovered open port 139/tcp on 10.0.0.177
Discovered open port 5900/tcp on 10.0.0.177
Discovered open port 25/tcp on 10.0.0.177
Discovered open port 53/tcp on 10.0.0.177
Discovered open port 111/tcp on 10.0.0.177
Discovered open port 23/tcp on 10.0.0.177
Discovered open port 21/tcp on 10.0.0.177
Discovered open port 22/tcp on 10.0.0.177
Discovered open port 80/tcp on 10.0.0.177
Discovered open port 514/tcp on 10.0.0.177
Discovered open port 2121/tcp on 10.0.0.177
Discovered open port 1524/tcp on 10.0.0.177
Discovered open port 512/tcp on 10.0.0.177
Discovered open port 513/tcp on 10.0.0.177
Discovered open port 5432/tcp on 10.0.0.177
Discovered open port 6667/tcp on 10.0.0.177
Discovered open port 6000/tcp on 10.0.0.177
Increasing send delay for 10.0.0.177 from 0 to 5 due to max_successful_tryno increase to 4
Discovered open port 8009/tcp on 10.0.0.177
Discovered open port 1099/tcp on 10.0.0.177
Discovered open port 8180/tcp on 10.0.0.177
Discovered open port 2049/tcp on 10.0.0.177
Completed Connect Scan at 01:14, 58.71s elapsed (1000 total ports)
Nmap scan report for 10.0.0.177
Host is up, received reset ttl 255 (0.015s latency).
Scanned at 2025-03-26 01:13:57 EDT for 59s
Not shown: 977 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
512/tcp  open  exec         syn-ack
513/tcp  open  login        syn-ack
514/tcp  open  shell        syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
2121/tcp open  ccproxy-ftp  syn-ack
3306/tcp open  mysql        syn-ack
5432/tcp open  postgresql   syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
6667/tcp open  irc          syn-ack
8009/tcp open  ajp13        syn-ack
8180/tcp open  unknown      syn-ack

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 58.81 seconds
           Raw packets sent: 4 (152B) | Rcvd: 1 (40B)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -vv
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:19 EDT
Initiating Ping Scan at 01:19
Scanning 10.0.0.177 [4 ports]
Completed Ping Scan at 01:19, 0.04s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 01:19
Completed Parallel DNS resolution of 1 host. at 01:19, 0.04s elapsed
Initiating Connect Scan at 01:19
Scanning 10.0.0.177 [1000 ports]
Discovered open port 111/tcp on 10.0.0.177
Discovered open port 139/tcp on 10.0.0.177
Discovered open port 5900/tcp on 10.0.0.177
Discovered open port 445/tcp on 10.0.0.177
Discovered open port 3306/tcp on 10.0.0.177
Discovered open port 53/tcp on 10.0.0.177
Discovered open port 21/tcp on 10.0.0.177
Discovered open port 23/tcp on 10.0.0.177
Discovered open port 22/tcp on 10.0.0.177
Discovered open port 80/tcp on 10.0.0.177
Discovered open port 25/tcp on 10.0.0.177
Discovered open port 1099/tcp on 10.0.0.177
Discovered open port 2121/tcp on 10.0.0.177
Discovered open port 6000/tcp on 10.0.0.177
Discovered open port 8180/tcp on 10.0.0.177
Discovered open port 1524/tcp on 10.0.0.177
Discovered open port 8009/tcp on 10.0.0.177
Discovered open port 6667/tcp on 10.0.0.177
Discovered open port 512/tcp on 10.0.0.177
Discovered open port 5432/tcp on 10.0.0.177
Increasing send delay for 10.0.0.177 from 0 to 5 due to 13 out of 43 dropped probes since last increase.
Discovered open port 2049/tcp on 10.0.0.177
Completed Connect Scan at 01:20, 50.30s elapsed (1000 total ports)
Nmap scan report for 10.0.0.177
Host is up, received reset ttl 255 (0.028s latency).
Scanned at 2025-03-26 01:19:18 EDT for 51s
Not shown: 979 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
512/tcp  open  exec         syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
2121/tcp open  ccproxy-ftp  syn-ack
3306/tcp open  mysql        syn-ack
5432/tcp open  postgresql   syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
6667/tcp open  irc          syn-ack
8009/tcp open  ajp13        syn-ack
8180/tcp open  unknown      syn-ack

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 50.45 seconds
           Raw packets sent: 4 (152B) | Rcvd: 1 (40B)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -n  -vv
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:20 EDT
Initiating Ping Scan at 01:20
Scanning 10.0.0.177 [4 ports]
Completed Ping Scan at 01:20, 0.04s elapsed (1 total hosts)
Initiating Connect Scan at 01:20
Scanning 10.0.0.177 [1000 ports]
Discovered open port 80/tcp on 10.0.0.177
Discovered open port 21/tcp on 10.0.0.177
Discovered open port 5900/tcp on 10.0.0.177
Discovered open port 25/tcp on 10.0.0.177
Discovered open port 111/tcp on 10.0.0.177
Discovered open port 23/tcp on 10.0.0.177
Discovered open port 445/tcp on 10.0.0.177
Discovered open port 53/tcp on 10.0.0.177
Discovered open port 139/tcp on 10.0.0.177
Discovered open port 22/tcp on 10.0.0.177
Discovered open port 3306/tcp on 10.0.0.177
Discovered open port 2121/tcp on 10.0.0.177
Discovered open port 8180/tcp on 10.0.0.177
Discovered open port 1099/tcp on 10.0.0.177
Discovered open port 1524/tcp on 10.0.0.177
Discovered open port 514/tcp on 10.0.0.177
Discovered open port 6000/tcp on 10.0.0.177
Discovered open port 2049/tcp on 10.0.0.177
Increasing send delay for 10.0.0.177 from 0 to 5 due to 11 out of 35 dropped probes since last increase.
Discovered open port 513/tcp on 10.0.0.177
Completed Connect Scan at 01:21, 35.32s elapsed (1000 total ports)
Nmap scan report for 10.0.0.177
Host is up, received reset ttl 255 (0.026s latency).
Scanned at 2025-03-26 01:20:27 EDT for 35s
Not shown: 981 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
513/tcp  open  login        syn-ack
514/tcp  open  shell        syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
2121/tcp open  ccproxy-ftp  syn-ack
3306/tcp open  mysql        syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
8180/tcp open  unknown      syn-ack

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 35.42 seconds
           Raw packets sent: 4 (152B) | Rcvd: 1 (40B)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -Pn -n -vv 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:21 EDT
Initiating Connect Scan at 01:21
Scanning 10.0.0.177 [1000 ports]
Discovered open port 25/tcp on 10.0.0.177
Discovered open port 139/tcp on 10.0.0.177
Discovered open port 21/tcp on 10.0.0.177
Discovered open port 3306/tcp on 10.0.0.177
Discovered open port 111/tcp on 10.0.0.177
Discovered open port 5900/tcp on 10.0.0.177
Discovered open port 53/tcp on 10.0.0.177
Discovered open port 22/tcp on 10.0.0.177
Discovered open port 80/tcp on 10.0.0.177
Discovered open port 23/tcp on 10.0.0.177
Discovered open port 445/tcp on 10.0.0.177
Discovered open port 1524/tcp on 10.0.0.177
Discovered open port 5432/tcp on 10.0.0.177
Discovered open port 513/tcp on 10.0.0.177
Discovered open port 514/tcp on 10.0.0.177
Discovered open port 512/tcp on 10.0.0.177
Discovered open port 2121/tcp on 10.0.0.177
Discovered open port 6667/tcp on 10.0.0.177
Discovered open port 8180/tcp on 10.0.0.177
Discovered open port 8009/tcp on 10.0.0.177
Discovered open port 1099/tcp on 10.0.0.177
Increasing send delay for 10.0.0.177 from 0 to 5 due to max_successful_tryno increase to 4
Discovered open port 6000/tcp on 10.0.0.177
Discovered open port 2049/tcp on 10.0.0.177
Completed Connect Scan at 01:23, 70.41s elapsed (1000 total ports)
Nmap scan report for 10.0.0.177
Host is up, received user-set (0.026s latency).
Scanned at 2025-03-26 01:21:59 EDT for 71s
Not shown: 977 filtered tcp ports (no-response)
PORT     STATE SERVICE      REASON
21/tcp   open  ftp          syn-ack
22/tcp   open  ssh          syn-ack
23/tcp   open  telnet       syn-ack
25/tcp   open  smtp         syn-ack
53/tcp   open  domain       syn-ack
80/tcp   open  http         syn-ack
111/tcp  open  rpcbind      syn-ack
139/tcp  open  netbios-ssn  syn-ack
445/tcp  open  microsoft-ds syn-ack
512/tcp  open  exec         syn-ack
513/tcp  open  login        syn-ack
514/tcp  open  shell        syn-ack
1099/tcp open  rmiregistry  syn-ack
1524/tcp open  ingreslock   syn-ack
2049/tcp open  nfs          syn-ack
2121/tcp open  ccproxy-ftp  syn-ack
3306/tcp open  mysql        syn-ack
5432/tcp open  postgresql   syn-ack
5900/tcp open  vnc          syn-ack
6000/tcp open  X11          syn-ack
6667/tcp open  irc          syn-ack
8009/tcp open  ajp13        syn-ack
8180/tcp open  unknown      syn-ack

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 70.43 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -Pn -n -p-
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:23 EDT

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -Pn -n -p-
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:26 EDT
Stats: 0:00:12 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.41% done; ETC: 01:40 (0:14:00 remaining)
Stats: 0:00:14 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.66% done; ETC: 01:40 (0:13:47 remaining)
Stats: 0:00:14 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.80% done; ETC: 01:39 (0:12:45 remaining)

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 10.0.0.177 -Pn -n --top-ports 5
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:27 EDT
Nmap scan report for 10.0.0.177
Host is up (0.0073s latency).

PORT    STATE    SERVICE
21/tcp  open     ftp
22/tcp  open     ssh
23/tcp  open     telnet
80/tcp  open     http
443/tcp filtered https

Nmap done: 1 IP address (1 host up) scanned in 1.26 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1                      


Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:30 EDT
Stats: 0:00:00 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.00% done; ETC: 01:30 (0:00:00 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000059s latency).
All 1000 scanned ports on localhost (127.0.0.1) are in ignored states.
Not shown: 1000 closed tcp ports (conn-refused)

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:32 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000068s latency).
All 1000 scanned ports on localhost (127.0.0.1) are in ignored states.
Not shown: 1000 closed tcp ports (conn-refused)

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ netstat -antp          
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 10.10.10.4:48386        34.149.100.209:443      TIME_WAIT   -                   
tcp        0      0 10.10.10.4:38376        34.107.243.93:443       ESTABLISHED 55087/firefox-esr   
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ netstat -antp
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 10.10.10.4:37778        23.215.0.136:80         ESTABLISHED 55087/firefox-esr   
tcp        0      0 10.10.10.4:37764        23.215.0.136:80         ESTABLISHED 55087/firefox-esr   
tcp        0      0 10.10.10.4:38376        34.107.243.93:443       ESTABLISHED 55087/firefox-esr   
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo service ssh start  
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ netstat -antp          
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp        0      0 10.10.10.4:37764        23.215.0.136:80         TIME_WAIT   -                   
tcp        0      0 10.10.10.4:47276        34.117.188.166:443      ESTABLISHED 55087/firefox-esr   
tcp        0      0 10.10.10.4:38376        34.107.243.93:443       ESTABLISHED 55087/firefox-esr   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1                      
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:36 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00012s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo service apache2 start 
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1    
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:37 EDT
Stats: 0:00:00 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 1.00% done; ETC: 01:37 (0:00:00 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000083s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ netstat -antp              
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp        0      0 10.10.10.4:38376        34.107.243.93:443       ESTABLISHED 55087/firefox-esr   
tcp6       0      0 :::80                   :::*                    LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo service ssh stop      
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo service apache2 stop  
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sT 127.0.0.1  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:41 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000057s latency).
All 1000 scanned ports on localhost (127.0.0.1) are in ignored states.
Not shown: 1000 closed tcp ports (conn-refused)

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  10.10.10.5 -sT   
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:43 EDT
Nmap scan report for 10.10.10.5
Host is up (0.00065s latency).
All 1000 scanned ports on 10.10.10.5 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 23.65 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  nmap  10.10.10.5 -sT  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 01:44 EDT
Nmap scan report for 10.10.10.5
Host is up (0.00050s latency).
All 1000 scanned ports on 10.10.10.5 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 23.80 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  nmap  10.0.0.198 -sT  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:13 EDT

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo  nmap  10.0.0.198 -sT 
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:13 EDT
Nmap scan report for 10.0.0.198
Host is up (0.00067s latency).
All 1000 scanned ports on 10.0.0.198 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 23.03 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  nmap  10.0.0.198 -sT -Pn
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:16 EDT
Stats: 0:01:15 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 37.00% done; ETC: 02:19 (0:02:09 remaining)
Stats: 0:01:16 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 37.50% done; ETC: 02:19 (0:02:08 remaining)

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  nmap  10.0.0.5 -sT -Pn  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:17 EDT

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  nmap  10.10.10.5 -sT -Pn
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:18 EDT
Stats: 0:00:53 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 26.00% done; ETC: 02:21 (0:02:31 remaining)
Stats: 0:01:03 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 31.00% done; ETC: 02:21 (0:02:20 remaining)
Stats: 0:03:07 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 92.00% done; ETC: 02:21 (0:00:16 remaining)
Stats: 0:03:08 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 92.50% done; ETC: 02:21 (0:00:15 remaining)
Stats: 0:03:22 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 99.50% done; ETC: 02:21 (0:00:01 remaining)
Nmap scan report for 10.10.10.5
Host is up.
All 1000 scanned ports on 10.10.10.5 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 203.53 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  sudo nmap  10.10.10.5 -sT -Pn
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:22 EDT
Stats: 0:00:33 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 16.00% done; ETC: 02:25 (0:02:59 remaining)
Stats: 0:01:57 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 57.50% done; ETC: 02:25 (0:01:27 remaining)
Stats: 0:02:41 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 69.53% done; ETC: 02:26 (0:01:11 remaining)
Stats: 0:02:41 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 69.62% done; ETC: 02:26 (0:01:11 remaining)
Stats: 0:08:13 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 99.99% done; ETC: 02:30 (0:00:00 remaining)
Stats: 0:08:19 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 99.99% done; ETC: 02:30 (0:00:00 remaining)
Stats: 0:08:21 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 99.99% done; ETC: 02:30 (0:00:00 remaining)

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ namp -sS 10.10.10.5           
Command 'namp' not found, did you mean:
  command 'pamp' from deb paml
  command 'wamp' from deb python3-autobahn
  command 'nam' from deb nam
  command 'nama' from deb nama
  command 'nmap' from deb nmap
Try: sudo apt install <deb name>
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sS 10.10.10.5
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:31 EDT
Nmap scan report for 10.10.10.5
Host is up (0.00072s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 2.18 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sS 10.0.0.177  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:31 EDT
Stats: 0:01:14 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 43.51% done; ETC: 02:34 (0:01:37 remaining)
Stats: 0:01:15 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 43.52% done; ETC: 02:34 (0:01:39 remaining)
Warning: 10.0.0.177 giving up on port because retransmission cap hit (10).

                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sS 10.10.10.6
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:34 EDT
Nmap scan report for 10.10.10.6
Host is up (0.00019s latency).
Not shown: 977 closed tcp ports (reset)
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
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 08:00:27:82:FA:6C (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.83 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sN 10.10.10.6
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:37 EDT
Nmap scan report for 10.10.10.6
Host is up (0.00034s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE         SERVICE
21/tcp   open|filtered ftp
22/tcp   open|filtered ssh
23/tcp   open|filtered telnet
25/tcp   open|filtered smtp
53/tcp   open|filtered domain
80/tcp   open|filtered http
111/tcp  open|filtered rpcbind
139/tcp  open|filtered netbios-ssn
445/tcp  open|filtered microsoft-ds
512/tcp  open|filtered exec
513/tcp  open|filtered login
514/tcp  open|filtered shell
1099/tcp open|filtered rmiregistry
1524/tcp open|filtered ingreslock
2049/tcp open|filtered nfs
2121/tcp open|filtered ccproxy-ftp
3306/tcp open|filtered mysql
5432/tcp open|filtered postgresql
5900/tcp open|filtered vnc
6000/tcp open|filtered X11
6667/tcp open|filtered irc
8009/tcp open|filtered ajp13
8180/tcp open|filtered unknown
MAC Address: 08:00:27:82:FA:6C (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 1.91 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sN 10.10.10.5

Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:37 EDT
Stats: 0:00:00 elapsed; 0 hosts completed (0 up), 1 undergoing ARP Ping Scan
ARP Ping Scan Timing: About 100.00% done; ETC: 02:37 (0:00:00 remaining)
Nmap scan report for 10.10.10.5
Host is up (0.00051s latency).
All 1000 scanned ports on 10.10.10.5 are in ignored states.
Not shown: 1000 closed tcp ports (reset)
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 2.04 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sN 10.10.10.6 --reason 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:39 EDT
Nmap scan report for 10.10.10.6
Host is up, received arp-response (0.00071s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE         SERVICE      REASON
21/tcp   open|filtered ftp          no-response
22/tcp   open|filtered ssh          no-response
23/tcp   open|filtered telnet       no-response
25/tcp   open|filtered smtp         no-response
53/tcp   open|filtered domain       no-response
80/tcp   open|filtered http         no-response
111/tcp  open|filtered rpcbind      no-response
139/tcp  open|filtered netbios-ssn  no-response
445/tcp  open|filtered microsoft-ds no-response
512/tcp  open|filtered exec         no-response
513/tcp  open|filtered login        no-response
514/tcp  open|filtered shell        no-response
1099/tcp open|filtered rmiregistry  no-response
1524/tcp open|filtered ingreslock   no-response
2049/tcp open|filtered nfs          no-response
2121/tcp open|filtered ccproxy-ftp  no-response
3306/tcp open|filtered mysql        no-response
5432/tcp open|filtered postgresql   no-response
5900/tcp open|filtered vnc          no-response
6000/tcp open|filtered X11          no-response
6667/tcp open|filtered irc          no-response
8009/tcp open|filtered ajp13        no-response
8180/tcp open|filtered unknown      no-response
MAC Address: 08:00:27:82:FA:6C (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 1.91 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sN 10.10.10.5 --reasonn 
/usr/lib/nmap/nmap: unrecognized option '--reasonn'
See the output of nmap -h for a summary of options.
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sN 10.10.10.6 --reason  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:42 EDT
Nmap scan report for 10.10.10.6
Host is up, received arp-response (0.00049s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE         SERVICE      REASON
21/tcp   open|filtered ftp          no-response
22/tcp   open|filtered ssh          no-response
23/tcp   open|filtered telnet       no-response
25/tcp   open|filtered smtp         no-response
53/tcp   open|filtered domain       no-response
80/tcp   open|filtered http         no-response
111/tcp  open|filtered rpcbind      no-response
139/tcp  open|filtered netbios-ssn  no-response
445/tcp  open|filtered microsoft-ds no-response
512/tcp  open|filtered exec         no-response
513/tcp  open|filtered login        no-response
514/tcp  open|filtered shell        no-response
1099/tcp open|filtered rmiregistry  no-response
1524/tcp open|filtered ingreslock   no-response
2049/tcp open|filtered nfs          no-response
2121/tcp open|filtered ccproxy-ftp  no-response
3306/tcp open|filtered mysql        no-response
5432/tcp open|filtered postgresql   no-response
5900/tcp open|filtered vnc          no-response
6000/tcp open|filtered X11          no-response
6667/tcp open|filtered irc          no-response
8009/tcp open|filtered ajp13        no-response
8180/tcp open|filtered unknown      no-response
MAC Address: 08:00:27:82:FA:6C (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 1.77 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sN 10.10.10.5 --reason  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:42 EDT
Nmap scan report for 10.10.10.5
Host is up, received arp-response (0.0011s latency).
All 1000 scanned ports on 10.10.10.5 are in ignored states.
Not shown: 1000 closed tcp ports (reset)
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 6.54 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sF 10.10.10.5         
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:53 EDT
Stats: 0:00:08 elapsed; 0 hosts completed (1 up), 1 undergoing FIN Scan
FIN Scan Timing: About 49.53% done; ETC: 02:53 (0:00:09 remaining)
Stats: 0:00:14 elapsed; 0 hosts completed (1 up), 1 undergoing FIN Scan
FIN Scan Timing: About 70.63% done; ETC: 02:53 (0:00:06 remaining)
Nmap scan report for 10.10.10.5
Host is up (0.00066s latency).
All 1000 scanned ports on 10.10.10.5 are in ignored states.
Not shown: 1000 closed tcp ports (reset)
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 22.80 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sF 10.10.10.6 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:53 EDT
Stats: 0:00:00 elapsed; 0 hosts completed (0 up), 1 undergoing ARP Ping Scan
ARP Ping Scan Timing: About 100.00% done; ETC: 02:53 (0:00:00 remaining)
Nmap scan report for 10.10.10.6
Host is up (0.00025s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE         SERVICE
21/tcp   open|filtered ftp
22/tcp   open|filtered ssh
23/tcp   open|filtered telnet
25/tcp   open|filtered smtp
53/tcp   open|filtered domain
80/tcp   open|filtered http
111/tcp  open|filtered rpcbind
139/tcp  open|filtered netbios-ssn
445/tcp  open|filtered microsoft-ds
512/tcp  open|filtered exec
513/tcp  open|filtered login
514/tcp  open|filtered shell
1099/tcp open|filtered rmiregistry
1524/tcp open|filtered ingreslock
2049/tcp open|filtered nfs
2121/tcp open|filtered ccproxy-ftp
3306/tcp open|filtered mysql
5432/tcp open|filtered postgresql
5900/tcp open|filtered vnc
6000/tcp open|filtered X11
6667/tcp open|filtered irc
8009/tcp open|filtered ajp13
8180/tcp open|filtered unknown
MAC Address: 08:00:27:82:FA:6C (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 2.12 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sX 10.10.10.6
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:56 EDT
Nmap scan report for 10.10.10.6
Host is up (0.00034s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE         SERVICE
21/tcp   open|filtered ftp
22/tcp   open|filtered ssh
23/tcp   open|filtered telnet
25/tcp   open|filtered smtp
53/tcp   open|filtered domain
80/tcp   open|filtered http
111/tcp  open|filtered rpcbind
139/tcp  open|filtered netbios-ssn
445/tcp  open|filtered microsoft-ds
512/tcp  open|filtered exec
513/tcp  open|filtered login
514/tcp  open|filtered shell
1099/tcp open|filtered rmiregistry
1524/tcp open|filtered ingreslock
2049/tcp open|filtered nfs
2121/tcp open|filtered ccproxy-ftp
3306/tcp open|filtered mysql
5432/tcp open|filtered postgresql
5900/tcp open|filtered vnc
6000/tcp open|filtered X11
6667/tcp open|filtered irc
8009/tcp open|filtered ajp13
8180/tcp open|filtered unknown
MAC Address: 08:00:27:82:FA:6C (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 1.43 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap  -sX 10.10.10.5
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 02:56 EDT
Stats: 0:00:03 elapsed; 0 hosts completed (1 up), 1 undergoing XMAS Scan
XMAS Scan Timing: About 30.23% done; ETC: 02:56 (0:00:09 remaining)
Nmap scan report for 10.10.10.5
Host is up (0.00068s latency).
All 1000 scanned ports on 10.10.10.5 are in ignored states.
Not shown: 1000 closed tcp ports (reset)
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 23.58 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  nmap  -Pn -n  10.10.10.5 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 03:15 EDT
Stats: 0:00:02 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 17.20% done; ETC: 03:15 (0:00:10 remaining)
Nmap scan report for 10.10.10.5
Host is up (0.00065s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 23.45 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  nmap  -Pn -n  10.10.10.5 -v
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 03:18 EDT
Initiating ARP Ping Scan at 03:18
Scanning 10.10.10.5 [1 port]
Completed ARP Ping Scan at 03:18, 0.06s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 03:18
Scanning 10.10.10.5 [1000 ports]
Discovered open port 445/tcp on 10.10.10.5
Discovered open port 135/tcp on 10.10.10.5
Discovered open port 139/tcp on 10.10.10.5
Increasing send delay for 10.10.10.5 from 0 to 5 due to 23 out of 76 dropped probes since last increase.
Increasing send delay for 10.10.10.5 from 5 to 10 due to 12 out of 39 dropped probes since last increase.
Completed SYN Stealth Scan at 03:18, 13.50s elapsed (1000 total ports)
Nmap scan report for 10.10.10.5
Host is up (0.00062s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 13.70 seconds
           Raw packets sent: 1064 (46.800KB) | Rcvd: 1001 (40.040KB)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo  nmap  -Pn -n  10.10.10.5 -v
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 03:19 EDT
Initiating ARP Ping Scan at 03:19
Scanning 10.10.10.5 [1 port]
Completed ARP Ping Scan at 03:19, 0.07s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 03:19
Scanning 10.10.10.5 [1000 ports]
Discovered open port 135/tcp on 10.10.10.5
Discovered open port 139/tcp on 10.10.10.5
Discovered open port 445/tcp on 10.10.10.5
Increasing send delay for 10.10.10.5 from 0 to 5 due to 24 out of 79 dropped probes since last increase.
Increasing send delay for 10.10.10.5 from 5 to 10 due to 12 out of 38 dropped probes since last increase.
Completed SYN Stealth Scan at 03:19, 17.72s elapsed (1000 total ports)
Nmap scan report for 10.10.10.5
Host is up (0.00069s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
MAC Address: 08:00:27:7B:0C:F9 (Oracle VirtualBox virtual NIC)

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 17.91 seconds
           Raw packets sent: 1067 (46.932KB) | Rcvd: 1001 (40.040KB)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo  nmap  -Pn -n  10.10.10.6 -v
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 03:20 EDT
Initiating ARP Ping Scan at 03:20
Scanning 10.10.10.6 [1 port]
Completed ARP Ping Scan at 03:20, 0.05s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 03:20
Scanning 10.10.10.6 [1000 ports]
Discovered open port 21/tcp on 10.10.10.6
Discovered open port 5900/tcp on 10.10.10.6
Discovered open port 139/tcp on 10.10.10.6
Discovered open port 25/tcp on 10.10.10.6
Discovered open port 22/tcp on 10.10.10.6
Discovered open port 53/tcp on 10.10.10.6
Discovered open port 111/tcp on 10.10.10.6
Discovered open port 445/tcp on 10.10.10.6
Discovered open port 80/tcp on 10.10.10.6
Discovered open port 3306/tcp on 10.10.10.6
Discovered open port 23/tcp on 10.10.10.6
Discovered open port 8180/tcp on 10.10.10.6
Discovered open port 1524/tcp on 10.10.10.6
Discovered open port 2049/tcp on 10.10.10.6
Discovered open port 2121/tcp on 10.10.10.6
Discovered open port 512/tcp on 10.10.10.6
Discovered open port 514/tcp on 10.10.10.6
Discovered open port 8009/tcp on 10.10.10.6
Discovered open port 5432/tcp on 10.10.10.6
Discovered open port 513/tcp on 10.10.10.6
Discovered open port 1099/tcp on 10.10.10.6
Discovered open port 6000/tcp on 10.10.10.6
Discovered open port 6667/tcp on 10.10.10.6
Completed SYN Stealth Scan at 03:20, 0.05s elapsed (1000 total ports)
Nmap scan report for 10.10.10.6
Host is up (0.00010s latency).
Not shown: 977 closed tcp ports (reset)
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
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 08:00:27:82:FA:6C (Oracle VirtualBox virtual NIC)

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.25 seconds
           Raw packets sent: 1001 (44.028KB) | Rcvd: 1001 (40.120KB)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$  nmap  -Pn -n  10.10.10.6 -v 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 03:21 EDT
Initiating ARP Ping Scan at 03:21
Scanning 10.10.10.6 [1 port]
Completed ARP Ping Scan at 03:21, 0.07s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 03:21
Scanning 10.10.10.6 [1000 ports]
Discovered open port 445/tcp on 10.10.10.6
Discovered open port 22/tcp on 10.10.10.6
Discovered open port 139/tcp on 10.10.10.6
Discovered open port 3306/tcp on 10.10.10.6
Discovered open port 23/tcp on 10.10.10.6
Discovered open port 80/tcp on 10.10.10.6
Discovered open port 5900/tcp on 10.10.10.6
Discovered open port 25/tcp on 10.10.10.6
Discovered open port 111/tcp on 10.10.10.6
Discovered open port 53/tcp on 10.10.10.6
Discovered open port 21/tcp on 10.10.10.6
Discovered open port 514/tcp on 10.10.10.6
Discovered open port 6667/tcp on 10.10.10.6
Discovered open port 5432/tcp on 10.10.10.6
Discovered open port 8180/tcp on 10.10.10.6
Discovered open port 513/tcp on 10.10.10.6
Discovered open port 6000/tcp on 10.10.10.6
Discovered open port 2121/tcp on 10.10.10.6
Discovered open port 512/tcp on 10.10.10.6
Discovered open port 1099/tcp on 10.10.10.6
Discovered open port 1524/tcp on 10.10.10.6
Discovered open port 8009/tcp on 10.10.10.6
Discovered open port 2049/tcp on 10.10.10.6
Completed SYN Stealth Scan at 03:21, 0.05s elapsed (1000 total ports)
Nmap scan report for 10.10.10.6
Host is up (0.000093s latency).
Not shown: 977 closed tcp ports (reset)
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
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 08:00:27:82:FA:6C (Oracle VirtualBox virtual NIC)

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.26 seconds
           Raw packets sent: 1001 (44.028KB) | Rcvd: 1001 (40.120KB)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ nmap -p80 example.com 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 03:27 EDT
Nmap scan report for example.com (23.215.0.138)
Host is up (0.0010s latency).
Other addresses for example.com (not scanned): 23.192.228.80 23.192.228.84 96.7.128.175 96.7.128.198 23.215.0.136 2600:1406:bc00:53::b81e:94c8 2600:1408:ec00:36::1736:7f24 2600:1406:bc00:53::b81e:94ce 2600:1406:3a00:21::173e:2e65 2600:1408:ec00:36::1736:7f31 2600:1406:3a00:21::173e:2e66
rDNS record for 23.215.0.138: a23-215-0-138.deploy.static.akamaitechnologies.com

PORT   STATE    SERVICE
80/tcp filtered http

Nmap done: 1 IP address (1 host up) scanned in 0.71 seconds
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ nmap -p80 example.com -v
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 03:27 EDT
Initiating Ping Scan at 03:27
Scanning example.com (23.215.0.136) [4 ports]
Completed Ping Scan at 03:27, 0.03s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 03:27
Completed Parallel DNS resolution of 1 host. at 03:27, 0.01s elapsed
Initiating SYN Stealth Scan at 03:27
Scanning example.com (23.215.0.136) [1 port]
Completed SYN Stealth Scan at 03:27, 0.26s elapsed (1 total ports)
Nmap scan report for example.com (23.215.0.136)
Host is up (0.00074s latency).
Other addresses for example.com (not scanned): 23.192.228.80 23.192.228.84 23.215.0.138 96.7.128.198 96.7.128.175 2600:1406:bc00:53::b81e:94ce 2600:1406:3a00:21::173e:2e65 2600:1406:bc00:53::b81e:94c8 2600:1406:3a00:21::173e:2e66 2600:1408:ec00:36::1736:7f24 2600:1408:ec00:36::1736:7f31
rDNS record for 23.215.0.136: a23-215-0-136.deploy.static.akamaitechnologies.com

PORT   STATE    SERVICE
80/tcp filtered http

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.46 seconds
           Raw packets sent: 6 (240B) | Rcvd: 3 (112B)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ sudo nmap -p80 example.com -v
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-26 03:28 EDT
Initiating Ping Scan at 03:28
Scanning example.com (23.192.228.80) [4 ports]
Completed Ping Scan at 03:28, 0.03s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 03:28
Completed Parallel DNS resolution of 1 host. at 03:28, 0.04s elapsed
Initiating SYN Stealth Scan at 03:28
Scanning example.com (23.192.228.80) [1 port]
Completed SYN Stealth Scan at 03:28, 0.23s elapsed (1 total ports)
Nmap scan report for example.com (23.192.228.80)
Host is up (0.00097s latency).
Other addresses for example.com (not scanned): 96.7.128.175 23.215.0.136 96.7.128.198 23.192.228.84 23.215.0.138 2600:1406:bc00:53::b81e:94ce 2600:1406:3a00:21::173e:2e65 2600:1406:3a00:21::173e:2e66 2600:1408:ec00:36::1736:7f31 2600:1406:bc00:53::b81e:94c8 2600:1408:ec00:36::1736:7f24
rDNS record for 23.192.228.80: a23-192-228-80.deploy.static.akamaitechnologies.com

PORT   STATE    SERVICE
80/tcp filtered http

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.44 seconds
           Raw packets sent: 6 (240B) | Rcvd: 3 (112B)
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ cd /usr/share/nmap/
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ cd /usr/share/nmap           
                                                                                                                                                                      
┌──(kali㉿kali)-[/usr/share/nmap]
└─$ ls
nmap.dtd  nmap-mac-prefixes  nmap-os-db  nmap-protocols  nmap-rpc  nmap-service-probes  nmap-services  nmap.xsl  nselib  nse_main.lua  scripts
                                                                                                                                                                      
┌──(kali㉿kali)-[/usr/share/nmap]
└─$ cat nmap-service-probes 




### References
