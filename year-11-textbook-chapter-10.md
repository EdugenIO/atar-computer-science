# Unit 2 — Chapter 10: Ethics, Law & Security Frameworks

This chapter introduces the fundamental concepts of cybersecurity ethics, legislation, and organizational security models. In **Unit 2**, the curriculum transitions from coding standalone computer programs to understanding how databases store massive amounts of personal information, and how we must legally, ethically, and structurally protect that data.

You will explore the distinction between ethical and unethical hacking, analyze how the **Privacy Act 1988** and the **Australian Privacy Principles (APPs)** govern software development, and master two key security models: the **CIA Triad** (Confidentiality, Integrity, Availability) and the **AAA Framework** (Authentication, Authorisation, Accounting). 

These models are heavily assessed in SCSA theory examinations and form the administrative core of **SCSA School-Based Assessment Task 6 (The Relational Database Project)**.

---

## Lesson 10.1: Ethical Hacking vs Unethical Hacking

### Your Goal
Distinguish between and evaluate the legal, ethical, and operational differences between ethical (white hat) hacking and unethical (black hat) hacking.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 8.3: Ethical & Legal Software Development](./year-11-textbook-chapter-8.md#lesson-83-ethical--legal-software-development) (IP and licensing concepts).
*   [Lesson 9.1: DoD TCP/IP Model and Protocols](./year-11-textbook-chapter-9.md#lesson-91-dod-tcpip-model-and-protocols).

### The Idea
In cybersecurity, the technical skills used to find a flaw in a system are identical regardless of whether they are deployed for good or bad. What separates an ethical computer professional from a cybercriminal is not *what* tools they use, but **authorization** and **intent**.

**The Analogy:**
Imagine a professional building safety inspector hired by a bank. At midnight, they walk around the building, physically checking windows and doors. They find an unlocked window on the ground floor. 
*   **The Ethical Inspector:** Immediately notes down the unlocked window in their official clipboard. They do not climb inside. The next morning, they deliver a secure report to the bank manager, detailing the vulnerability so it can be fixed.
*   **The Burglar:** Finds the same unlocked window. They climb through, bypass the security sensors, and steal cash from the registers for personal profit.

In computer systems, we define these two roles using standard security terminology:
1.  **Ethical Hacker (White Hat):** A security professional who has explicit, written, and prior authorization to probe a network or system for weaknesses. Their intent is to report vulnerabilities back to the owner so they can be patched before malicious actors exploit them.
2.  **Unethical Hacker (Black Hat):** A malicious actor who attempts to bypass security controls without authorization. Their intent is personal gain, data theft, disruption of service, or extortion.

#### **SCSA Key Terms**
*   **Ethical Hacking:** Probing computer systems, networks, or applications with explicit permission to identify vulnerabilities, assess security risks, and implement defensive fixes.
*   **Penetration Testing (Pen Testing):** A structured, authorized security exercise where a professional simulates a cyberattack against an organization's infrastructure to evaluate its defenses.
*   **Vulnerability Scanning:** An automated, high-level scan of a network or system to detect known software weaknesses, unpatched ports, or default configurations.
*   **Scope of Work (SOW):** A legally binding document defining the exact systems, IP addresses, and hours within which a penetration tester is authorized to operate.
*   **Written Authorization:** The prior legal sign-off from a company's executive or system owner. This is the **absolute legal line** dividing legitimate research from criminal prosecution under the *Cybercrime Act 2001* (Cth).

---

### See It Worked
#### **The Scenario**
While testing a new registration system for the **WA Junior Sports Carnival**, a year-11 student developer notices that modifying the athlete ID number in the browser URL from `http://10.0.0.5/athlete?id=12` to `id=13` displays another student’s private registration page. 

Let's compare the ethical reporting path versus the unethical exploit path:

```
                  [ VULNERABILITY DISCOVERED ]
                     (Insecure Athlete URL)
                               |
            +------------------+------------------+
            |                                     |
     [ ETHICAL PATH ]                      [ UNETHICAL PATH ]
- Do not access other IDs.            - Scrape data for all IDs.
- Document the URL pattern.           - Post private emails online.
- Draft a secure, private report.     - Alter race times for friends.
- Deliver report to Committee.        - Demand payment to hide bug.
            |                                     |
[ OUTCOME: Patch applied;            [ OUTCOME: System compromised;
  Database secured; no harm done. ]    Police notified; SCSA expulsion. ]
```

#### **How the Logic Flows**
*   **The Ethical Path:** The student stops testing the moment they discover the vulnerability. They do not proceed to look at student 14, 15, or 16, as doing so would exceed the minimum necessary testing steps. They document the steps to reproduce the bug, write a private email to the carnival administrator, and offer a simple remediation step (such as server-side authentication checking on the athlete session).
*   **The Unethical Path:** The student writes a script to auto-generate URLs from ID 1 to 1200, downloads everyone's emergency phone numbers, edits their teammate's 100m sprint time to 9.5 seconds, and demands free lunch from the school sports coordinator to show them the flaw.

---

### Try It with Help
#### **The Problem**
A local West Australian IT business, *Swan Security Ltd*, has been hired by a Perth regional hospital to perform an authorized external network vulnerability assessment. The hospital's network manager signs a Scope of Work (SOW) permitting *Swan Security* to scan the domain range `192.168.10.0/24` on weekends between 8 PM and 4 AM.

During the scan, the security analyst notices that an unlisted backup server hosting database files at IP address `192.168.20.45` (which is outside their SOW) is wide open.

Evaluate the actions the security analyst should take next.

#### **Structural Hints**
1.  **Check the Scope:** Does the unlisted server fall inside the agreed range of `192.168.10.0/24`? (Recall that a subnet mask `/24` limits operations to IP range `192.168.10.1` through `192.168.10.254`).
2.  **Define the Risk:** Probing the unlisted IP without permission, even with good intentions, violates federal cyber crime laws (e.g., unauthorized access to computer material).
3.  **Propose the Solution:** State how the analyst should report this discovery without running active scans against that external server.

#### **Scaffolded Student Guide**
*   Step 1: Identify that IP `192.168.20.45` is **outside the scope of work**.
*   Step 2: Acknowledge that running a scan on `192.168.20.45` without written authorization constitutes **unethical/illegal hacking**.
*   Step 3: Draft an advisory note to the client detailing that an out-of-scope system was noted and request an **amendment to the SOW** to legally authorize testing on that IP.

---

### Try It Yourself
#### **The Problem**
Two computer science students, Mark and Sarah, discover an unpatched vulnerability in their school's library portal that allows any student to view other users' borrowing histories. 
*   **Mark** decides to write an automated script to download the entire list of checkouts to prove the bug exists, and then prints out a list of the principal's borrowed books to show his friends.
*   **Sarah** takes a screenshot of her own borrowing page displaying a mock error, immediately logs out, drafts a private email outlining the technical steps of the vulnerability, and sends it directly to the school's IT support team.

Write an evaluation (approx. 150 words) comparing the actions of Mark and Sarah. Justify which student acted as an ethical hacker and which acted unethically, referencing **prior written authorization** and **intent**.

---

### Check Your Reasoning
#### **The Answer**
An expert response must highlight the following core elements:

1.  **Sarah acted ethically (White Hat approach):**
    *   **Authorization:** She did not have prior written authorization to perform general testing, but her actions upon discovering the bug were safe and contained. She minimized data exposure by taking a screenshot of *only her own data* rather than probing others.
    *   **Intent:** Her intent was purely defensive. She immediately exited the system and reported the flaw through a confidential, private channel (the school's IT support) to enable them to patch it before any breach could occur.
2.  **Mark acted unethically (Black Hat approach):**
    *   **Authorization:** He had no authorization to run automated scripts or access records beyond his own user profile.
    *   **Intent:** His intent was malicious and exhibitionist. By scraping the entire database and sharing the principal's private borrowing history with friends, he violated user privacy laws, exceeded minimum necessary demonstration of a bug, and actively compromised personal data. His actions constitute unauthorized access under Australian law.

#### **Common SCSA Student Errors**
*   **"Good intentions equal ethical hacking":** Claiming Mark was ethical because he did it to "prove the bug existed" is a fatal exam mistake. Proving a bug does *not* require stealing real user data or publicizing confidential info.
*   **Confusing scanning with hacking:** Believing that merely scanning a system is always legal. Any unauthorized scanning or diagnostic probing is legally actionable if it does not have signed authorization.

---

### Review and Connect
In this lesson, you learned that ethical hacking requires explicit written authorization and is conducted entirely to improve a system's defense. In the next lesson, we will examine the specific Australian legislation—the **Privacy Act 1988**—that forces WA organizations to take these security duties seriously.

---

## Lesson 10.2: Privacy Act 1988 & Australian Privacy Principles (APPs)

### Your Goal
Apply the **Privacy Act 1988** and the **Australian Privacy Principles (APPs)** to the design, execution, and security management of relational databases storing personal student and customer data.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.4: Fundamental Data Types](./year-11-textbook-chapter-1.md#lesson-14-fundamental-data-types) (representing personal fields as strings and numbers).
*   The general concept of a flat-file database vs. a relational system.

### The Idea
When we design databases to manage users, we aren't just storing abstract bytes; we are holding people's real lives, contact details, medical histories, and security credentials in trust. In Australia, this trust is not merely a moral guideline—it is heavily regulated by federal law.

#### **The Legislation: Privacy Act 1988 (Cth)**
The **Privacy Act 1988** is the primary federal law regulating how Australian government agencies and private businesses with an annual turnover of more than $3 million (along with all private health service providers and businesses trading in personal information) handle personal information. 

#### **The Framework: Australian Privacy Principles (APPs)**
The Privacy Act contains **13 Australian Privacy Principles (APPs)** which dictate the standards for collecting, using, disclosing, securing, and giving individuals access to their personal information.

As database developers and network designers, we must build systems that conform to these principles. The most critical principle for computer science is **APP 11: Security of personal information**.

**The Analogy:**
Imagine you run a physical locker service. 
*   If you let customers store their valuables, but you leave the lockers completely unlocked in a public hallway, you are responsible if they get stolen.
*   If you demand that customers show their birth certificates, passports, and dental records just to store an umbrella for an hour, you are violating principles of proportionality.

In a database system, this translates to:
1.  **Data Minimization:** Only collect personal fields that are strictly necessary for your software's functional scope (e.g., a sports timer does not need to collect an athlete's home address or credit card details).
2.  **Robust Protection (APP 11):** You must take active, reasonable steps to protect stored personal information from misuse, loss, unauthorized modification, or breach (e.g., using passwords, encryption, and secure network hosting).

#### **SCSA Key Terms**
*   **Privacy Act 1988:** The federal Australian legislation that establishes the legal framework for privacy and data protection.
*   **Australian Privacy Principles (APPs):** A set of 13 legally binding rules governing the collection, management, use, and security of personal data.
*   **Personally Identifiable Information (PII):** Any data that can be used to identify, contact, or locate a specific individual (e.g., full name, phone number, email address, physical address, date of birth).
*   **Sensitive Data:** A subset of personal information that requires higher security controls under the APPs, including health records, religious beliefs, criminal records, or biometric data.
*   **APP 11 (Security of personal information):** The principle stating that an entity must take active steps to protect data from misuse, interference, loss, unauthorized access, modification, or disclosure, and destroy/de-identify data when it is no longer required.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival committee designs an online registration table. The initial draft structure of their `athlete_registration` table includes the following fields:

| Field Name | Data Type | Reason for Collection | SCSA Assessment (APP Compliance) |
| :--- | :--- | :--- | :--- |
| `athlete_id` | `INTEGER` | Primary key identifier | **Compliant**: Essential relational identifier. |
| `full_name` | `TEXT` | Athlete identification | **Compliant**: Essential personal information. |
| `emergency_phone` | `TEXT` | Medical emergency contact | **Compliant**: Essential safety requirement. |
| `dietary_requirements`| `TEXT` | Lunch catering preparation | **Compliant**: Relevant, but contains Sensitive (Health) Info. Requires strict user consent and access controls. |
| `parents_credit_card` | `TEXT` | Event entry payment fee | **Non-Compliant**: Extreme risk. The card should be processed live via an external secure gateway and *never* stored permanently in the local database. |
| `parents_annual_income`| `INTEGER`| Demographic data collection | **Non-Compliant (Violation of Data Minimization)**: Excess collection. Annual income is completely irrelevant to running a sports race. |

#### **How the Design is Remedied**
To align with the **Privacy Act 1988**:
1.  **De-identify or Destroy:** The `parents_annual_income` field is deleted entirely from the schema.
2.  **Live Payment Integration:** The `parents_credit_card` field is removed. Payment is routed through an encrypted API, ensuring the local server never stores or writes sensitive credit card numbers to disk.
3.  **Encrypted Sensitive Storage:** The `dietary_requirements` database column is encrypted, and access is restricted only to catering administrators.

---

### Try It with Help
#### **The Problem**
A private WA sports academy designed an app to manage student physical training logs. The database stores athlete names, email addresses, phone numbers, and physical health assessments (Sensitive Data). Due to a server misconfiguration, the database backups folder on their web server was left with "Directory Listing" enabled, allowing any external browser to view and download raw SQL database dumps.

Analyse this incident in relation to the **Privacy Act 1988** and the **Australian Privacy Principles**.

#### **Structural Hints**
*   **Identify the PII & Sensitive Data:** Name what personal data was exposed.
*   **Identify the Violated Principle:** Which specific APP deals with securing information from unauthorized access, loss, or disclosure? (Hint: Review **APP 11**).
*   **Detail the Consequences:** What must the business do now under the Australian *Notifiable Data Breaches (NDB)* scheme if this data was accessed by malicious actors?

#### **Scaffolded Student Guide**
*   Step 1: Point out that names and contact details are **PII**, and fitness assessments are **Sensitive Health Data**.
*   Step 2: Explicitly state that leaving the SQL backup folder open to the public directly violates **APP 11 (Security of Personal Information)** because the academy failed to take "reasonable steps" to secure the data.
*   Step 3: Note that because sensitive health data was exposed, this constitutes an **Eligible Data Breach** under Australian law, legally requiring the academy to notify the Office of the Australian Information Commissioner (OAIC) and all affected athletes.

---

### Try It Yourself
#### **The Problem**
The **WA Junior Sports Carnival** plans to launch a mobile smartphone app that tracks athlete positions around the athletics park using GPS telemetry. The coordinator wants to collect and log:
*   Real-time GPS coordinates of each student every 10 seconds.
*   The student's full name, school, date of birth, and home address.
*   The parent's email address and password.

The coordinator plans to keep this data stored on a local office PC in an unencrypted CSV flat file so they can look at trends next year.

Write a formal privacy assessment brief (approx. 200 words) advising the coordinator of the legal risks of this app under **APP 11** and the **Privacy Act 1988**. Propose three concrete technical improvements to make the system legally compliant.

---

### Check Your Reasoning
#### **The Answer**
An expert response must address the following legal and technical points:

1.  **Legal Violations & Risks:**
    *   **Data Over-Collection & Minimization:** Storing home addresses and continuous 10-second GPS tracking data on minors constitutes a major privacy risk and violates data minimization standards. This tracking is not strictly necessary to run standard running races.
    *   **APP 11 Violation (Lack of Security):** Storing PII (names, DOB, GPS logs) in an *unencrypted CSV file on a local office PC* represents a failure to take "reasonable steps" to protect data. A local office computer lacks firewalls, access logs, physical entry locks, and database encryption.
2.  **Proposed Improvements for Compliance:**
    *   **Data Minimization:** Delete the "home address" field entirely and restrict GPS tracking to active race boundaries rather than general park-wide tracking.
    *   **Secure Infrastructure (RDBMS over CSV):** Transition the data from an unencrypted CSV flat file to a relational database with access controls, forcing users to authenticate to view records.
    *   **Security Controls (APP 11 alignment):** Encrypt the database at rest and in transit. Set up automatic data destruction protocols to purge precise GPS tracking tables within 30 days of the carnival's conclusion.

#### **Common SCSA Student Errors**
*   **Ignoring the age factor:** Forgetting that athletes in school carnivals are minors (under 18). Collecting GPS data on minors without explicit parent consent is an severe ethical and legal violation.
*   **Vague technical recommendations:** Writing generic statements like "make it secure" or "install an antivirus". SCSA examiners expect specific database actions like: "transition to a relational database with role-based access controls and apply cryptographic hashing to user passwords."

---

### Review and Connect
In this lesson, you explored how the Privacy Act 1988 and the APPs govern database design. In the next lesson, we will learn about the **CIA Triad**, which provides us with a structured logical model to analyze these security threats systematically.

---

## Lesson 10.3: The CIA Triad of Security Analysis

### Your Goal
Use the **CIA Triad model of security analysis** to evaluate system security profiles, diagnose cyber security incidents, and design balanced defense strategies.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 9.2: Physical Media & Hardware](./year-11-textbook-chapter-9.md#lesson-92-physical-media--hardware) (specifically firewalls and switches).
*   [Lesson 10.2: Privacy Act 1988 & APPs](./year-11-textbook-chapter-10.2).

### The Idea
When computer scientists assess the security of a computer network or database system, they don't just ask, "Is it secure?" Security is multi-dimensional. To systematically evaluate risks, we use a gold-standard framework known as the **CIA Triad**.

The CIA Triad breaks security down into three complementary, independent objectives: **Confidentiality**, **Integrity**, and **Availability**.

```
                [ THE CIA TRIAD ]
                       /                      /                       /                        /                         /________ [CONFIDENTIALITY]            [AVAILABILITY]
   Authorized access           System uptime &
   only (Encryption)           redundancy (Backups)
                   \          /
                    \        /
                     \      /
                      \    /
                       \  /
                        \/
                   [INTEGRITY]
                 Data accuracy &
                no illegal changes
```

1.  **Confidentiality:** Preventing unauthorized disclosure of information. Ensuring that only those with legitimate authorization can read or access the data.
2.  **Integrity:** Ensuring that data is accurate, complete, and protected against unauthorized or accidental modification. Data must not be altered in transit or in storage.
3.  **Availability:** Ensuring that authorized users have reliable, timely access to systems, networks, and data when they need it.

**The Analogy:**
Imagine an emergency medical box in a school gym:
*   **Confidentiality:** The box is locked so curious students cannot open it and read other students’ medical files.
*   **Integrity:** The seals on the bandages are intact, and the medicine labels have not been swapped or tampered with.
*   **Availability:** The physical education teacher has the key in their pocket at all times, meaning the box can be accessed instantly if a child is injured.

If any one of these three elements is broken, the entire security posture of the system fails.

#### **SCSA Key Terms**
*   **CIA Triad:** A foundational cybersecurity model used to guide policies and analyze security threats across three components: Confidentiality, Integrity, and Availability.
*   **Confidentiality:** The security objective of preventing unauthorized access to sensitive information (e.g., solved via encryption, passwords, and multi-factor authentication).
*   **Integrity:** The security objective of ensuring information remains unaltered, authentic, and reliable (e.g., solved via hashing, file permissions, and database transaction controls).
*   **Availability:** The security objective of ensuring systems and data are operational and accessible to authorized users when needed (e.g., solved via hardware redundancy, daily backups, and UPS battery systems).

---

### See It Worked
#### **The Scenario**
The **WA Junior Sports Carnival** database server experiences a series of security events during the track finals. Let's analyze how each incident maps to a failure of one specific pillar of the CIA Triad:

| Security Incident | Core CIA Pillar Broken | Reason for Classification | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| **Incident A:** A power surge at the sports field pavilion shuts down the main database server, preventing marshals from reading the lanes list for the 400m final. | **Availability** | The system was functional and secure, but authorized users could not access the data when needed due to server offline status. | Install an Uninterruptible Power Supply (UPS) battery backup in the server rack. |
| **Incident B:** A student intercepts the network packets of the public display monitor and modifies the 100m sprint record time from `11.2` seconds to `9.1` seconds. | **Integrity** | The data was modified in transit by an unauthorized person, compromising the truth and reliability of the score. | Implement network packet encryption (HTTPS/TLS) and apply file write permissions. |
| **Incident C:** An administrator leaves their laptop unlocked at the recording desk. A spectator reads the medical records and contact numbers of two athletes. | **Confidentiality** | Sensitive, private information was exposed to an unauthorized individual. | Configure automatic screensaver lock policies (e.g., lock after 2 minutes of idle time). |

---

### Try It with Help
#### **The Problem**
A malicious actor launches a **Denial of Service (DoS)** attack against a Perth high school’s student portal by flooding the web server with 50,000 automated connections per second. This causes the server’s CPU usage to hit 100%, and legitimate parents attempting to log in to sign permission slips receive a "504 Gateway Timeout" error page.

Identify which component of the CIA Triad has been compromised by this attack, and propose a network-level defense strategy.

#### **Structural Hints**
*   **Read the Symptoms:** Is the student data being read by unauthorized people (Confidentiality issue)? Is the database being edited with fake information (Integrity issue)? Or is the system simply crashing and refusing connection to legitimate users?
*   **Map to CIA:** Based on your assessment, name the primary broken pillar.
*   **Propose a Solution:** Review network defensive devices. What hardware device can intercept and filter out malicious traffic before it reaches the web server? (Hint: Review firewalls).

#### **Scaffolded Student Guide**
*   Step 1: State that because the parents are blocked from logging in, **Availability** is the pillar that is compromised.
*   Step 2: Explain that the DoS attack floods the connection bandwidth, rendering the system *unavailable* to authorized actors.
*   Step 3: Recommend deploying a network **Firewall** configured with *rate limiting* and integrating a Content Delivery Network (CDN) to filter out traffic flood vectors.

---

### Try It Yourself
#### **The Problem**
As part of their end-of-year review, the sports carnival committee decides to evaluate three distinct security measures they want to deploy on their SQL database system:
1.  **Implementing Daily Database Backups:** Storing encrypted SQL dumps on a secure offsite cloud storage server.
2.  **Using Secure Hash Algorithms (SHA-256):** Hashing all administrator and coordinator passwords stored in the user login table.
3.  **Generating Checksums (MD5/SHA-1) for Data Files:** Creating logical file hashes of the registration tables before transferring them between ovals.

Draft a concise technical review matrix (in markdown table format) mapping each of these three security measures to its primary CIA Triad component. Write a brief sentence for each, justifying your mapping.

---

### Check Your Reasoning
#### **The Answer**
Your response should match this structured analysis:

| Proposed Measure | Primary CIA Component | Rationale and Justification |
| :--- | :--- | :--- |
| **1. Daily Database Backups** | **Availability** | Backups ensure that if the primary local database is destroyed by physical fire, hardware crash, or ransomware, the data can be quickly restored, maintaining system *availability*. |
| **2. Secure Hash Algorithms (SHA-256)** | **Confidentiality** | Hashing passwords ensures that if the database is leaked, the plain-text passwords remain unreadable to hackers, protecting administrator account access and credential privacy. |
| **3. Generating Checksums (MD5/SHA-1)** | **Integrity** | Checksums allow the receiving system to verify that no bytes were altered or corrupted during file transfer. If the calculated checksum doesn't match the source, *integrity* has been broken. |

#### **Common SCSA Student Errors**
*   **Conflating Backup with Confidentiality:** Students often argue backups are for "confidentiality" because they are encrypted. While encryption helps, the *primary operational purpose* of a backup is to recover from data loss, which directly serves **Availability**.
*   **Using "Integrity" to mean "Honesty":** Defining Integrity as "being a good developer". In the CIA Triad, Integrity has a precise technical definition: **the prevention of unauthorized modification of data.**

---

### Review and Connect
You have mastered the CIA Triad, the core security analysis model. In the next lesson, we will explore the **AAA Security Framework**, which defines the technical sequence required to enforce Confidentiality and Integrity during real-time system access.

---

## Lesson 10.4: The AAA Security Framework

### Your Goal
Analyze, implement, and audit system security profiles using the three pillars of the **AAA Security Framework**: **Authentication**, **Authorisation**, and **Accounting**.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 2.2: Selection (if/else)](./year-11-textbook-chapter-2.md#lesson-22-selection-if-else) (coding logical gates).
*   [Lesson 10.3: The CIA Triad model](./year-11-textbook-chapter-10.3).

### The Idea
How does a computer system physically enforce the goals of the CIA Triad when a user attempts to log in? We deploy a structured operational sequence known as the **AAA Security Framework** (pronounced "Triple-A").

The AAA Framework consists of three sequential steps:

```
[ USER ACCESS ATTEMPT ] ---> (1) AUTHENTICATION ---> (2) AUTHORISATION ---> (3) ACCOUNTING
                               Who are you?         What can you do?       What did you do?
                             (Password/2FA)         (User Permissions)       (Log Files)
```

1.  **Authentication:** Verifying the identity of the user attempting to access the system. It answers the question: *"Who are you, and can you prove it?"*
2.  **Authorisation:** Granting specific access levels, file permissions, and operational rights to an authenticated user. It answers the question: *"What are you allowed to do in this system?"*
3.  **Accounting:** Tracking and logging the actions, data modifications, and transactions performed by the user. It answers the question: *"What did you do while you were in the system?"*

**The Analogy:**
Imagine checking in to stay at a secure resort hotel:
*   **Authentication:** You stand at the lobby desk and present your physical driver’s license or passport to the clerk to prove you are the person who booked the room.
*   **Authorisation:** The clerk hands you a plastic keycard. This keycard is programmed to open only your room door (Room 302) and the public gym. It will *not* open the manager's office or other guests' rooms.
*   **Accounting:** When you tap your keycard to enter the gym at 11:15 PM, or charge a drink to your room at the pool bar, the hotel’s central server logs the exact time, location, and charge under your booking record.

In a database application, this process must be executed programmatically for every single user session.

#### **SCSA Key Terms**
*   **AAA Security Framework:** A foundational cybersecurity access control framework composed of Authentication, Authorisation, and Accounting.
*   **Authentication:** The process of validating a user's claimed identity (e.g., using passwords, SMS 2FA codes, smart cards, or fingerprints).
*   **Authorisation:** The process of determining what system objects, files, database tables, or commands an authenticated user has rights to access (e.g., Read, Write, Execute).
*   **Accounting:** The process of recording and tracking user activities, logins, file modifications, and session durations in secure, un-editable audit files (Log Files).
*   **Principle of Least Privilege (PoLP):** A core security practice where users are given the *minimum* level of authorization necessary to perform their specific job function, preventing accidental or malicious damage.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival uses an SQLite relational database with web access. The system must accommodate three distinct user roles:
1.  **Spectators (Parents):** Can only view published race times.
2.  **Marshals (Teachers):** Can view athlete names and insert/update race times.
3.  **Database Administrator (DBA):** Has full control over tables, backups, and user settings.

Let's see how the AAA framework is implemented and audited:

#### **Step 1: Authentication (Checking Identity)**
A user enters their username `j_smith_marshal` and password. The server checks the secure database hash. To strengthen authentication, the server requests a 6-digit Multi-Factor Authentication (MFA) token sent to J. Smith’s verified phone number.
*   *Outcome:* Identity verified. J. Smith is authenticated as a valid "Marshal" account.

#### **Step 2: Authorisation (Checking Rights)**
Authenticated J. Smith attempts to run an SQL command to drop the table: `DROP TABLE athlete_registration;`.
The database engine intercepts the query and references J. Smith’s role profile in the access control list:

```python
# Conceptual user access control check
user_role = "Marshal"
authorized_commands = ["SELECT", "INSERT", "UPDATE"]

attempted_command = "DROP TABLE"

if attempted_command in authorized_commands:
    # Execute command
    pass
else:
    print("Access Denied: 403 Forbidden. User not authorized to drop tables.")
```
*   *Outcome:* Query blocked. J. Smith is only *authorized* to run SELECT, INSERT, and UPDATE queries. They cannot execute administration commands.

#### **Step 3: Accounting (Audit Logging)**
The system automatically appends the event to a secure system text file (`audit.log`) on the server disk:

```
[2026-09-06 09:14:22] [AUTHENTICATE] User 'j_smith_marshal' successfully logged in from IP 10.0.0.12 (MFA verified)
[2026-09-06 09:15:04] [UPDATE] User 'j_smith_marshal' modified athlete 105: set 'sprint_100m' = '11.42s'
[2026-09-06 09:16:30] [REJECTED_DROP] User 'j_smith_marshal' attempted 'DROP TABLE athlete_registration' from IP 10.0.0.12. Action Blocked (Unauthorized).
```
*   *Outcome:* The event is permanently logged. Security teams can review this file later to catch malicious activity or system misuse.

---

### Try It with Help
#### **The Problem**
An employee at a WA sports medicine clinic logs in using their credentials and edits a patient’s health record. A week later, the patient complains that their medical data was modified incorrectly. The clinic director opens the server console but discovers that the audit log system was disabled to save disk space.

Evaluate this security failure using the **AAA Framework**.

#### **Structural Hints**
*   **Check Step 1 (Authentication):** Was the employee's identity verified? (Yes, they logged in with credentials).
*   **Check Step 2 (Authorisation):** Was the employee permitted to edit records? (Yes, as medical clinic staff, they have read/write rights).
*   **Check Step 3 (Accounting):** Can the clinic prove *which* specific employee made the incorrect change? Why or why not? Which component of AAA has failed?

#### **Scaffolded Student Guide**
*   Step 1: State that **Authentication** and **Authorisation** functioned correctly.
*   Step 2: Identify that **Accounting** failed completely because the audit log was turned off.
*   Step 3: Conclude that without accounting, there is no *non-repudiation*—the clinic cannot trace the data modifications back to a specific individual, making security auditing impossible.

---

### Try It Yourself
#### **The Problem**
During an audit of the WA Junior Sports Carnival's score-recording portal, the school IT administrator discovers the following vulnerabilities:
1.  All teachers and student marshals share a single, public username (`carnival_staff`) and a blank password to record sprint times on ovals.
2.  Once logged in, any marshal account can access the server control console and delete database tables.
3.  The system writes all events to an audit file, but this file is stored in a public, shared folder that any logged-in user can edit or clear.

Explain how this system violates all three pillars of the **AAA Security Framework**. Propose three specific structural remedies to align the portal with professional AAA standards.

---

### Check Your Reasoning
#### **The Answer**
Your auditing report should contain the following direct mappings:

1.  **Pillar Violations:**
    *   **Authentication Failure:** Sharing a single username (`carnival_staff`) with no password makes authentication useless. It is impossible to prove the true identity of the physical person sitting at the keyboard.
    *   **Authorisation Failure:** Allowing standard track-marshal accounts to access the admin console and delete tables violates the **Principle of Least Privilege**. Marshals do not require structural database modification rights to enter race times.
    *   **Accounting Failure:** Although log files are written, storing the audit log in a *publicly editable folder* invalidates accounting integrity. A rogue user could easily modify the log file to erase evidence of their actions, breaking the reliability of the audit trail.
2.  **Proposed Remedies:**
    *   **Authentication Remedy:** Require unique, individual user accounts for all staff (e.g., `j_doe_marshal`) with strict password complexity requirements (minimum 8 characters, numbers, and symbols).
    *   **Authorisation Remedy:** Implement Role-Based Access Control (RBAC). Restrict the `carnival_staff` role to `INSERT` and `UPDATE` permissions on the timing tables, blocking administrative commands.
    *   **Accounting Remedy:** Move the system audit logs to a secure, write-once, read-many (WORM) directory. Strip standard users of write/delete permissions on the log folder, ensuring logs can only be read by head systems administrators.

#### **Common SCSA Student Errors**
*   **Confusing Authentication and Authorisation:** Forgetting that *proving who you are* (entering your individual password) must happen *before* the system determines *what you can do* (blocking you from dropping tables). Keep these steps distinct.
*   **Weak Accounting remedies:** Recommending "reminding staff to log out" instead of secure, server-controlled write-restrictions on audit files.

---

## Chapter 10: Teacher Support & Exam Module

### **SCSA Syllabus Mapping**
This chapter directly supports and covers the following SCSA Year 11 Computer Science ATAR curriculum points:
*   **Unit 2, Area 1: Systems Analysis (Cyber Security)**
    *   *Role of ethical hacking in network security: purpose (improving security), penetration testing, comparison with unethical hacking.*
    *   *Role of the Privacy Act 1988; the concept of the Australian privacy principles; APPs in relation to keeping data secure.*
    *   *The CIA Triad model of security analysis: Confidentiality, Integrity, Availability; use the CIA Triad to analyse security threats and incidents.*
    *   *The AAA framework for securing systems: Authentication, Authorisation, Accounting; use the AAA framework for security analysis and auditing.*

### **Prerequisite Diagnostics**
Before teaching this module, ensure students have completed:
1.  **Chapter 8 (Software Process)** – Specifically licensing and Australian copyright laws.
2.  **Chapter 9 (Networking)** – To understand how IP addressing, firewalls, and ports establish basic traffic flow.

### **WA Classroom Discussion Starters**
1.  **The Ethics of Bug Hunting:** "If a WA student finds a security loophole in the Transperth smart-rider ticketing system, under what conditions is it legal for them to test it? What are the consequences of reporting it on social media vs. notifying Transperth privately?"
2.  **The Privacy Trade-off:** "As schools increasingly deploy biometric scanners (like fingerprints for library book borrowing or canteen payments), how do the APPs govern how this sensitive biometric data is secured, stored, and eventually destroyed?"

### **Misconception Busters**
*   **Misconception A (Hacking is Hacking):** Many students believe that any hacking is illegal. Teachers must emphasize that **written, prior, and explicit authorization** signed by the asset owner is the absolute shield against criminal prosecution. Without it, even "helping" a business find a bug is a punishable offense.
*   **Misconception B (MFA is Authorization):** Students often write that MFA is "authorization" because it "authorizes access". This is incorrect. MFA is an **Authentication** control (proving who you are). **Authorisation** only happens *after* you pass authentication, determining which files you can read or edit.
*   **Misconception C (Privacy Act covers everyone):** Some students assume the Privacy Act 1988 applies to every single individual and small hobby blog in WA. Clarify that it primarily covers government agencies, medical providers, and businesses with an annual turnover exceeding $3 million (though all developers should strive for compliance).

---

### **Ready-to-Print Classroom Assessment**
**Time Allowed: 25 minutes | Total Marks: 20**

#### **Question 1: Short Answer (Ethics and Law) [4 Marks]**
The WA Junior Sports Carnival committee wants to hire a former student to scan their database for vulnerabilities.
1.  Explain the primary difference between **ethical hacking** and **unethical hacking** in this scenario. [2 Marks]
2.  State the name of the primary Australian legislation that governs how the committee must secure and handle athlete personal information. [1 Mark]
3.  Which specific Australian Privacy Principle (APP) governs the protection of personal data from misuse or loss? [1 Mark]

#### **Question 2: Case Study (CIA Triad) [6 Marks]**
During the junior athletic finals, a rogue student plugs a physical device into the timing pavilion switch and triggers a script that floods the local intranet with garbage data, crashing the central scoreboard database. At the same time, the script copies the ovals' master check-in files to an external cloud server.
1.  Using the **CIA Triad**, identify which two components of security have been compromised in this incident. Justify your selection for each. [4 Marks]
2.  Recommend one physical or hardware-based defense to prevent this attack from occurring again. [2 Marks]

#### **Question 3: Scenario Audit (AAA Framework) [10 Marks]**
Read the following system profile for the *Perth Regional Sports Registry*:
> "The sports registry operates a web-accessible database. To log in, coordinators enter a shared password on the registry website. Once logged in, any coordinator has the administrative rights to edit scores, download raw medical files, and add new administrator accounts. The database server logs all connections to a central audit console, but has no mechanism to trace which specific coordinator initiated each record change."

1.  Evaluate this database system against the three pillars of the **AAA Security Framework**. Identify one failure point for **Authentication**, one for **Authorisation**, and one for **Accounting**. [6 Marks]
2.  Using the **Principle of Least Privilege**, explain how the administrator should redesign user access levels for standard sports coordinators. [4 Marks]

---

### **Marking Guide & Solutions**

#### **Question 1: Short Answer [4 Marks]**
1.  **Ethical vs Unethical:** 
    *   *1 Mark* for identifying that ethical hacking operates with **prior written authorization**, whereas unethical hacking does not.
    *   *1 Mark* for identifying that the ethical hacker's **intent** is defensive (to report and patch), while the unethical hacker's intent is malicious (data theft or disruption).
2.  **Legislation:** *1 Mark* for **Privacy Act 1988** (Cth).
3.  **APP Principles:** *1 Mark* for **APP 11** (Security of personal information).

#### **Question 2: Case Study [6 Marks]**
1.  **Triad Breakdown:**
    *   *1 Mark* for identifying **Availability** has been compromised.
    *   *1 Mark* for the justification: Flooding the network crashed the database, rendering systems *unavailable* to timing officials.
    *   *1 Mark* for identifying **Confidentiality** has been compromised.
    *   *1 Mark* for the justification: Master check-in files were copied to an external cloud, disclosing private data to unauthorized actors.
2.  **Mitigation:** 
    *   *2 Marks* (1 Mark select, 1 Mark justify) for: Physical locks on network switch cabinets to block rogue devices, OR deploying a Managed Switch with *Port Security* configured to disable ports if an unauthorized MAC address is detected.

#### **Question 3: Scenario Audit [10 Marks]**
1.  **AAA Failures:**
    *   *2 Marks (1 select, 1 justify) for Authentication:* Shared password means there is no unique authentication. The system cannot verify *who* is accessing the account.
    *   *2 Marks (1 select, 1 justify) for Authorisation:* Standard coordinators have administrative rights to delete/add accounts, violating role boundaries.
    *   *2 Marks (1 select, 1 justify) for Accounting:* Audit logs only log the connection event, not data transactions, meaning changes cannot be traced to specific individuals.
2.  **Least Privilege Redesign:**
    *   *1 Mark* for defining the Principle of Least Privilege (providing users with the absolute minimum rights necessary to do their job).
    *   *1 Mark* for recommending individual accounts with passwords for all coordinators.
    *   *1 Mark* for stripping standard coordinators of administrative database permissions (dropping tables, adding users).
    *   *1 Mark* for restricting standard accounts strictly to `SELECT` and `UPDATE` commands on specific scoring tables.
