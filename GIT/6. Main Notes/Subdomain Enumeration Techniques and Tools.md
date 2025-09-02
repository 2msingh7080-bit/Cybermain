2024-12-20 16:23

Status:

Tags:


# **Subdomain Enumeration Techniques and Tools**

### **1. Manual Enumeration with Google Search**

- **Site Operator:** `site:*.cbs.com`
    - Displays results **only within the specified domain**.
    - Initially, the `www` subdomain is returned.
- **Excluding Subdomains:**
    - Modify the search query to exclude specific subdomains as follows:  
        `site:*.cbs.com -site:www.cbs.com`
    - This process helps discover new subdomains like `CBS News`, `Radio`, etc.
- **Iterative Process:**
    - Keep excluding discovered subdomains until **no more results** appear.
    - Use a text file or tools like FreeMind to track findings.

**Pros:** Simple method using basic search.  
**Cons:** Tedious and time-consuming.

---

### **2. Using Online Tools – Netcraft**

- **Tool:** Netcraft
- **Process:**
    - Visit Netcraft's site and input the target domain (e.g., `cbs.com`).
    - Quickly retrieves a list of subdomains.

**Pros:** Fast and user-friendly.  
**Cons:** Results are less exhaustive compared to Google search.

---

### **3. Automated Tools for Subdomain Enumeration**

#### **A. DNS-CNM**

- **Purpose:** Automates subdomain discovery via Google search.
- **Key Options:**
    - `-p 20`: Analyzes the first 20 pages of Google results.
    - `-S 100`: Limits results to 100 subdomains.
    - `--threads 5`: Speeds up the process using multiple threads.
- **Command Syntax:**
    
    bash
    
    Copy code
    
    `dnsenum -p 20 -S 100 --threads 5 cbs.com`
    
- **Output:** Displays subdomains and additional information efficiently.

---

#### **B. SubBrute**

- **Purpose:** Uses a **word list** for brute-force subdomain enumeration.
- **Setup:** Requires downloading from GitHub.
- **Default Word List:** `names.txt` (pre-included).
- **Command Syntax:**
    
    bash
    
    Copy code
    
    `subbrute cbs.com`
    
- **Output Options:**
    - Results can be saved in **grepable** or **JSON** formats.

**Note:** SubBrute can be stopped anytime with `Ctrl + C`.

---

### **Key Takeaways**

- **Manual Approach:** Use Google search with iterative exclusions.
- **Netcraft:** A fast starting point but limited results.
- **Automated Tools:**
    - **DNS-CNM:** Automates Google search with options for speed and result limits.
    - **SubBrute:** Brute-force tool that uses word lists.

**Best Practice:**  
Always document findings systematically in a file, spreadsheet, or database for reference during penetration tests.



### References
