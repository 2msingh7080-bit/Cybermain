2025-05-09 11:32

Status:

Tags:

# TGPT

## process for generating prompts   

- To run and compile any code using ai for  tgpt 
- ask ai to give **shell script** that compiles and runs a (name of language ) program (task that you in code)
	- Example 
		- simple shell script that compiles and runs a C++ program to add two numbers:

- or (manully) 
	- ==tgpt  -c "c++ code for multipe two number with correct syntax  "  (add correct syntax  )==
- first save the code in file 
- compile file
	- `` g++ <codename> -o <runfile>`` 
	- if compile fails then 
		- try to fix using online [complier](https://www.onlinegdb.com/) s 
		- remove cpp in top 
- run 
	- ``./<filename> 
- tgpt  -c "c++ code for multipe two number with correct syntax  "  
# so to 
so to run any shell command in tgpt (when it does not do )

- ask chat gpt for shell command 
- then give and ask tgpt -i mode to give prompt for it 
- then run 
- when you have shell command then 
	- it should perform this " `<shell command> `" for that give me prompt
# TGPT Prompts / Commands 

- Prompts for nmap scan 

```bash
tgpt  -s "namp scan for version, os, for the ip 10.10.10.6 and save output in ip.txt file"
```



#### nmap scan vun
- Prompts for nmap scan
```bash
tgpt  -s "Perform an advanced Nmap scan on  IPs 10.10.10.6 using firewall evasion techniques such as decoys, fragmentation, and randomizing source ports. Save the results of all scans to bypass.txt."
 
```
-  command 
```bash
  nmap -sV --script vuln -p- --open --script=http-headers -oA bypass.txt 10.10.10.6 --data-string "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36" --max-rate 1000 --randomize-hosts --send eth 0
```

- files as output 
	-  bypass.txt.gnmap  bypass.txt.nmap  bypass.txt.xml 
-------- 









- scan using nikto 




----- 
# prompt 

```bash
This command searches for potential vulnerabilities in IP addresses and domains found in the 'ip.txt' file. It uses grep to extract valid IP addresses and domain names, then pipes the results to a while loop that performs the following actions for each match:
   
1. Prints a header line in the 'vuln2.txt' file indicating which item is being searched.
2. Uses the searchsploit tool to search for exploits related to the extracted IP address or domain name.
3. Appends the search results to the 'vuln2.txt' file.                                                                                                                                                                                                                                   
4. Adds a separator line between each search result.                                                                                           
The command will process all unique entries in the 'ip.txt' file, potentially uncovering security vulnerabilities across various networks and systems.  
```

# Command

```bash
grep -oP '\b(?:\d{1,3}\.){3}\d{1,3}\b|\b[A-Za-z0-9.-]+\.[A-Za-z]{2,}' ip.txt | sort -u | while read line; do echo "$line" >> vuln2.txt; searchsploit "$line" | grep -v "^#" | sed 's/^/Y4:0/' >> vuln2.txt; echo "------------------------" >> vuln2.txt; done
 
```
- files as output  - vun1.txt
-----




- [x] make page on tgpt ans use case 
- [ ] bito



# web application pen test using AI 
1. download seclists 
2. to perform any scan make copy of list in 
3. desktop then do it 

----
# prompt 
```bash
  tgpt -s "Use gobuster to fuzz directories on http://10.10.10.6 using the wordlist at common.txt and save the output to results.txt"

```
# command

```bash
 gobuster dir -u http://10.10.10.6 -w common.txt -o commonresults.txt 
```

- files as output  - commonresults.txt
----
# prompt 

```bash
tgpt -s "Use Gobuster to enumerate directories on http://10.10.10.6. Use the default wordlist located at /usr/share/wordlists/dirb/common.txt to generate potential directory names. Look for php, html, and txt file extensions.Show only status code and  Save results to gobuster_advanced.txt." 
```
# command
```bash
 gobuster dir -u http://10.10.10.6 -w /usr/share/wordlists/dirb/common.txt -e php,html,txt -o gobuster_advanced.txt
```
- files as output  - gobuster_advanced.txt
-----

- using feroxbuster

 tgpt -s "Use feroxbuster to fuzz directories on http://10.10.10.6 using the wordlist at common. txt and save results to ferox.txt"
feroxbuster -u http://10.10.10.6 -w common.txt -o ferox.txt
- brute force attack using AI 


- [ ] start https://youtu.be/yw5j1kNRrMI?t=7338
- [ ] make proper structure of tgpt 


### References
