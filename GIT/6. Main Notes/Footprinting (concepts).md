2025-07-10 15:07

Status:

Tags:

# Lab Hands on (concepts)

# Footprinting Mind Map (CEH v13)

This document presents a detailed breakdown of footprinting techniques, as visualized in a mind map format, based on the CEH v13 curriculum. Footprinting, the initial phase of ethical hacking, involves gathering information about a target organization to understand its security posture and potential vulnerabilities. This document outlines the various aspects of footprinting, including information gathering methods, tools, and countermeasures, providing a comprehensive overview for cybersecurity professionals and aspiring ethical hackers.

## I. Footprinting Concepts

- **Definition:** Gathering information about a target system or network.
    
- **Objectives:**
    
    - Learn security posture.
        
    - Identify potential vulnerabilities.
        
    - Reduce focus area.
        
    - Draw network map.
        
- **Types:**
    
    - **Active:** Direct interaction with the target. Higher risk of detection.
        
    - **Passive:** Gathering information without direct interaction. Lower risk of detection.
        

## II. Information Gathering Methods

- **Search Engines:**
    
    - Google Hacking (Advanced search operators).
        
        - `site:` (Specific website).
            
        - `filetype:` (Specific file type).
            
        - `intitle:` (Specific title).
            
        - `inurl:` (Specific URL).
            
    - Shodan (IoT devices, open ports).
        
    - DuckDuckGo (Privacy-focused).
        
- **Websites:**
    
    - Whois (Domain registration information).
        
    - Netcraft (Website technology information).
        
    - BuiltWith (Technology profile of a website).
        
    - Archive.org (Historical website data).
        
- **Social Media:**
    
    - LinkedIn (Employee information, company structure).
        
    - Twitter (Real-time updates, employee activities).
        
    - Facebook (Personal information, social connections).
        
    - Instagram (Images, location data).
        
- **Job Sites:**
    
    - Indeed, LinkedIn, Glassdoor (Technology stack, skills required).
        
- **Financial Records:**
    
    - SEC Filings (Financial information, company structure).
        
- **DNS Records:**
    
    - NSLookup, Dig (DNS information, IP addresses).
        
- **Network Information:**
    
    - Traceroute (Network path).
        
    - Ping (Host availability).
        
- **Email Footprinting:**
    
    - Email header analysis (IP addresses, server information).
        
    - Email tracking tools.
        
- **OSINT Framework:**
    
    - Centralized repository of OSINT tools and resources.
## III. Footprinting Tools

- **Recon-ng:**
    
    - Open-source reconnaissance framework.
        
    - Modules for various information gathering tasks.
        
- **theHarvester:**
    
    - Gathers emails, subdomains, hosts, employee names from multiple sources.
        
- **Maltego:**
    
    - Graphical link analysis tool.
        
    - Visualizes relationships between entities.
        
- **Shodan:**
    
    - Search engine for internet-connected devices.
        
- **Nmap:**
    
    - Network scanner for host discovery and service enumeration.
        
- **Metagoofil:**
    
    - Extracts metadata from public documents.
        
- **FOCA (Fingerprinting Organizations with Collected Archives):**
    
    - Automated tool for finding metadata and hidden information in documents.
        
- **Central Ops:**
    
    - Online tools for DNS lookup, reverse IP lookup, and other network information.
        
- **Netcraft:**
    
    - Provides website information, including hosting location and technology.
        
- **Whois Tools:**
    
    - Various online tools for querying Whois databases.

## IV. Footprinting Techniques

- **DNS Footprinting:**
    
    - Gathering DNS records to identify servers and network infrastructure.
        
    - Tools: `nslookup`, `dig`, online DNS lookup tools.
        
- **Website Footprinting:**
    
    - Analyzing website structure, technologies, and content.
        
    - Tools: `BuiltWith`, web browser developer tools, `wget`, `curl`.
        
- **Email Footprinting:**
    
    - Extracting information from email headers.
        
    - Tools: Email header analyzers.
        
- **Social Engineering:**
    
    - Manipulating individuals to reveal information.
        
    - Techniques: Phishing, pretexting, baiting.
        
- **Whois Footprinting:**
    
    - Obtaining domain registration information.
        
    - Tools: Whois lookup tools.
        
- **Network Footprinting:**
    
    - Mapping network topology and identifying devices.
        
    - Tools: `traceroute`, `ping`, `Nmap`.
        

## V. Footprinting Countermeasures

- **Limit Information Disclosure:**
    
    - Reduce the amount of information available online.
        
    - Review and remove unnecessary data from websites and social media.
        
- **Privacy Settings:**
    
    - Configure privacy settings on social media accounts.
        
- **Whois Privacy:**
    
    - Use private registration services to hide domain owner information.
        
- **Employee Training:**
    
    - Educate employees about social engineering tactics.
        
- **Firewall Configuration:**
    
    - Configure firewalls to restrict access to sensitive services.
        
- **Intrusion Detection Systems (IDS):**
    
    - Monitor network traffic for suspicious activity.
        
- **Honeypots:**
    
    - Decoy systems to attract and detect attackers.
        
- **Regular Security Audits:**
    
    - Identify and address vulnerabilities.
        
- **Use Strong Passwords:**
    
    - Implement strong password policies.
        
- **Keep Software Updated:**
    
    - Patch vulnerabilities promptly.
        
- **Implement Access Controls:**
    
    - Restrict access to sensitive information.
        

## VI. Legal and Ethical Considerations

- **Legality:**
    
    - Understand and comply with local laws and regulations.
        
    - Avoid unauthorized access to systems and data.
        
- **Ethics:**
    
    - Obtain permission before conducting footprinting activities.
        
    - Respect privacy and confidentiality.
        
    - Disclose findings responsibly.
        
- **Compliance:**
    
    - Adhere to industry standards and best practices.
        
    - Comply with data protection regulations (e.g., GDPR, CCPA).
        

## VII. Footprinting Reporting

- **Document Findings:**
    
    - Record all information gathered during footprinting.
        
- **Analyze Data:**
    
    - Identify potential vulnerabilities and security weaknesses.
        
- **Prepare Report:**
    
    - Summarize findings in a clear and concise report.
        
- **Recommendations:**
    
    - Provide recommendations for improving security posture.
        
- **Presentation:**
    
    - Present findings to stakeholders.
        

This document provides a structured overview of footprinting, covering essential concepts, techniques, tools, countermeasures, and ethical considerations. By understanding these aspects, cybersecurity professionals can effectively gather information about target organizations, identify vulnerabilities, and develop strategies to improve security posture.

# Module : 2 Footprinting 
## Types of Footprinting/Reconnaissance
1. Passive Footprinting 
	 gathering information about the target without direct interaction. It is mainly useful when the information gathering activities are not to be detected by the target.
	 - It involves: 
	    -  Open-source Intelligence (OSINT) gathering
	    -  Proprietary databases and paid services 
	    -  Sharing intelligence with partner organizations or industry groups
2.  Active Footprinting
	Active footprinting involves gathering information about the target with direct interaction
	- It involves: 
		-  DNS interrogation
		-  Social engineering 
		-   Network/port scanning 
		- User and service enumeration
## Information Obtained in Footprinting
The major objectives of footprinting include collecting the network information, system information, and organizational information of the target.

1. Organization Information. 
	 The information about an organization is available from its website. In addition, you can query the target’s domain name against the Whois database and obtain valuable information.
- The information collected includes: 
	- Employee details (employee names, contact addresses, designations, and work experience)
	- Addresses and mobile/telephone numbers
	-  Branch and location details 
	- Partners of the organization 
	- Web links to other company-related sites o Background of the organization 
	- Web technologies 
	- News articles, press releases, and related documents 
	- Legal documents related to the organization 
	- Patents and trademarks related to the organization
2.  Network Information:   
	You can gather network information by performing Whois database analysis, trace routing, and so on. The information collected includes: 
	-  Domain and sub-domains 
	- Network blocks 
	- Network topology, trusted routers, and firewalls 
	- IP addresses of the reachable systems 
	- Whois records 
	- DNS records and related information
3. System Information:
	 You can gather system information by performing network footprinting, DNS footprinting, website footprinting, email footprinting, and so on. 
	 - The information collected includes: 
	 - Web server OS
	 -  Location of web servers 
	 - Publicly available email addresses 
	 - Usernames, passwords, and so on
## Footprinting Methodology 

![1000](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*X8CNU3vwBv-2bmjFEFkB7A.png)

### Google Hacking Techniques


| Search Operator <br> | Purpose                                                                                 |
| -------------------- | --------------------------------------------------------------------------------------- |
| cache:               | Displays the web pages stored in the Google cache                                       |
| link:                | Lists web pages that have links to the specified web page<br>                           |
| related:             | Lists web pages that are similar to the specified web page                              |
| info:                | Presents some information that Google has about a particular web page                   |
| site:                | Restricts the results to those websites in the given domain                             |
| allintitle:          | Restricts the results to those websites containing all the search keywords in the title |
| intitle:             | Restricts the results to documents containing the search keyword in the title           |
| allinurl:            | Restricts the results to those containing all the search keywords in the URL            |
| inurl:               | Restricts the results to documents containing the search keyword in the URL             |
| location:            | Finds information for a specific location                                               |
| intext:              |                                                                                         |
| inanchor:            |                                                                                         |
| phonebook:           |                                                                                         |
| after:               |                                                                                         |
| allinanchor:         |                                                                                         |
| filetype:            |                                                                                         |
| source:              |                                                                                         |
| before:              |                                                                                         |
### VPN Footprinting through Google Hacking Database
![900](https://cdn.hashnode.com/res/hashnode/image/upload/v1732954954834/2538a7c3-7873-4ca3-b781-c5f71bd14abc.png?auto=compress,format&format=webp)

## Footprinting through SHODAN Search engines 


### Gathering Information using Google image  search 
- reverse image search 

### Gathering Information using video search engine 
- Using video analysis tools such as
	- YouTube Metadata and  YouTube DataViewer
	- MW Metadata
	- EZGif 
	- VideoReverser.com

### Gathering Information using Meta Search Engine
- Using meta search engines, such as
	- Startpage
	- MetaGer
	-  eTools.ch
###  Gathering Information from (FTP) Search Engines
- Using FTP search engines such as
	- NAPALM FTP Indexe -  example 
	- FreewareWeb FTP File Search
	- Mamont 
	- Globalfilesearch.com
###  Gathering Information from IoT Search Engines
- IoT search engines such as 
	- Shodan
	- Censys
	-  ZoomEye
## Footprinting through Internet Research Services
### Finding a Company’s Top-Level Domains (TLDs) and Sub-domains 
-  The target organization’s external URL can be located with the help of search engines such as Google and Bing.
	`` site:microsoft.com -inurl:www``
- Tools to Search Company’s Sub-domains 
	- Netcraft 
	-  DNSdumpster
	- Pentest-Tools Find Subdomains
	- sublist3r
### Extracting Website Information from ``https://archive.org`` 
- use https://archives.org for website records 

Attackers can use tools such as Photon to retrieve archived URLs of the target website from archive.org. Run the following command to retrieve the archive.org links of the target website:

- using photon 
	``photon.py -u <URL of the Target Website> -l 3 -t 200 --wayback``

### Footprinting through People Search Services You can use
-  People Search Service - Spokeo
Attackers can use the Spokeo people search online service to search for people belonging to the target organization. 

### Footprinting through Job search People Search 
### Dark Web Footprinting

Attackers use dark web searching tools, such as Tor Browser and ExoneraTor, and Onionland to gather confidential information about the target.

- Searching the Dark Web with Advanced Search Parameters 
	-  Personal profiles: Search for information related to the victim’s personal profiles such as profiles of social media or personal websites. 
		- For example, "John Doe" site:facebook.com OR site:linkedin.com
	-  Scientific publications: Search for publications on specific publications such as academic or scientific research papers, and articles.
		- For example, "John Doe" site:scholar.google.com
	-  Court records: Search for legal documents related to court records or cases. 
		- For example, "John Doe" court records
	-  Member directories: Search for directories of members employed to the organizations. 
		- For example, "John Doe" site:example.com "employee directory"
	-  Medical records: Search for medical information or health history of the victim. 
		- For example, "John Doe" medical records
	-  Location records: Search for location information such as location history or GPS information of the victim.
		- For example, "John Doe" location history
- visit page -176 (for detail table view)

### Determining the Operating System
- using tools like 
	- Netcraft 
	- SHODAN Search Engine
	-  Censys 

### Competitive Intelligence Gathering
Competitive intelligence gathering is the process of identifying, gathering, analyzing, verifying, and using information about your competitors from resources such as the Internet
- Sources of Competitive Intelligence 
	1. Direct Approach
		- Direct approach techniques include gathering information from trade shows, social engineering of employees and customers, and so on.
	2.  Indirect Approach
		-  Company websites and employment ads o Support threads and reviews o Search engines, Internet, and online database o Social media postings o Press releases and annual reports o Trade journals, conferences, and newspapers o Patent and trademarks o Product catalogs and retail outlets o Analyst and regulatory reports o Customer and vendor interviews o Agents, distributors, and suppliers o Industry-specific blogs and publications o Legal databases, e.g., LexisNexis o Business information databases, e.g., D&B Hoovers
- competitive Intelligence - When Did this Company Begin? How Did it Develop?
	- when did it begin 
	- How they develop
	- Who leads 
	- where is the located
- Information Resource Sites
	-  EDGAR Database
	- D&B Hoovers
	-  LexisNexis
	- Business Wire
	- Factiva
- Competitive Intelligence - What Are the Company's Plans?
	- MarketWatch
	- The Wall Street Transcript
	- Euromonitor
	-  Experian 
	- The Search Monitor
	-  USPTO  
- Competitive Intelligence - What Expert Opinions Say About the Company?
	-  SEMRush 
	- ABI/INFORM Global 
	- SERanking
	-  SimilarWeb

### Other Techniques for Footprinting through Internet Research Services

| Footprinting Technique                                     | Tools Used                                      |
| ---------------------------------------------------------- | ----------------------------------------------- |
| Finding the Geographical Location of the Target            | Google Earth, Google Maps, and Wikimapia        |
| Gathering Information from Financial Services              | Google Finance, MSN Money, and Yahoo! Finance   |
| Gathering Information from Business Profile Sites          | opencorporates, Crunchbase, and corporationwiki |
| Monitoring Targets Using Alerts                            | Google Alerts, X Alerts, and Giga Alerts        |
| Tracking the Online Reputation of the Target               | Mention, ReviewPush, and Reputology             |
| Gathering Information from Groups, Forums, and Blogs<br>   | Google Groups and Linkedin Groups               |
| Gathering Information from Public Source-Code Repositories | Recon-ng                                        |

1.  Finding the Geographical Location of the Target 
	- Tools for Finding the Geographical Location
		- Attackers may use tools such as 
		- Google Earth 
		- Google Maps 
		- Wikimapia
2.   Gathering Information from Financial Services
	-  Financial services such as
	- Google Finance
	- MSN Money 
	- Yahoo Finance 
	- Investing.com
3.  Gathering Information from Business Profile Sites
	- Attackers use business profile sites such as
		- opencorporates
		- Crunchbase
		- corporationwik
4.  Monitoring Targets Using Alerts
	-  information based on user preference, usually via email or SMS
		- Tools such as 
			- Google Alerts
			- X Alerts
			-  Giga Alerts 
5.  Tracking the Online Reputation of the Target
	- Online Reputation Tracking Tools
		- Attackers can use tools such as 
		- Mention
		- ReviewPush 
		- Reputology
6.  Gathering Information from Public Source-Code Repositories
	- Source code–based repositories are online services or tools available on internal servers or can be hosted on third-party websites such as GitHub, GitLab, SourceForge, and BitBucket.
	- Attackers can use  to discover public source-code repositories using  tools such as 
		- Recon-ng

## Demonstrate Footprinting through Social Networking Sites
### People Search on Social Networking Sites
Social networking sites such as Facebook, Twitter, LinkedIn, and Instagram allow you to find people by name, keyword, company, school, friends, colleagues, and the people living around them. Searching for people on these sites returns personal information such as name, position, organization name, current location, and educational qualifications
- Social networking sites such as
	- Facebook
	- Twitter
	- LinkedIn
	-  Instagram
### Gathering Inform at ion from LinkedIn

- Attackers can use theHarvester tool to gather information from LinkedIn based on the target organization name 
	- use tool like
		- theHarvester 
			``theHarvester -d microsoft -l 200 -b linked``

### Harvesting Email Lists with AI
- Attackers use automated tools such as theHarvester and Email Spider to collect publicly available email addresses of the target organization that helps them perform social engineering and brute-force attack
	- tools like 
		- theHarvester 
			- `` theharvester -d microsoft.com -l 200 -b baidu``
			- prompt 
				- ``“Use theHarvester to gather email accounts associated with microsoft.com, limiting results to 200, and leveraging 'baidu' as a data source ``
		- Email Spider
### Analyzing Target Social Media Presence
  - Attackers track social media sites using BuzzSumo, Google Trend, Hashatit, etc. to discover most shared content using hashtags or keywords, track accounts and URLs, email addresses, etc.
- Attackers use this information to perform phishing, social engineering, and other types of attack
- tools such as
	-  BuzzSumo
	- Google Trend
	- Hashatit
### Tools for Footprint ing through Social Networking Sites 
- tools such as 
	- Sherlock
		- Sherlock tool is used to search a vast number of social networking sites for a target username
		- use - `` sherlock "username"``
	- Social Searcher
		- Social Searcher allows you to search for content in social networks in real-time and provides deep analytics data
### Footprinting through Social Networking Sites with AI
- prompt `` “Use Sherlock to gather personal information about Sundar Pichai and save the result in recon2.txt” ``
## Whois Footprinting
- Whois query returns
	- Domain name details • Contact details of domain owners • Domain name servers • NetRange • When a domain was created • Expiry records • Last updated record
-  Thick Whois (Distributed Model) - Stores the complete Whois information from all the registrars for a particular set of data.
- Thin Whois (Centralized Model) - Stores only the name of the Whois server of the registrar of a domain, which in turn holds complete details on the data being looked up.
- Decentralized Whois - Stores complete WHOIS information and has multiple independent entities to manage the WHOIS database
### Finding IP Geolocation Information 
- IP geolocation lookup tools such as
	- IP2Location
	- IP Location Finder
	-  IP Address Geographical Location Finder

## DNS Footprinting
- DNS records provide important information about the location and types of servers
- Attackers can gather DNS information to determine key hosts in the network and can perform social engineering attacks
-  Attackers query DNS servers using DNS interrogation tools, such as SecurityTrails, Fierce, DNSChecker, and zdns, to retrieve the record structure that contains information about the target DNS
### Extracting DNS Information
- DNS footprinting helps in determining the following records about the target DNS:

| Record Type | Description                                      |
| ----------- | ------------------------------------------------ |
| A           | Points to a host's IP address                    |
| AAAA        | Points to a host's IPv6 address                  |
| MX          | Points to domain's mail server                   |
| NS          | Points to host's name server                     |
| CNAME       | Canonical naming allows aliases to a host        |
| SOA         | Indicate authority for a domain                  |
| SRV         | Service records                                  |
| PTR         | Maps IP address to a hostname                    |
| RP          | Responsible person                               |
| HINFO       | Host information record includes CPU type and OS |
| TXT         | Unstructured text records                        |
### DNS Interrogation Tools
- Attackers use DNS  interrogation tools such as
	- SecurityTrails
	- Fierce
	- DNSChecker
	- zdns 
	- DNSdumpster.com 
### Fierce (T)
- to use 
	*  `` python fierce.py --domain hackerschool.in``
	* `` python fierce.py fierce –-domain hackerschool.in -–subdomains write admin mail``
	* `` python fierce.py --domain google.com  --subdomains mail --traverse 10``
	* connect to HTTP connection on discovered domains
		* ``python fierce.py --domain hackerschool.in --subdomains mail --connect``
-  discovered records of the target domain, i.e., a full detailed scan:
	- `` python fierce.py --domain googel.com  --wide ``
### DNS Lookup with AI
- "Install and use DNSRecon to perform DNS enumeration on the target domain www.certifiedhacker.com"
- DNSRecon
- after installing do 
	- pip install --upgrade dnspython --break-system-packages
###  Reverse DNS Lookup
- the Reverse Lookup tool performs a reverse IP lookup by taking an IP address and locating a DNS PTR record for that IP address.
- using website
	- mxtoolbox.com
## Network and Email Footprinting
### Locate the Network Range 
 - an attacker can obtain information about how the network is structured and which machines in the network are alive. The network range also helps identify the network topology, access control device, and OS used in the target network. To find the network range of the target network, one must enter the server IP address (gathered in Whois footprinting) in the
- ARIN Whois database search tool. A user can also visit the ARIN website (https://www.arin.net/about/welcome/region) and enter the server IP into the SEARCH Site or Whois text box. This yields the network range of the target network.
- using tool li`ke  
	- ARIN

### Traceroute
- refer material for more info 
- inding the route of the target host on the network is necessary to test against man-in-the-middle attacks and other related attacks. Most operating systems come with a Traceroute utility to perform this task. It traces the path or route through which the target host packets travel in the network.
- Traceroute uses the ICMP protocol and Time to Live (TTL) field of the IP header to find the path of the target host in the network. 

- ICMP Traceroute 
	- open cmd 
		- ``tracert 216.239.36.10``
 - TCP Traceroute
	- sudo tcptraceroute google.com
- UDP Traceroute
	- traceroute google.com 
### Traceroute Tools
Traceroute tools such as NetScanTools Pro, PingPlotter, Traceroute NG, and tracert are useful for extracting information about the geographical location of routers, servers, and IP devices in a network. Such tools help us to trace, identify, and monitor the network activity on a world map. Some of the features of these tools are as follows:
-  Hop-by-hop traceroutes 
- Reverse tracing 
- Historical analysis 
- Packet loss reporting 
- Reverse DNS
- Ping plotting 
- Port probing 
- Detect network problems 
- Performance metrics analysis 
- Network performance monitoring
### Tracking Email Communications
 Email tracking tools allow an attacker to collect information such as IP addresses, mail servers, and service providers involved in sending the email.
- email tracking tools include
	- IP2LOCATION’s Email Header Tracer
	-  MxToolbox
	-  eMailTrackerPro 
	- Holehe
	- DNS Checker Email Header Analyzer
	- Social Catfish.
## Footprinting through Social Engineering


## Automate Footprinting Tasks using Advanced Tools and AI
- using Footprint ing Tools like
	- Maltego 
	- Recon-ng 
		- recon/domains-hosts/brute_hosts to extract a list of hosts associated with the target URL.
	-  FOCA
	-  subfinder 
	- OSINT 
	- Recon-Dog
	-  BillCipher 
- Some additional footprinting tools are listed below: ▪
	- Sudomy (https://github.com) 
	- theHarvester (https://www.edge-security.com) 
	- whatweb (https://github.com) 
	- Raccoon (https://github.com) 
	- Orb (https://github.com) 
	- Web Check (https://web-check.xyz) 
	- OSINT.SH (https://osint.sh)

### AI-Powered OSINT Tools
- AI powered OSINT TOOLs such as 
	- Taranis AI
	- OSS Insight 
- Additional AI-Powered OSINT Tools
	- for google dorking 
		- DorkGenius
		- DorkGPT 
		- Google Word Sniper 
	- OSINT
		- Cylect.io 
		- Bardeen.ai
		- PenLink Cobwebs
	- PDF
		- ChatPDF 
	- Youtube
		-  Explore AI 
	- Web data scraper
		- AnyPicker 

### create and Run Custom Python Script to Automate Footprinting Tasks with AI  
- Example for prompt 
	- ``" "Develop a Python script which will accept the domain name www.microsoft.com as input and execute a series of website footprinting commands, including DNS lookups, WHOIS records retrieval, email enumeration, and more, to gather information about the target domain."``
- coustom made python script for domain recon 
- here  as ``python domain_recon.py -d hackerschool.in`` 

# Lab 1: Perform Footprinting Through Search Engines

## Task 1: Gather Information using Advanced Google Hacking Techniques
1. open Windows 11 and open browser 
2. search in search bar 
	- ``intitle:login site:eccouncil.org``
	- ``EC-Council filetype:pdf``
# Lab 2: Perform Footprinting Through Internet Research Services
## Task 1: Find the Company's Domains, Subdomains and Hosts using Netcraft and DNSdumpster
1. open in browser ``https://www.netcraft.com``
2. search for 
	- ``https://www.certifiedhacker.com``
	- look for need to look 
3. go to ``https://dnsdumpster.com/``
	- Search for ``certifiedhacker.com``
# Lab 3: Perform Footprinting Through Social Networking Sites
## Task 1: Gather Personal Information from Various Social Networking Sites using Sherlock
- open Parrot 
1. open terminal and run sherlock 
	- ``sherlock "Elon Musk"``
# Lab 4: Perform Whois Footprinting
## Task 1: Perform Whois Lookup using DomainTools

1. open windows 11 
2.  go to ``https://whois.domaintools.com``
	- search for ``www.certifiedhacker.com``
# Lab 5: Perform DNS Footprinting
## Task 1: Gather DNS Information using nslookup Command Line Utility and Online Tool
1. open  Windows 11 machine, launch  Command Prompt
	-  run ``nslookup ``command
	- ``set type=a``
	- target domain ``www.certifiedhacker.com``
2.  to obtain the domain's authoritative name server.
	- ``set type=cname``
	- `` certifiedhacker.com``
3.  to determine the IP address of the name server.
	- ``set type=a``
- online tool NSLOOKUP
1. open browser and go to ``http://www.kloth.net/services/nslookup.php``
	- **Domain:** field, enter ``www.certifiedhacker.com``
- You can also use DNS lookup tools such as **DNSdumpste**
# Lab 6: Perform Network Footprinting
## Task 1: Perform Network Tracerouting in Windows and Linux Machines
- open  Windows 11 and open the **Command Prompt** window. 
1. Run ``tracert www.certifiedhacker.com``
	- command to view the different options for the command
		- ``tracert /?``
2.  to perform the trace, but with only 5 maximum hops allowed.
	- ``tracert -h 5 www.certifiedhacker.com``
- switch to the **Parrot Security
1. Run  in Terminal ``traceroute www.certifiedhacker.com``
# Lab 7: Perform Email Footprinting
## Task 1: Gather Information about a Target by Tracing Emails using eMailTrackerPro
- open windows 11
1. cd ``**E:\CEH-Tools\CEHv13 Module 02 Footprinting and Reconnaissance\Email Tracking Tools\eMailTrackerPro**``
	- open ``emt.exe``




# Lab 8: Perform Footprinting using Various Footprinting Tools
refer [[Recon-ng]]
# Lab 9: Perform Footprinting using AI
## Task 1: Footprinting a Target using ShellGPT
- open parrot as sudo 
1. harvesting emails pertaining to a target organization.
	- ``sgpt --chat footprint --shell "Use theHarvester to gather email accounts associated with 'microsoft.com', limiting results to 200, and leveraging 'baidu' as a data source" ``
	- command 
		- ``theHarvester -d microsoft.com -1 200 -b baidu -f microsoft_emails.xml``
2. 
### References


Imp Sections 

| Google doeking                                   |     |
| ------------------------------------------------ | --- |
| search engines<br>image <br>video <br>meta date  |     |
| shodan                                           |     |
- [ ] make hands on for sublist3r 
	- python sublist3r.py -d google.com 
- [ ] make hands on for photon
    - run 
	    - `` sudo photon. py -u <URL of the Target Website> -1 3 -t 200 --wayback``
    - installing 
	    - ``sudo apt install python3-tld``


learn about Recon-ng
learn about DNSrecon  / DNSfootprinting 
learm about Traceroute

| manual tools |     |
| ------------ | --- |
| sublist3r    |     |
	banker code -59912 , alpha - 98763w