2024-12-19 22:03

Status: done  

Tags:
###### CANVAS

[[(HACK THE BOX) Information Gathering.canvas|(HACK THE BOX) Information Gathering]]
****
# Information Gathering Techniques

## **Gathering Domain Information for Penetration Testing**

### **Tools and Methods Used** 

1. **(T)Whois**: Retrieves domain ownership and technical information.
2. **FreeMind**: A tool to organize and store collected data in a mind map.
3. **NSLookup**: Queries DNS records for more information.
4. **(T)Netcraft**: Provides additional domain insights and operating system details.

---
### **Steps for Information Gathering**

#### **Step 1: Initial Whois Data Retrieval**

- **Access Whois results** to collect key domain details:
    - **Registrar**: GoDaddy.com
    - Organization name (if available)
- **Data Organization**:
    - Open **FreeMind** to organize findings.
    - Primary node: `elsefoo.com`
    - Child nodes:
        - General information (Registrar, Organization, etc.)
        - Whois data: IP location and Autonomous System Number (ASN).

#### **Step 2: Organize Whois Data in FreeMind**

- Use **FreeMind’s child nodes** to segment data for clarity:
    - **Whois Node**: Store IP addresses, technical details.
    - **IP Node**:
        - Store IP address.
        - Store **NetBlock owner** (ownership of IP range).
- Data is progressively added into FreeMind to maintain an organized map.

---

#### **Step 3: DNS Record Information**

- DNS details retrieved include:
    - Name servers
    - MX (Mail Exchange) servers
    - Any other DNS records
- **NSLookup Command**:
    - Query MX records:
        
        bash
        
        Copy code
        
        `set query type=MX elsfoo.com`
        
    - Query all DNS records:
        
        python
        
        Copy code
        
        `set query type=Any`
        
- **Key Information Stored**:
    - MX Records (Email server addresses)
    - General DNS entries found in Whois or NSLookup.

---

#### **Step 4: Additional Tools – Netcraft**

- **Purpose**: Cross-check and retrieve further insights.
- **Process**:
    - Enter the target domain in the Netcraft tool.
    - Analyze the results:
        - Admin email address.
        - Web server information (e.g., IIS 7.5).
        - Operating system indicators (e.g., likely Windows OS).
- **Organize Data in FreeMind**:
    - Store admin contact details, OS, and web server insights.

---

### **Key Insights Gathered**

1. **Domain Registrar**: GoDaddy.com
2. **IP Information**:
    - IP addresses
    - NetBlock owner
3. **DNS Records**:
    - Name servers
    - MX records
4. **Server and OS Data**:
    - Web server type: IIS 7.5
    - Indications of a Windows operating system.
5. **Additional Data**:
    - Admin contact email (retrieved via Netcraft).




### References
