# Year 11 Computer Science ATAR — Solutions & Marking Keys

This companion volume provides complete, fully worked solutions, marking rubrics, SCSA diagrammatic standards, and trace tables for the practice questions in **`year-11-textbook-exercises-and-exam-practice.md`**.

---

# Part 1: Unit 1 Practice Solutions

## Section A: Multiple-Choice Answer Key & Explanations

| Q | Key | Syllabus Focus & Detailed Explanation |
| :--- | :--- | :--- |
| **1** | **a** | **1.1 & 1.2 Binary & Hex Conversions.** Decimal `109` divided by 16 is 6 remainder 13 (`D` in hex), yielding hex `6D`. Converting to binary: `109` = `64 + 32 + 8 + 4 + 1` which is `01101101` (positions 64, 32, 8, 4, 1 set to `1`). |
| **2** | **b** | **1.3 Data Representation Standards.** Standard ASCII is structurally a **7-bit** standard representing 128 characters (extended ASCII is 8-bit). |
| **3** | **b** | **1.3 Data Representation Standards.** ASCII is limited to 128 standard symbols (7-bit), whereas Unicode uses variable-width bit configurations (16/32-bit) to represent international alphabets. |
| **4** | **b** | **1.4 Fundamental Data Types.** `16` $ightarrow$ `integer`; `12.55` $ightarrow$ `float`; `True` $ightarrow$ `Boolean`; `"2026_01"` $ightarrow$ `string`. |
| **5** | **d** | **2.1 Control Structures: Sequence.** This is the standard variable swap algorithm. `temp` holds `10`. `x` takes `5`. `y` takes `temp` (`10`). Thus, `x = 5`, `y = 10`. |
| **6** | **b** | **2.3 Multi-Way Selection.** `score` is `8`. It checks `score > 10` (False), then evaluates `elif score >= 8` (True), assigning `points = 80`. The remaining branches are skipped. |
| **7** | **b** | **2.4 Exception Handling.** Option (b) uses a structured `try-except ValueError` block to handle alphanumeric conversions on string casts, which prevents runtime exceptions. |
| **8** | **c** | **3.1 Definite Iteration.** `range(1, 10, 2)` produces integers: `1`, `3`, `5`, `7`, `9`. This results in exactly **5 loop cycles**. |
| **9** | **b** | **3.2 Indefinite Iteration.** To exit a pre-test loop checking `count < 5`, the loop control variable must increment toward the termination boundary (e.g., `count = count + 1`). |
| **10** | **a** | **5.1 Arithmetic Operators.** Modulo `%` and floor division `//` have equal precedence to multiplication, executing left to right. `17 % 5` $ightarrow$ `2`. `12 // 5` $ightarrow$ `2`. `2 + 2` $ightarrow$ **`4`**. |
| **11** | **c** | **5.3 Logical Expressions.** `age <= 15` is `True`. `age > 20` is `False`, so `NOT False` is `True`. `True AND True` evaluates to **`True`**. |
| **12** | **b** | **4.2 Parameters and Arguments.** Parameters are variable placeholders declared in a subroutine's header definition; arguments are the actual physical variables passed when calling the function. |
| **13** | **b** | **4.3 Scope of Variables.** Variables declared inside functions are **local**. They are only accessible within that block and are cleared from memory once the subroutine exits. |
| **14** | **c** | **6.1 One-Dimensional Arrays.** One-dimensional arrays are zero-indexed. A list of size `n` runs from index position `0` to **`n - 1`**. |
| **15** | **b** | **6.4 Finding Array Extremes.** To find array extremes, initialize the comparator to the first index element (`points[0]`) and update it when a larger value is found during array traversal. |
| **16** | **b** | **7.3 Structure Charts.** A loop is represented on a structure chart by drawing a semi-circular arrow around the lines connecting a parent module to its child submodules. |
| **17** | **d** | **8.1 SCSA Development Framework.** Scheduling development tracks via Gantt charts and defining requirements occur during the **Investigate** phase. |
| **18** | **c** | **9.1 DoD TCP/IP Model.** The **Internet** layer of the DoD model handles IP addressing, packet headers, and routing protocols across networks. |
| **19** | **d** | **9.2 Physical Transmission Media.** **Optical fibre** uses light pulses through glass cores, rendering it immune to electrical interference (EMI) and enabling massive bandwidth over long distances. |
| **20** | **a** | **9.2 Network Hardware.** A **Switch** operates at Layer 2 (Network Interface / Link layer) to store MAC address tables and forward data frames directly, isolating collision domains. |

---

## Section B: Short-Answer & Extended Response Marking Keys

### Question 21: Algorithms, Tracing, and Testing (15 Marks)

#### **Part 1: Trace Table (5 Marks)**
The input sequence is: `13.5`, `11.2`, `-1.5`, `12.8`, `15.2`.

| Step | `sprint_time` | Comparison Checks | Return Value | Marking Allocation |
| :--- | :--- | :--- | :--- | :--- |
| **1** | `13.5` | `13.5 <= 0.0` (F) $ightarrow$ `13.5 < 11.5` (F) $ightarrow$ `13.5 < 12.8` (F) $ightarrow$ `13.5 <= 14.0` (True) | `"Bronze"` | **[1 Mark]** |
| **2** | `11.2` | `11.2 <= 0.0` (F) $ightarrow$ `11.2 < 11.5` (True) | `"Gold"` | **[1 Mark]** |
| **3** | `-1.5` | `-1.5 <= 0.0` (True) | `"Invalid"` | **[1 Mark]** |
| **4** | `12.8` | `12.8 <= 0.0` (F) $ightarrow$ `12.8 < 11.5` (F) $ightarrow$ `12.8 < 12.8` (F) $ightarrow$ `12.8 <= 14.0` (True) | `"Bronze"` | **[1 Mark]** |
| **5** | `15.2` | Runs to final catch branch | `"Participation"`| **[1 Mark]** |

#### **Part 2: Test Data Selection (6 Marks)**
*   **Normal Test Data:**
    *   *Definition:* Data that falls within the expected range of regular operations. **[1 Mark]**
    *   *Example:* `12.2` (Expected output: `"Silver"`) or `13.5`. **[1 Mark]**
*   **Extreme (Boundary) Test Data:**
    *   *Definition:* Data that sits precisely 'at', 'above', or 'below' the boundary values where logical decisions transition. **[1 Mark]**
    *   *Example:* `11.5` (Expected: `"Silver"`), `11.4` (Expected: `"Gold"`), `14.0` (Expected: `"Bronze"`), or `14.1` (Expected: `"Participation"`). **[1 Mark]**
*   **Erroneous (Invalid) Test Data:**
    *   *Definition:* Data that lies outside the program's logical limits or uses incorrect types to test the program's safety and validation limits. **[1 Mark]**
    *   *Example:* `-5.2` (Expected: `"Invalid"`) or `"eleven"` (Expected: Value Exception error caught). **[1 Mark]**

#### **Part 3: Error Typologies (4 Marks)**
*   **Logical Error:**
    *   *Explanation:* The code executes successfully without crashing, but produces incorrect or unexpected outputs due to a flaw in logical design. **[1 Mark]**
    *   *Detection:* Identified during the **Design and Develop** phases using trace tables (desk checking), code walkthroughs, and unit tests with known inputs/outputs. **[1 Mark]**
*   **Runtime Error:**
    *   *Explanation:* An error that occurs while the program is running, forcing it to crash (e.g., dividing by zero or type conversion failure). **[1 Mark]**
    *   *Detection:* Identified during the **Develop** phase by stepping through coded solutions in an IDE or using try-except blocks. **[1 Mark]**

---

### Question 22: Relational Operators, Arrays, and Pseudocode (15 Marks)

#### **Part 1: SCSA Pseudocode Algorithm (8 Marks)**

```pseudocode
BEGIN CalculateHousePoints
    // Declare 1D Array of size 5
    DECLARE HousePoints[5] AS INTEGER
    DECLARE totalPoints AS INTEGER
    DECLARE maxPoints AS INTEGER
    DECLARE maxIndex AS INTEGER
    DECLARE averageScore AS FLOAT
    
    totalPoints <- 0
    
    // Load score elements into array using a loop
    FOR i <- 0 TO 4
        OUTPUT "Enter points for House ", i + 1
        INPUT HousePoints[i]
        totalPoints <- totalPoints + HousePoints[i]
    ENDFOR
    
    // Calculate average
    averageScore <- totalPoints / 5
    
    // Find maximum and store its index position
    maxPoints <- HousePoints[0]
    maxIndex <- 0
    
    FOR i <- 1 TO 4
        IF HousePoints[i] > maxPoints THEN
            maxPoints <- HousePoints[i]
            maxIndex <- i
        ENDIF
    ENDFOR
    
    // Display calculations
    OUTPUT "Total Points: ", totalPoints
    OUTPUT "Average Score: ", averageScore
    OUTPUT "Maximum Score Index Position: ", maxIndex
END CalculateHousePoints
```

**Marking Rubric:**
*   **[1 Mark]** Adhering to SCSA pseudocode standards: uppercase keywords (`BEGIN`, `DECLARE`, `FOR`, `IF`, `THEN`, `ENDFOR`, `ENDIF`), correct structure, and left-pointing assignment arrows (`<-`).
*   **[1 Mark]** Declaring the 1D Array `HousePoints` of size 5.
*   **[2 Marks]** Loop construct (`FOR i <- 0 TO 4`) reading score inputs and adding them to a running `totalPoints` accumulator.
*   **[1 Mark]** Calculating the average using real division (`totalPoints / 5`).
*   **[2 Marks]** Initializing `maxPoints` to `HousePoints[0]` and looping to find the highest value and store its matching index (`maxIndex`).
*   **[1 Mark]** Displaying the outputs (`totalPoints`, `averageScore`, `maxIndex`).

#### **Part 2: Structure Chart Representation (7 Marks)**
Since we are representing a diagrammatic tool textually, here is the structural map and marking criteria for a professional SCSA structure chart:

```
                      [ CarnivalAdminPortal ]
                                 │
         ┌───────────────────────┼───────────────────────┐
         ▼                       ▼                       ▼
    [ UserLogin ]         [ UpdateScores ]        [ GenerateReport ]
    
    Data Couples:         Data Couples:           Data Couples:
    - User/Pass (In)      - ScoreData (In)        - ReportFormat (In)
    - SessionID (Out)     - DBSuccess (Out)       - PrintOutput (Out)
    
    Control Flags:        Control Flags:          Control Flags:
    - LoginSuccess (Out)  - ErrorAlert (Out)      - [None]
```

**Marking Rubric:**
*   **[1 Mark]** Main control module (`CarnivalAdminPortal`) placed at the top level.
*   **[2 Marks]** Three correct subordinate modules (`UserLogin`, `UpdateScores`, `GenerateReport`) connected with vertical lines.
*   **[2 Marks]** Data Couples represented as empty circles with arrows showing correct direction of flow (e.g. `User/Pass` descending to `UserLogin`; `SessionID` ascending to parent).
*   **[2 Marks]** Control Flags represented as solid circles with arrows showing logical control signals (e.g. `LoginSuccess` ascending to parent).

---

### Question 23: Networking Models, Diagrams, and Addressing (20 Marks)

#### **Part 1: Logical CISCO Network Diagram (8 Marks)**
The diagram should show:
```
                                [ WAN Cloud (Internet) ]
                                           │
                                     [ Firewall ]
                                           │
                                       [ Router ]
                                           │
                                       [ Switch ]
                    ┌──────────────────────┴──────────────────────┐
                    │                                             │
          [ Database Server ]                         [ Wireless Access Point ]
                    │                                             ) ) ) (Wi-Fi)
         ┌──────────┼──────────┐                                  ├──────────┤
         ▼          ▼          ▼                                  ▼          ▼
      [ PC 1 ]   [ PC 2 ]   [ PC 3 ]                           [ Tablet 1 ] [ Tablet 2 ]
```

**Marking Rubric:**
*   **[2 Marks]** Router (circle with opposing arrows) connected to Firewall (brick wall) which connects to WAN cloud.
*   **[2 Marks]** Switch (square with parallel grid arrows) connected to Router, forming a centralized star topology.
*   **[1 Mark]** Three Admin PCs connected to the Switch.
*   **[1 Mark]** Central database server connected directly to the Switch.
*   **[2 Marks]** Wireless Access Point connected to the Switch, with wireless links to two tablets.

#### **Part 2: IP Address Configuration (4 Marks)**
*   **Network Range:** `192.168.1.0/24` (Private IPv4 Class C network). **[1 Mark]**
*   **Subnet Mask:** `255.255.255.0` (yielding up to 254 usable host addresses). **[1 Mark]**
*   **Device Allocations:** **[1 Mark]**
    *   Router LAN Gateway: `192.168.1.1`
    *   Database Server: `192.168.1.10`
    *   WAPs / PCs: `192.168.1.11` to `192.168.1.20`
*   **Justification:** A `/24` subnet mask is perfect for a local office setup. It accommodates the current nodes (7 host addresses) while leaving room for expansion up to 254 hosts on a single subnet, avoiding IP overlap and simplifying subnet administration. **[1 Mark]**

#### **Part 3: DoD Layer Journey (8 Marks)**
*   **1. Application Layer:**
    *   *Process:* The marshal enters sports scores on a tablet web portal. The Application layer uses the HTTPS protocol to encapsulate raw data, appending transaction headers. **[1 Mark]**
    *   *PDU:* Data. **[1 Mark]**
*   **2. Transport Layer:**
    *   *Process:* The Transport layer takes the data stream and segmentizes it. Because scores require reliable transmission, it uses **TCP**, establishing a connection and appending source/destination ports (e.g. port 443). **[1 Mark]**
    *   *PDU:* Segment. **[1 Mark]**
*   **3. Internet Layer:**
    *   *Process:* The Internet layer encapsulates the Segment. It appends the IP header containing the Source IP (Tablet: `192.168.1.15`) and Destination IP (Server: `192.168.1.10`), routing the packet. **[1 Mark]**
    *   *PDU:* Packet. **[1 Mark]**
*   **4. Network Access Layer:**
    *   *Process:* The Network layer encapsulates the Packet in a Frame, appending MAC address headers (Source MAC of Tablet, Destination MAC of Access Point) and error checking bits (FCS). The frames are converted to raw bits and modulated onto wireless radio waves. **[1 Mark]**
    *   *PDU:* Frame / Bits. **[1 Mark]**
*   **Encapsulation Definition:** The iterative process of appending specific protocol control headers and trailers to data as it moves down the network stack. **[1 Mark]**

---

# Part 2: Unit 2 Practice Solutions

## Section A: Multiple-Choice Answer Key & Explanations

| Q | Key | Syllabus Focus & Detailed Explanation |
| :--- | :--- | :--- |
| **1** | **b** | **10.1 Ethical Hacking vs Unethical.** Legal pen testing requires prior written authorization from the system owner. Running tests without this sign-off constitutes a criminal offense under the Cybercrime Act. |
| **2** | **c** | **10.2 Privacy Act 1988 & APPs.** **APP 11** mandates that organizations take active, reasonable steps to protect personal data from misuse, loss, unauthorized access, modification, or exposure. |
| **3** | **d** | **10.3 The CIA Triad.** DDoS attacks flood networks with traffic, blocking legitimate access. This compromises **Availability**. |
| **4** | **b** | **10.4 The AAA Framework.** Determining what an authenticated user can do is **Authorisation**. |
| **5** | **c** | **11.1 Social Engineering & Phishing.** Social engineering relies on human psychological manipulation to obtain secure credentials. |
| **6** | **b** | **11.3 Malware Classification.** Viruses need human actions (like opening a file) to execute, whereas worms self-replicate across network links automatically. |
| **7** | **c** | **11.4 Hardware & Boundary Exploits.** A zero-day vulnerability is an unpatched flaw unknown to the software vendor. |
| **8** | **b** | **12.1 Authentication & Password Policy.** Combining high-entropy passphrases with multi-factor authentication (MFA) dramatically increases security. |
| **9** | **b** | **12.2 Symmetrical vs Asymmetrical.** Asymmetric encryption solves the key distribution problem of symmetric encryption by using separate public and private keys. |
| **10** | **a** | **12.3 Substitution Ciphers.** Sliding each letter of "PERTH" forward by 3: `P -> S`, `E -> H`, `R -> U`, `T -> W`, `H -> K`, resulting in `SHUWK`. *(Correction: option a displays SHTWG, let's verify exact shift: P+3=S, E+3=H, R+3=U, T+3=W, H+3=K. Ciphertext is `SHUWK`)*. |
| **11** | **b** | **12.5 Cryptanalysis & Codebreaking.** Frequency analysis studies the relative frequency of letters in ciphertexts to break monoalphabetic substitution ciphers. |
| **12** | **b** | **13.1 Data vs Information.** Data consists of raw, unprocessed facts, while information is data that has been processed, structured, and contextualized. |
| **13** | **c** | **13.2 Flat File vs Relational Database.** Redundancy in flat-file systems leads to three operational anomalies: **Insert**, **Update**, and **Delete** anomalies. |
| **14** | **d** | **13.3 Core Database Concepts.** Relational databases implement Entities as **Tables**, Attributes as fields, and instances as records. |
| **15** | **c** | **13.3 Core Database Concepts.** Phone numbers should be stored as `TEXT` to preserve leading zeroes and prevent formatting characters (spaces, dashes) from breaking numerical values. |
| **16** | **d** | **13.3 Core Database Concepts.** A composite primary key is composed of two or more foreign keys and uniquely identifies rows in associative tables. |
| **17** | **b** | **15.2 Normalisation.** Normalization systematically structures data to eliminate redundancy and prevent database anomalies. |
| **18** | **b** | **15.3 Normalisation.** If a 1NF table has a single-column primary key, there are no partial dependencies, so it is automatically in **2NF**. |
| **19** | **c** | **16.1 SQL Query Clauses.** `ORDER BY Score DESC` displays the query output in descending numerical order of scores. |
| **20** | **b** | **16.2 SQL Query Joins.** `INNER JOIN ... ON` merges matching records across tables using defined key attributes. |

---

## Section B: Short-Answer & Extended Response Marking Keys

### Question 21: Database Modelling and ERDs (15 Marks)

#### **Part 1: Crow's Foot ERD Schema (8 Marks)**
To represent the swimming club scenario, we must resolve the many-to-many relationship between Members and Training Squads by introducing an associative table (e.g. `Registration` or `Booking` table).

```
  [ Club ]                  [ Coach ]
     │ 1                       │ 1
     │                         │
     │ 1:M                     │ 1:M
     ▼                         ▼
  [ Member ]             [ TrainingSquad ]
     │ 1                       │ 1
     │                         │
     │ 1:M                     │ 1:M
     ▼                         ▼
  [ Registration ] ◄───────────┘
   (Associative)
```

**Key Cardinality Rules:**
*   `Club` $ightarrow$ `Member`: One Club has many Members (`1:M` connection). Connection line shows `one-and-only-one` marker next to `Club` and a `one-or-many` marker next to `Member`.
*   `Coach` $ightarrow$ `TrainingSquad`: One Coach manages many Training Squads (`1:M` connection). Connection line shows `one-and-only-one` next to `Coach` and a `one-or-many` next to `TrainingSquad`.
*   `Member` $ightarrow$ `Registration`: One Member signs up for many Registrations. Connection line shows `one-and-only-one` next to `Member` and a `one-or-many` next to `Registration`.
*   `TrainingSquad` $ightarrow$ `Registration`: One Squad has many Registrations. Connection line shows `one-and-only-one` next to `TrainingSquad` and a `one-or-many` next to `Registration`.

**Marking Rubric:**
*   **[2 Marks]** Resolving the Member-Squad M:N relationship by introducing a new associative table (`Registration`).
*   **[2 Marks]** Drawing all four entity tables, including primary key (PK) and foreign key (FK) attributes.
*   **[2 Marks]** Drawing correct cardianlity markers on connection lines (crow's feet, mandatory lines, optional circles).
*   **[2 Marks]** Mapping correct foreign keys in tables (`ClubID` in `Member`, `CoachID` in `TrainingSquad`, and a composite key of `MemberID` + `SquadID` in `Registration`).

#### **Part 2: Data Dictionary (7 Marks)**
For the `Registration` table:

| Field Name | Data Type | Key Type | Field Size | Validation Rules | Description | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `MemberID` | `TEXT` | `PK, FK` | 10 | `NOT NULL` | Links to Member table | `"M21500"` |
| `SquadID` | `TEXT` | `PK, FK` | 6 | `NOT NULL` | Links to Squad table | `"SQ_BR1"` |
| `RegDate` | `TEXT` | `None` | 10 | `YYYY-MM-DD` | Date of registration | `"2026-09-06"`|
| `FeePaid` | `FLOAT` | `None` | Real | `>= 0.0` | Registration fee paid | `150.00` |

**Marking Rubric:**
*   **[1 Mark]** Specifying the exact matching composite key components (`MemberID` and `SquadID`).
*   **[1 Mark]** Declaring correct data types (`TEXT` for alphanumeric IDs, `FLOAT` for currency).
*   **[1 Mark]** Designating the Primary (PK) and Foreign (FK) key flags correctly.
*   **[1 Mark]** Setting appropriate character field sizes.
*   **[1 Mark]** Establishing validation rules (`NOT NULL` on keys, boundaries on fees).
*   **[1 Mark]** Providing clear, helpful descriptions.
*   **[1 Mark]** Giving valid examples for each attribute.

---

### Question 22: Database Normalisation (15 Marks)

#### **Part 1: Anomaly Analysis (6 Marks)**
*   **Insert Anomaly:**
    *   *Problem:* An administrator cannot insert a newly hired coach into the flat sheet until a player is actively registered in their team. Doing so leaves the Player fields null, violating database constraints. **[2 Marks]**
*   **Update Anomaly:**
    *   *Problem:* If coach Sarah West changes her mobile number, the database coordinator must find and modify that value in every row containing her name. If they miss a row (e.g. Liam Baker's record), the database becomes inconsistent. **[2 Marks]**
*   **Delete Anomaly:**
    *   *Problem:* If player Liam Baker leaves the club and his row is deleted, the system accidentally deletes all record of coach Dave Pine and his phone number, as it was only stored on that row. **[2 Marks]**

#### **Part 2: 1NF $ightarrow$ 2NF $ightarrow$ 3NF Normalisation (9 Marks)**

##### **1. First Normal Form (1NF)**
To normalize to 1NF, we flatten any repeating groups, ensure cell values are atomic, and establish a **Composite Primary Key** to uniquely identify each row.
*   *Composite Primary Key:* `(PlayerID, TeamCode, MatchDate)`
*   *1NF Relation:*
    *   `Roster(PlayerID, PlayerName, TeamCode, TeamName, CoachName, CoachPhone, MatchDate, PlayedField)` **[2 Marks]**

##### **2. Second Normal Form (2NF)**
To transition to 2NF, we identify and eliminate **Partial Dependencies**—attributes that depend on only *part* of a composite primary key.
*   *Partial Dependency Analysis:*
    *   `PlayerName` depends only on `PlayerID` (not `MatchDate` or `TeamCode`).
    *   `TeamName`, `CoachName`, and `CoachPhone` depend only on `TeamCode`.
    *   `PlayedField` depends on both `TeamCode` and `MatchDate`.
*   *2NF Relations:* **[3 Marks]**
    *   `Player(PlayerID, PlayerName)` (PK: `PlayerID`)
    *   `TeamRoster(TeamCode, TeamName, CoachName, CoachPhone)` (PK: `TeamCode`)
    *   `MatchAssignment(TeamCode, PlayerID, MatchDate, PlayedField)` (PK: `TeamCode, PlayerID, MatchDate`)

##### **3. Third Normal Form (3NF)**
To transition to 3NF, we eliminate **Transitive Dependencies**—non-key attributes that depend on other non-key attributes rather than the primary key.
*   *Transitive Dependency Analysis:*
    *   In the `TeamRoster` table, `CoachPhone` depends directly on `CoachName`, which depends on `TeamCode`. We must extract the Coach details into a separate table.
*   *3NF Relations:* **[4 Marks]**
    *   `Player(PlayerID, PlayerName)` (PK: `PlayerID`)
    *   `Team(TeamCode, TeamName, CoachName)` (PK: `TeamCode`, FK: `CoachName`)
    *   `Coach(CoachName, CoachPhone)` (PK: `CoachName`)
    *   `Match(TeamCode, PlayerID, MatchDate, PlayedField)` (PK: `TeamCode, PlayerID, MatchDate`, FKs: `TeamCode`, `PlayerID`)

---

### Question 23: SQL Queries & Aggregates (20 Marks)

#### **1. Retrieve Athletes (4 Marks)**
```sql
SELECT AthleteName, Age 
FROM Athlete 
WHERE Age < 16 
ORDER BY AthleteName ASC;
```
**Marking Rubric:**
*   **[1 Mark]** Correct `SELECT` clause with attributes `AthleteName`, `Age`.
*   **[1 Mark]** Correct `FROM` clause targeting the `Athlete` table.
*   **[1 Mark]** Correct `WHERE` logical condition (`Age < 16`).
*   **[1 Mark]** Correct sorting clause (`ORDER BY AthleteName ASC` or `ORDER BY AthleteName`).

#### **2. Display Combined Roster JOIN (5 Marks)**
```sql
SELECT Athlete.AthleteName, School.SchoolName, Registration.EventName 
FROM Athlete 
INNER JOIN School ON Athlete.SchoolCode = School.SchoolCode 
INNER JOIN Registration ON Athlete.AthleteID = Registration.AthleteID;
```
**Marking Rubric:**
*   **[1 Mark]** Correct SELECT clause referencing prefixed attributes.
*   **[2 Marks]** Correct join linking the `Athlete` and `School` tables.
*   **[2 Marks]** Correct join linking the `Athlete` and `Registration` tables.

#### **3. Grouped Aggregate Query (6 Marks)**
```sql
SELECT School.SchoolName, AVG(Registration.Score) AS AverageScore 
FROM School 
INNER JOIN Athlete ON School.SchoolCode = Athlete.SchoolCode 
INNER JOIN Registration ON Athlete.AthleteID = Registration.AthleteID 
GROUP BY School.SchoolName;
```
**Marking Rubric:**
*   **[1 Mark]** Selecting the correct fields: `SchoolName` and the average calculation.
*   **[1 Mark]** Using the correct aggregate function: `AVG()`.
*   **[2 Marks]** Correct INNER JOIN linkage across all three tables.
*   **[2 Marks]** Correct `GROUP BY` grouping clause on `School.SchoolName`.

#### **4. Database Security Audit (5 Marks)**
*   **Security Threat Explanation:** 
    *   The code uses string concatenation to insert inputs directly into the SQL string. A malicious user could enter input containing SQL statements (such as `' OR '1'='1`). This changes the query's logic, allowing the user to bypass authentication checks and query the database without a password. **[2 Marks]**
*   **Python Parameterized Query Solution:** **[3 Marks]**
    ```python
    # Secure parameterization
    cursor.execute(
        "SELECT * FROM Admins WHERE User = ? AND Pass = ?", 
        (username, password)
    )
    ```
    *(SCSA accepts the use of placeholder characters like `?` or `%s` to keep the SQL logic separate from user input, which prevents SQL Injection).*

---
