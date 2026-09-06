# Year 11 Computer Science ATAR — Cumulative Exercises & Exam Practice

This practice book contains a comprehensive suite of curriculum-aligned practice questions designed to prepare Western Australian students for school-based assessments, practical tests, and written semester examinations in Year 11 Computer Science ATAR (Units 1 & 2). 

The exam layout, question structures, and difficulty tiers mirror the **SCSA Examination Design Brief** guidelines. The questions are structured into two logical parts:

*   **Part 1: Unit 1 Practice & Semester 1 Exam (Programming and Network Communications)**
*   **Part 2: Unit 2 Practice & Semester 2 Exam (Database Solutions and Cyber Security)**

*Note: Fully worked solutions, trace tables, sample network diagrams, and detailed marking keys are located in the companion volume: **`year-11-textbook-solutions-and-marking-keys.md`**.*

---

# Part 1: Unit 1 Exercises & Exam Practice

## Section A: Multiple-Choice Questions (20 Marks)
*Answer all questions. Each question is worth 1 mark.*

**1. Which of the following represents the decimal number `109` in 8-bit binary and hexadecimal?**
(a) `01101101` and `6D`
(b) `01101111` and `6F`
(c) `01111101` and `7D`
(d) `01101001` and `69`

**2. A student's first name, stored as a string variable, is typed into a registration form. Under standard 7-bit ASCII representation, how many bits of secondary storage are used to represent each character?**
(a) 4 bits
(b) 7 bits
(c) 8 bits
(d) 16 bits

**3. What is the fundamental difference between the ASCII and Unicode data representation standards?**
(a) ASCII can only represent whole numbers, whereas Unicode is optimized for alphanumeric characters.
(b) ASCII is limited to a 7-bit/8-bit range representing 128/256 characters, whereas Unicode uses variable-width sizing (16-bit/32-bit) to represent international language symbols.
(c) ASCII uses binary base-2 representation, whereas Unicode uses base-16 hexadecimal structures.
(d) ASCII is used for operating systems, whereas Unicode is strictly utilized for internet-connected web servers.

**4. Consider the following Python variable assignments:**
```python
age = 16
speed = 12.55
is_registered = True
student_id = "2026_01"
```
**Which list represents the correct sequence of data types for these variables?**
(a) `float`, `integer`, `string`, `Boolean`
(b) `integer`, `float`, `Boolean`, `string`
(c) `integer`, `float`, `string`, `Boolean`
(d) `float`, `integer`, `Boolean`, `string`

**5. Consider the following Python program sequence:**
```python
x = 10
y = 5
temp = x
x = y
y = temp
```
**What are the final values of `x` and `y` after execution?**
(a) `x = 10, y = 10`
(b) `x = 5, y = 5`
(c) `x = 10, y = 5`
(d) `x = 5, y = 10`

**6. Examine the following conditional branching algorithm:**
```python
score = 8
if score > 10:
    points = 100
elif score >= 8:
    points = 80
elif score > 5:
    points = 50
else:
    points = 0
```
**What is the value of `points` after the program executes?**
(a) 100
(b) 80
(c) 50
(d) 0

**7. Which of the following blocks will successfully catch a user entering text where an integer is expected, preventing a program crash?**
(a)
```python
if type(user_input) != int:
    print("Error")
```
(b)
```python
try:
    user_input = int(input("Enter age: "))
except ValueError:
    print("Invalid age entered.")
```
(c)
```python
while int(user_input) != True:
    user_input = input("Enter age: ")
```
(d)
```python
except ValueError:
    user_input = int(input("Enter age: "))
```

**8. How many times will the body of the following loop execute?**
```python
for i in range(1, 10, 2):
    print(i)
```
(a) 10 times
(b) 9 times
(c) 5 times
(d) 4 times

**9. Consider the following indefinite iteration structure:**
```python
count = 0
while count < 5:
    # line of code here
```
**Which line must be placed in the body of the loop to prevent an infinite loop?**
(a) `count = count - 1`
(b) `count = count + 1`
(c) `print(count)`
(d) `count = 0`

**10. What is the value of the variable `result` after evaluating the following expression?**
```python
result = 17 % 5 + 12 // 5
```
(a) 4
(b) 5.4
(c) 5
(d) 7

**11. Consider the variable definition `age = 15`. Which of the following logical expressions evaluates to `True`?**
(a) `age > 10 AND NOT age < 18`
(b) `NOT age == 15 OR age < 12`
(c) `age <= 15 AND NOT age > 20`
(d) `NOT (age > 12) AND age == 15`

**12. When passing a variable to a function, what is the key difference between a parameter and an argument?**
(a) An argument is defined in the function's header, whereas a parameter is the actual value passed during a function call.
(b) A parameter is defined in the function's header, whereas an argument is the actual value passed during a function call.
(c) A parameter resides in global scope, whereas an argument resides in local scope.
(d) Parameters are used in Python, while arguments are used in SCSA pseudocode.

**13. A local variable is declared inside a Python function. What is the scope and lifetime of this variable?**
(a) It can be accessed anywhere in the program, and its lifetime matches the program run.
(b) It can only be accessed within the function, and it is destroyed once the function returns.
(c) It can be modified globally but read locally, and its lifetime is permanent.
(d) It resides in the sequential file scope and is retained after power loss.

**14. What are the zero-indexed positions of the first and last elements in a one-dimensional array of size `n`?**
(a) First: `1`, Last: `n`
(b) First: `0`, Last: `n`
(c) First: `0`, Last: `n - 1`
(d) First: `1`, Last: `n - 1`

**15. Consider the following array of integers: `points = [12, 18, 5, 23, 15]`. Which algorithm is structurally correct for finding the maximum value in the array?**
(a) Initialize `max_val` to `0`, iterate through each element, if an element is less than `max_val`, update `max_val`.
(b) Initialize `max_val` to `points[0]`, iterate through each element, if an element is greater than `max_val`, update `max_val`.
(c) Initialize `max_val` to `points[4]`, iterate through each element, if an element is greater than `points[0]`, update `max_val`.
(d) Divide the array by the length, and assign the remainder to `max_val`.

**16. Which SCSA pseudocode syntax represents a correct modular structure chart loop construct?**
(a) A double-headed arrow pointing downwards.
(b) A semi-circular loop arrow drawn around the lines connecting a parent module to its child modules.
(c) A shaded rectangle containing data labels.
(d) A diamond decision box connected to local stubs.

**17. What phase of the SCSA Software Development Framework includes creating a Gantt chart and defining user requirements?**
(a) Evaluate
(b) Develop
(c) Design
(d) Investigate

**18. Which layer of the 4-layer DoD TCP/IP model is responsible for packet routing, path determination, and addressing?**
(a) Application
(b) Transport
(c) Internet
(d) Network

**19. Which transmission medium is immune to Electromagnetic Interference (EMI), offers the highest physical bandwidth, and can transmit data over kilometres without degradation?**
(a) Unshielded Twisted Pair (UTP) Category 6
(b) Shielded Twisted Pair (STP)
(c) Wi-Fi Radio Waves
(d) Optical Fibre

**20. A technician wants to connect a local athletics timing tent to a server room located 150 metres away. Which device operates at Layer 2 to segment collision domains and route frames within the local area network?**
(a) Switch
(b) Hub
(c) Repeater
(d) Modem

---

## Section B: Short-Answer & Extended Response (50 Marks)
*Answer all questions. Show working where appropriate.*

### Question 21: Algorithms, Tracing, and Testing (15 Marks)
A programmer at the WA Junior Sports Carnival writes the following Python subroutine to calculate and award final placement medals:

```python
def award_medal(sprint_time):
    if sprint_time <= 0.0:
        return "Invalid"
    elif sprint_time < 11.5:
        return "Gold"
    elif sprint_time < 12.8:
        return "Silver"
    elif sprint_time <= 14.0:
        return "Bronze"
    else:
        return "Participation"
```

1.  **Construct a complete SCSA-style trace table (desk check)** for the algorithm with the following consecutive sequential inputs: `13.5`, `11.2`, `-1.5`, `12.8`, `15.2`. *(5 Marks)*
2.  **Define the three types of test data** required by SCSA guidelines: **Normal**, **Extreme (Boundary)**, and **Erroneous (Invalid)**. Provide a specific example of each for the `award_medal` subroutine. *(6 Marks)*
3.  **Explain the difference between a logical error and a runtime error**, and identify how each is detected during the SCSA development framework. *(4 Marks)*

---

### Question 22: Relational Operators, Arrays, and Pseudocode (15 Marks)
1.  **Translate the following scenario into formal SCSA pseudocode** (adhering to strict uppercase syntax, left-pointing assignment arrows, and explicit closing structures):
    
    *Read a list of 5 house scores into a one-dimensional array named `HousePoints`. Calculate and print the sum of all points, the average of the scores, and identify the index position of the highest score.* *(8 Marks)*

2.  Draw a **Structure Chart** representing the modular decomposition of a carnival management portal. The portal must handle `UserLogin`, `UpdateScores`, and `GenerateReport`. Draw data couples and control flags communicating between modules. *(7 Marks)*

---

### Question 23: Networking Models, Diagrams, and Addressing (20 Marks)
The WA Junior Sports Carnival administration desk needs a network. The desk consists of:
*   Three admin desktop computers (wired connection).
*   One central database server hosting ovals registrations.
*   Two wireless tablets utilized by marshals at the field ovals.
*   The entire network must be protected from external internet threats and link securely to SCSA headquarters in Perth.

1.  **Draw a logical network diagram** representing this topology using standard **SCSA-compliant CISCO symbols**. You must explicitly show:
    *   The local area network (LAN) devices.
    *   The wireless local area network (WLAN) access point.
    *   The wide area network (WAN) boundary cloud.
    *   All necessary security and routing components. *(8 Marks)*
2.  **Assign appropriate IPv4 private addresses and subnet masks** using CIDR notation for the local network, explaining why a `/24` subnet mask is suitable for this office environment. *(4 Marks)*
3.  **Map the journey of a secure data packet** containing athlete scores as it descends from the marshal tablet (Application layer) down through the 4 layers of the **DoD TCP/IP model** to the physical medium, explaining the concept of **encapsulation** at each layer. *(8 Marks)*

---

# Part 2: Unit 2 Exercises & Exam Practice

## Section A: Multiple-Choice Questions (20 Marks)
*Answer all questions. Each question is worth 1 mark.*

**1. What is the fundamental legal dividing line under Australian law between ethical hacking (penetration testing) and unethical/illegal cyber access?**
(a) The type of software tools used.
(b) The presence of explicit, prior, written authorization from the system owner.
(c) The profit margin generated by the compromise.
(d) Whether the hacker was using a secure VPN connection.

**2. Which section of the Privacy Act 1988 is most critical for database developers, requiring organizations to take active, reasonable steps to protect personal data from loss, misuse, or unauthorized access?**
(a) APP 1 (Open and transparent management)
(b) APP 5 (Notification of collection)
(c) APP 11 (Security of personal information)
(d) APP 13 (Correction of personal information)

**3. A school database is targeted by a DDoS (Distributed Denial of Service) attack, causing the public leaderboard screen to drop offline for several hours. Which pillar of the CIA Triad has been compromised?**
(a) Confidentiality
(b) Integrity
(c) Accountability
(d) Availability

**4. A hospital security auditor notices that a receptionist's terminal can access and view medical records, but cannot write prescriptions or modify patient records. Which security control of the AAA framework does this policy represent?**
(a) Authentication
(b) Authorisation
(c) Accounting
(d) Auditing

**5. Which cyber threat vector involves manipulating humans into giving up sensitive passwords or security credentials voluntarily?**
(a) SQL Injection
(b) Man-in-the-Middle (MitM)
(c) Social Engineering
(d) Cross-Site Scripting (XSS)

**6. How does a computer virus differ structurally from a computer worm?**
(a) A virus encrypts files, whereas a worm steals passwords.
(b) A virus requires an active human host action to execute and replicate, whereas a worm self-replicates across network links automatically.
(c) A virus operates on wireless networks, whereas a worm is confined to copper UTP wiring.
(d) A virus is open-source, whereas a worm is proprietary malware.

**7. An unpatched software flaw that is completely unknown to a software vendor, leaving them with zero days to prepare defenses before active exploits occur, is known as a:**
(a) Trojan horse
(b) Back door
(c) Zero-day vulnerability
(d) Root exploit

**8. Which of the following describes a strong organizational password policy?**
(a) Requiring passwords to be changed every 3 days to simple incremental variations.
(b) Mandating high-entropy passphrases combined with multi-factor authentication (MFA).
(c) Storing passwords in a flat CSV text file for rapid supervisor reference.
(d) Permitting users to reuse old passwords on multiple platforms.

**9. In cryptography, what is the core benefit of asymmetric (public-key) encryption over symmetric encryption?**
(a) Asymmetric encryption uses the same key for both encryption and decryption, making it much faster.
(b) Asymmetric encryption completely resolves the "key distribution problem" by utilizing linked public and private key pairs.
(c) Asymmetric encryption is immune to brute-force attacks.
(d) Asymmetric encryption does not require computer systems to run mathematical divisions.

**10. A soldier encrypts the word "PERTH" using a Caesar rotation cipher with a shift key of `+3`. What is the resulting ciphertext?**
(a) `SHTWG`
(b) `SGUWJ`
(c) `RFQUI`
(d) `RGSUK`

**11. Which cryptographic attack analyzes letter frequencies in scrambled ciphertext to break simple monoalphabetic rotation systems?**
(a) Brute force
(b) Frequency analysis
(c) Parameterized query
(d) Rainbow table profiling

**12. What is the fundamental difference between data and information?**
(a) Data is digital, whereas information is always printed on paper.
(b) Data consists of raw, unprocessed facts, while information is data that has been structured, processed, and contextualized to be meaningful.
(c) Data resides in databases, while information is stored on flash drives.
(d) Data is secure, whereas information is public.

**13. A relational database system is preferred over a flat-file spreadsheet because it avoids data redundancy. What are the three common operational anomalies caused by data redundancy in flat sheets?**
(a) Authentication, Authorization, Accounting anomalies
(b) Select, Insert, Update anomalies
(c) Insert, Update, Delete anomalies
(d) Read, Write, Execute anomalies

**14. What database object physically implements an Entity in a Relational Database Management System?**
(a) Attribute
(b) Record
(c) Field
(d) Table

**15. Which field format is most appropriate for storing Australian mobile phone numbers (e.g., `0412345678`)?**
(a) `INTEGER` (size 10)
(b) `FLOAT`
(c) `TEXT`
(d) `BOOLEAN`

**16. Which database schema key is composed of two or more foreign keys and is used to uniquely identify records in an associative (junction) table?**
(a) Super Key
(b) Primary Key
(c) Candidate Key
(d) Composite Primary Key

**17. What is the main purpose of database normalisation up to Third Normal Form (3NF)?**
(a) To increase the speed of disk backups.
(b) To systematically eliminate data redundancy and prevent operational anomalies.
(c) To encrypt table fields against SQL Injection.
(d) To establish multi-factor authentication for DBAs.

**18. If a relational database table is in First Normal Form (1NF) and has a single-column primary key (e.g., `StudentID`), what normal form is it guaranteed to be in?**
(a) Un-normalised Form (UNF)
(b) Second Normal Form (2NF)
(c) Third Normal Form (3NF)
(d) Boyce-Codd Normal Form

**19. Examine the following SQL statement:**
```sql
SELECT StudentName, Score 
FROM Results 
WHERE Score >= 80 
ORDER BY Score DESC;
```
**In what order will the results be displayed?**
(a) Ascending numerical order of scores (lowest to highest).
(b) Alphabetical order of student names.
(c) Descending numerical order of scores (highest to lowest).
(d) Chronological order of entry.

**20. Which SQL clause is used to merge records from two different tables based on a matching key attribute?**
(a) `GROUP BY`
(b) `INNER JOIN ... ON`
(c) `SELECT DISTINCT`
(d) `WHERE EXISTS`

---

## Section B: Short-Answer & Extended Response (50 Marks)
*Answer all questions. Show working where appropriate.*

### Question 21: Database Modelling and ERDs (15 Marks)
A regional swimming club runs a database tracking members, ovals lanes, coaches, and training registrations.
*   Each member swims at one-and-only-one club. A club has many members.
*   A member can sign up for many training squads. A training squad has many members.
*   Each training squad is assigned to exactly one coach. A coach can teach many squads.

1.  **Design and draw a complete Entity-Relationship Diagram (ERD)** for this swimming database using standard **Crow’s Foot Notation**. Your diagram must contain:
    *   Exactly four entities (including the resolved associative entity).
    *   All correct cardinality symbols (One-and-only-one, one-or-many, etc.).
    *   Explicitly marked Primary Keys (PK) and Foreign Keys (FK). *(8 Marks)*
2.  **Construct a Data Dictionary** for the Resolved Associative table, specifying: Field Name, Data Type, Key Type, Field Size, Validation rules, and a descriptive Example. *(7 Marks)*

---

### Question 23: Database Normalisation (15 Marks)
A local WA junior soccer club coordinates rosters using a flat spreadsheet. The database coordinator notes massive data redundancy and recurrent spelling errors. Below is a sample slice of their flat-file database:

**Messy Flat Roster Sheet (UNF)**

| PlayerID | PlayerName | TeamCode | TeamName | CoachName | CoachPhone | MatchDate | PlayedField |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| P210 | Toby Jones | TM_RED | Red Giants | Sarah West | 0411111111 | 2026-09-05 | Field A |
| P210 | Toby Jones | TM_BLU | Blue Rays | Mark Swan | 0422222222 | 2026-09-12 | Field B |
| P305 | Alice Finch | TM_RED | Red Giants | Sarah West | 0411111111 | 2026-09-05 | Field A |
| P412 | Liam Baker | TM_GRN | Green Hares | Dave Pine | 0433333333 | 2026-09-05 | Field C |

1.  **Identify and explain** concrete scenarios of **insert, update, and delete anomalies** that could occur within this flat roster layout. *(6 Marks)*
2.  **Normalise this dataset to Third Normal Form (3NF)**. You must show the tables at each stage of the normalisation process:
    *   First Normal Form (1NF) schema.
    *   Second Normal Form (2NF) schema (explaining partial dependencies).
    *   Third Normal Form (3NF) schema (explaining transitive dependencies). *(9 Marks)*

---

### Question 24: SQL Queries & Aggregates (20 Marks)
A database containing sports information consists of three tables:

**`School` Table**
*   `SchoolCode` (TEXT, PK)
*   `SchoolName` (TEXT)
*   `Suburb` (TEXT)

**`Athlete` Table**
*   `AthleteID` (TEXT, PK)
*   `AthleteName` (TEXT)
*   `SchoolCode` (TEXT, FK linking to `School`)
*   `Age` (INTEGER)

**`Registration` Table**
*   `RegID` (INTEGER, PK)
*   `AthleteID` (TEXT, FK linking to `Athlete`)
*   `EventName` (TEXT)
*   `Score` (FLOAT)

Write complete SQL queries to achieve the following database goals:

1.  **Retrieve** the names of all athletes who are younger than 16 years old, sorted alphabetically by name. *(4 Marks)*
2.  **Display** a combined table showing the `AthleteName`, their matching `SchoolName`, and their registered `EventName` using appropriate multi-table joins. *(5 Marks)*
3.  **Calculate the average score** achieved by athletes from each school. Display the `SchoolName` alongside their average score, grouped by school. *(6 Marks)*
4.  A database developer is writing a login script for the carnival website. They construct the query using standard string concatenation:
    ```python
    query = "SELECT * FROM Admins WHERE User = '" + username + "' AND Pass = '" + password + "'"
    ```
    *   **Explain the security threat** associated with this coding practice.
    *   **Show how to rewrite the database query in Python** using secure parameterization to completely neutralize the exploit. *(5 Marks)*

---
