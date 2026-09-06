# Unit 2 — Chapter 13: Database Foundations

This chapter introduces the structural architecture, storage designs, and key constraints of modern relational database management systems. In **Unit 2**, the curriculum shifts focus from procedural programming (writing code sequences) to data modelling and management. You will learn how databases organize vast stores of records, enforce integrity, and establish secure multi-user systems.

You will master the fundamental distinction between raw data and processed information, analyze the systemic hazards of flat-file spreadsheets (specifically data redundancy and anomalies), justify the use of a Relational Database Management System (RDBMS), and learn to structure data hierarchies using primary, foreign, and composite keys.

These foundational relational theories are highly examinable in SCSA theory papers and form the conceptual core of **SCSA School-Based Assessment Task 6 (The Relational Database Project)**.

---

## Lesson 13.1: Data vs Information

### Your Goal
Contrast and explain the structural and cognitive differences between raw data and contextualized information, and outline how processing converts one to the other.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.4: Fundamental Data Types](./year-11-textbook-chapter-1.md#lesson-14-fundamental-data-types) (representing numeric, text, and Boolean values).
*   [Lesson 8.2: Good Programming Practices](./year-11-textbook-chapter-8.md#lesson-82-good-programming-practices) (structuring variables clearly).

### The Idea
In computer science, the words "data" and "information" are often used interchangeably in everyday conversation, but they have completely distinct, rigid meanings. A computer processor consumes *data* to produce *information*.

**The Analogy:**
Suppose you look at a scrap of paper on a desk at the athletics field containing the scribbled list: `11.85`, `12.40`, `13.10`. 
To an observer, these are just numbers. They could be wind speeds, ticket prices in Australian dollars, high-jump heights, or random digits. This is **raw data**. It has no meaning, no context, and is useless on its own.

Now, imagine the sports marshal takes that scrap of paper and typing those numbers into a computer system that associates them with specific labels:
*   `11.85` $ightarrow$ "Ben (Year 11, Melvista High School), 100m Sprint Time, 1st Place."
*   `12.40` $ightarrow$ "Chloe (Year 11, Swan River Grammar), 100m Sprint Time, 2nd Place."
*   `13.10` $ightarrow$ "Dan (Year 11, Kings Park High), 100m Sprint Time, 3rd Place."

By structuring, labeling, and placing those raw numbers into a clear context, they have been transformed into **information**. The regional sports coordinators can now use this information to award medals, update school leaderboards, and publish the official carnival newsletter.

```
+------------------+       Processing:       +-------------------------+
|     RAW DATA     |   Contextualization,    |       INFORMATION       |
| Unstructured,    |  Formatting, Sorting,   |   Structured, Meaning,  |
| No context,      |  Logical Association    |   Actionable, Decision- |
| e.g., "11.85"    |------------------------>|   ready, e.g., "Ben     |
|                  |                         |   won Gold with 11.85s" |
+------------------+                         +-------------------------+
```

#### **SCSA Key Terms**
*   **Data:** Raw, unorganized, and unprocessed facts, figures, symbols, or observations without context or inherent meaning. Data is the input to a system.
*   **Information:** Data that has been processed, structured, formatted, or contextualized so that it becomes meaningful, useful, and actionable for human decision-making. Information is the output of a system.
*   **Processing:** The manipulation, organization, calculation, or analysis of raw data to convert it into structured information.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival registration manager receives an automated export from a timing gate sensor containing raw data. We need to analyze this raw input and trace how it is transformed into meaningful information on the parent public leaderboard.

#### **Raw Data Export (CSV String)**
```text
"T",20260905,101,14.52,F
```

#### **The Transformation Process (Logical Steps)**
1.  **De-encapsulation and Extraction:** The database parser reads the raw comma-separated values (CSV) and isolates each individual data element.
2.  **Contextual Association (Using Data Dictionaries & Schemas):**
    *   The first value `"T"` is mapped to the event type: *Track Event*.
    *   The second value `20260905` is parsed using a date format (YYYYMMDD): *5th September 2026*.
    *   The third value `101` is looked up in the Athlete table: *Mapped to Athlete ID 101 ("Aisha Patel")*.
    *   The fourth value `14.52` is mapped to the event measurement field: *14.52 seconds*.
    *   The fifth value `"F"` is evaluated against a verification lookup table: *Flagged as "Foul" (False attempt/Disqualified)*.
3.  **Logical Evaluation:** Since the attempt is flagged as "Foul", this sprint time cannot be counted toward the qualifying final.

#### **Processed Information Output (Presented to Coordinator)**
> **WA Junior Sports Carnival — Incident Report**  
> **Date:** 5 September 2026  
> **Athlete:** Aisha Patel (ID: 101)  
> **Event:** 100m Track Sprint  
> **Result:** 14.52s (Disqualified - Foot foul at starting block).  
> **Status:** Run invalid. No points awarded to house.

By converting the raw characters `"T",20260905,101,14.52,F` into a structured, clear report, the carnival marshal can make an immediate, legally compliant decision regarding point allocations.

---

### Try It with Help
#### **The Problem**
A local swimming pool's water-quality sensor records a raw stream of floating-point values once every hour: `7.2`, `7.4`, `7.9`, `8.2`. Explain how a database system processes these raw data points into actionable information for pool lifeguards.

#### **Structural Hints**
1.  **Define the Raw Data:** What do these decimal numbers represent without context?
2.  **Explain the Processing Steps:** How can we structure and evaluate these values? (Hint: Swimming pools require a safe pH balance between `7.2` and `7.8`).
3.  **Produce the Actionable Information:** What does the output report tell the lifeguard to *do* when the pH hits `8.2`?

#### **Scaffolded Student Guide**
*   The raw data consists of **unlabeled decimal values** (`7.2`, `7.4`, etc.).
*   The system processes this data by **matching them to timestamps**, labeling them as **pH measurements**, and comparing them against a safe-threshold logical expression (`pH >= 7.2 AND pH <= 7.8`).
*   The system outputs **actionable information**: *"Warning: Pool pH has risen to 8.2 (Alkaline). Action Required: Add acid treatment immediately to prevent skin irritation."*

---

### Try It Yourself
#### **The Problem**
The WA Junior Sports Carnival timing booth receives a raw Bluetooth packet from a high-jump bar sensor:  
`"HJ",114,1.45,0`  
Write a short response (approx. 100 words) tracing how this raw data packet is converted into structured, actionable information for the high-jump marshal's tablet screen.

---

### Check Your Reasoning
#### **The Answer**
An expert response must detail the following steps:
1.  **Identify Raw Data:** The raw comma-separated elements (`"HJ"`, `114`, `1.45`, `0`) have no context, units, or identities on their own.
2.  **Detail Processing/Contextualization:** 
    *   `"HJ"` is parsed as the *High Jump* event.
    *   `114` is processed via database lookup to identify the athlete: *Jack Ryan (Swan River Grammar)*.
    *   `1.45` is labeled as the bar height in *metres*.
    *   `0` is evaluated as a Boolean flag representing *Failure/Knocked Bar* (where `1` would represent success).
3.  **Actionable Information Output:** The system outputs: *"Jack Ryan failed to clear the high-jump bar at 1.45m. This is his third consecutive failure. Status: Knocked out of competition. Field marshal action: Record final height as 1.40m."*

#### **Common SCSA Student Errors**
*   **Vague Definitions:** Writing that data is "numbers" and information is "words". This is incorrect; data can contain words (e.g. `"HJ"`, `"F"`), and information can contain numbers (e.g. final heights and rankings). The true distinction is **structure, meaning, and context**.
*   **Omitting the "Processing" Stage:** Skipping straight from raw CSV values to a final sentence without explaining *how* the system mapped, looked up, or mathematically evaluated the raw elements.

---

### Review and Connect
In this lesson, you mastered the logical transformation of raw inputs into decision-ready outputs. Now that you understand how data must be processed, we will examine the storage systems we use to hold this data: comparing traditional, flat spreadsheets with professional **Relational Databases**.

---

## Lesson 13.2: Flat File vs Relational Database

### Your Goal
Analyze the systemic limitations of flat-file database structures and justify the implementation of a Relational Database Management System (RDBMS) based on data redundancy, integrity, and independence.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 8.1: The SCSA Framework for Development](./year-11-textbook-chapter-8.md#lesson-81-the-scsa-framework-for-development) (understanding software limitations).
*   [Lesson 10.2: Privacy Act 1988 & Australian Privacy Principles](./year-11-textbook-chapter-10.md#lesson-10-2-privacy-act-1988--australian-privacy-principles-apps) (system security requirements).

### The Idea
In the early days of computing, organizations stored records in single, massive text files or spreadsheets. This is known as a **flat-file database**. While simple to set up, flat files quickly break down when systems grow, causing severe errors that can compromise an entire business's records.

**The Analogy:**
Suppose the volunteer coordinators of the **WA Junior Sports Carnival** use a single, shared Excel spreadsheet to manage all registrations, school houses, and event times. Every row in the spreadsheet represents a single race entry:

| Athlete_Name | School_Name | School_Address | Event_Name | Coach_Name | Run_Time |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Aisha Patel | Melvista High | 12 Broadway, Nedlands | 100m Sprint | Mr. Smith | 14.52 |
| Aisha Patel | Melvista High | 12 Broadway, Nedlands | 200m Sprint | Mr. Smith | 29.10 |
| Jack Ryan | Swan River | 50 Esplanade, Perth | 100m Sprint | Ms. Jones | 15.10 |
| Aisha Patel | Melvista High | 12 Brodway, Nedlands | Shot Put | Mr. Smith | 8.40 |

Look closely at this flat table. It suffers from major structural issues:
1.  **Extreme Redundancy:** Aisha's school name, coach, and school address are typed out three separate times. If 1,000 students from Melvista High register, that address will be stored 1,000 times, wasting memory.
2.  **Typos & Inconsistencies:** On row 4, a volunteer mistyped the school address as "12 **Brodway**". Now, a search for students at "Broadway" will miss Aisha's third event.
3.  **Delete Anomaly:** If Jack Ryan withdraws from the 100m Sprint and we delete his row, we completely lose the information that Ms. Jones is the coach for Swan River, and we lose Swan River's address!
4.  **Insert Anomaly:** We cannot add a new school (e.g., Fremantle High) to our system until they have registered at least one athlete for an event, because the rows require athlete details.

#### **The Solution: The Relational Database & RDBMS**
To solve these issues, we break the single flat table into three dedicated, linked tables: **School**, **Athlete**, and **EventEntry**. Each piece of information is stored in **one place only**.

```
  +------------------+             +-------------------+
  |      SCHOOL      |             |      ATHLETE      |
  |------------------|             |-------------------|
  | PK  SchoolID     |1           1| PK  AthleteID     |
  |     SchoolName   |--+       +--|     AthleteName   |
  |     Address      |  |       |  | FK  SchoolID     |
  |     CoachName    |  |       |  +-------------------+
  +------------------+  |       |            |1
                        |1:M    |1:M         |
                        |       |            |1:M
                      +------------------------+
                      |       EVENTENTRY       |
                      |------------------------|
                      | PK,FK  EntryID         |
                      |        EventName       |
                      |        RunTime         |
                      | FK     AthleteID       |
                      +------------------------+
```

An **RDBMS (Relational Database Management System)** is the specialized software program we use to manage these tables, control access, and enforce relational rules (such as preventing a user from deleting a school if there are still athletes linked to it).

#### **SCSA Key Terms**
*   **Flat-File Database:** A database stored in a single, unstructured file (like a CSV or spreadsheet table) where all data fields are kept in one flat record layout.
*   **Relational Database:** A digital database containing multiple tables of structured data that are logically linked or related to one another through key fields.
*   **RDBMS (Relational Database Management System):** Software application (e.g., SQLite, MySQL, Microsoft SQL Server) that manages, queries, and secures relational databases.
*   **Data Redundancy:** The unnecessary repetition of data across a database (e.g., repeating a school's address on every athlete's row).
*   **Data Integrity:** The overall accuracy, completeness, and consistency of data stored in a database.
*   **Data Independence:** The structural separation of database data from the application programs that access it, allowing developers to change the database layout without breaking software interfaces.
*   **Anomalies (Insert, Update, Delete):** Unintended, corruptive data states that occur in flat or poorly structured tables when modifying records.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival RDBMS needs to update the coach name for *Swan River Grammar* from "Ms. Jones" to "Mrs. Davis". Let's compare how this update performs in a flat file vs. a relational database:

#### **Flat File Execution**
The program must scan every single line of the massive CSV registration file. For every athlete representing Swan River Grammar, the system must overwrite the text "Ms. Jones" with "Mrs. Davis".
*   *Risk:* If the program is interrupted halfway through, or if Swan River Grammar is spelled "Swan River" on some rows, the data becomes corrupt and inconsistent (some rows will show Ms. Jones, others Mrs. Davis). This is an **Update Anomaly**.

#### **Relational Database Execution (RDBMS)**
Because the database is normalized and relational, Swan River Grammar exists as a **single row** inside the dedicated `School` table.
*   *Action:* The RDBMS executes a single update query targeting only that specific row:
```sql
UPDATE School SET CoachName = 'Mrs. Davis' WHERE SchoolID = 3;
```
*   *Result:* The change is made in exactly **one place**. Every athlete linked to School `3` immediately references the new coach name automatically. There is zero data redundancy, zero risk of partial updates, and data consistency is perfectly preserved.

---

### Try It with Help
#### **The Problem**
The carnival coordinators are tracking medical alerts for students. In their old flat spreadsheet, they have rows like:
`Aisha Patel | Melvista High | Asthma | Ventolin puffer in bag`
`Aisha Patel | Melvista High | Nut Allergy | EpiPen in first-aid kit`

Explain what happens if Aisha changes her school to *Kings Park High* and a volunteer updates her school name on only the *first* row. What systemic database issue does this represent, and how does an RDBMS resolve it?

#### **Structural Hints**
1.  **Identify the Inconsistency:** What state is Aisha's school record in now?
2.  **Define the Anomaly:** Which of the three operational anomalies (insert, update, delete) occurred here?
3.  **Propose the RDBMS Relational Fix:** How would separating `Athlete` from `MedicalAlerts` solve this?

#### **Scaffolded Student Guide**
*   Updating Aisha's school on only one row creates **inconsistent data**, where she appears to attend two different schools simultaneously.
*   This is an **Update Anomaly** caused by data redundancy in the flat file structure.
*   An RDBMS resolves this by keeping Aisha's profile in a single **Athlete Table** (where her school is stored exactly once) and linking her medical alerts in a separate **Medical Table** via her unique ID.

---

### Try It Yourself
#### **The Problem**
A school sporting association wants to upgrade its regional tournament tracker from a shared Google Sheets spreadsheet to an SQLite Relational Database Management System. 

Write a brief executive justification (approx. 120 words) detailing how the RDBMS will prevent **data redundancy** and provide **data independence** for their application developers.

---

### Check Your Reasoning
#### **The Answer**
An expert-level justification must address:
1.  **Elimination of Data Redundancy:** By splitting the spreadsheet into distinct entities (e.g., Teams, Players, Matches), parent school details and tournament venues are recorded once in their respective tables. This saves storage space and eliminates the risk of spelling inconsistencies and update anomalies.
2.  **Enforcing Data Integrity:** The RDBMS uses referential constraints (foreign keys) to ensure a player cannot be assigned to a non-existent team, preserving structural accuracy.
3.  **Ensuring Data Independence:** In a flat sheet, any change to column order or headers breaks the parsing code of client applications. An RDBMS isolates data structures from the client programs. Developers can optimize index tables or add fields without modifying or breaking the core application software queries.

#### **Common SCSA Student Errors**
*   **Confusing "Data Independence" with "Security":** Believing data independence means "restricting unauthorized users." Data independence is the structural separation of the logical data schema from the physical software applications accessing it.
*   **Failing to name the Anomalies:** Talking vaguely about "mistakes" without using SCSA terminology: **Insert, Update, and Delete Anomalies**.

---

### Review and Connect
In this lesson, you analyzed why flat-file systems fail under load, and how relational schemas managed by an RDBMS preserve integrity. Now, we will drill down into the physical architecture of these relational tables, examining how records are structured and linked using **Primary, Foreign, and Composite Keys**.

---

## Lesson 13.3: Core Database Concepts & Hierarchy

### Your Goal
Design relational tables that conform to the standard data hierarchy, select optimal datatypes, and implement primary, foreign, and composite keys to link entities.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.4: Fundamental Data Types](./year-11-textbook-chapter-1.md#lesson-14-fundamental-data-types) (matching variables to physical datatypes).
*   [Lesson 13.2: Flat File vs Relational Database](./year-11-textbook-chapter-13.md#lesson-13-2-flat-file-vs-relational-database).

### The Idea
To build a functional relational database, we must organize our storage following a rigid, nested structure. This structural organization is called the **data hierarchy**.

**The Analogy:**
Think of a physical filing cabinet in the sports office:
*   The **Cabinet** itself represents the entire **Database**.
*   Each **Drawer** in the cabinet represents a specific **Table** (e.g., the "Athlete" drawer).
*   Inside the drawer, each physical **Folder** represents a single **Record** for one specific athlete.
*   Inside that folder, each individual **Line on the form** (First Name, Date of Birth, Emergency Phone Number) represents a **Field/Attribute**.

```
  DATABASE (The Sports Cabinet)
     └── TABLE / ENTITY (The "Athlete" Drawer)
          └── RECORD / ROW (A Student's Folder)
               └── FIELD / ATTRIBUTE (The student's Date of Birth)
```

To logically link these tables together without redundancy, we use specific key constraints:
1.  **Primary Key (PK):** A field (or group of fields) that uniquely identifies each record in a table. No two rows can share the same Primary Key, and it can never be empty (Null).
    *   *Example:* `AthleteID` (e.g., `101`, `102`).
2.  **Foreign Key (FK):** A primary key from one table that is placed into another table to establish a logical relationship.
    *   *Example:* Putting `SchoolID` into the `Athlete` table allows us to look up which school Jack Ryan represents.
3.  **Composite Key:** A primary key that is composed of two or more attributes, usually where each attribute is a foreign key in its own right. This is essential for resolving **Many-to-Many (M:N)** relationships.
    *   *Example:* An athlete can enter many events, and an event has many athletes. We create a linking table called `EventEntry`. Its primary key is a **Composite Key** made of `(AthleteID, EventCode)`.

#### **SCSA Key Terms**
*   **Entity / Table:** A real-world person, place, object, or event about which data is captured and stored. Implemented as a database table.
*   **Attribute / Field:** A specific property or characteristic of an entity (e.g., an athlete's age). Implemented as a table column.
*   **Record / Row:** A collection of related fields representing a single, unique instance of an entity. Implemented as a table row.
*   **Primary Key (PK):** A unique identifier for every record in a table.
*   **Foreign Key (FK):** An attribute in a table that references a primary key in a parent table to create a relational link.
*   **Composite Key:** A primary key consisting of multiple columns combined to uniquely identify a record.
*   **SCSA Datatypes:**
    *   **TEXT:** Alphanumeric characters (e.g. Names, Phone Numbers).
    *   **INTEGER:** Whole numbers without decimals (e.g. Points, Years).
    *   **FLOAT:** Decimal numbers (e.g. Race times, Heights).
    *   **BOOLEAN:** Logical flags (`True` / `False`).
    *   **DATE:** Structured calendar values (YYYY-MM-DD).

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival needs to record which athletes are assigned to compete in which sports events. 
*   An athlete (e.g., Aisha Patel) can compete in multiple events (100m, 200m, Shot Put).
*   An event (e.g., 100m Sprint) contains multiple competing athletes.
This is a **Many-to-Many (M:N)** relationship. We must design an associative schema to resolve this cleanly.

#### **The Relational Schema Design**

```text
Table 1: Athlete
+-------------+-------------+------------+-----------+
| AthleteID   | FirstName   | LastName   | SchoolID  |
| (PK) [INT]  | [TEXT]      | [TEXT]     | (FK) [INT]|
+-------------+-------------+------------+-----------+
| 101         | Aisha       | Patel      | 3         |
| 102         | Jack        | Ryan       | 5         |
+-------------+-------------+------------+-----------+

Table 2: Event
+--------------+------------------+-------------+
| EventCode    | EventName        | BasePoints  |
| (PK) [TEXT]  | [TEXT]           | [INT]       |
+--------------+------------------+-------------+
| "T100"       | 100m Sprint      | 10          |
| "FSP"        | Field Shot Put   | 15          |
+--------------+------------------+-------------+

Table 3: EventEntry (Associative Table)
+--------------+--------------+-------------+
| AthleteID    | EventCode    | FinalResult |
| (PK,FK) [INT]| (PK,FK)[TEXT]| [FLOAT]     |
+--------------+--------------+-------------+
| 101          | "T100"       | 14.52       |
| 101          | "FSP"        | 8.40        |
| 102          | "T100"       | 15.10       |
+--------------+--------------+-------------+
```

#### **How the Keys Flow**
*   In the `Athlete` table, `AthleteID` is the **Primary Key**. It uniquely identifies each student.
*   In the `Event` table, `EventCode` is the **Primary Key**.
*   To link them, we create `EventEntry`. 
*   Because any student can compete in many events, neither `AthleteID` nor `EventCode` can be the primary key *individually* inside `EventEntry` (look at rows 1 and 2: Athlete `101` appears twice!).
*   Instead, we combine them into a **Composite Primary Key**: `(AthleteID, EventCode)`. The combination `(101, "T100")` is completely unique, linking Aisha Patel securely to her 100m run result.

---

### Try It with Help
#### **The Problem**
A school textbook hire scheme tracks which textbooks are loaned to which students. A student can borrow multiple books, and a textbook title is loaned to multiple students over time. 
Identify the data entities, select appropriate datatypes, and design an associative table schema showing the primary, foreign, and composite keys.

#### **Structural Hints**
1.  **Identify Entities:** You will need three tables: `Student`, `Textbook`, and `BookLoan`.
2.  **Define Attributes and Keys:**
    *   What field uniquely identifies a student? (`StudentID`, Integer).
    *   What field uniquely identifies a physical book? (`BarcodeNumber`, Integer).
    *   What composite elements are needed inside the linking table `BookLoan`?

#### **Scaffolded Student Template**
*   **Table: Student** $ightarrow$ PK: `StudentID` [INT], Name [TEXT], YearGroup [INT].
*   **Table: Textbook** $ightarrow$ PK: `BookID` [INT], Title [TEXT], Subject [TEXT].
*   **Table: BookLoan** $ightarrow$ PK (Composite): (`StudentID` [INT], `BookID` [INT]), DateBorrowed [DATE], DateReturned [DATE].

---

### Try It Yourself
#### **The Problem**
A local tennis club manages court bookings.
*   Members have a unique Member Number, Name, and Mobile Number.
*   Courts have a Court Number (1 to 8) and a Surface Type (Grass, Hard, Clay).
*   Members book specific courts on specific dates/times.

Design a relational schema (list of tables, columns, datatypes, and keys) that resolves this system. Highlight any **Composite Keys** and justify your design choices.

---

### Check Your Reasoning
#### **The Answer**
```text
Table 1: Member
- MemberNo [INTEGER] (PK)
- MemberName [TEXT]
- MobileNo [TEXT] (Stored as TEXT to preserve leading zeros and formatting)

Table 2: Court
- CourtNo [INTEGER] (PK)
- SurfaceType [TEXT]

Table 3: CourtBooking
- MemberNo [INTEGER] (FK references Member.MemberNo)
- CourtNo [INTEGER] (FK references Court.CourtNo)
- BookingDate [DATE]
- BookingTime [TEXT] (e.g., "14:00")
Primary Key (Composite): (CourtNo, BookingDate, BookingTime)
```

#### **Key Justification Details**
*   **Selecting the PK for Booking:** Using `(MemberNo, CourtNo)` as a composite key is a common mistake. This would prevent a member from ever booking the same court twice in their lifetime!
*   **The Correct Composite Key:** Combining `(CourtNo, BookingDate, BookingTime)` as a composite primary key guarantees database integrity. It ensures that Court 3 cannot be booked by two different members at 2:00 PM on 5th September 2026.
*   **Phone Number Datatype:** Storing `MobileNo` as `TEXT` rather than `INTEGER` is critical. An integer datatype strips away leading zeros (converting `0412` to `412`) and crashes if spaces or country code characters (e.g., `+61`) are entered.

---

### Review and Connect
You have mastered the hierarchical structure of relational database design, moving from raw fields to complex associative composite keys. In the next chapter, we will learn how to formally document these structures using standard industry symbols: **Crow's Foot Entity-Relationship Diagrams (ERDs)**.

---

## Teacher Support Module

### **SCSA Syllabus Mapping**
*   **SCSA Year 11 Unit 2 Theory Syllabus Objectives:**
    *   *Relationship between data and information.*
    *   *Flat file vs relational database; relational database management system (RDBMS); role of an RDBMS in handling access to data; independence of data from RDBMS.*
    *   *Organisation of a relational database: entities, attributes, relationships (one-to-one, one-to-many, many-to-many); tables as the implementation of entities, consisting of fields and records; hierarchical structure of data: field/attribute, record, table/entity; datatypes (integer, float, Boolean, text, date); primary and foreign keys; composite key.*

### **Prerequisite Diagnostics**
Before teaching this module, ensure students have completed:
*   **Chapter 1 (Data Types)**: Students must understand how computers store characters, numbers, and Booleans.
*   **Chapter 8 (The Development Framework)**: Students must understand why clear data modeling is an essential part of the "Design" phase of any project.

### **Misconception Busters**
1.  **"Text is only for sentences":** Students frequently store telephone numbers, zip codes, and ID numbers as integers. Explain that *if you are not going to perform arithmetic on it (adding, multiplying), it should be stored as TEXT*. Phone numbers with leading zeros require text storage.
2.  **"Data and Information are synonyms":** Direct students to define processing as the functional bridge between data and information. Remind them: *Data is the fuel; Information is the functional output.*
3.  **"A Foreign Key must have the same name as its Primary Key":** While it is standard database practice (e.g., `SchoolID` in both tables), an FK can have any attribute name (e.g. `SchoolOriginID`) as long as its data type matches the PK it references exactly.

### **Assessment Integration Guide**
*   These database theories prepare students directly for **SCSA Task 6: The Relational Database Project (20% Weight)**. 
*   In Task 6, SCSA requires students to take a messy flat-file tournament database, document its structural limitations, design an ERD, normalization matrix, and deploy it inside an SQLite RDBMS. Use Lesson 13.2's flat-file comparison directly as a worksheet practice template for Task 6 documentation.

---

## Classroom Assessment & Practice Test

### **SCSA Unit 2 - Relational Databases Foundations Exam**
*   **Duration:** 25 Minutes  
*   **Total Marks:** 20 Marks  
*   **Conditions:** Closed book, calculator permitted.

---

#### **Section 1: Short Answer Questions (12 Marks)**

**Question 1 (3 Marks)**  
A regional WA health portal collects patient sensor records. One patient records the data stream: `38.2`, `38.5`, `39.1`.  
Explain how this data is processed into information. Use SCSA terminology.

**Question 2 (4 Marks)**  
The WA Junior Sports Carnival committee stores its scheduling details in a flat-file spreadsheet. It contains the following row:  
`Athlete_ID: 405 | Name: Leo Chang | School: Stirling High | Event: 400m Race | Field_Lanes: 6`  
*   Describe how a **Delete Anomaly** could occur in this system if Leo Chang decides to withdraw from the competition.
*   State how an RDBMS resolves this risk.

**Question 3 (5 Marks)**  
Analyze the following database table schema designed to track textbook issues in a school:  
`BorrowingRecord(StudentID, StudentName, BookID, Title, DateIssued)`  
*   Identify the structural issue with using `(StudentID, BookID)` as a composite primary key if students can borrow the same textbook multiple times across a semester. (2 Marks)
*   Redesign the schema list to resolve this problem, clearly identifying your revised primary key, attributes, and datatypes. (3 Marks)

---

#### **Section 2: Practical Schema Application (8 Marks)**

**Scenario:**  
A local Western Australian yachting marina manages boat slips.
*   **Boats** have a Boat ID (PK, Integer), Boat Name (Text), and Length in metres (Float).
*   **Slips** (parking bays) have a Slip Number (PK, Integer) and Max Width (Float).
*   A boat can park in **one slip** at a time. A slip can hold **one boat** at a time.
*   The marina keeps track of the **StartDate** (Date) and **EndDate** (Date) for each boat's stay.

Construct a complete relational schema layout for this yacht marina database. Your answer must:
1.  Define all necessary tables, identifying field names, keys, and datatypes. (4 Marks)
2.  Resolve the boat-to-slip allocation, explaining how relationships are enforced via foreign keys. (2 Marks)
3.  Explain how you prevent the data redundancy of boat parameters using this design. (2 Marks)

---

### **Teacher Marking Guide & Solutions**

#### **Section 1 Solution Key**

**Question 1 (3 Marks)**
*   **1 Mark:** Identifies that `38.2`, `38.5`, `39.1` are **raw, unprocessed data values** lacking units or meaning.
*   **1 Mark:** Explains the **processing/contextualization** steps: matching values to a thermometer sensor, labeling them as body temperatures in degrees Celsius ($^\circ	ext{C}$), and linking them to a specific patient ID.
*   **1 Mark:** Provides the **actionable information output**: *"Warning: Patient ID 402 is running a fever of 39.1C. Trigger medical response protocol immediately."*

**Question 2 (4 Marks)**
*   **2 Marks (Delete Anomaly Description):** If Leo Chang is deleted from the spreadsheet, the system completely loses the structural information that Stirling High is an active school, and we lose the field configurations of the 400m race. Deleting an athlete's membership should not delete organizational structures.
*   **2 Marks (RDBMS Resolution):** An RDBMS breaks this single table into three related tables: `Athlete`, `School`, and `Event`. Deleting a row from `Athlete` has no effect on the records inside the `School` or `Event` tables, preserving information.

**Question 3 (5 Marks)**
*   **2 Marks (PK Issue):** If `(StudentID, BookID)` is the composite key, a student can borrow a specific book exactly *once* in the system's lifetime. If they return it and borrow it again next term, the RDBMS will reject the record as a duplicate primary key violation.
*   **3 Marks (Revised Schema Design):**  
    Introduce a transaction date or transactional ID field:  
    `LoanRecord(LoanID [INT, PK], StudentID [INT, FK], StudentName [TEXT], BookID [INT, FK], Title [TEXT], DateIssued [DATE])`  
    *(Alternatively, using `(StudentID, BookID, DateIssued)` as a composite primary key is acceptable).*

---

#### **Section 2 Solution Key**

**Marina Schema Design (8 Marks)**

**1. Table Schemas & Keys (4 Marks):**
*   **Table: Boat**  
    `BoatID` [INTEGER] (PK) | `BoatName` [TEXT] | `Length` [FLOAT]
*   **Table: Slip**  
    `SlipNo` [INTEGER] (PK) | `MaxWidth` [FLOAT]
*   **Table: SlipBooking**  
    `BookingID` [INTEGER] (PK) | `BoatID` [INTEGER] (FK references Boat) | `SlipNo` [INTEGER] (FK references Slip) | `StartDate` [DATE] | `EndDate` [DATE]

*(Marking: Deduct 1 Mark for missing datatypes, deduct 1 Mark for missing primary/foreign labels).*

**2. Enforcing Relationships (2 Marks):**
*   **1 Mark:** The `SlipBooking` table acts as the relational bridge linking the `Boat` and `Slip` tables.
*   **1 Mark:** Relational referential integrity is enforced because the RDBMS will reject a booking if a non-existent `BoatID` or `SlipNo` is inputted, ensuring complete database accuracy.

**3. Redundancy Prevention Justification (2 Marks):**
*   **1 Mark:** Boat specifications (e.g. Boat Name, Length) are stored exactly **once** inside the parent `Boat` table.
*   **1 Mark:** When a boat books a slip multiple times, we only record its numeric `BoatID` in the booking table. The system does not repeat boat descriptions or measurements across booking logs, reducing database size and eliminating update anomalies.
