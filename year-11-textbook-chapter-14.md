# Unit 2 — Chapter 14: Database Design & Modelling

This chapter moves from the general concepts of databases into the practical tools developers use to plan, document, and model professional relational systems. You will learn to express database logic visually using **Crow's Foot Notation Entity-Relationship Diagrams (ERDs)**, define physical field constraints using structured **Data Dictionaries**, and solve complex logical barriers by **resolving Many-to-Many (M:N) relationships** into physical, implementable tables.

These modelling skills are highly examinable in written papers (often carrying 8 to 12 marks in SCSA exams) and represent the critical planning milestones for your **SCSA School-Based Assessment Task 6 (The Relational Database Project)**.

---

## Lesson 14.1: Crow's Foot Notation ERDs

### Your Goal
Design, draw, and interpret relational database Entity-Relationship Diagrams (ERDs) featuring 3 to 6 tables using correct SCSA-compliant Crow's Foot cardinality notation.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 13.3: Core Database Concepts & Hierarchy](./year-11-textbook-chapter-13.md#lesson-133-core-database-concepts--hierarchy) (Entities, fields, PKs, and FKs).

### The Idea
Before writing a single line of SQL or setting up tables in SQLite, database developers must draw a blueprint. This blueprint is called an **Entity-Relationship Diagram (ERD)**. It shows the logical tables (entities) and visually represents how they link together.

In SCSA exams and professional systems, we use **Crow's Foot Notation** to show the exact rules of our relationships. These rules are called **cardinalities**—they represent the minimum and maximum number of times an instance in one table can relate to an instance in another table.

**The Analogy:**
Imagine mapping out how the ovals at the **WA Junior Sports Carnival** host track-and-field matches:
*   A physical oval can host **many** scheduled matches throughout the day, or it might host **none** (zero) if it is being rested.
*   However, any specific match must take place on **one and only one** specific oval. It cannot exist on multiple ovals simultaneously.

In an ERD, we draw a line between the `Oval` entity and the `Match` entity, and we place custom symbolic "ticks" or "forks" on each end of the line to represent these exact rules.

#### **SCSA Key Terms**
*   **Entity-Relationship Diagram (ERD):** A visual model representing the logical structure of a database, showing entities, attributes, and their relationship constraints.
*   **Cardinality:** The numerical limit (minimum and maximum) of relationship occurrences between linked entities.
*   **Crow's Foot Symbol:** The split three-pronged fork symbol on a relationship connector line representing "Many" ($N$ or $M$).
*   **Identifying Relationship:** A relationship where the child entity cannot exist logically or physically without the parent entity (drawn as a solid line).

#### **The Cardinality Symbols**
To read or draw a Crow's Foot ERD, you must master the four standard cardinality symbol combinations placed at the ends of relationship lines:

1.  **One and Only One (Mandatory One):** Represented by two parallel vertical lines perpendicular to the connector (`-||-`).
2.  **Zero or One (Optional One):** Represented by a circle and a vertical line (`-o|-`).
3.  **One or Many (Mandatory Many):** Represented by a vertical line and a three-pronged crow's foot (`-|-<`).
4.  **Zero or Many (Optional Many):** Represented by a circle and a three-pronged crow's foot (`-o-<`).

```
  ONE AND ONLY ONE           ZERO OR ONE             ONE OR MANY             ZERO OR MANY
   ---||-------------      ---o|-------------      ---|-------------       ---o-------------
      ||                       o|                     |     <              o     <
```

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival administration database needs to track three linked tables:
1.  `SCHOOL` (Each school in WA has a unique school code).
2.  `ATHLETE` (Students registered to compete).
3.  `EMERGENCY_CONTACT` (The primary guardian file for each student).

The business rules are defined as follows:
*   A **School** can register **one or many** competing Athletes (each school must have at least one athlete registered to participate in the carnival).
*   An **Athlete** must belong to **one and only one** School.
*   An **Athlete** can have **zero or one** Emergency Contact registered in the database (optional, in case parents co-register).
*   An **Emergency Contact** belongs to **one and only one** Athlete.

#### **The Logical ERD Schema Diagram**
In SCSA exams, you must represent this logical layout using structured rectangular boxes containing entity names, listing key attributes, and drawing correct connector endpoints.

```
+-------------------+                    +-------------------+                    +-------------------+
|      SCHOOL       |                    |      ATHLETE      |                    | EMERGENCY_CONTACT |
+-------------------+                    +-------------------+                    +-------------------+
| PK | SchoolID     |------||--------o-< | PK | AthleteID    |------|o--------||--| PK | ContactID    |
+-------------------+                    | FK | SchoolID     |                    | FK | AthleteID    |
|    | SchoolName   |                    +-------------------+                    +-------------------+
|    | Region       |                    |    | FirstName    |                    |    | ContactName  |
+-------------------+                    |    | LastName     |                    |    | PhoneNum     |
                                         +-------------------+                    +-------------------+
```

#### **How the Logic Flows**
*   **Reading from SCHOOL to ATHLETE:** Follow the line from `SCHOOL` to `ATHLETE`. Look at the symbol right next to the `ATHLETE` box. It is `-o-<` (**Zero or Many** or `-|-<` **One or Many** depending on rule strictness). According to our rule, a school has *one or many* athletes, so we draw a vertical line and a fork (`-|-<`).
*   **Reading from ATHLETE to SCHOOL:** Follow the line back to `SCHOOL`. The symbol right next to `SCHOOL` is `-||-` (**One and Only One**). This represents that every athlete *must* belong to exactly one school.
*   **Reading from ATHLETE to EMERGENCY_CONTACT:** The endpoint next to `EMERGENCY_CONTACT` is `-o|-` (**Zero or One**). This shows that the emergency contact record is optional for an athlete.
*   **Reading from EMERGENCY_CONTACT to ATHLETE:** The endpoint next to `ATHLETE` is `-||-` (**One and Only One**). An emergency contact cannot exist in the database without being linked to a valid athlete.

---

### Try It with Help
#### **The Problem**
The carnival coordinators want to extend their schema to include ovals and scheduled matches. 
*   An **Oval** (e.g., "Main Oval", "West Field") can host **zero or many** scheduled Matches throughout the day.
*   A **Match** must take place on **one and only one** Oval.

Complete the missing cardinality symbols on the connector line between `OVAL` and `MATCH` below.

```
+-------------------+                                         +-------------------+
|       OVAL        |                                         |       MATCH       |
+-------------------+                                         +-------------------+
| PK | OvalID       |----------- [Symbol A] -------- [Symbol B] | PK | MatchID      |
+-------------------+                                         | FK | OvalID       |
|    | OvalName     |                                         +-------------------+
|    | SurfaceType  |                                         |    | EventTime    |
+-------------------+                                         |    | RoundNum     |
                                                              +-------------------+
```

#### **Structural Hints**
*   **Symbol A (near OVAL):** This represents "How many Ovals can a single Match belong to?". The business rule states: *"A Match must take place on one and only one Oval."* What is the correct symbol for "One and Only One"?
*   **Symbol B (near MATCH):** This represents "How many Matches can take place on a single Oval?". The business rule states: *"An Oval can host zero or many scheduled Matches."* What is the correct symbol for "Zero or Many"?

---

### Try It Yourself
#### **The Problem**
A regional WA sports network wants to build a database to track local sports clubs, their physical fields, and local coaches. Draw an SCSA-compliant, 3-table Crow's Foot ERD based on the following business specifications:
1.  Each **Club** has a unique `ClubID` (PK), a `ClubName`, and a `SportType`.
2.  Each **Field** has a unique `FieldID` (PK), a `FieldName`, and a `Capacity`.
3.  Each **Coach** has a unique `CoachID` (PK), a `CoachName`, and a `LicenseLevel`.
4.  **Relationship 1:** A Club can lease **one or many** physical Fields. A physical Field must belong to **one and only one** parent Club.
5.  **Relationship 2:** A Club can employ **zero or many** Coaches. A Coach must work for **one and only one** Club.

*Include all Primary Keys (PK) and Foreign Keys (FK) inside your table diagram blocks.*

---

### Check Your Reasoning
#### **The Answer**
Your drawn ERD should match the structural layout and cardinality endpoints below:

```
+-------------------+                    +-------------------+
|       FIELD       |                    |       CLUB        |
+-------------------+                    +-------------------+
| PK | FieldID      |------||--------|-< | PK | ClubID       |
| FK | ClubID       |                    +-------------------+
+-------------------+                    |    | ClubName     |
|    | FieldName    |                    |    | SportType    |
|    | Capacity     |                    +-------------------+
+-------------------+                              |
                                                   |
                                                   ||
                                                   |
                                                   o
                                                   <
                                         +-------------------+
                                         |       COACH       |
                                         +-------------------+
                                         | PK | CoachID      |
                                         | FK | ClubID       |
                                         +-------------------+
                                         |    | CoachName    |
                                         |    | LicenseLevel |
                                         +-------------------+
```

#### **Key Verification Steps:**
1.  **FIELD to CLUB:** The line next to `CLUB` terminates in a mandatory one symbol (`-||-`). The line next to `FIELD` terminates in a mandatory many symbol (`-|-<`). This shows a Club has *one or many* Fields, while a Field belongs to *one and only one* Club.
2.  **COACH to CLUB:** The line next to `CLUB` terminates in a mandatory one symbol (`-||-`). The line next to `COACH` terminates in an optional many symbol (`-o-<`). This shows a Club has *zero or many* Coaches, while a Coach works for *one and only one* Club.
3.  **Foreign Key Placement:** The `ClubID` column must be placed inside the `FIELD` and `COACH` entities as a Foreign Key (FK) to link them back to their parent record.

#### **Common SCSA Student Errors**
*   **Reversing Foreign Keys:** Putting `FieldID` inside the `CLUB` table. This is a fatal logical error. A club can have multiple fields; if you put `FieldID` inside `CLUB`, you could only store a single field per club unless you duplicated the club row (violating primary key uniqueness). **The Foreign Key always goes on the "Many" side of a 1:M relationship.**
*   **Disconnected Lines:** Drawing lines that float between tables without directly touching the entity borders. In SCSA exams, symbols must touch or overlap the box border to earn marks.
*   **Incorrect Cardianlity Direction:** Confusing "Zero or Many" with "One or Many". Always read the exact wording of the business scenario carefully.

---

### Review and Connect
In this lesson, you mastered the visual rules of database design. However, an ERD only shows the shapes and connections. To document the exact size, constraints, and data types of every field inside those boxes, we must pair our ERD with a structured **Data Dictionary**, which we will explore next.

---

## Lesson 14.2: Data Dictionaries

### Your Goal
Construct a complete, SCSA-compliant Data Dictionary specifying field properties, key mappings, sizes, and validation rules for a relational database schema.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.4: Fundamental Data Types](./year-11-textbook-chapter-1.md#lesson-14-fundamental-data-types) (choosing integer, float, string, and Boolean types).
*   [Lesson 13.3: Core Database Concepts & Hierarchy](./year-11-textbook-chapter-13.md#lesson-133-core-database-concepts--hierarchy).

### The Idea
An ERD is a fantastic visual reference, but it does not tell a database engineer how to configure the actual database software. For instance, an ERD doesn't state if an athlete's phone number can be left blank, or what the maximum allowed length of a student's surname is.

To provide this technical detail, developers create a **Data Dictionary**. This is a structured reference table that documents the metadata (data about data) for every field in every table of our relational database.

**The Analogy:**
Think of a Data Dictionary as an architect’s structural blueprint detailing a building's doors. The floor plan (ERD) shows where the doors are. The door schedule (Data Dictionary) details exactly what material each door is made of, its height in millimeters, its fire rating, and what key code is required to unlock it.

#### **SCSA Key Terms**
*   **Data Dictionary:** A centralized metadata document that defines the name, data type, length, keys, validation rules, and description of every field within a database schema.
*   **Metadata:** Structured data that describes other data, providing technical constraints and descriptions.
*   **Field Size (Length):** The maximum storage capacity allocated to a field (e.g., characters for text, bytes for integers).
*   **Validation Rule:** A structural check enforced by the database engine to ensure entered data is logical, secure, and accurate before it is saved (e.g., a range check or format pattern).

#### **Standard SCSA Data Dictionary Structure**
In SCSA exams and school projects, your data dictionary must feature these specific columns:

| Field Name | Data Type | Key Type | Field Size / Format | Validation Rule / Nullability | Description & Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| The name used in code | e.g. TEXT, INT | PK, FK, or blank | Max length or pattern | e.g. NOT NULL, > 0 | What is stored, with an example |

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival needs to document the `ATHLETE` table in its central data dictionary. The table must store:
*   A unique Athlete ID (a whole number).
*   The Athlete's First Name and Last Name.
*   Their Date of Birth.
*   Their School ID (linking back to the `SCHOOL` table).

#### **The Data Dictionary Entry**

**Table: ATHLETE**

| Field Name | Data Type | Key Type | Field Size / Format | Validation Rule / Nullability | Description & Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `AthleteID` | INTEGER | PK | Auto-increment | NOT NULL, Primary Key | Unique identifier for each athlete. (e.g., `24015`) |
| `FirstName` | TEXT | | 35 characters | NOT NULL | Competing student's first name. (e.g., `"Sarah"`) |
| `LastName` | TEXT | | 35 characters | NOT NULL | Competing student's family surname. (e.g., `"O'Connor"`) |
| `DateOfBirth`| DATE | | YYYY-MM-DD | NOT NULL, Age must be between 14 and 18 | Student birthday for age division grouping. (e.g., `"2010-04-12"`) |
| `SchoolID` | TEXT | FK | 4 characters | NOT NULL, Must exist in SCHOOL table | Foreign link to athlete's school. (e.g., `"SHS1"`) |

#### **How the Design Constraints Protect Data**
*   **`LastName` size set to 35:** This ensures the database allocates enough memory for long or hyphenated surnames (e.g., `"Menzies-Chamberlain"`) without wasting space on infinite characters.
*   **`DateOfBirth` validation rules:** By specifying that the age must be between 14 and 18, the database will automatically reject corrupt entry dates (like `"1890-01-01"` or `"2026-05-12"`), enforcing **data integrity**.
*   **`SchoolID` defined as text size 4:** Aligns with standard WA SCSA school registration codes which consist of four alphanumeric characters.

---

### Try It with Help
#### **The Problem**
The carnival timing desk needs to document the `EVENT` table inside the data dictionary. This table tracks individual competitive events (e.g., "100m Sprint", "Shot Put"). 
*   `EventID` (PK, integer, auto-incremented).
*   `EventName` (up to 50 characters, cannot be empty).
*   `RecordTime` (floating-point decimal, optional because some events are measured in distances, must be greater than zero).

Complete the missing properties in the data dictionary table below.

**Table: EVENT**

| Field Name | Data Type | Key Type | Field Size / Format | Validation Rule / Nullability | Description & Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `EventID` | **[DataType A]** | PK | Auto-increment | NOT NULL | Unique database identifier. (e.g., `102`) |
| `EventName` | TEXT | | **[Size B]** | NOT NULL | Official name of athletic event. (e.g., `"100m Sprint"`) |
| `RecordTime`| REAL / FLOAT | | Decimal (00.00) | **[Validation C]** | Existing record in seconds. (e.g., `10.82`, can be NULL) |

#### **Structural Hints**
*   **DataType A:** What data type represents a whole number for a database identifier?
*   **Size B:** The problem states: *"EventName can be up to 50 characters."* How is this written under Field Size?
*   **Validation C:** The problem states: *"RecordTime must be greater than zero and is optional."* How do you write this constraint, knowing "optional" means it can be left blank (NULL)?

---

### Try It Yourself
#### **The Problem**
Construct a complete Data Dictionary for a table named `RESULT` which links athletes to scheduled matches. The table contains the following fields:
1.  `ResultID` – A unique whole-number primary key.
2.  `AthleteID` – A whole-number foreign key linking to the `ATHLETE` table.
3.  `MatchID` – A whole-number foreign key linking to the `MATCH` table.
4.  `PointsScored` – An integer representing points earned, which must be a positive number between 0 and 100 inclusive. It cannot be left empty.
5.  `MatchDate` – A date field tracking when the match occurred, stored in `YYYY-MM-DD` format. It is mandatory.

---

### Check Your Reasoning
#### **The Answer**

**Table: RESULT**

| Field Name | Data Type | Key Type | Field Size / Format | Validation Rule / Nullability | Description & Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `ResultID` | INTEGER | PK | Auto-increment | NOT NULL, Primary Key | Unique identifier for each event result entry. (e.g., `1`) |
| `AthleteID` | INTEGER | FK | Integer | NOT NULL, Must exist in ATHLETE table | Foreign link associating an athlete with this result. (e.g., `24015`) |
| `MatchID` | INTEGER | FK | Integer | NOT NULL, Must exist in MATCH table | Foreign link associating a match with this result. (e.g., `450`) |
| `PointsScored`| INTEGER | | Integer | NOT NULL, Range check: $0 \le 	ext{PointsScored} \le 100$ | Points earned by athlete during match. (e.g., `15`) |
| `MatchDate` | DATE | | YYYY-MM-DD | NOT NULL | Calendar date of scheduled fixture. (e.g., `"2026-09-05"`) |

#### **Common SCSA Student Errors**
*   **Omitting Nullability Rules:** Forgetting to write `NOT NULL` for primary keys or foreign keys. Keys *must* always contain valid data; leaving a foreign link blank breaks referential integrity.
*   **Vague Field Sizes:** Writing "Variable" or leaving the Field Size block empty. You must specify logical characters or system bytes (e.g., 20 characters, or standard Integer format).
*   **Missing PK/FK Indicators:** Forgetting to mark foreign keys in the "Key Type" column, which makes it impossible for database engineers to map relationships.

---

### Review and Connect
A data dictionary ensures technical consistency. However, both your ERD models and Data Dictionaries can run into structural roadblocks when complex real-world actions occur. In our next lesson, we will learn how to identify and resolve the ultimate database structural conflict: the **Many-to-Many (M:N) Relationship**.

---

## Lesson 14.3: Resolving Many-to-Many (M:N) Relationships

### Your Goal
Identify, explain, and resolve Many-to-Many ($M:N$) relational database conflicts by designing and implementing associative entities with composite primary keys.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 14.1: Crow's Foot Notation ERDs](./year-11-textbook-chapter-14.md#lesson-141-crows-foot-notation-erds).
*   [Lesson 13.3: Core Database Concepts & Hierarchy](./year-11-textbook-chapter-13.md#lesson-133-core-database-concepts--hierarchy) (specifically understanding Primary Keys and Composite Keys).

### The Idea
In real-world database design, relationships naturally occur in three varieties:
1.  **One-to-One (1:1):** (e.g., A student has exactly one locker; a locker belongs to exactly one student).
2.  **One-to-Many (1:M):** (e.g., A school has many competing athletes; an athlete belongs to only one school).
3.  **Many-to-Many (M:N):** (e.g., An athlete competes in many events; a sports event hosts many competing athletes).

While One-to-Many relationships are simple to implement (we just put a Foreign Key on the "Many" side), **Many-to-Many (M:N) relationships are structurally impossible to build directly in a relational database management system.**

**Why?**
If we link `ATHLETE` and `EVENT` directly:
*   If we put `EventID` inside the `ATHLETE` table, an athlete competing in 5 events would require us to store a comma-separated list (e.g. `101, 102, 105`) in a single cell, which violates the **atomicity rule** (each field must contain only one value).
*   Alternatively, we could duplicate the athlete's details on five separate rows, but this violates the **primary key uniqueness constraint** and floods our database with redundant data.

**The Solution:**
To resolve an $M:N$ relationship, we must break it apart by introducing a middle-man table. In database science, this is called an **associative entity** (or junction/bridge table). 
*   We place this new table in the middle, creating **two separate One-to-Many (1:M) relationships** facing back-to-back.
*   This bridge table absorbs the keys from both parent tables, often combining them to form a **Composite Primary Key**.

```
    UNRESOLVED M:N RELATIONSHIP (Direct - Broken)
    [ ATHLETE ] -------(Can compete in many)------o-< [ EVENT ]
         |                                              |
         +-------(Can host many athletes)--------o------+

    RESOLVED 1:M - M:1 RELATIONSHIP ( Juntion Bridge - Clean )
    [ ATHLETE ] --||------o-< [ REGISTRATION ] >-o------||-- [ EVENT ]
                                 (Bridge)
```

**The Analogy:**
Imagine a popular sports equipment shed. There are 100 students (Athletes) and 20 different balls and rackets (Equipment). 
*   A student can check out many items of equipment. An item of equipment can be checked out by many students over a week.
*   To keep track of this, the gym teacher does not write names directly on the balls, nor do they write lists of balls on students' hands. Instead, they set up a **"Sign-out Sheet"** (the associative table). 
*   Every single line on that sheet represents a single, atomic transaction: `StudentID` paired with `EquipmentID`, noting the exact date and return status.

#### **SCSA Key Terms**
*   **Many-to-Many Relationship (M:N):** A logical relationship where multiple records in one entity can relate to multiple records in another.
*   **Associative Entity (Junction/Bridge Table):** A physical database table used to resolve many-to-many relationships, containing foreign keys that reference the primary keys of the linked tables.
*   **Composite Primary Key:** A primary key composed of two or more foreign attributes that together guarantee the absolute uniqueness of a record.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival allows **Athletes** to compete in multiple **Events**.
*   Athlete 101 (`Sarah`) competes in Event 5 (`100m Sprint`) and Event 8 (`High Jump`).
*   Event 5 (`100m Sprint`) hosts Athlete 101 (`Sarah`) and Athlete 105 (`John`).

Let's resolve this $M:N$ relationship by creating a physical bridge entity named `REGISTRATION`.

#### **Step 1: The Parent Tables**
*   `ATHLETE` Table (PK: `AthleteID`)
*   `EVENT` Table (PK: `EventID`)

#### **Step 2: Designing the Bridge Table (`REGISTRATION`)**
The bridge table must inherit the Primary Keys of both parent tables as Foreign Keys (`AthleteID` and `EventID`). Together, they form a **Composite Primary Key** (`AthleteID` + `EventID`), ensuring Sarah cannot be registered for the 100m sprint twice. We can also attach specific transaction attributes, like `LaneNumber` or `HeatNum`.

#### **The Physical Schema Layout (ERD)**
Notice how the Crow's Foot prongs point **directly at the associative bridge table** from both parents.

```
+-------------------+                    +-------------------+                    +-------------------+
|      ATHLETE      |                    |   REGISTRATION    |                    |       EVENT       |
+-------------------+                    +-------------------+                    +-------------------+
| PK | AthleteID    |------||--------o-< | PK | AthleteID    | >-o--------||------| PK | EventID      |
+-------------------+                    | PK | EventID      |                    +-------------------+
|    | FirstName    |                    +-------------------+                    |    | EventName    |
|    | LastName     |                    |    | LaneNumber   |                    |    | TargetRecord |
+-------------------+                    |    | HeatNum      |                    +-------------------+
                                         +-------------------+
```

#### **How the Physical Data Maps**

**Table: ATHLETE (Parent 1)**
| AthleteID (PK) | FirstName | LastName |
| :--- | :--- | :--- |
| 101 | Sarah | O'Connor |
| 105 | John | Menzies |

**Table: EVENT (Parent 2)**
| EventID (PK) | EventName | TargetRecord |
| :--- | :--- | :--- |
| 5 | 100m Sprint | 10.82 |
| 8 | High Jump | 1.62 |

**Table: REGISTRATION (Associative Bridge)**
| AthleteID (PK/FK) | EventID (PK/FK) | LaneNumber | HeatNum |
| :--- | :--- | :--- | :--- |
| **101** | **5** | 3 | Heat A |
| **101** | **8** | NULL (N/A) | Flight 1 |
| **105** | **5** | 4 | Heat A |

#### **Why this resolves the conflict:**
*   There are no repeating comma-separated cells. All values are atomic.
*   We do not duplicate Sarah's name or John's name in multiple rows. Personal details reside safely in `ATHLETE`.
*   We can easily query registrations using simple SQL relationships.

---

### Try It with Help
#### **The Problem**
A school textbook hire database has a many-to-many relationship between **Students** and **Textbooks**:
*   A **Student** can hire **one or many** Textbooks throughout the year.
*   A **Textbook** (e.g., "Year 11 CS ATAR") can be hired by **one or many** different Students across different semesters.

Resolve this relationship by introducing an associative table named `LOAN`. Map the correct keys and cardianlity lines using the template below.

```
+-------------------+                                         +-------------------+
|      STUDENT      |                                         |     TEXTBOOK      |
+-------------------+                                         +-------------------+
| PK | StudentID    |                                         | PK | TextbookID   |
+-------------------+                                         +-------------------+
|    | FirstName    |                                         |    | BookTitle    |
|    | YearLevel    |                                         |    | Subject      |
+-------------------+                                         +-------------------+
                                          |
                                          |
                                    [ Bridge Table ]
                                   +----------------+
                                   |      LOAN      |
                                   +----------------+
                                   | PK | [Key A]   |
                                   | PK | [Key B]   |
                                   +----------------+
                                   |    | DateDue   |
                                   +----------------+
```

#### **Structural Hints**
*   What are the two foreign fields that must be imported into `LOAN` from `STUDENT` and `TEXTBOOK` to form the **Composite Primary Key**?
*   Assign **Key A** and **Key B** their correct field names.
*   Draw two Crow's Foot connector lines from the parent tables pointing at the `LOAN` bridge table. Remember: **The "many" prongs of the crow's foot must always point *at* the bridge table.**

---

### Try It Yourself
#### **The Problem**
In a local WA soccer league, **Teams** compete against each other in **Matches**:
*   A **Team** plays in **many** scheduled Matches throughout a season.
*   A **Match** is played by exactly **two** Teams.
*   Because a Match inherently links multiple Teams together, a direct relational database implementation of `TEAM` and `MATCH` creates a logical many-to-many conflict when recording the unique statistics (such as yellow cards, scores, or fouls) for *each team in each match*.

Design a physical database schema to resolve this many-to-many conflict.
1.  Identify the two parent tables and specify their Primary Keys.
2.  Design a middle associative bridge table named `TEAM_MATCH_STATS`.
3.  Specify the **Composite Primary Key** of this bridge table.
4.  Draw a complete Crow's Foot ERD showing the resolved schema, including keys and field links.

---

### Check Your Reasoning
#### **The Answer**
1.  **Parent Tables:**
    *   `TEAM` (PK: `TeamID`)
    *   `MATCH` (PK: `MatchID`)
2.  **Associative Table:**
    *   `TEAM_MATCH_STATS`
3.  **Composite Primary Key:**
    *   (`TeamID` + `MatchID`) – This guarantees that a team can only record one set of stats for a specific match.
4.  **The Resolved ERD Model:**

```
+-------------------+                    +-------------------+                    +-------------------+
|       TEAM        |                    | TEAM_MATCH_STATS  |                    |       MATCH       |
+-------------------+                    +-------------------+                    +-------------------+
| PK | TeamID       |------||--------o-< | PK | TeamID       | >-o--------||------| PK | MatchID      |
+-------------------+                    | PK | MatchID      |                    +-------------------+
|    | TeamName     |                    +-------------------+                    |    | MatchDate    |
|    | CoachName    |                    |    | Score           |                    |    | Venue        |
+-------------------+                    |    | Fouls            |                    +-------------------+
                                         |    | YellowCards  |
                                         +-------------------+
```

#### **Common SCSA Student Errors**
*   **Drawing the Crow's Feet Backwards:** Pointing the "many" fork symbols at the parent tables and placing the "one" lines on the bridge table. Remember: **The bridge table is the "child" of both parents. The "prongs" must touch the bridge border.**
*   **Missing Composite Markers:** Forgetting to designate *both* inherited foreign fields as Primary Keys inside the bridge table. If only `TeamID` is marked as a PK in the bridge, then a team can only play in one match ever in the database.
*   **Adding Unnecessary Autonumber PKs:** Adding an artificial `ID` (e.g. `StatsID`) to the bridge table is technically possible, but SCSA exam marking guides prioritize composite key mapping (`TeamID` + `MatchID`) to evaluate relational conceptual understanding.

---

## Chapter 14: Teacher Support Module

### **SCSA Syllabus Alignment Matrix**
*   **SCSA Unit 2 Course Content Codes:**
    *   *Database Documentation:* Entity-Relationship (ER) diagrams (3 to 6 tables) using Crow's Foot Notation.
    *   *Data Dictionary:* Creating and analyzing data dictionaries detailing table constraints and validation.
    *   *Relational Operations:* Resolving many-to-many ($M:N$) relationship limitations.

### **Classroom Diagnostic & Prerequisite Check**
Before students begin normalisation in Chapter 15, run this 5-minute checkpoint:
1.  *Can they identify a Composite Key?* (Ask them why a single Primary Key fails in an associative bridge table).
2.  *Can they locate the Foreign Key?* (Check if they can identify that the FK is always placed on the "Many" side of a 1:M relationship).
3.  *Do they know why phone numbers are stored as Text?* (Remind them: phone numbers feature leading zeros and non-mathematical symbols like spaces or `+`, which integer types drop or evaluate algebraically).

### **High-Frequency Student Misconceptions**
1.  **"ERD lines can connect any field to any field."**  
    *Correction:* ERD relationship lines logically connect the *tables themselves*, but represent the mapping of a Primary Key in the parent table to a Foreign Key in the child table. Connectors must point clean and square to table boundaries.
2.  **"A database can have a many-to-many table."**  
    *Correction:* In relational theory, $M:N$ exists conceptually. However, in actual RDBMS engines (SQLite, MS Access, SQL Server), they are physically impossible to implement directly without causing atomic failures or massive key duplication.
3.  **"Null is the same as zero."**  
    *Correction:* In Data Dictionaries, `NULL` represents the *complete absence of value* (e.g., an optional field not yet filled). `0` is a concrete mathematical integer.

---

## Chapter 14: Practice Assessment (20 Marks)

**Assessment Style:** Written Theory & Schema Design  
**Duration:** 25 Minutes  
**Focus:** WA SCSA ATAR Year 11 Unit 2 Exam Standards  

### **The Scenario**
The WA Junior Sports Carnival coordinators want to add a medical-incident tracking system to their database. They have provided the following business rules:
*   Each **Incident** has a unique `IncidentID` (integer, PK), an `IncidentTime` (text, HH:MM format), and a `TreatmentGiven` (text description).
*   Each **Medic** has a unique `MedicID` (integer, PK), a `MedicName` (text), and a `RadioChannel` (integer, range 1 to 10).
*   A **Medic** can respond to **zero or many** Incidents throughout the day.
*   An **Incident** must be responded to by **one and only one** Medic.
*   An **Incident** is reported by **one and only one** Athlete.
*   An **Athlete** can have **zero or many** recorded Incidents.

---

### **Questions**

#### **Question 1: Data Dictionary Construction** (6 Marks)
Construct a complete Data Dictionary for the `INCIDENT` table based on the scenario guidelines.

#### **Question 2: Entity-Relationship Diagramming** (8 Marks)
Draw an SCSA-compliant Crow's Foot ERD linking the `MEDIC`, `INCIDENT`, and `ATHLETE` tables. 
*   *Include all entity names, primary keys (PK), foreign keys (FK), and relationship cardinalities.*

#### **Question 3: Relational Resolution Analysis** (6 Marks)
The carnival committee proposes adding an `EQUIPMENT` table to track safety gear (e.g., "Ice Packs", "Splints", "Stretcher").
*   An **Incident** can involve **zero or many** items of Equipment.
*   An item of **Equipment** can be deployed in **zero or many** Incidents.

1.  Explain the technical problem created by implementing this relationship directly in the database (2 Marks).
2.  Describe how a database developer resolves this specific problem (2 Marks).
3.  Write the table layout (specifying the primary keys) for the resulting bridge table (2 Marks).

---

### **Marking Key & Exemplar Solutions**

#### **Question 1: Data Dictionary Construction (6 Marks)**

**Table: INCIDENT**

| Field Name | Data Type | Key Type | Field Size | Validation Rule / Nullability | Description & Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `IncidentID` | INTEGER | PK | Auto | NOT NULL, Primary Key | Unique ID for the incident (e.g., `5001`) |
| `IncidentTime`| TEXT | | 5 chars | NOT NULL, Pattern: `[0-2][0-9]:[0-5][0-9]` | Time of day of injury (e.g., `"14:35"`) |
| `Treatment` | TEXT | | 250 chars | NOT NULL | Details of first-aid action (e.g., `"Ice pack applied to ankle"`) |
| `MedicID` | INTEGER | FK | Integer | NOT NULL, Must exist in MEDIC table | Foreign link to responding medic. (e.g., `12`) |
| `AthleteID` | INTEGER | FK | Integer | NOT NULL, Must exist in ATHLETE table | Foreign link to injured athlete. (e.g., `24015`) |

*   **Marking Allocation:**
    *   **1 Mark** for correct designation of Primary Key (`IncidentID`) and data type.
    *   **1 Mark** for designating both `MedicID` and `AthleteID` as Foreign Keys (FK) with matching data types.
    *   **1 Mark** for logical validation rules (e.g. format constraint on time, `NOT NULL` on keys).
    *   **1 Mark** for logical field sizes (e.g. 5 chars for `HH:MM`, 250 for description).
    *   **2 Marks** for perfect complete metadata structure matching SCSA standards.

---

#### **Question 2: Entity-Relationship Diagramming (8 Marks)**

```
+-------------------+                    +-------------------+                    +-------------------+
|       MEDIC       |                    |     INCIDENT      |                    |      ATHLETE      |
+-------------------+                    +-------------------+                    +-------------------+
| PK | MedicID      |------||--------o-< | PK | IncidentID   | >-o--------||------| PK | AthleteID    |
+-------------------+                    | FK | MedicID      |                    +-------------------+
|    | MedicName    |                    | FK | AthleteID    |                    |    | FirstName    |
|    | RadioChannel |                    +-------------------+                    |    | LastName     |
+-------------------+                    |    | IncidentTime |                    +-------------------+
                                         |    | Treatment    |
                                         +-------------------+
```

*   **Marking Allocation:**
    *   **2 Marks** for correct Entity blocks (`MEDIC`, `INCIDENT`, `ATHLETE`) listing all Primary and Foreign Keys correctly.
    *   **2 Marks** for drawing `MEDIC` to `INCIDENT` cardinality correctly: **One and Only One** (`-||-`) on Medic end; **Zero or Many** (`-o-<`) on Incident end.
    *   **2 Marks** for drawing `ATHLETE` to `INCIDENT` cardinality correctly: **One and Only One** (`-||-`) on Athlete end; **Zero or Many** (`-o-<`) on Incident end.
    *   **2 Marks** for placing Foreign Keys (`MedicID`, `AthleteID`) inside the child table (`INCIDENT`) to link the relations.

---

#### **Question 3: Relational Resolution Analysis (6 Marks)**

1.  **The Technical Problem (2 Marks):**
    *   A direct relationship creates a many-to-many ($M:N$) logical linkage. If implemented directly, it causes **data redundancy** (duplicating incident details on separate rows) or violates **data atomicity** (storing a list of multiple equipment IDs inside a single cell), which breaks relational database rules.
2.  **The Resolution Method (2 Marks):**
    *   The developer must resolve the many-to-many relationship by introducing a middle **associative entity** (or junction/bridge table) to create **two separate One-to-Many (1:M) relationships** facing back-to-back.
3.  **Bridge Table Design (2 Marks):**
    *   Bridge Table Name: `INCIDENT_EQUIPMENT` (or similar).
    *   Primary Keys: `IncidentID` and `EquipmentID` (combined to form a **Composite Primary Key**).
    *   *Exemplar Schema block:*
        *   `INCIDENT_EQUIPMENT` (<u>`IncidentID`</u> [FK], <u>`EquipmentID`</u> [FK], `QuantityDeployed`).

---
