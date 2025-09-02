2024-12-20 16:35

Status:

Tags:

# Fingerprinting Web Application using Netcat, WhatWeb, and Wappalyzer

## **1. Introduction to Connection Establishment**

- **Purpose**: Establish a connection with a target web server to gather basic information.
- **Target**: `Microsoft.com`
- **Command**:
    
    bash
    
    Copy code
    
    `nc microsoft.com 80`
    
    - `nc` stands for **Netcat**.
    - `80` is the **HTTP port**.

---

## **2. Sending the HTTP Request**

- **Request Syntax**:
    
    Copy code
    
    `HEAD / HTTP/1.1`
    
    - **HEAD**: HTTP verb used to request headers without the body.
    - **/**: The root document (index file).
    - **HTTP/1.1**: HTTP version.
- **Key Steps**:
    
    - Press **Enter** twice to send the request.
    - **Response**: HTTP code `301` (redirect), but headers contain critical information.

### **Response Headers Analysis**

1. **Server Header**:
    
    - Indicates the web server software.
    - Example: `IIS version 8.5` (Microsoft Internet Information Services).
2. **Technology Used**:
    
    - Found in headers.
    - Example: `ASP.NET` (web application framework).

---

## **3. Fingerprinting with WhatWeb**

### **Tool Overview**

- **Purpose**: Fingerprints web applications to gather detailed information.
- **Installation**:
    
    bash
    
    Copy code
    
    `git clone <WhatWeb_Repo_URL>`
    
- **Usage**:
    - Run the tool without options to display the help manual:
        
        bash
        
        Copy code
        
        `whatweb`
        
    - **Basic Command**:
        
        bash
        
        Copy code
        
        `whatweb microsoft.com -v`
        
        - `-v`: Enables verbose output for more readable results.

### **WhatWeb Output Analysis**

1. **Summary**: Overview of results.
    
2. **Details**:
    
    - Confirms `ASP.NET` and `IIS version 8.5`.
    - Provides additional information like:
        - Country of the IP address.
        - Software versions.
3. **Handling Redirects**:
    
    - If the server responds with `301`:
        - WhatWeb **automatically follows redirects**.
        - Scans subsequent URLs (e.g., `www.microsoft.com`).
4. **Additional Insights**:
    
    - Detects specific versions of frameworks and servers.

---

## **4. Web Application Analysis with Wappalyzer**

### **Tool Overview**

- **Purpose**: Browser plugin that fingerprints web applications.
- **Installation**:
    - Install from the Wappalyzer website.
    - Enable the plugin in the browser.

### **Usage**

1. Navigate to the target domain (e.g., `Microsoft.com`).
2. Click the Wappalyzer icon in the browser toolbar.

### **Wappalyzer Output Analysis**

1. **Web Server**: Confirms `IIS 8.0`.
2. **Web Framework**: Confirms `ASP.NET V4`.
3. **Additional Frameworks**:
    - Detects frontend technologies like `jQuery`.
4. **Output Display**:
    - A pop-up provides organized and detailed information.

---

## **5. Key Takeaways**

- **Netcat**:
    - Establishes a raw HTTP connection.
    - Analyzes server headers to extract basic details.
- **WhatWeb**:
    - Performs advanced web application fingerprinting.
    - Handles redirections and detects multiple technologies.
- **Wappalyzer**:
    - Provides browser-based fingerprinting.
    - Identifies both server-side and client-side frameworks.
- **Information Collected**:
    - Web server type and version (`IIS`).
    - Framework used (`ASP.NET`).
    - Frontend technologies (`jQuery`).

**Next Steps**:

- Store gathered information using a **MindMap** tool for organized analysis.
- Use this data for deeper penetration testing.




### References
