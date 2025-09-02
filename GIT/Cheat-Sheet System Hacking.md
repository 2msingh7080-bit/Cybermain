2025-04-08 18:25

Status:

Tags:

# Cheat-Sheet System Hacking

# Cheat-Sheet Metasploit
start 
	sudo service postgresql start
run
	msfconsole 
1. search for exploit and read information 
- search ``<keyword>``
	- search ``<exploit><keyword>``




| Keywords                                                                                                                                                     | usecase                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| search                                                                                                                                                       | searches for anything                                 |
| type:exploit                                                                                                                                                 | shows only exploit                                    |
| info                                                                                                                                                         | gives information about exploit                       |
| RHOSTS                                                                                                                                                       | Target's IP                                           |
| RPORT                                                                                                                                                        | Target' port number                                   |
| LHOST                                                                                                                                                        | Attacker's IP                                         |
| LPORT                                                                                                                                                        | Attacker's port                                       |
| use ``<modulepath >``                                                                                                                                        | specifies to use                                      |
| show options                                                                                                                                                 | gives the options that is available  for the  exploit |
| show payloads                                                                                                                                                | shows payloads                                        |
| set ``<option> <value>``<br>           set RHOSTS ``<Target's IP>``<br>		    set payload ``<payloadfilepath``<br>			set LPORT ``<Attacker's port>``<br>	<br> | sets the options and value                            |
|                                                                                                                                                              |                                                       |
|                                                                                                                                                              |                                                       |

### References
