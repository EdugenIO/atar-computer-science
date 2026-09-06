# Unit 2 — Chapter 15: Database Normalisation & Integrity

This chapter explores the logical design and systematic refinement of relational databases. Storing data is not simply a matter of dumping fields into a single flat file or spreadsheet. To build reliable, scaleable, and secure information systems, database developers must understand the mathematical and structural principles of **normalisation** and **data integrity**.

You will learn to identify and explain operational **data anomalies** (insert, update, and delete anomalies), apply the systematic process of normalising data from an un-normalised form (UNF) through to **First Normal Form (1NF)**, **Second Normal Form (2NF)**, and **Third Normal Form (3NF)** for schemas comprising three to four tables, and evaluate systems against the core factors of **data integrity** (currency, authenticity, accuracy, and relevance).

These concepts are critical for designing robust systems, preventing data corruption, and excel in the theoretical and practical components of **SCSA School-Based Assessment Task 6 (The Relational Database Project)** and semester examinations.

---

## Lesson 15.1: Data Anomalies

### Your Goal
Identify, describe, and explain **insert, update, and delete anomalies** in flat-file or un-normalised datasets, and analyze their impact on database operations.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 13.2: Flat File vs Relational Database](./year-11-textbook-chapter-13.md#lesson-132-flat-file-vs-relational-database).
*   [Lesson 13.3: Core Database Concepts & Hierarchy](./year-11-textbook-chapter-13.md#lesson-133-core-database-concepts--hierarchy) (specifically understanding tables, records, and fields).

### The Idea
When we store different types of entities—such as ovals, events, and athletes—in a single flat spreadsheet, we force the database engine to repeat the same information across multiple rows. This redundancy is not just a waste of storage space; it introduces operational defects known as **data anomalies**.

There are three types of data anomalies that occur when trying to modify flat or poorly designed tables:

1.  **Insert Anomaly:** A state where you cannot record new data because it is dependent on the existence of other, unrelated data that does not yet exist.
    *   *Analogy:* You cannot write down the details of a newly upgraded sports oval because the school hasn't registered any athletes to run on it yet, and the spreadsheet requires an athlete to create a row.
2.  **Update Anomaly:** A state where a change to a single fact must be manually repeated across multiple rows. If even one row is missed, the database becomes inconsistent.
    *   *Analogy:* If the coordinator of "Gold House" changes their mobile phone number, you have to find and update all 150 rows where an athlete from Gold House is listed.
3.  **Delete Anomaly:** A state where deleting a record to remove one fact unintentionally destroys a completely different, unique fact that you wished to preserve.
    *   *Analogy:* Deleting the single athlete registered for the "Shot Put" event because they withdrew from the carnival accidentally deletes the event's duration and scoring rules from the system entirely.

#### **SCSA Key Terms**
*   **Data Redundancy:** The unnecessary repetition of data within a database.
*   **Insert Anomaly:** The inability to insert data because other dependent data is missing.
*   **Update Anomaly:** Inconsistency resulting from a data update not being applied uniformly to all duplicate records.
*   **Delete Anomaly:** The unintentional loss of unique data when a record is deleted.

---

### See It Worked
#### **The Scenario**
Below is a portion of a flat-file spreadsheet used by the volunteer coordinators of the **WA Junior Sports Carnival** to record events, locations, and athlete assignments:

| AthleteID | AthleteName | HouseName | EventCode | EventName | OvalName | OvalCoordinator |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 104 | Riley Smith | Red | E101 | 100m Sprint | Main Track | Mr. Henderson |
| 105 | Chloe Patel | Blue | E101 | 100m Sprint | Main Track | Mr. Henderson |
| 106 | Jaxson Wong | Red | E102 | Shot Put | Field North | Mrs. Kovac |
| 107 | Mia Robinson| Blue | E103 | High Jump | Field South | Mr. Davis |

Let's trace how this design triggers the three SCSA-defined anomalies:

#### **1. The Insert Anomaly**
*   **The Goal:** The committee wants to add a new event to the carnival: **E104 (Javelin)**, to be held at **Field North** coordinated by **Mrs. Kovac**.
*   **The Problem:** Because this is a single flat sheet, to add E104, we must create a row. However, no athletes have registered for Javelin yet! The database requires a primary identifier (like `AthleteID`) to create a record. We cannot insert the new event without fabricating a "fake" athlete, resulting in an **insert anomaly**.

#### **2. The Update Anomaly**
*   **The Goal:** The coordinator of the **Main Track**, **Mr. Henderson**, resigns and is replaced by **Ms. Liang**.
*   **The Problem:** To update this fact, we cannot change a single cell. We must write a query or manually update every single row where an event is scheduled on the Main Track (rows 1 and 2 in our snippet, and potentially hundreds of others in the full file). If we update row 1 but miss row 2, the database lists two different coordinators for the same physical oval, resulting in an **update anomaly**.

#### **3. The Delete Anomaly**
*   **The Goal:** Athlete **107 (Mia Robinson)** injures her ankle and withdraws from the carnival. The registrar deletes her row to cancel her registration.
*   **The Problem:** Deleting Mia’s row (the fourth row) removes her details from the database. However, because she was the *only* athlete registered for the **High Jump (E103)** at **Field South**, deleting her row also erases the fact that E103 exists, that it is called High Jump, and that it is held on Field South coordinated by Mr. Davis. This unintentional loss of unique event data is a **delete anomaly**.

---

### Try It with Help
#### **The Problem**
A local West Australian school uses a flat-file database to track library textbook loans:

| StudentID | StudentName | BookBarcode | BookTitle | Subject | LoanDate | TeacherInCharge |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2045 | Caleb Miller | B901 | ATAR CS Y11 | Computer Science | 2026-02-05 | Mrs. Jenkins |
| 2045 | Caleb Miller | B902 | ATAR Math Methods | Mathematics | 2026-02-05 | Mr. Salinger |
| 3108 | Emily Chen  | B901 | ATAR CS Y11 | Computer Science | 2026-02-06 | Mrs. Jenkins |

Explain how this flat file exhibits:
1.  An **insert anomaly** when adding a new textbook named "ATAR Chemistry Y11" that has not yet been loaned.
2.  An **update anomaly** if Mrs. Jenkins changes her room number (which is currently tied to her teacher record).
3.  A **delete anomaly** if Emily Chen returns book `B901` and her loan record is deleted.

#### **Structural Hints**
*   For the *insert anomaly*: Think about whether a book row can exist in this table without a `StudentID`.
*   For the *update anomaly*: Look for repeated instances of Mrs. Jenkins and explain what happens if they are not all updated at once.
*   For the *delete anomaly*: Identify if Emily's record is the only link to any unique library facts.

#### **Scaffolded Student Guide**
*   *Insert:* "We cannot add a new textbook because there is no..."
*   *Update:* "Mrs. Jenkins' name appears multiple times. If we change her details in one row..."
*   *Delete:* "If Emily returns her book and we delete her record, we might lose..." (Wait, is Emily the only one borrowing B901? No, Caleb is too! But what if Emily was the only one? Trace carefully!)

---

### Try It Yourself
#### **The Problem**
An online registration system for an arcade amusement park in Perth records game plays in a flat table:

| CardNumber | PlayerName | ArcadeUnitID | GameName | CabinetType | HighScore | PlayDate |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| C101 | Sarah Connor | U501 | Pac-Man | Classic Standup | 85000 | 2026-03-01 |
| C102 | John Connor  | U502 | Galaga  | Table Cockpit  | 120000| 2026-03-01 |
| C101 | Sarah Connor | U502 | Galaga  | Table Cockpit  | 95000 | 2026-03-02 |
| C103 | Kyle Reese   | U503 | Donkey Kong | Classic Standup | 45000 | 2026-03-02 |

Draft a formal, structured evaluation (approx. 150 words) identifying and explaining concrete examples of **insert, update, and delete anomalies** that are structurally inherent to this table's design.

---

### Check Your Reasoning
#### **The Answer**
*   **Insert Anomaly:** The arcade cannot add a newly purchased physical cabinet (e.g., unit `U504`, running "Street Fighter") to the database until a customer scans their card and plays it. This is because the table is organized around card plays, and inserting a row without a `CardNumber` is impossible.
*   **Update Anomaly:** If Sarah Connor changes her `PlayerName` (e.g., after updating her profile name), this change must be manually repeated across every row containing `C101` (rows 1 and 3). If one row is missed, the database will contain conflicting, inconsistent names for the same card holder.
*   **Delete Anomaly:** If Kyle Reese requests his profile to be deleted and we remove the row for card `C103` (row 4), we completely erase physical machine `U503` (Donkey Kong, Classic Standup) from our arcade unit inventory, as this row contains the only record of its existence.

#### **Common SCSA Student Errors**
*   **Vague definitions:** Writing "An update anomaly is when you can't update data" will score zero marks. You must explain *why* (data redundancy forces manual multi-row updates, risking logical inconsistency).
*   **Confusing the terms:** Swapping the explanations of insert and delete anomalies. Remember: *Insert* is about missing parent data; *Delete* is about losing unintended data.

---

### Review and Connect
In this lesson, you analyzed the three operational threats of unstructured flat files. In the next lesson, we will begin the mathematical process of **normalisation** to systematically dismantle these anomalies by splitting our data into clean, logical tables.

---

## Lesson 15.2: Normalisation: UNF to 1NF

### Your Goal
Convert a dataset from Un-normalised Form (UNF) to **First Normal Form (1NF)** by ensuring value atomicity and defining a unique primary or composite key.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 13.3: Core Database Concepts & Hierarchy](./year-11-textbook-chapter-13.md#lesson-133-core-database-concepts--hierarchy) (specifically primary keys and composite keys).
*   [Lesson 14.2: Data Dictionaries](./year-11-textbook-chapter-14.md#lesson-14-data-dictionaries).

### The Idea
The normalisation process is a step-by-step structural progression designed to eliminate data redundancy and prevent operational anomalies. We begin this process at the absolute bottom: **Un-normalised Form (UNF)**.

A table is in **Un-normalised Form (UNF)** if it contains **repeating groups** or **non-atomic attributes**.
*   **Repeating Groups:** Multiple fields of the same type in a single row (e.g., `Event1`, `Event2`, `Event3` columns).
*   **Non-Atomic Attributes:** Multiple data values packed into a single cell, separated by commas or slashes (e.g., an "EventNames" cell containing `"100m Sprint, Shot Put, High Jump"`). This violates the principle of **atomicity** (data values must be indivisible).

To transition a table from UNF to **First Normal Form (1NF)**, you must apply three rules:
1.  **Flatten the Table:** Remove all repeating groups and comma-separated lists, expanding the dataset so that every cell contains exactly *one* atomic value.
2.  **Ensure Uniformity:** Every row must have the same structural layout and column definitions.
3.  **Establish a Primary Key:** Define a unique identifier (or a combination of fields forming a **Composite Primary Key**) that can uniquely identify every single row in the flattened table.

**The Analogy:**
Imagine a student writing down their class schedule on an index card:
`Sarah: [Methods, English, Physics]`
To store this in a computer-readable structure, we cannot have a single row containing a list. We must "flatten" it so that Sarah has three distinct, atomic rows:
*   `Sarah, Methods`
*   `Sarah, English`
*   `Sarah, Physics`

#### **SCSA Key Terms**
*   **Un-normalised Form (UNF):** Data organized with repeating groups or non-atomic data values.
*   **First Normal Form (1NF):** A relation with no repeating groups or multi-valued attributes, where every attribute is atomic, and a unique primary or composite key has been established.
*   **Atomicity:** The property of a data value that represents an indivisible, single unit of information.

---

### See It Worked
#### **The Scenario**
Below is a messy registration sheet (UNF) from the **WA Junior Sports Carnival** registrar. Notice the non-atomic, comma-separated lists of events and ovals under each student's name:

| StudentID | StudentName | HouseName | RegisteredEvents (UNF) | Ovals (UNF) |
| :--- | :--- | :--- | :--- | :--- |
| 104 | Riley Smith | Red | 100m Sprint, Shot Put | Main Track, Field North |
| 105 | Chloe Patel | Blue | High Jump | Field South |
| 106 | Jaxson Wong | Red | 100m Sprint, High Jump, Javelin | Main Track, Field South, Field North |

#### **The Transition to 1NF**
To normalise this to 1NF, we must:
1.  Split the multi-value fields into individual rows (flattening).
2.  Repeat the parent fields (`StudentID`, `StudentName`, `HouseName`) for each row.
3.  Designate a primary identifier. Because a `StudentID` is no longer unique on its own (it appears multiple times now), we must create a **Composite Primary Key** combining `StudentID` and `RegisteredEvents` (underlined below).

#### **The 1NF Relational Table**

| **<u>StudentID</u>** | StudentName | HouseName | **<u>RegisteredEvents</u>** | Oval |
| :--- | :--- | :--- | :--- | :--- |
| **<u>104</u>** | Riley Smith | Red | **<u>100m Sprint</u>** | Main Track |
| **<u>104</u>** | Riley Smith | Red | **<u>Shot Put</u>** | Field North |
| **<u>105</u>** | Chloe Patel | Blue | **<u>High Jump</u>** | Field South |
| **<u>106</u>** | Jaxson Wong | Red | **<u>100m Sprint</u>** | Main Track |
| **<u>106</u>** | Jaxson Wong | Red | **<u>High Jump</u>** | Field South |
| **<u>106</u>** | Jaxson Wong | Red | **<u>Javelin</u>** | Field North |

#### **Why this is in 1NF**
*   All cell values are **atomic** (e.g., there are no commas or nested lists).
*   There are **no repeating columns** (e.g., no `Event1`, `Event2` structures).
*   A unique **Composite Primary Key** has been established: `(StudentID, RegisteredEvents)`. For example, the combination `(104, "Shot Put")` appears exactly once in the entire table.

---

### Try It with Help
#### **The Problem**
A school sports team's equipment roster is recorded in the following un-normalised form (UNF):

| TeamID | CoachName | EquipmentItems | ItemQuantities |
| :--- | :--- | :--- | :--- |
| T01 | Coach Ken | Baseballs, Bat, Helmets | 12, 2, 6 |
| T02 | Coach Barb| Volleyballs, Net | 8, 1 |

Convert this table into **First Normal Form (1NF)**.

#### **Structural Hints**
*   Ensure that the comma-separated items under `EquipmentItems` and `ItemQuantities` are expanded into separate records.
*   Make sure that `ItemQuantities` values align correctly with their matching items (e.g., 12 Baseballs, 2 Bats).
*   Determine what combination of fields must be designated as the **Composite Primary Key** to ensure uniqueness.

#### **Scaffolded Template**
```
| TeamID (PK/FK?) | CoachName | EquipmentItems (PK/FK?) | ItemQuantities |
| :--- | :--- | :--- | :--- |
| T01 | Coach Ken | Baseballs | 12 |
| T01 | ... | ... | ... |
```

---

### Try It Yourself
#### **The Problem**
The sports registrar records high school swimming trial matches in this un-normalised sheet (UNF):

| SchoolCode | SchoolName | Coach | SwimmerNames | SwimmerAges | SwimmerTimes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| S10 | Hale School | Mr. Roy | Liam, Ryan | 16, 17 | 54.2, 56.5 |
| S20 | Trinity Coll | Mr. Lee | Noah, Ethan, Owen | 15, 17, 16 | 58.1, 55.4, 59.2 |

Convert this dataset into a single table in **First Normal Form (1NF)**. Clearly specify:
1.  The complete 1NF data table layout.
2.  The defined Primary Key or Composite Primary Key (using standard underline notation).
3.  Why your resulting schema satisfies SCSA guidelines for 1NF.

---

### Check Your Reasoning
#### **The Answer**
**1. The 1NF Data Table:**

| **<u>SchoolCode</u>** | SchoolName | Coach | **<u>SwimmerName</u>** | SwimmerAge | SwimmerTime |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **<u>S10</u>** | Hale School | Mr. Roy | **<u>Liam</u>** | 16 | 54.2 |
| **<u>S10</u>** | Hale School | Mr. Roy | **<u>Ryan</u>** | 17 | 56.5 |
| **<u>S20</u>** | Trinity Coll | Mr. Lee | **<u>Noah</u>** | 15 | 58.1 |
| **<u>S20</u>** | Trinity Coll | Mr. Lee | **<u>Ethan</u>** | 17 | 55.4 |
| **<u>S20</u>** | Trinity Coll | Mr. Lee | **<u>Owen</u>** | 16 | 59.2 |

**2. Key Designation:**
*   Composite Primary Key: `(SchoolCode, SwimmerName)`

**3. Rationale for 1NF Compliance:**
*   **Value Atomicity:** All multi-valued comma-separated arrays under `SwimmerNames`, `SwimmerAges`, and `SwimmerTimes` have been split into discrete cells. No nested structures exist.
*   **Row Uniformity:** Each row contains exactly one structured record.
*   **Unique Identifier:** The composite primary key `(SchoolCode, SwimmerName)` uniquely identifies every record in the table, preventing duplicates.

#### **Common SCSA Student Errors**
*   **Partial Atomicity:** Splitting the swimmer names but leaving the swimmer times as comma-separated lists. *All* columns must be split to achieve true atomicity.
*   **Selecting a single column primary key:** Selecting `SchoolCode` alone as the primary key. This is incorrect because `SchoolCode` repeats multiple times in the 1NF table.

---

### Review and Connect
You have successfully converted messy un-normalised arrays into atomic 1NF structures. However, our new table is heavily redundant—the school name and coach are repeated multiple times. In the next lesson, we will solve this issue by stepping up to **Second Normal Form (2NF)**.

---

## Lesson 15.3: Normalisation: 1NF to 2NF

### Your Goal
Identify and remove **partial dependencies** from a 1NF table to decompose it into multiple tables conforming to **Second Normal Form (2NF)**.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 15.2: Normalisation: UNF to 1NF](./year-11-textbook-chapter-15.md#lesson-152-normalisation-unf-to-1nf).
*   [Lesson 13.3: Core Database Concepts & Hierarchy](./year-11-textbook-chapter-13.md#lesson-133-core-database-concepts--hierarchy) (specifically primary keys vs. foreign keys).

### The Idea
Even when a table is in First Normal Form (1NF), it can still suffer from significant data redundancy. If a table uses a **Composite Primary Key**, we often find that some non-key fields do not depend on the *entire* composite key. Instead, they depend on only *one part* of it. This logical error is called a **partial dependency**.

To transition from 1NF to **Second Normal Form (2NF)**, you must apply two rules:
1.  The table must already be in **First Normal Form (1NF)**.
2.  You must remove all **partial dependencies**. 

Any attribute that depends on only a portion of the composite key must be extracted and placed into its own separate table, linked back to the original using a **Foreign Key**.

**The Analogy:**
Imagine a composite key consisting of `(LibraryCardID, BookBarcode)`. 
*   The field `BorrowDate` depends on *both* the card and the book (who borrowed what, and when). This is a **full dependency**.
*   The field `UserEmail` depends *only* on the `LibraryCardID`. It does not change based on what book is borrowed. This is a **partial dependency**.
*   To reach 2NF, we must extract user details into their own `User` table, leaving only the loan transaction in the `Borrow` table.

> **Crucial Rule:** Any table in 1NF that has a **single-column primary key** (not a composite key) is **automatically in 2NF** because it is mathematically impossible to have a partial dependency on a single attribute!

#### **SCSA Key Terms**
*   **Second Normal Form (2NF):** A relation that is in First Normal Form and contains no partial dependencies (every non-key attribute is fully functionally dependent on the entire primary key).
*   **Dependency:** A relationship between attributes where the value of one attribute determines the value of another.
*   **Partial Dependency:** A dependency where a non-key attribute is functionally dependent on only *part* of a composite primary key.

---

### See It Worked
#### **The Scenario**
Let's analyze our 1NF table from the **WA Junior Sports Carnival** from Lesson 15.2:

*   **Composite Primary Key:** `(StudentID, RegisteredEvents)`
*   **Non-Key Attributes:** `StudentName`, `HouseName`, `Oval`

Let's evaluate the functional dependencies of our non-key fields:
1.  Does `StudentName` depend on *both* `StudentID` and `RegisteredEvents`? No! Riley Smith is named Riley Smith regardless of whether he registers for Shot Put or 100m Sprint. `StudentName` depends solely on `StudentID`. This is a **partial dependency**.
2.  Does `HouseName` depend on *both*? No. A student’s house assignment is tied strictly to their `StudentID`, not their sports selection. This is a **partial dependency**.
3.  Does `Oval` depend on *both*? Yes. An event is held on a specific oval (e.g. 100m Sprint on Main Track). To know which oval to go to, you must know the specific `RegisteredEvents` value. `Oval` depends on the `RegisteredEvents` portion of the key. This is a **partial dependency**.

#### **Decomposing to 2NF**
To resolve these partial dependencies, we split our single 1NF table into three separate, cohesive tables:

**1. STUDENT Table** (Primary Key: `StudentID`)
*   *Note:* Single-column primary key $ightarrow$ Automatically in 2NF.

| **<u>StudentID</u>** | StudentName | HouseName |
| :--- | :--- | :--- |
| **<u>104</u>** | Riley Smith | Red |
| **<u>105</u>** | Chloe Patel | Blue |
| **<u>106</u>** | Jaxson Wong | Red |

**2. EVENT Table** (Primary Key: `RegisteredEvents` / `EventName`)
*   *Note:* Single-column primary key $ightarrow$ Automatically in 2NF.

| **<u>EventName</u>** | Oval |
| :--- | :--- |
| **<u>100m Sprint</u>** | Main Track |
| **<u>Shot Put</u>** | Field North |
| **<u>High Jump</u>** | Field South |
| **<u>Javelin</u>** | Field North |

**3. REGISTRATION Table** (Composite Primary Key: `StudentID` + `EventName`)
*   *Note:* Tracks who is signed up for what event. Every attribute here is fully dependent on the composite key.

| **<u>StudentID (FK)</u>** | **<u>EventName (FK)</u>** |
| :--- | :--- |
| **<u>104</u>** | **<u>100m Sprint</u>** |
| **<u>104</u>** | **<u>Shot Put</u>** |
| **<u>105</u>** | **<u>High Jump</u>** |
| **<u>106</u>** | **<u>100m Sprint</u>** |
| **<u>106</u>** | **<u>High Jump</u>** |
| **<u>106</u>** | **<u>Javelin</u>** |

---

### Try It with Help
#### **The Problem**
A textbook hire library uses a 1NF table:

| **<u>BorrowerID</u>** | **<u>TextbookBarcode</u>** | BorrowerName | CardStatus | Title | Subject | ReturnDate |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **<u>B101</u>** | **<u>TX88</u>** | Sam Jones | Active | Yr 11 CS ATAR | Computer Science | 2026-11-20 |
| **<u>B101</u>** | **<u>TX99</u>** | Sam Jones | Active | Methods Unit 1 | Mathematics | 2026-11-21 |
| **<u>B102</u>** | **<u>TX88</u>** | Lily Evans | Blocked | Yr 11 CS ATAR | Computer Science | 2026-11-20 |

Decompose this table into **Second Normal Form (2NF)**.

#### **Structural Hints**
*   Identify the composite primary key: `(BorrowerID, TextbookBarcode)`.
*   Determine which non-key fields depend on `BorrowerID` alone (e.g., `BorrowerName`, `CardStatus`).
*   Determine which non-key fields depend on `TextbookBarcode` alone (e.g., `Title`, `Subject`).
*   Determine which non-key fields depend on *both* parts of the key (e.g., `ReturnDate`).
*   Decompose the single table into three 2NF tables: `BORROWER`, `TEXTBOOK`, and `LOAN`.

---

### Try It Yourself
#### **The Problem**
An online registration program tracking regional sports teams in WA uses a 1NF table schema:

| **<u>TeamCode</u>** | **<u>SponsorID</u>** | TeamName | Division | HomeGround | SponsorName | SponsorPhone | AllocationDate |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **<u>T01</u>** | **<u>SP50</u>** | Joondalup Giants | Under-16 | Arena North | Westcorp | 0893001122 | 2026-03-01 |
| **<u>T01</u>** | **<u>SP60</u>** | Joondalup Giants | Under-16 | Arena North | Suncorp  | 0892004455 | 2026-03-05 |
| **<u>T02</u>** | **<u>SP50</u>** | Fremantle Dockers| Under-18 | South Oval  | Westcorp | 0893001122 | 2026-03-01 |

Apply the normalisation process to convert this 1NF schema into **Second Normal Form (2NF)** relations. For your final submission:
1.  Identify the partial dependencies present in the 1NF table.
2.  Present the schemas for the new decomposed 2NF tables (using standard underline notation for primary keys).
3.  Explain why your decomposed tables now conform to SCSA 2NF specifications.

---

### Check Your Reasoning
#### **The Answer**
**1. Identified Partial Dependencies:**
*   `TeamName`, `Division`, and `HomeGround` depend solely on `TeamCode` (part of the composite primary key).
*   `SponsorName` and `SponsorPhone` depend solely on `SponsorID` (part of the composite primary key).
*   Only `AllocationDate` is fully dependent on the entire composite key `(TeamCode, SponsorID)`.

**2. 2NF Decomposed Schema:**

*   **TEAM Table** (Primary Key: `TeamCode`)
    *   `TEAM(`<u>TeamCode</u>, TeamName, Division, HomeGround`)`
*   **SPONSOR Table** (Primary Key: `SponsorID`)
    *   `SPONSOR(`<u>SponsorID</u>, SponsorName, SponsorPhone`)`
*   **SPONSORSHIP_ALLOCATION Table** (Composite Primary Key: `TeamCode` + `SponsorID`)
    *   `ALLOCATION(`<u>TeamCode (FK)</u>, <u>SponsorID (FK)</u>, AllocationDate`)`

**3. Rationale for 2NF Compliance:**
*   The tables are in 1NF (atomic values, no repeating columns).
*   All partial dependencies have been removed. Every non-key attribute in the `TEAM` and `SPONSOR` tables is fully dependent on their single-column primary keys.
*   In the associative `ALLOCATION` table, the only non-key attribute (`AllocationDate`) requires the *entire* composite key combination of `TeamCode` and `SponsorID` to determine its value.

#### **Common SCSA Student Errors**
*   **Forgetting foreign key links:** Decomposing tables but failing to leave the composite keys in the associative table. If you delete `TeamCode` or `SponsorID` from the link table, you destroy the relationship entirely.
*   **Incorrectly grouping transitive attributes:** Leaving `SponsorName` inside the `TEAM` table.

---

### Review and Connect
By removing partial dependencies, you decomposed the data into distinct entity tables. However, we still have redundant columns where non-key fields depend on *other* non-key fields. In the next lesson, we will complete our journey by normalising to **Third Normal Form (3NF)**.

---

## Lesson 15.4: Normalisation: 2NF to 3NF

### Your Goal
Identify and remove **transitive dependencies** from a 2NF schema to decompose it into multiple tables conforming to **Third Normal Form (3NF)**.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 15.3: Normalisation: 1NF to 2NF](./year-11-textbook-chapter-15.md#lesson-153-normalisation-1nf-to-2nf).
*   [Lesson 14.1: Crow's Foot Notation ERDs](./year-11-textbook-chapter-14.md#lesson-141-crows-foot-notation-erds).

### The Idea
Now that our tables are in Second Normal Form (2NF), all partial dependencies on composite keys have been eliminated. However, we can still have data redundancy within our single-column key tables. This occurs when a non-key attribute depends on another non-key attribute, rather than depending directly on the primary key. This is called a **transitive dependency**.

To transition from 2NF to **Third Normal Form (3NF)**, you must apply two rules:
1.  The tables must already be in **Second Normal Form (2NF)**.
2.  You must remove all **transitive dependencies**.

Any non-key attribute that depends on another non-key attribute must be extracted and placed into its own separate table, with the determining attribute serving as a **Foreign Key** in the original table.

**The Analogy:**
Imagine a `STUDENT` table with the fields:
`StudentID (PK) -> StudentName -> SchoolCode -> SchoolAddress`
*   `StudentName` depends directly on `StudentID`. (Full dependency)
*   `SchoolCode` depends directly on `StudentID` (which school the student attends). (Full dependency)
*   `SchoolAddress` depends on `SchoolCode`. It does not change based on which individual student is selected. It only changes if the school changes.
*   This is a transitive link: `StudentID -> SchoolCode -> SchoolAddress`.
*   To reach 3NF, we must extract school details into a separate `SCHOOL` table, leaving `SchoolCode` as a foreign key in the `STUDENT` table.

#### **SCSA Key Terms**
*   **Third Normal Form (3NF):** A relation that is in Second Normal Form and contains no transitive dependencies (no non-key attribute depends on any other non-key attribute).
*   **Transitive Dependency:** A functional dependency between two or more non-key attributes.
*   **Determinant:** Any attribute whose value determines the value of another attribute.

---

### See It Worked
#### **The Scenario**
Let's analyze our 2NF **STUDENT** table from Lesson 15.3:

*   **Primary Key:** `StudentID`
*   **Non-Key Attributes:** `StudentName`, `HouseName`

What if the school registrar adds two more columns to track sports houses: **HouseColour** and **HouseMaster**?

| **<u>StudentID</u>** | StudentName | HouseName | HouseColour | HouseMaster |
| :--- | :--- | :--- | :--- | :--- |
| **<u>104</u>** | Riley Smith | Red | Scarlet | Mr. Henderson |
| **<u>105</u>** | Chloe Patel | Blue | Sapphire | Ms. Liang |
| **<u>106</u>** | Jaxson Wong | Red | Scarlet | Mr. Henderson |

Let's evaluate the functional dependencies in this table:
1.  Does `StudentName` depend on `StudentID`? Yes.
2.  Does `HouseName` depend on `StudentID`? Yes, each student is assigned to one house.
3.  Does `HouseColour` depend directly on `StudentID`? No. The house colour is determined by the *sports house* itself. If you change houses, your colour changes.
4.  Does `HouseMaster` depend directly on `StudentID`? No. The housemaster is determined by the *sports house*.
5.  This is a **transitive dependency**: `StudentID -> HouseName -> HouseColour / HouseMaster`.

#### **Decomposing to 3NF**
To resolve this transitive dependency, we extract the sports house attributes into their own relation, leaving `HouseName` behind as a **Foreign Key**:

**1. HOUSE Table** (Primary Key: `HouseName`)

| **<u>HouseName</u>** | HouseColour | HouseMaster |
| :--- | :--- | :--- |
| **<u>Red</u>** | Scarlet | Mr. Henderson |
| **<u>Blue</u>** | Sapphire | Ms. Liang |

**2. STUDENT Table** (Primary Key: `StudentID`, Foreign Key: `HouseName`)

| **<u>StudentID</u>** | StudentName | HouseName (FK) |
| :--- | :--- | :--- |
| **<u>104</u>** | Riley Smith | Red |
| **<u>105</u>** | Chloe Patel | Blue |
| **<u>106</u>** | Jaxson Wong | Red |

#### **Why this is in 3NF**
*   The tables are in 2NF.
*   All transitive dependencies have been removed. Every non-key attribute (e.g. `StudentName`, `HouseColour`) depends directly and *only* on the primary key of its table.

---

### Try It with Help
#### **The Problem**
A database tracking regional athletics events is in 2NF:

| **<u>EventCode</u>** | EventName | CategoryCode | CategoryName | CategoryAgeLimit |
| :--- | :--- | :--- | :--- | :--- |
| **<u>E101</u>** | 100m Sprint | CAT-A | Junior Track | Under-12 |
| **<u>E102</u>** | Shot Put | CAT-B | Senior Field | Under-18 |
| **<u>E103</u>** | 200m Sprint | CAT-A | Junior Track | Under-12 |

Decompose this table into **Third Normal Form (3NF)**.

#### **Structural Hints**
*   Identify the transitive path: `EventCode` determines `CategoryCode`, which in turn determines `CategoryName` and `CategoryAgeLimit`.
*   Extract the category details into a separate `CATEGORY` table with `CategoryCode` as the primary key.
*   Leave `CategoryCode` as a foreign key in the original `EVENT` table to preserve the relationship.

---

### Try It Yourself
#### **The Problem**
A database table recording WA Junior Sports Carnival school affiliations is in 2NF:

| **<u>SchoolCode</u>** | SchoolName | PrincipalID | PrincipalName | PrincipalEmail |
| :--- | :--- | :--- | :--- | :--- |
| **<u>S10</u>** | Hale School | P901 | Dr. C. J. Hill | c.hill@hale.wa.edu.au |
| **<u>S20</u>** | Trinity College | P902 | Mr. D. A. Banks| d.banks@trinity.wa.edu.au|
| **<u>S30</u>** | Wesley College | P901 | Dr. C. J. Hill | c.hill@hale.wa.edu.au |

Apply the normalisation process to convert this 2NF schema into **Third Normal Form (3NF)** relations. For your final submission:
1.  Identify the transitive dependencies present in the table.
2.  Present the schemas for the new decomposed 3NF tables (using standard underline notation for primary keys).
3.  Explain why your decomposed tables now conform to SCSA 3NF specifications.

---

### Check Your Reasoning
#### **The Answer**
**1. Identified Transitive Dependency:**
*   The attributes `PrincipalName` and `PrincipalEmail` depend functionally on the non-key attribute `PrincipalID`, which in turn depends on the primary key `SchoolCode`.
*   Transitive Path: `SchoolCode -> PrincipalID -> PrincipalName, PrincipalEmail`.

**2. 3NF Decomposed Schema:**

*   **PRINCIPAL Table** (Primary Key: `PrincipalID`)
    *   `PRINCIPAL(`<u>PrincipalID</u>, PrincipalName, PrincipalEmail`)`
*   **SCHOOL Table** (Primary Key: `SchoolCode`, Foreign Key: `PrincipalID`)
    *   `SCHOOL(`<u>SchoolCode</u>, SchoolName, PrincipalID (FK)`)`

**3. Rationale for 3NF Compliance:**
*   The tables are in 2NF.
*   The transitive dependency has been eliminated. The attributes `PrincipalName` and `PrincipalEmail` are now in the `PRINCIPAL` table, depending directly on the primary key `PrincipalID`. The `SCHOOL` table now only holds fields directly related to the school, using `PrincipalID` as a foreign key link to connect the two tables without redundancy.

#### **Common SCSA Student Errors**
*   **Deleting the linking key entirely:** Decomposing the tables but failing to leave `PrincipalID` in the `SCHOOL` table. This breaks the logical connection between the school and its principal.
*   **Retaining redundant fields:** Leaving `PrincipalName` in both tables. Only the foreign key (`PrincipalID`) should remain in the parent table.

---

### Review and Connect
Congratulations! You have mastered database normalisation from UNF to 3NF. In the final lesson of this chapter, we will learn how to evaluate and protect our newly designed database using **data integrity** factors.

---

## Lesson 15.5: Data Integrity Factors

### Your Goal
Evaluate and maintain database quality by applying the four factors of **data integrity**: **currency, authenticity, accuracy, and relevance**.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 10.2: Privacy Act 1988 & Australian Privacy Principles (APPs)](./year-11-textbook-chapter-10.md#lesson-102-privacy-act-1988--australian-privacy-principles-apps).
*   [Lesson 13.3: Core Database Concepts & Hierarchy](./year-11-textbook-chapter-13.md#lesson-133-core-database-concepts--hierarchy).

### The Idea
Designing a normalised 3NF database schema is a massive step forward, but a database is only as good as the actual data stored inside it. If users input fake, outdated, or corrupted values, the system will fail to provide useful information.

To prevent this, computer scientists evaluate database design against the four standard **SCSA Data Integrity Factors**:

| Factor | Description | Implementation Strategy |
| :--- | :--- | :--- |
| **Currency** | How up-to-date and timely the stored data is in relation to real-world events. | Implement date/time stamps (e.g., `LastUpdated` columns) and archiving protocols. |
| **Authenticity** | The degree to which data can be verified as genuine and originating from a trusted, authorized source. | Use digital signatures, role-based access logs (AAA framework), and secure user authentication. |
| **Accuracy** | The degree to which data is correct, precise, and free from error. | Enforce structural validation rules, drop-down menus, and data dictionaries. |
| **Relevance** | The degree to which the stored data is useful and directly applicable to the functional purpose of the system. | Enforce strict data-minimization policies (APP compliance) and discard unnecessary fields. |

**The Analogy:**
Imagine a passport application database:
*   If your address is 10 years out of date, the database lacks **currency**.
*   If anyone can upload a digital photo without identity verification, it lacks **authenticity**.
*   If your birthdate is typed in as "1895" instead of "1995" due to a typo, it lacks **accuracy**.
*   If the system asks you to input your favorite movie genre, it lacks **relevance**.

#### **SCSA Key Terms**
*   **Data Integrity:** The maintenance of, and the assurance of, data accuracy and consistency over its entire life-cycle.
*   **Currency:** The timeliness of data.
*   **Authenticity:** The genuineness and verification of data origin.
*   **Accuracy:** The correctness of data.
*   **Relevance:** The applicability and usefulness of data to the system's purpose.

---

### See It Worked
#### **The Scenario**
The **WA Junior Sports Carnival** registrar is building an SQLite database to manage track results. To ensure maximum data integrity, they implement validation controls directly into the schema.

Let's look at the schema design in SQLite:

```sql
CREATE TABLE AthleteResults (
    ResultID INTEGER PRIMARY KEY AUTOINCREMENT,
    AthleteID INTEGER,
    EventCode TEXT,
    RaceTime REAL,
    RunDate TEXT DEFAULT CURRENT_DATE, -- Ensures CURRENCY
    RecordedBy TEXT,
    -- Enforces ACCURACY: Times cannot be negative or physically impossible
    CONSTRAINT Check_Time CHECK (RaceTime > 5.00 AND RaceTime < 300.00),
    FOREIGN KEY(AthleteID) REFERENCES Athlete(AthleteID) -- Referential Integrity
);
```

#### **How this SQL Enforces Data Integrity:**
1.  **Accuracy:** The `CHECK` constraint ensures that no user can accidentally type a race time of `-12.5` seconds or `9999.0` seconds. If they attempt to do so, SQLite rejects the entry.
2.  **Currency:** The `DEFAULT CURRENT_DATE` automatic timestamp ensures that the database records *exactly* when the race took place, preventing stale data.
3.  **Referential Integrity (Accuracy):** The `FOREIGN KEY` constraint ensures that no result can be logged for an `AthleteID` that does not exist in the master `Athlete` table.

---

### Try It with Help
#### **The Problem**
A regional high school records student medical records. The IT support team conducts an audit of their database and discovers the following four issues:
1.  A student's emergency contact phone number has been entered as `"abc-1234"`.
2.  A student's diabetic medication requirements listed on their profile date back to 2018 and have not been reviewed.
3.  An external volunteer was able to modify a student's allergy log without logging in or verifying their credentials.
4.  The database stores every student's favorite video game and shoe size.

Identify which **data integrity factor** has been compromised in each scenario and suggest a technical fix.

#### **Structural Hints**
*   *Issue 1:* Considers the format of telephone characters (accuracy vs. relevance).
*   *Issue 2:* Deals with historical data that has not been updated (currency).
*   *Issue 3:* Deals with verifying who entered the data and their permissions (authenticity).
*   *Issue 4:* Deals with storing unneeded, non-applicable data (relevance).

---

### Try It Yourself
#### **The Problem**
A local WA medical practice is upgrading its patient check-in database. The practice coordinator asks you to write a design brief justifying how the system will protect the four SCSA data integrity factors during patient intake.

Write a structured response (approx. 200 words) detailing:
1.  How you will technically enforce **accuracy** and **authenticity** at the check-in terminal.
2.  How you will maintain **currency** and **relevance** as patient records age.

---

### Check Your Reasoning
#### **The Answer**
*   **Accuracy:** We will implement strict input masks and validation rules at the check-in terminal (e.g. forcing date-of-birth fields to match valid date ranges, and using drop-down selectors for medications rather than raw text fields).
*   **Authenticity:** Patients must verify their identity using a secure SMS code or a physical Medicare card scan. Staff modifications to patient charts will require individual user accounts, logging every transaction to track the trusted source of any modifications (AAA accounting).
*   **Currency:** The database will prompt patients to confirm or update their contact details annually upon login. Stale check-in records will feature a `LastVerifiedDate` timestamp to flag records requiring immediate review.
*   **Relevance:** The database will employ data-minimization practices by only collecting medical history details relevant to active treatments. Fields asking for hobbies or general employment details will be eliminated to comply with APP relevance guidelines.

#### **Common SCSA Student Errors**
*   **Confusing Accuracy and Authenticity:** Stating that a password ensures accuracy. A password verifies *who* you are (authenticity); it does not stop you from typing in a spelling mistake (accuracy).
*   **Confusing Currency with Security:** Believing currency refers to cash or banking transactions. In computer science, **currency** refers exclusively to the timeliness and freshness of data.

---

### Review and Connect
In this chapter, you mastered the logical progression of database normalisation from UNF to 3NF, dismantled data anomalies, and analyzed the factors that protect database quality. You are now fully prepared to write SQL queries to construct and manage these tables in **Chapter 16: SQL Implementation**.

---

## Teacher Support Module

### **SCSA Syllabus Mapping**
*   **Unit 2 — Database Solutions:**
    *   *SCSA Syllabus Code*: Know the process to normalise data to 3NF.
    *   *SCSA Syllabus Code*: Apply the process to normalise data to 3NF (three to four tables): normalise data to 1NF, 2NF, 3NF.
    *   *SCSA Syllabus Code*: Data anomalies: insert, update, delete.
    *   *SCSA Syllabus Code*: Data integrity: currency, authenticity, accuracy, relevance.

### **Prerequisite Knowledge Diagnostic**
Before starting Chapter 15, ensure students can:
1.  Explain what a primary key is and identify a composite key in a table structure.
2.  Read and interpret basic entities and attributes in a logical schema.

### **Classroom Misconception Busters**
1.  **The "1-column 2NF" shortcut:** Students often struggle to determine if a 1NF table is in 2NF. Teach them this absolute rule: *If the 1NF table has a single-column primary key, it contains zero partial dependencies and is automatically in 2NF!*
2.  **"Data Integrity" is not "Security":** Students often write "encrypting data makes it accurate." Explain that encryption prevents unauthorized reading (confidentiality) but does not stop a user from entering wrong numbers (accuracy).
3.  **The Transitive Key Fallacy:** Students sometimes think that any relationship between tables is a transitive dependency. Emphasize that a transitive dependency is a relationship between *non-key* attributes *within* a single table.

### **Classroom Discussion Starters**
*   "If normalisation reduces data redundancy by splitting tables, why might some real-world enterprise databases choose to 'de-normalise' (combine tables) for high-performance applications?" (Focus: Relational JOIN operations require processing power; sometimes speed beats storage savings).
*   "How does the Australian Privacy Principle 11 (Security of personal information) connect directly to our data integrity factors?"

---

## Classroom Assessment Task
### **Chapter 15 Theory Quiz — Relational Normalisation & Integrity**

**Assessment Type:** Theory Test  
**Time Allowed:** 25 Minutes  
**Total Marks:** 20 Marks  

---

#### **Question 1: Data Anomalies (4 Marks)**
An online WA sports equipment store stores all rental bookings in a single flat-file spreadsheet:

`RentalBooking(`<u>BookingID</u>, CustomerName, CustomerEmail, EquipmentID, Category, RentalRate, ReturnDate`)`

Describe how this flat table is vulnerable to:
*   An **insert anomaly** when purchasing new inventory (2 Marks).
*   A **delete anomaly** when a customer cancels their booking (2 Marks).

#### **Question 2: Relational Normalisation (12 Marks)**
A regional athletic club records team training allocations in the following un-normalised form (UNF):

| ClubCode | ClubName | RegionalOffice | TeamIDs | CoachNames | TrainingDays | TrainingTimes |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| C10 | Perth Athletics | Subiaco | T01, T02 | Coach Dan, Coach Mel | Mon, Wed | 16:00, 17:00 |
| C20 | Fremantle Harriers| Fremantle | T03 | Coach Sam | Tue | 16:30 |

a) Convert this UNF dataset into **First Normal Form (1NF)**. Ensure you underline the **Composite Primary Key** (4 Marks).  
b) Convert your 1NF schema into **Second Normal Form (2NF)**. Write out your decomposed tables using relational schema notation (4 Marks).  
c) Convert your 2NF schema into **Third Normal Form (3NF)**. Write out your final tables using relational schema notation, identifying primary and foreign keys (4 Marks).

#### **Question 3: Data Integrity (4 Marks)**
Identify which SCSA data integrity factor (accuracy, authenticity, currency, relevance) is best addressed by each of the following system controls:
1.  An automated date stamp that logs when an athlete's physical assessment was last reviewed (1 Mark).
2.  An SQLite constraint that blocks users from entering a student's age as greater than 100 (1 Mark).
3.  Implementing database tables that only store contact details necessary to run the track event (1 Mark).
4.  Implementing secure individual staff login accounts to log who entered the race scores (1 Mark).

---

### **Marking Guide & Exemplar Solutions**

#### **Question 1 (4 Marks)**
*   **Insert Anomaly (2 Marks):**
    *   *1 Mark* for identifying that the store cannot record a newly purchased piece of equipment (`EquipmentID`, `Category`, `RentalRate`) until a customer actually rents it.
    *   *1 Mark* for explaining that this is because `BookingID` is the primary key, and null values cannot be stored in key fields.
*   **Delete Anomaly (2 Marks):**
    *   *1 Mark* for identifying that deleting a booking for a unique piece of equipment will delete all details of that equipment.
    *   *1 Mark* for explaining that this erases its category and rental rate from the system, as no other record of it exists.

#### **Question 2 (12 Marks)**
*   **a) First Normal Form (1NF) (4 Marks):**
    *   *1 Mark* for flattening all repeating groups to ensure value atomicity.
    *   *1 Mark* for repeating parent attributes (`ClubCode`, `ClubName`, `RegionalOffice`) for each row.
    *   *2 Marks* for identifying and underlining the correct **Composite Primary Key**: `(ClubCode, TeamID)`.

    *Exemplar 1NF Table:*
    
    | **<u>ClubCode</u>** | ClubName | RegionalOffice | **<u>TeamID</u>** | CoachName | TrainingDay | TrainingTime |
    | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
    | **<u>C10</u>** | Perth Athletics | Subiaco | **<u>T01</u>** | Coach Dan | Mon | 16:00 |
    | **<u>C10</u>** | Perth Athletics | Subiaco | **<u>T02</u>** | Coach Mel | Wed | 17:00 |
    | **<u>C20</u>** | Fremantle Harriers| Fremantle | **<u>T03</u>** | Coach Sam | Tue | 16:30 |

*   **b) Second Normal Form (2NF) (4 Marks):**
    *   *1 Mark* for identifying that `ClubName` and `RegionalOffice` depend partially on `ClubCode`.
    *   *1 Mark* for identifying that `CoachName`, `TrainingDay`, and `TrainingTime` depend partially on `TeamID`.
    *   *2 Marks* for providing the correct relational schemas:
        *   `CLUB(`<u>ClubCode</u>, ClubName, RegionalOffice`)`
        *   `TEAM(`<u>TeamID</u>, CoachName, TrainingDay, TrainingTime`)`
        *   `CLUB_TEAM_ALLOCATION(`<u>ClubCode (FK)</u>, <u>TeamID (FK)</u>`)` *(Note: Since no other fields depend on the composite key, this is the join table).*

*   **c) Third Normal Form (3NF) (4 Marks):**
    *   *1 Mark* for identifying the transitive dependency: `ClubCode -> RegionalOffice` (since the office location is determined by the club, but the office is a non-key field). Let's look closely at the question data: C10 has Subiaco, C20 has Fremantle. If a club's regional office is an independent entity, we can extract it.
    *   *3 Marks* for providing the final normalized schemas:
        *   `CLUB_OFFICE(`<u>RegionalOffice</u>, OfficeDetails...`)` or simply extracting:
        *   `CLUB(`<u>ClubCode</u>, ClubName, RegionalOffice (FK)`)`
        *   `OFFICE(`<u>RegionalOffice</u>`)` *(Note: Under the simple syllabus, we focus on removing the transitive relation between Club and RegionalOffice if it is determined by another attribute. Let's look at the standard SCSA model: `ClubCode -> RegionalOffice -> OfficeAddress`).*
        *   If we assume `RegionalOffice` is transitive, we extract it. Let's ensure the relationship is fully resolved:
            *   `CLUB(`<u>ClubCode</u>, ClubName, RegionalOffice (FK)`)`
            *   `OFFICE(`<u>RegionalOffice</u>`)`
            *   `TEAM(`<u>TeamID</u>, CoachName, TrainingDay, TrainingTime`)`
            *   `ALLOCATION(`<u>ClubCode (FK)</u>, <u>TeamID (FK)</u>`)`
        *   *Marking standard:* Award 4 marks for clean logical decomposition that is fully in 2NF and has all transitive non-key relationships extracted.

#### **Question 3 (4 Marks)**
*   1.  **Currency** (1 Mark)
*   2.  **Accuracy** (1 Mark)
*   3.  **Relevance** (1 Mark)
*   4.  **Authenticity** (1 Mark)
