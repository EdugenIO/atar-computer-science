# Unit 2 — Chapter 16: SQL Implementation & Developer Issues

This final chapter brings your database designs to life by implementing them in a real-world Relational Database Management System (RDBMS) using **SQLite**. You will learn to construct and execute core SQL commands to manage data, join multiple tables to extract meaningful relationships, calculate database-wide statistics using aggregate functions, and establish critical developer security and backup protocols.

These practical database implementation and querying skills are directly assessed in **SCSA School-Based Assessment Task 6 (The Relational Database Project)** and the **SCSA SQL Practical Examination (Assessment Task 7)**, representing major practical milestones in Unit 2.

---

## Lesson 16.1: Database Creation & Data Manipulation

### Your Goal
Create a multi-table database schema in SQLite and implement core Data Manipulation Language (DML) commands (`SELECT`, `INSERT`, `UPDATE`, `DELETE`) to manage records.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 13.3: Core Database Concepts & Hierarchy](./year-11-textbook-chapter-13.md#lesson-133-core-database-concepts--hierarchy) (Primary/Foreign Keys and datatypes).
*   [Lesson 14.2: Data Dictionaries](./year-11-textbook-chapter-14.md#lesson-142-data-dictionaries) (specifying field constraints).

### The Idea
An Entity-Relationship Diagram (ERD) is a blueprint, but a blueprint cannot store data. To build the actual database, we write **Structured Query Language (SQL)**. SQL is the universal language used to communicate with an RDBMS.

**The Analogy:**
Imagine a physical filing cabinet (the database) containing blank folder templates (tables). 
*   **Creating a table** is like setting up a new folder template with pre-labeled columns (fields) such as "First Name" and "Date of Birth".
*   **Manipulating data** is like writing a new student profile on a index card and sliding it into the folder (`INSERT`), reading a student card to find their phone number (`SELECT`), erasing a spelling mistake on a card (`UPDATE`), or shredding a card when a student leaves the school (`DELETE`).

#### **SCSA Key Terms**
*   **SQLite:** A lightweight, self-contained, serverless relational database engine used widely in mobile apps, web browsers, and educational software.
*   **Data Definition Language (DDL):** SQL commands used to define, alter, or delete database structures (e.g., `CREATE TABLE`).
*   **Data Manipulation Language (DML):** SQL commands used to store, retrieve, modify, and delete data *within* those structures.
*   **SQL Clause:** A unit of an SQL statement, such as `WHERE` or `ORDER BY`, used to filter or sort data.

| SQL Command | Purpose | General SQL Syntax Example |
| :--- | :--- | :--- |
| `CREATE TABLE` | Defines a new table, its columns, datatypes, and key constraints. | `CREATE TABLE Name (Field1 TYPE PK, ...);` |
| `SELECT` | Retrieves specific records from one or more tables. | `SELECT Field1, Field2 FROM Table WHERE Condition;` |
| `INSERT INTO` | Adds a new row of data to an existing table. | `INSERT INTO Table (Field1, Field2) VALUES (Val1, Val2);` |
| `UPDATE` | Modifies existing values inside specific rows. | `UPDATE Table SET Field1 = NewVal WHERE Condition;` |
| `DELETE FROM` | Permanently removes rows from a table. | `DELETE FROM Table WHERE Condition;` |

---

### See It Worked
#### **The Scenario**
The **WA Junior Sports Carnival** needs to implement a relational database to store competitor records. We will create a `School` table and an `Athlete` table, establish a One-to-Many (1:M) relationship, populate them, and manipulate the records.

#### **Step 1: Database Creation (DDL)**
```sql
-- Create the parent School table
CREATE TABLE School (
    SchoolID INTEGER PRIMARY KEY AUTOINCREMENT,
    SchoolName TEXT NOT NULL UNIQUE,
    HouseColour TEXT NOT NULL
);

-- Create the child Athlete table (establishing the Foreign Key relationship)
CREATE TABLE Athlete (
    AthleteID INTEGER PRIMARY KEY AUTOINCREMENT,
    FirstName TEXT NOT NULL,
    LastName TEXT NOT NULL,
    Gender TEXT CHECK(Gender IN ('M', 'F')),
    DateOfBirth TEXT NOT NULL,
    SchoolID INT,
    FOREIGN KEY (SchoolID) REFERENCES School(SchoolID)
);
```

#### **Step 2: Inserting Records (DML)**
```sql
-- Populate the School table
INSERT INTO School (SchoolName, HouseColour) VALUES ('Swan Athletic', 'Blue');
INSERT INTO School (SchoolName, HouseColour) VALUES ('Darling Range', 'Red');

-- Populate the Athlete table
INSERT INTO Athlete (FirstName, LastName, Gender, DateOfBirth, SchoolID) 
VALUES ('Sarah', 'Smith', 'F', '2010-04-12', 1);

INSERT INTO Athlete (FirstName, LastName, Gender, DateOfBirth, SchoolID) 
VALUES ('Mark', 'Johnston', 'M', '2009-11-23', 2);
```

#### **Step 3: Querying and Updating Records (DML)**
```sql
-- Query: Find all male athletes born after 2009
SELECT FirstName, LastName FROM Athlete 
WHERE Gender = 'M' AND DateOfBirth > '2009-12-31';

-- Update: Sarah Smith changes her school to Darling Range (SchoolID 2)
UPDATE Athlete 
SET SchoolID = 2 
WHERE AthleteID = 1;

-- Delete: Remove Mark Johnston from the database
DELETE FROM Athlete 
WHERE AthleteID = 2;
```

#### **How the Logic Flows**
*   The `FOREIGN KEY` constraint in the `Athlete` table ensures **Referential Integrity**. You cannot insert an athlete with a `SchoolID` of `99` because school `99` does not exist in the parent `School` table.
*   The `AUTOINCREMENT` keyword tells SQLite to automatically assign sequential integers (1, 2, 3...) to the primary key, preventing duplicate key entry errors.
*   In SQL, text values and dates must be wrapped in single quotes (`'M'`, `'2010-04-12'`), while numerical values do not require quotes.

---

### Try It with Help
#### **The Problem**
Write the SQL DML commands to manage a new table called `Event` designed to log carnival track and field events.
1.  **Insert** a new event: `"100m Sprint"`, which has an `EventID` of `5` and a record threshold of `11.50` seconds.
2.  **Update** this event's record threshold to `11.20` seconds.
3.  **Select** the names of all events that have a record threshold of less than `12.00` seconds.

#### **Structural Hints**
*   The `Event` table has three columns: `EventID` (integer), `EventName` (text), and `RecordThreshold` (float).
*   For the `UPDATE` command, identify the specific record using its `EventID`.
*   For the `SELECT` query, use the less-than operator (`<`) in the `WHERE` clause.

#### **Scaffolded Code Template**
```sql
-- 1. Insert the record
INSERT INTO Event (EventID, EventName, RecordThreshold) 
VALUES (5, '100m Sprint', 11.50);

-- 2. Update the record
UPDATE Event 
SET RecordThreshold = ??? -- enter value here
WHERE EventID = ???;      -- enter condition here

-- 3. Select with filtering
SELECT EventName 
FROM Event 
WHERE RecordThreshold < ???; -- enter comparison float here
```

---

### Try It Yourself
#### **The Problem**
Write a complete, SCSA-compliant SQL script from scratch that:
1.  Creates a table named `Device` to track marshal tablets at ovals, with the columns: `DeviceID` (Primary Key, integer), `Model` (text), and `BatteryLevel` (integer).
2.  Inserts two device records:
    *   Device 101: Model `'iPad Air'`, Battery Level `95`.
    *   Device 102: Model `'Galaxy Tab'`, Battery Level `12`.
3.  Write an SQL statement that selects all devices with a battery level of strictly less than `20` percent, sorting the output from lowest battery to highest.
4.  Write an SQL statement that deletes all devices with a battery level of `0`.

---

### Check Your Reasoning
#### **The Answer**
```sql
-- 1. Table Creation
CREATE TABLE Device (
    DeviceID INTEGER PRIMARY KEY,
    Model TEXT NOT NULL,
    BatteryLevel INTEGER CHECK(BatteryLevel BETWEEN 0 AND 100)
);

-- 2. Record Insertion
INSERT INTO Device (DeviceID, Model, BatteryLevel) VALUES (101, 'iPad Air', 95);
INSERT INTO Device (DeviceID, Model, BatteryLevel) VALUES (102, 'Galaxy Tab', 12);

-- 3. Filtered and Sorted Query
SELECT DeviceID, Model, BatteryLevel 
FROM Device 
WHERE BatteryLevel < 20 
ORDER BY BatteryLevel ASC;

-- 4. Record Deletion
DELETE FROM Device 
WHERE BatteryLevel = 0;
```

#### **Common SCSA Student Errors**
1.  **Forgetting SQL Semicolons:** Omitting the semicolon (`;`) at the end of each independent SQL statement, which will cause syntax compilation crashes in SQLite.
2.  **Using `UPDATE` without a `WHERE` clause:** Writing `UPDATE Device SET BatteryLevel = 100;` without specifying `WHERE DeviceID = 101` will overwrite the battery level of *every single row* in the database to 100.
3.  **Incorrect Order of Operations:** Placing the `ORDER BY` clause before the `WHERE` clause. Remember the mandatory syntactic SQL order: `SELECT ... FROM ... WHERE ... ORDER BY ...;`.

---

### Review and Connect
In this lesson, you mastered basic SQL table creation and DML operations. However, storing data in isolated tables is of limited use. On the next page, we will learn how to write queries that weave data from multiple tables together using SQL relations.

---

## Lesson 16.2: Relational Queries & Joins

### Your Goal
Construct multi-table SQL queries using `INNER JOIN` statements to retrieve connected records from related database entities.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 14.3: Resolving Many-to-Many Relationships](./year-11-textbook-chapter-14.md#lesson-143-resolving-many-to-many-mn-relationships) (understanding Foreign Key linkages).
*   [Lesson 16.1: Database Creation & Data Manipulation](#lesson-161-database-creation--data-manipulation) (basic `SELECT` statement syntax).

### The Idea
In a normalised relational database, information is intentionally divided among multiple tables to prevent redundancy. For example, the `Athlete` table does not contain the name of the student's school; it only contains a `SchoolID` integer. 

If a timing official needs to print a leaderboard showing the **Athlete's Name** alongside their **School's Name**, the RDBMS must fetch records from both tables simultaneously, matching them based on the shared `SchoolID` field.

We achieve this in SQL using the **`INNER JOIN`** clause.

**The Analogy:**
Imagine you have two separate lists of paper on your desk:
*   List A: Athletes (shows: Sarah Smith, SchoolID: 1).
*   List B: Schools (shows: SchoolID 1 = Swan Athletic, SchoolID 2 = Darling Range).

To find Sarah's school, you look at Sarah's row, grab her `SchoolID` (`1`), slide over to the School list, find row `1`, and read `'Swan Athletic'`. An `INNER JOIN` is the database engine performing this matching task automatically, returning a combined virtual row only where matching keys exist on both lists.

```
+-----------------------------------+        +-----------------------------------+
|          ATHLETE TABLE            |        |           SCHOOL TABLE            |
| AthleteID | FirstName | SchoolID  |        | SchoolID  | SchoolName            |
|-----------|-----------|-----------|        |-----------|-----------------------|
| 1001      | Sarah     | 1  ====== | =====> | 1         | Swan Athletic         |
| 1002      | Mark      | 2  ====== | =====> | 2         | Darling Range         |
+-----------------------------------+        +-----------------------------------+
                                  \\        //
                                   \\      //
                          [ SQL INNER JOIN OPERATION ]
                                     ||
                                     \\/
                   +--------------------------------------------+
                   |               VIRTUAL RESULT               |
                   | FirstName | SchoolID | SchoolName          |
                   |-----------|----------|---------------------|
                   | Sarah     | 1        | Swan Athletic       |
                   | Mark      | 2        | Darling Range       |
                   +--------------------------------------------+
```

#### **SCSA Key Terms**
*   **INNER JOIN:** An SQL clause that returns rows from multiple tables when the join condition is met (i.e. when there is a matching value in both tables).
*   **Join Condition:** The logical statement (specified after the `ON` keyword) defining which fields link the tables together (usually `TableA.PrimaryKey = TableB.ForeignKey`).
*   **Ambiguity Resolution:** Prefixing field names with their table names (e.g. `Athlete.SchoolID` vs `School.SchoolID`) to tell the RDBMS exactly which column to pull from when two tables share identical column names.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival timing booth needs a live display showing the runner's first name, last name, and their school name on the screen. 

We must query the `Athlete` table and the `School` table together, joining them on their shared `SchoolID` field.

#### **The Query Statement**
```sql
SELECT Athlete.FirstName, Athlete.LastName, School.SchoolName
FROM Athlete
INNER JOIN School ON Athlete.SchoolID = School.SchoolID
WHERE School.HouseColour = 'Blue'
ORDER BY Athlete.LastName ASC;
```

#### **How the Logic Flows**
1.  **`FROM Athlete`**: Specifies `Athlete` as the primary table.
2.  **`INNER JOIN School`**: Tells the database engine to connect the `School` table.
3.  **`ON Athlete.SchoolID = School.SchoolID`**: Tells the engine *how* to match the rows. It looks for matching values in the `SchoolID` columns of both tables.
4.  **`WHERE School.HouseColour = 'Blue'`**: Filters the results, displaying only athletes belonging to schools with Blue house colours.
5.  **`SELECT Athlete.FirstName...`**: Grabs only the specified columns to present in the final output. Note how we prefix the table names (`Athlete.FirstName`) to ensure clear, bug-free queries.

---

### Try It with Help
#### **The Problem**
At the carnival, athletes sign up for individual events, creating a Many-to-Many (M:N) relationship. This has been resolved into a three-table layout using an intermediate table named `Registration`:
*   `Athlete` table (Primary Key: `AthleteID`)
*   `Event` table (Primary Key: `EventID`)
*   `Registration` table (Foreign Keys: `AthleteID`, `EventID`)

Write an SQL statement that joins these three tables to list the `LastName` of the athlete and the `EventName` of every event they are registered to run.

#### **Structural Hints**
*   To join three tables, you must use **two consecutive `INNER JOIN`** statements.
*   Join table 1 (`Athlete`) to table 2 (`Registration`) first, using `AthleteID`.
*   Immediately join table 2 (`Registration`) to table 3 (`Event`), using `EventID`.

#### **Scaffolded Code Template**
```sql
SELECT Athlete.LastName, Event.EventName
FROM Athlete
INNER JOIN Registration ON Athlete.AthleteID = Registration.AthleteID
INNER JOIN Event ON Registration.EventID = Event.EventID
ORDER BY Athlete.LastName ASC;
```

---

### Try It Yourself
#### **The Problem**
Consider a database schema designed to track sports team assignments:
*   `Team` table (columns: `TeamID`, `TeamName`, `Division`)
*   `Player` table (columns: `PlayerID`, `PlayerName`, `Score`, `TeamID`)

Write an SQL statement that retrieves the `PlayerName`, their `Score`, and the corresponding `TeamName` for all players who are in the `'Under 16'` division and scored more than `50` points.

---

### Check Your Reasoning
#### **The Answer**
```sql
SELECT Player.PlayerName, Player.Score, Team.TeamName
FROM Player
INNER JOIN Team ON Player.TeamID = Team.TeamID
WHERE Team.Division = 'Under 16' AND Player.Score > 50;
```

#### **Common SCSA Student Errors**
1.  **Incorrect Join Conditions:** Writing `ON Player.TeamID = Team.TeamID` backwards as `ON Player.TeamID = Player.PlayerID`. This attempts to join a foreign key to a text field, causing a database type crash or returning zero records.
2.  **Ambiguous Column Errors:** Writing `SELECT PlayerName, TeamID FROM Player INNER JOIN Team ON Player.TeamID = Team.TeamID;`. Because `TeamID` exists in *both* tables, SQLite will throw an `"ambiguous column name"` error. You must write `Player.TeamID` or `Team.TeamID`.
3.  **Join Chain Fragmentation:** Forgetting to declare the join links in sequence when querying three tables. You cannot join table 1 to table 3 without passing through the intermediate foreign-key table 2.

---

### Review and Connect
You have now unlocked the power of relational queries using `INNER JOIN`. Next, we will expand our toolkit to perform calculations over large sets of matching rows—such as calculating a school's total sports points—using SQL aggregate functions.

---

## Lesson 16.3: Aggregates & Grouping

### Your Goal
Construct SQL statements utilizing aggregate functions (`COUNT`, `SUM`, `AVG`) and the `GROUP BY` clause to calculate, group, and summarize numerical data.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 6.3: Accumulating Data](./year-11-textbook-chapter-6.md#lesson-63-accumulating-data) (understanding the programmatic concept of sums and averages).
*   [Lesson 16.2: Relational Queries & Joins](#lesson-162-relational-queries--joins).

### The Idea
In programming, to calculate the average score of a group of students, we have to write a `for` loop to traverse an array, maintain an accumulator variable, and divide the total sum by the count.

In SQL, we can calculate these statistics in a single line of code using **Aggregate Functions**. These functions take multiple values from a column and compress them into a single, summary calculation.

**The Analogy:**
Imagine a stack of ovals scorecards. 
*   If you count the physical cards, you are running a `COUNT` function.
*   If you add up all the points written on the cards, you are running a `SUM` function.
*   If you calculate the typical point score on a card, you are running an `AVG` function.
*   If you divide the cards into stacks *by school* before doing these calculations, you are executing a `GROUP BY` clause.

```
       [ RAW ATHLETE DATABASE RECORD ROWS ]
   +------------------------------------------+
   | Name   | SchoolID | RaceTime (Seconds)   |
   |--------|----------|----------------------|
   | Sarah  | Red      | 12.50                |
   | Mark   | Blue     | 14.10                |
   | Amy    | Red      | 13.10                |
   | John   | Blue     | 15.30                |
   +------------------------------------------+
                        ||
                        \\/
         [ GROUP BY SchoolID SEPARATION ]
            /                        \\
    { RED HOUSE STACK }       { BLUE HOUSE STACK }
    | Sarah | 12.50   |       | Mark | 14.10     |
    | Amy   | 13.10   |       | John | 15.30     |
            \\                        /
             \\                      /
          [ APPLY AVG() AGGREGATE FUNCTION ]
              ||                    ||
              \\/                    \\/
         Avg = 12.80s          Avg = 14.70s
```

#### **SCSA Key Terms**
*   **Aggregate Function:** A mathematical operation performed on a set of rows to return a single value.
*   **`COUNT()`:** Returns the total number of records that match the query criteria.
*   **`SUM()`:** Calculates the mathematical total of all values in a numeric column.
*   **`AVG()`:** Calculates the arithmetic mean of all values in a numeric column.
*   **`GROUP BY`:** An SQL clause that groups rows with identical values in designated columns into single, summary rows.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival coordinator wants to see a breakdown of the **average race time** and the **total number of runners** for each participating school.

#### **The Query Statement**
```sql
SELECT School.SchoolName, 
       COUNT(Athlete.AthleteID) AS TotalRunners, 
       AVG(Athlete.RaceTime) AS AverageSprintTime
FROM Athlete
INNER JOIN School ON Athlete.SchoolID = School.SchoolID
GROUP BY School.SchoolName;
```

#### **How the Logic Flows**
1.  **`GROUP BY School.SchoolName`**: The RDBMS sorts all athlete records into distinct piles based on their school names.
2.  **`COUNT(Athlete.AthleteID)`**: The engine counts how many athlete records are in each school's pile, outputting the result under the alias name `TotalRunners`.
3.  **`AVG(Athlete.RaceTime)`**: The engine calculates the average of the race times in each pile, outputting the result as `AverageSprintTime`.
4.  **Result Table**: Instead of displaying hundreds of individual athletes, the output displays exactly one summary row per school.

---

### Try It with Help
#### **The Problem**
A database tracks carnival house points scored in individual athletic trials:
*   `Result` table (columns: `ResultID`, `AthleteID`, `PointsScored`, `EventID`)

Write an SQL query that calculates:
1.  The **total points** scored across the entire carnival.
2.  The **maximum points** scored in any single trial.
*   *Note:* You can use the SQLite built-in aggregate function `MAX(column)` to find the largest value.

#### **Structural Hints**
*   To sum points, use the `SUM()` aggregate function.
*   To find the largest point value, use the `MAX()` aggregate function.
*   Since you are calculating a single, global summary for the entire table, you **do not** need a `GROUP BY` clause.

#### **Scaffolded Code Template**
```sql
SELECT SUM(PointsScored) AS TotalCarnivalPoints, 
       MAX(PointsScored) AS HighestSingleScore
FROM Result;
```

---

### Try It Yourself
#### **The Problem**
Consider a school library loan database:
*   `Loan` table (columns: `LoanID`, `BookID`, `StudentID`, `OverdueDays`, `FineAmount`)

Write an SQL statement that displays each `StudentID` alongside the **total sum of their fines** (`FineAmount`) and the **average number of days overdue** (`OverdueDays`). Only include loans where `FineAmount` is greater than `0`, and group the final summary by the `StudentID`.

---

### Check Your Reasoning
#### **The Answer**
```sql
SELECT StudentID, 
       SUM(FineAmount) AS TotalFines, 
       AVG(OverdueDays) AS AverageDaysOverdue
FROM Loan
WHERE FineAmount > 0
GROUP BY StudentID;
```

#### **Common SCSA Student Errors**
1.  **Forgetting `GROUP BY`:** Attempting to query individual attributes alongside aggregate columns without a grouping clause (e.g., `SELECT StudentID, SUM(FineAmount) FROM Loan;`). Without a `GROUP BY StudentID` clause, the database will fail or return a single row containing a random Student ID and the total sum of all student fines.
2.  **Using `WHERE` instead of `HAVING` for Aggregates:** Trying to write `WHERE SUM(FineAmount) > 50` to filter group outputs. The `WHERE` clause filters *individual rows* before they are grouped. To filter *group calculation results*, you must use the `HAVING` clause: `GROUP BY StudentID HAVING SUM(FineAmount) > 50;`.
3.  **Averages on Non-Numeric Fields:** Attempting to perform mathematical aggregates like `SUM()` or `AVG()` on string fields (e.g. `AVG(FirstName)`). This will return `0` or cause compilation errors.

---

### Review and Connect
You have mastered multi-table joins and statistical group aggregates. In our final lesson, we will shift focus from data extraction to professional database administration, securing database installations against malicious exploitation and system failures.

---

## Lesson 16.4: Developer Security, Backups & SQL Injection Defense

### Your Goal
Design comprehensive database backup strategies and implement secure, parameterised queries to defend software solutions against SQL Injection (SQLi) attacks.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 10.3: The CIA Triad of Security Analysis](./year-11-textbook-chapter-10.md#lesson-103-the-cia-triad-of-security-analysis) (Confidentiality, Integrity, Availability).
*   [Lesson 11.2: Active System Exploits](./year-11-textbook-chapter-11.md#lesson-112-active-system-exploits-sqli-dos-xss-mitm-back-doors) (specifically how SQL Injection operates).

### The Idea
A professional database developer is responsible for more than just database schemas and SQL queries. They must also safeguard the **availability** of the system through robust backups and preserve its **confidentiality and integrity** by writing secure code that resists hostile manipulation.

#### **1. Database Backup Strategies**
If a server's storage drive fails, or if a ransomware attack encrypts the school's record system, the database is lost. To defend against data loss, developers implement structured backup schedules combining three distinct methods:

*   **Full Backup:** Captures a complete copy of the entire database file.
    *   *Pros:* Simplest recovery. All data is in one file.
    *   *Cons:* Very slow to execute and consumes massive storage space.
*   **Differential Backup:** Captures only the data that has changed since the **last full backup**.
    *   *Pros:* Quicker than a full backup; saves storage.
    *   *Cons:* To restore, you need both the last full backup *and* the last differential file.
*   **Incremental Backup:** Captures only the data that has changed since the **last backup of any kind** (full or incremental).
    *   *Pros:* The fastest backup method; consumes the least storage space.
    *   *Cons:* Most complex recovery. To restore, you must sequentially rebuild the database using the last full backup and *every single consecutive incremental file* in order.

#### **2. SQL Injection (SQLi) and Parameterisation**
As studied in Chapter 11, SQL Injection occurs when user inputs (like a username or search term) are joined directly into an SQL command string as executable code. 

To prevent SQLi, developers **never** use string concatenation (`+` or f-strings) to build SQL queries. Instead, they write **Parameterised Queries** (also called prepared statements).

**The Analogy:**
Imagine a restaurant customer ordering a burger.
*   **Raw Concatenation:** The chef hands the customer a blank order pad. The customer writes: `"Give me a beef burger AND burn down the kitchen"`. The kitchen blindly reads and executes the entire string.
*   **Parameterisation:** The chef hands the customer a strict, laminated form with a single box labeled "Burger Fillings". The customer writes `"beef AND burn down the kitchen"` inside the box. The chef reads the input solely as a physical ingredient, placing literal "burn down the kitchen" text on the burger patty without executing the text as an order command.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival public terminal allows parents to search for their child's name using an input box. 

Let's look at how insecure string concatenation leaves the system vulnerable, and how to rewrite the code safely in Python/SQLite using parameterisation.

#### **The Insecure Approach (String Concatenation)**
```python
# Malicious user input entered into the search box
user_input = "Sarah' OR '1'='1"

# The insecure query construction
insecure_query = "SELECT * FROM Athlete WHERE FirstName = '" + user_input + "';"

print("Executable Insecure Query:")
print(insecure_query)
# Output: SELECT * FROM Athlete WHERE FirstName = 'Sarah' OR '1'='1';
# DANGER: The SQL engine interprets '1'='1' as True, returning EVERY row in the database!
```

#### **The Secure Approach (Parameterised Query)**
```python
import sqlite3

# Establish a connection
connection = sqlite3.connect("carnival.db")
cursor = connection.cursor()

# Safe User Input
user_search = "Sarah"

# Use a placeholder (?) instead of concatenating variables
secure_query = "SELECT * FROM Athlete WHERE FirstName = ?;"

# Execute the query, passing the variable as a separate, sanitized tuple
cursor.execute(secure_query, (user_search,))

results = cursor.fetchall()
connection.close()
```

#### **How the Logic Flows**
*   The `?` character is a **placeholder**. It tells the database engine: *"An input value will go here, but do not compile it. Treat it strictly as a raw literal value."*
*   When `cursor.execute()` is called, the database engine compiles the SQL structure *before* looking at the user input. Even if the user inputs `' OR '1'='1, the engine simply searches for an athlete whose physical first name matches that exact, bizarre string, neutralizing the injection threat.

---

### Try It with Help
#### **The Problem**
You are designing a data backup policy for a WA regional hospital's medical database. The database is heavily modified during business hours (8 AM to 6 PM) on weekdays. Due to legal requirements, the hospital cannot afford to lose more than 24 hours of data.
1.  Propose a **weekly backup schedule** that minimizes storage usage and backup times while meeting this 24-hour data safety requirement.
2.  Briefly outline which backup files must be restored if the database system crashes on a **Thursday afternoon**.

#### **Structural Hints**
*   Start the schedule with a **Full Backup** on Sunday night when system activity is lowest.
*   To minimize storage consumption and daily processing times on weekdays, use **Incremental** backups rather than Full or Differential.
*   Recall that to restore from incremental backups, you must have the original Full backup and *all* subsequent incremental files up to the point of failure.

#### **Scaffolded Student Guide**
*   Step 1 (Schedule Proposal):
    *   Sunday 11:00 PM: Execute a **Full Backup**.
    *   Monday through Friday 11:00 PM: Execute an **Incremental Backup**.
*   Step 2 (Thursday Restore Procedure):
    *   1. Restore the **Full Backup** from Sunday.
    *   2. Restore the **Incremental Backup** from Monday.
    *   3. Restore the **Incremental Backup** from Tuesday.
    *   4. Restore the **Incremental Backup** from Wednesday.

---

### Try It Yourself
#### **The Problem**
A database developer is writing a backend Python script to update athlete password records. They write the following code:

```python
def update_password(athlete_id, new_password):
    # Establish connection
    db = sqlite3.connect("carnival.db")
    cursor = db.cursor()
    
    # Insecure query
    query = f"UPDATE Athlete SET Password = '{new_password}' WHERE AthleteID = {athlete_id};"
    
    cursor.execute(query)
    db.commit()
    db.close()
```

1.  Explain why this code block is highly vulnerable to an SQL Injection attack.
2.  Rewrite the function so that it uses a **secure parameterised query** with placeholders to neutralize the vulnerability.

---

### Check Your Reasoning
#### **The Answer**
1.  **Vulnerability Explanation:**
    *   The function uses Python f-strings (`f"UPDATE..."`) to perform direct string concatenation, merging user-supplied variables directly into the SQL executable structure.
    *   If a malicious user passes the string `"secret', Gender = 'F"` as the password, the executed query becomes: `UPDATE Athlete SET Password = 'secret', Gender = 'F' WHERE AthleteID = 101;`, allowing unauthorized modification of other fields. 
    *   Additionally, if a user inputs `' OR AthleteID > 0; --`, they can bypass the `WHERE` filter and overwrite *every* user password to the same value.

2.  **Secure Refactoring:**
```python
def update_password(athlete_id, new_password):
    db = sqlite3.connect("carnival.db")
    cursor = db.cursor()
    
    # Secure parameterised query using placeholders
    query = "UPDATE Athlete SET Password = ? WHERE AthleteID = ?;"
    
    # Pass variables inside a tuple as the second parameter of execute()
    cursor.execute(query, (new_password, athlete_id))
    
    db.commit()
    db.close()
```

#### **Common SCSA Student Errors**
1.  **Incorrect Tuple Formatting for Single Parameters:** Writing `(user_input)` instead of `(user_input,)`. In Python, a tuple with a single element *must* contain a trailing comma, or Python will treat it as a grouped string parenthetical, causing execution crashes.
2.  **Confusing Differential vs. Incremental Backups:** Claiming that a differential backup only tracks changes since the last incremental backup. Remember: **Differential relates back to the last Full backup; Incremental relates back to the last backup of *any* type.**

---

### Review and Connect
In this lesson, you mastered the security and administrative tasks of the database developer—scheduling full/incremental backups to preserve Availability, and writing parameterised queries to safeguard Confidentiality and Integrity. 

---

## Teacher Support Module

### SCSA Syllabus Mapping
*   **Unit 2 Databases:** SQL commands: `SELECT`, `INSERT`, `UPDATE`, `DELETE`; Database creation in SQLite; `INNER JOIN`s; Aggregate functions: `COUNT`, `SUM`, `AVG`.
*   **Unit 2 Cyber Security:** Developer backup strategies; database security and access control.

### Prerequisite Knowledge Diagnostic Checklist
Before teaching this chapter, ensure students can:
*   Identify Primary and Foreign Keys in relational schemas.
*   Differentiate between entity classes and instantiated record rows.
*   Understand the basic operation of variables and values in Python.

### High-Frequency Student Misconceptions
1.  **The "Blank Field" Misconception:** Students often assume that a field left empty or unpopulated stores an empty string `""` or numerical zero `0`. Emphasise that database fields without values hold a special **`NULL`** token, which behaves differently under query filters.
2.  **The "Automatic Join" Fallacy:** Students frequently assume that because a Foreign Key relationship is defined in an ERD, they can select fields from both tables without explicitly writing `INNER JOIN` in their SQL queries. Remind them that *all joins must be explicitly declared and mapped* in SQL.
3.  **The "Backup Protection" Myth:** Students often believe that having daily incremental backups secures a database against physical server room fires. Clarify that backups are only secure if stored **off-site** (or in a secure remote cloud environment), away from the primary server.

---

## Classroom Assessment Task
### **Chapter 16 Exam — SQLite Implementation & Security**
**Time Allowed:** 25 Minutes  
**Total Marks:** 20 Marks  

---

### **Section A: Short Answer & Calculations (10 Marks)**

#### **Question 1** (3 Marks)
Define the difference between **Data Definition Language (DDL)** and **Data Manipulation Language (DML)** in SQL. Provide one specific command example for each type.

*Space for Answer:*


<br><br><br>

#### **Question 2** (3 Marks)
A database administrator performs a **Full Backup** of a school's database on Sunday night. On Monday night, they perform an **Incremental Backup**. On Tuesday night, they perform another **Incremental Backup**.
The server's hard drive crashes on Wednesday morning.
Detail the exact steps and files required to completely restore the database system.

*Space for Answer:*


<br><br><br>

#### **Question 3** (4 Marks)
Consider the following two relational database tables:

**`House` Table**
| HouseID | HouseName | LeaderName |
| :--- | :--- | :--- |
| 1 | Gold | Mr. Davis |
| 2 | Silver | Mrs. Chang |

**`Competitor` Table**
| CompetitorID | Name | Points | HouseID |
| :--- | :--- | :--- | :--- |
| 501 | Alex | 120 | 1 |
| 502 | Beth | 90 | 1 |
| 503 | Cole | 150 | 2 |

Predict the exact tabular output returned when the database engine executes the following SQL query:
```sql
SELECT House.HouseName, 
       COUNT(Competitor.CompetitorID) AS TotalCompetitors, 
       SUM(Competitor.Points) AS TotalPoints
FROM Competitor
INNER JOIN House ON Competitor.HouseID = House.HouseID
GROUP BY House.HouseName;
```

*Space for Answer:*


<br><br><br>

---

### **Section B: SQL Query Design (10 Marks)**

#### **Scenario**
The WA Junior Sports Carnival uses a relational database to track high-jump results. The schema contains the following three tables:

*   **`School`** (`SchoolID` [PK], `SchoolName`, `Location`)
*   **`Athlete`** (`AthleteID` [PK], `FirstName`, `LastName`, `SchoolID` [FK])
*   **`JumpAttempt`** (`AttemptID` [PK], `AthleteID` [FK], `HeightCleared`, `IsFoul` [Boolean])

#### **Question 4** (3 Marks)
Write an SQL query that inserts a new school record into the `School` table:
*   `SchoolID`: `15`
*   `SchoolName`: `'Hills Grammar'`
*   `Location`: `'Darlington'`

*Space for Answer:*


<br><br><br>

#### **Question 5** (3 Marks)
Write a relational query using an `INNER JOIN` that returns the `FirstName` and `LastName` of every athlete alongside the `SchoolName` of their school, sorted alphabetically by the athlete's `LastName`.

*Space for Answer:*


<br><br><br>

#### **Question 6** (4 Marks)
Write a complex SQL query that displays the `AthleteID` and the **average height cleared** (`HeightCleared`) for all athletes who have cleared an average height of strictly greater than **1.50 metres**. Only include jump attempts where there was no foul (`IsFoul = 0`), and group the results by `AthleteID`.

*Space for Answer:*


<br><br><br>

---

### **Teacher Marking Guide & Solutions**

#### **Question 1 Marking Guide** (3 Marks)
*   **1 Mark:** Correctly defines DDL as structural schema commands (e.g., defines tables, columns, constraints).
*   **1 Mark:** Correctly defines DML as data-level transaction commands (e.g., handles records, insertions, queries).
*   **1 Mark:** Provides appropriate examples (e.g. DDL: `CREATE TABLE`, `DROP TABLE`; DML: `SELECT`, `INSERT`, `UPDATE`, `DELETE`).
*   *Model Answer:* DDL (Data Definition Language) is used to create or modify the structure of the database, such as tables and columns (Example: `CREATE TABLE`). DML (Data Manipulation Language) is used to manipulate and retrieve the actual data stored within those structures (Example: `SELECT`).

#### **Question 2 Marking Guide** (3 Marks)
*   **1 Mark:** Mentions restoring the Full Backup from Sunday first.
*   **1 Mark:** Mentions applying both incremental backup files in chronological order (Monday then Tuesday).
*   **1 Mark:** Explains that without the sequential application of all incremental files, data integrity is compromised.
*   *Model Answer:* To restore the system:
    1. Replace the damaged drive and restore the **Sunday Full Backup** file.
    2. Sequentially apply the **Monday Incremental Backup** file to catch Monday's updates.
    3. Apply the **Tuesday Incremental Backup** file to catch Tuesday's updates up to the close of business.

#### **Question 3 Marking Guide** (4 Marks)
*   **1 Mark:** Correctly structures table columns (HouseName, TotalCompetitors, TotalPoints).
*   **1 Mark:** Correctly calculates Silver house stats (1 competitor, 150 points).
*   **1 Mark:** Correctly calculates Gold house stats (2 competitors, 210 points).
*   **1 Mark:** Excludes keys or extra fields, displaying only the requested attributes.
*   *Model Answer:*
    | HouseName | TotalCompetitors | TotalPoints |
    | :--- | :--- | :--- |
    | Gold | 2 | 210 |
    | Silver | 1 | 150 |

#### **Question 4 Marking Guide** (3 Marks)
*   **1 Mark:** Correct syntax for `INSERT INTO School (SchoolID, SchoolName, Location)`.
*   **1 Mark:** Correct syntax for `VALUES (15, 'Hills Grammar', 'Darlington')`.
*   **1 Mark:** Correct inclusion of quotes for string types and a terminating semicolon.
*   *Model Answer:*
    ```sql
    INSERT INTO School (SchoolID, SchoolName, Location) 
    VALUES (15, 'Hills Grammar', 'Darlington');
    ```

#### **Question 5 Marking Guide** (3 Marks)
*   **1 Mark:** Correct `SELECT` clause with disambiguated table prefixes.
*   **1 Mark:** Correct `INNER JOIN` syntax and join condition (`Athlete.SchoolID = School.SchoolID`).
*   **1 Mark:** Correct sorting clause (`ORDER BY Athlete.LastName ASC`).
*   *Model Answer:*
    ```sql
    SELECT Athlete.FirstName, Athlete.LastName, School.SchoolName
    FROM Athlete
    INNER JOIN School ON Athlete.SchoolID = School.SchoolID
    ORDER BY Athlete.LastName ASC;
    ```

#### **Question 6 Marking Guide** (4 Marks)
*   **1 Mark:** Correct `SELECT` using aggregate function `AVG(HeightCleared)`.
*   **1 Mark:** Correct filter for non-fouls using `WHERE IsFoul = 0` (or `IsFoul = 'False'`).
*   **1 Mark:** Correct grouping using `GROUP BY AthleteID`.
*   **1 Mark:** Correct group-level filtering using `HAVING AVG(HeightCleared) > 1.50`.
*   *Model Answer:*
    ```sql
    SELECT AthleteID, AVG(HeightCleared) AS AvgHeight
    FROM JumpAttempt
    WHERE IsFoul = 0
    GROUP BY AthleteID
    HAVING AVG(HeightCleared) > 1.50;
    ```
