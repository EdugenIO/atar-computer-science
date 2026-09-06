# Unit 1 — Chapter 8: Software Development Process

This chapter explores how software projects are planned, styled, and managed under the Western Australian SCSA Computer Science ATAR curriculum, and the legal and ethical frameworks that govern developer code. 

You will master the iterative **SCSA Technology Process** (Investigate, Design, Develop, Evaluate), implement standard **Good Programming Practices** to write clean, maintainable Python, and examine **Australian Copyright Laws** alongside licensing models (open source versus proprietary) to ensure ethical and lawful development.

These processes are critical for successfully organizing, documenting, and executing your **SCSA School-Based Programming Project (Assessment Task 1)** and written theory exams.

---

## Lesson 8.1: The SCSA Framework for Development

### Your Goal
Design, schedule, and document a software project lifecycle using the four structured phases of the SCSA framework: Investigate, Design, Develop, and Evaluate.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 7.3: Structure Charts & Stubs](./year-11-textbook-chapter-7.md#lesson-73-structure-charts--stubs) for early program design.
*   The overall scope of your **Unit 1 Programming Project (Assessment Task 1)**.

### The Idea
Imagine organizing the entire school's sports carnival. You wouldn't simply turn up on the day and start shouting names over a megaphone. If you did, lanes would be empty, times would go unrecorded, and the event would fall into absolute chaos. 

Instead, you plan systematically:
1.  **Investigate:** Survey the physical ovals, list how many student teams are participating, determine timing needs, and create a timeline schedule.
2.  **Design:** Draw layouts of the tracks, design scheduling sheets, and map out timing desk procedures.
3.  **Develop:** Set up the cones, configure the stopwatches, run practice timings, and test the digital recording system.
4.  **Evaluate:** Conduct the carnival, collect feedback from officials, and write a report detailing what worked and what should be improved next year.

In computer science, software development follows this exact logical sequence. SCSA defines this as the **Technology Process**, divided into four essential phases:

```
┌────────────────────────────────────────────────────────┐
│                      INVESTIGATE                       │
│  - Problem Description  - User Requirements            │
│  - Feasibility Studies  - Gantt Schedules              │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│                         DESIGN                         │
│  - Data Structures      - Pseudocode Algorithms        │
│  - User Interfaces      - Trace Table Testing          │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│                        DEVELOP                         │
│  - Code Implementation  - Syntax/Runtime Debugging     │
│  - Modular Compilation  - Unit Test Validations        │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│                        EVALUATE                        │
│  - User Acceptance Test - Client Feedback Assessment   │
│  - SCSA Marking Audit   - Developer Retrospective      │
└───────────────────────────┴────────────────────────────┘
```

#### **SCSA Key Terms**
*   **Investigate:** The initial phase where developers define the problem description, establish constraints, list user requirements, and construct development schedules (Gantt charts).
*   **Design:** The architectural phase where developers plan data structures, design and test algorithms (using pseudocode, flowcharts, or structure charts), and design user interfaces before coding.
*   **Develop:** The active implementation phase where developers write, debug, and validate code modules, conducting comprehensive unit testing against sample datasets.
*   **Evaluate:** The final review phase where developers conduct user acceptance testing, compile client feedback, and complete a reflective developer retrospective.
*   **Gantt Chart:** A horizontal bar chart that visually represents a project schedule, showing task names, start dates, durations, and overlapping milestones.

---

### See It Worked
#### **The Scenario**
The **WA Junior Sports Carnival** needs a digital stopwatch program to record and validate 100m sprint times. Below is how the development team documents this project through the SCSA framework.

#### **1. Investigate Phase**
*   **Problem Description:** Manual stopwatches lead to human errors. A software tool is required to read race times, validate inputs, and identify the winning runner.
*   **User Requirements:**
    *   **REQ-01:** The system must capture 3 sprint times as decimal floats.
    *   **REQ-02:** The system must reject negative times or times exceeding 60 seconds.
    *   **REQ-03:** The system must identify and display the minimum time.
*   **Development Schedule (Gantt Chart):**

| Task Name | Week 1 | Week 2 | Week 3 | Week 4 |
| :--- | :---: | :---: | :---: | :---: |
| **Investigate:** Requirements & Gantt Setup | █▒▒▒▒▒ | | | |
| **Design:** ERD, UI & Pseudocode | | █▒▒▒▒▒ | | |
| **Develop:** Coding, Debugging & Unit Tests | | | █▒▒▒▒▒ | |
| **Evaluate:** UAT & Retrospective Review | | | | █▒▒▒▒▒ |

#### **2. Design Phase**
*   **Data Structure:** Float variables `t1`, `t2`, `t3` to store times; string `winner` to store the school name.
*   **Algorithm Design (Pseudocode):**
    ```text
    BEGIN RecordSprint
        DISPLAY "Enter lane 1 time:"
        INPUT t1
        WHILE t1 <= 0 OR t1 > 60 DO
            DISPLAY "Invalid! Re-enter lane 1 time:"
            INPUT t1
        ENDWHILE
        
        DISPLAY "Enter lane 2 time:"
        INPUT t2
        ... [Repeat for t2, t3] ...
        
        IF t1 < t2 AND t1 < t3 THEN
            winner <- "Lane 1"
        ELSE IF t2 < t1 AND t2 < t3 THEN
            winner <- "Lane 2"
        ELSE
            winner <- "Lane 3"
        ENDIF
        DISPLAY winner, " wins!"
    END RecordSprint
    ```

#### **3. Develop Phase**
The developer writes the Python code, runs it, and executes **Unit Tests** to ensure bounds are checked:

| Test ID | Test Goal | Input Values | Expected Result | Actual Result | Pass/Fail |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **UT-01** | Standard Data | `12.5`, `13.1`, `11.8` | Output: "Lane 3 wins!" | Output: "Lane 3 wins!" | **PASS** |
| **UT-02** | Lower Boundary | `-1.5` | Reject input, trigger loop | Rejected, loop active | **PASS** |
| **UT-03** | Upper Boundary | `65.4` | Reject input, trigger loop | Rejected, loop active | **PASS** |

#### **4. Evaluate Phase**
*   **User Acceptance Testing (UAT):** The track marshal uses the stopwatch live. They confirm it is extremely accurate but suggest a larger on-screen display font size (Client Feedback).
*   **Developer Retrospective:** *"The try/except handler successfully prevented crashes when letters were inputted. However, in future iterations, we should load runner names from an external text file (Chapter 6) to speed up setup times."*

---

### Try It with Help
#### **The Problem**
The carnival coordinators want to build a **School Points Tracker** that adds points to one of three school houses: Gold, Blue, or Red. Use the scaffolded SCSA framework template below to document the planning phase.

#### **Scaffolded Planning Template**
*   **Problem Description:** We need a script to record points awarded for sports events and update the house totals.
*   **User Requirements:**
    *   **REQ-01:** System must accept points as an integer value.
    *   **REQ-02:** User must specify the team colour (Gold, Blue, Red).
    *   **REQ-03:** Invalid team names must be rejected.
*   **Gantt Scheduling Task (Complete the Chart):**
    *   Draw/fill in the boxes to schedule the **Design** phase for Week 2, **Coding/Development** for Week 3, and **Evaluation** for Week 4.

| Task Name | Week 1 | Week 2 | Week 3 | Week 4 |
| :--- | :---: | :---: | :---: | :---: |
| **Investigate:** Specs and Requirements | [X] | [ ] | [ ] | [ ] |
| **Design:** Logical algorithms and dictionaries | [ ] | [ ? ] | [ ] | [ ] |
| **Develop:** Python coding & point assertions | [ ] | [ ] | [ ? ] | [ ] |
| **Evaluate:** House master sign-off review | [ ] | [ ] | [ ] | [ ? ] |

*   **Design Phase (Algorithm Draft):**
    *   *Hint:* Complete the pseudocode block below to update point registers.
    ```text
    BEGIN UpdatePoints
        DISPLAY "Enter house colour:"
        INPUT colour
        WHILE colour != "Gold" AND colour != "Blue" AND colour != "Red" DO
            DISPLAY "Invalid House! Try again:"
            INPUT colour
        ENDWHILE
        
        DISPLAY "Enter points awarded:"
        INPUT points
        
        IF colour = "Gold" THEN
            gold_total <- gold_total + points
        ELSE IF colour = "Blue" THEN
            # ??? Complete the assignment
        ELSE
            # ??? Complete the assignment
        ENDIF
    END UpdatePoints
    ```

---

### Try It Yourself
#### **The Problem**
Design a comprehensive **SCSA Technology Process Plan** (Investigate, Design, Develop, Evaluate) for a regional high-jump monitoring database system. 
1.  Write a brief **Problem Description** and define **three technical user requirements** (including a data integrity validation rule).
2.  Sketch a simple **Gantt Chart table** mapping out a 4-week development timeline.
3.  Draft a short **Developer Retrospective prompt** explaining how you would evaluate the final system after it runs at the track.

---

### Check Your Reasoning
#### **The Answer**
```text
SCSA Technology Process Plan: High-Jump Monitoring System

1. INVESTIGATE PHASE
   - Problem Description: High-jump records are currently tracked on paper, resulting in transcript errors, lost records, and delays in ranking athletes. A digital logging tool is required.
   - User Requirements:
     * REQ-01: System must capture the athlete's ID (integer), attempt number (1, 2, or 3), and height cleared (float in metres).
     * REQ-02: Height values must be validated; inputs < 0.5m or > 2.5m must be rejected.
     * REQ-03: The system must store the data and identify the maximum height cleared for each athlete.

2. GANTT TIMELINE SCHEDULE
   - Week 1: Investigate (Requirements gathering & project scope document).
   - Week 2: Design (ERD database design, UI mockup, input-validation pseudocode).
   - Week 3: Develop (SQLite database creation, Python data-entry script, validation testing).
   - Week 4: Evaluate (User acceptance testing with track officials, retrospective reporting).

3. DEVELOPER RETROSPECTIVE EXCERPT
   "The input-validation loop successfully restricted erroneous height entries. However, during the event, marshals found typing heights manual and tedious. A future version should integrate barcode scanners for athlete IDs, and drop-down selectors for height values to eliminate manual keyboard input errors."
```

#### **Common SCSA Student Errors**
1.  **Overlapping Lifecycle Activities:** Attempting to write code (Develop) during the Investigate or Design phases. SCSA assessors expect clear boundaries—**no programming code should ever be written in the Design phase.**
2.  **Weak Requirements:** Writing vague requirements like *"The system must be fast and easy to use."* Requirements must be **functional, technical, and measurable** (e.g., *"System must reject values outside 0.5m to 2.5m"*).
3.  **Vague Retrospectives:** Focusing only on self-praise rather than critiquing the software's performance, user feedback, and structural technical scalability.

---

### Review and Connect
In this lesson, you explored the structured, iterative nature of the SCSA Technology Process. In the next lesson, you will learn how to write the code within the **Develop** phase to meet professional style and maintenance expectations.

---

## Lesson 8.2: Good Programming Practices

### Your Goal
Refactor unreadable, poorly structured Python code into a professional, self-documenting, and SCSA-compliant software solution.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 4.3: Scope of Variables](./year-11-textbook-chapter-4.md#lesson-43-scope-of-variables-global-vs-local).
*   The general conventions of Python comments and white space.

### The Idea
Imagine entering a library where none of the books have titles, they are randomly scattered on the floor, and there are no signs pointing to different genres. Even if the library technically has all the information, you would never be able to find anything or maintain the collection.

In software engineering, **writing code that merely "works" is not enough**. Other developers—or even you, six months from now—must be able to read, debug, and maintain the code. SCSA assesses **eight strict good programming practices** that ensure software is structured professionally:

1.  **Validate Input:** Stop garbage data entering your program loops before it causes a crash.
2.  **Meaningful Variable Names:** Use clear descriptors (e.g., `sprint_time_seconds` instead of `s` or `temp1`).
3.  **Constants for Readability:** Declare fixed settings in uppercase (e.g., `MAX_LANES = 8`) to make updates central and clear.
4.  **Comments to Explain Code:** Use `#` comments to document the *why* of complex logic, not just the *what*.
5.  **Standard Control Structures:** Stick to clean sequences, explicit branching, and controlled iteration blocks.
6.  **Indentation and White Space:** Separate distinct blocks with blank lines and indent loops consistently.
7.  **One Logical Task per Module:** Keep functions focused on a single job (e.g., `calculate_average()`).
8.  **Meaningful Names for Modules:** Name functions descriptively (e.g., `save_results_file()` instead of `do_stuff()`).

#### **SCSA Key Terms**
*   **Good Programming Practice:** A set of stylistic, architectural, and safety guidelines followed by developers to make code readable, robust, and maintainable.
*   **Constant:** A variable identifier whose value is set at compilation and remains unchanged throughout execution. Written in `UPPERCASE` by convention.
*   **Modular Cohesion:** The degree to which a programming module (function) performs a single, well-defined logical task.
*   **Refactoring:** The process of restructuring existing computer code without changing its external behaviour, aimed at improving readability and structure.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival timing desk has received a working script from a parent volunteer to calculate the average speed of a runner. While it runs successfully, it is completely unreadable and fails multiple SCSA design criteria.

#### **The Bad Code (Monolithic and Obfuscated)**
```python
# Bad Code
a = input("Enter distance:")
b = float(a)
c = input("Enter time:")
d = float(c)
if d > 0:
    e = b / d
    print("Result:", e)
else:
    print("Error")
```

#### **The SCSA-Compliant Refactored Solution**
```python
# ==========================================
# WA JUNIOR SPORTS CARNIVAL - SPEED MONITOR
# ==========================================
# Module Name: calculate_runner_speed
# Description: Validates inputs and calculates average speed in m/s.
# ==========================================

# 1. Constants (SCSA Practice: uppercase, readable settings)
MIN_RACE_TIME = 0.5
MAX_RACE_TIME = 60.0

def get_valid_time():
    """Module: get_valid_time
    Task: Loop input requests until a logical float time is captured."""
    while True:
        try:
            # SCSA Practice: Meaningful variable name
            time_seconds = float(input("Enter sprint time (seconds): "))
            
            # SCSA Practice: Input validation logic
            if MIN_RACE_TIME <= time_seconds <= MAX_RACE_TIME:
                return time_seconds
            else:
                print(f"Error: Time must be between {MIN_RACE_TIME} and {MAX_RACE_TIME}s.")
        except ValueError:
            print("Error: Invalid numerical format entered. Try again.")

def calculate_speed(distance_metres, time_seconds):
    """Module: calculate_speed
    Task: Core mathematical speed equation. Does ONE logical task."""
    # SCSA Practice: Whitespace and comments explaining formula
    speed_mps = distance_metres / time_seconds
    return speed_mps

# Main Execution Sequence
race_distance = 100.0  # Constant track distance
validated_time = get_valid_time()
average_speed = calculate_speed(race_distance, validated_time)

# Structured Output Display
print(f"\n--- RACE LEADERBOARD RESULT ---")
print(f"Distance: {race_distance} metres")
print(f"Sprint Time: {validated_time:.2f} seconds")
print(f"Average Speed: {average_speed:.2f} m/s")
```

#### **Why the Refactored Code is Better**
*   **Defensive Design:** If a user types `"twelve"` or enters `-5.0`, the system validates the error gracefully instead of crashing.
*   **Self-Documenting:** The variables `time_seconds` and `distance_metres` explain exactly what data is held.
*   **High Cohesion:** The input capture (`get_valid_time`) is isolated from the mathematical speed logic (`calculate_speed`). This makes debugging much easier if a formula changes.

---

### Try It with Help
#### **The Problem**
The junior scoring desk uses a script to calculate points based on house rankings. However, it uses global variables, cryptic names, and lacks structure. Refactor this script using the SCSA good programming standards.

#### **The Bad Code**
```python
# Raw point adder
g = 100 # gold
b = 85  # blue
r = 90  # red

def add(t, p):
    global g, b, r
    if t == 1:
        g = g + p
    elif t == 2:
        b = b + p
    else:
        r = r + p

add(1, 10)
print(g)
```

#### **Scaffolded Refactoring Guide**
*   Replace cryptic house variables `g`, `b`, `r` with a descriptive dictionary or localized variables.
*   Remove the `global` references. Use explicit parameter inputs and return statements.
*   Add `#` comments and function docstrings explaining the logical task.
*   Validate that points `p` cannot be negative.

#### **Code Template to Complete**
```python
# Constants for point limits
MAX_AWARDABLE_POINTS = 50

def update_house_points(current_total, points_to_add):
    """Calculates updated points for a single house.
    Performs ONE logical task and validates input."""
    # 1. Validate that points_to_add is positive and logical
    if points_to_add < 0 or points_to_add > MAX_AWARDABLE_POINTS:
        print("Error: Invalid point award.")
        return current_total
        
    # 2. Add points to total and return
    new_total = current_total + points_to_add
    return new_total

# Active program execution
gold_points = 100
blue_points = 85
red_points = 90

# SCSA Practice: Descriptively update points
points_input = 10
gold_points = update_house_points(gold_points, points_input)

print("Updated Gold House Total:", gold_points)
```

---

### Try It Yourself
#### **The Problem**
Write a fully refactored, SCSA-compliant Python script to manage a high-jump bar log. The script must:
1.  Define a constant `MIN_BAR_HEIGHT = 0.5` and `MAX_BAR_HEIGHT = 2.5`.
2.  Contain a single cohesive function `validate_height(prompt_string)` that repeatedly prompts the user, validates that the input is a float and is within constant limits, and returns the verified float.
3.  Implement a main execution sequence that captures heights for three consecutive athlete attempts, saves them to a list, and prints the highest cleared height.
4.  Apply all eight elements of SCSA good practice, including extensive explanatory comments and vertical whitespace.

---

### Check Your Reasoning
#### **The Answer**
```python
# ==========================================
# WA JUNIOR SPORTS CARNIVAL - HIGH JUMP LOG
# ==========================================
# Purpose: Validates high-jump attempts and identifies the maximum cleared height.
# ==========================================

# 1. Constants (SCSA Practice: uppercase, fixed boundaries)
MIN_BAR_HEIGHT = 0.5
MAX_BAR_HEIGHT = 2.5
TOTAL_ATTEMPTS = 3

def validate_height(prompt_string):
    """Prompts, type-checks, and validates a float high-jump height.
    This function performs ONE logical input validation task."""
    while True:
        try:
            # Capture input and cast to float
            height = float(input(prompt_string))
            
            # SCSA Practice: Boundary checking
            if MIN_BAR_HEIGHT <= height <= MAX_BAR_HEIGHT:
                return height
            else:
                print(f"Error: Height must be between {MIN_BAR_HEIGHT}m and {MAX_BAR_HEIGHT}m.")
        except ValueError:
            # Handles non-numeric entry errors gracefully
            print("Error: Please enter a valid decimal number.")

# ==========================================
# MAIN ROUTINE EXECUTION
# ==========================================
# SCSA Practice: Indentation, whitespace, and meaningful structures
jump_attempts = []

print("--- Start of High Jump Attempt Logging ---")

# Definite loop to collect a fixed number of attempts
for attempt_num in range(1, TOTAL_ATTEMPTS + 1):
    prompt = f"Enter height cleared for attempt {attempt_num} (m): "
    validated_jump = validate_height(prompt)
    jump_attempts.append(validated_jump)

# Identify the maximum jump height using a built-in search extreme
highest_jump = max(jump_attempts)

# Display final validated statistics
print("\n--- VALIDATED ATHLETE SUMMARY ---")
print("Recorded Attempts:", jump_attempts)
print(f"Highest Cleared Jump: {highest_jump:.2f} metres")
```

#### **Common SCSA Student Errors**
1.  **Omitting Try-Except Blocks on Float Conversions:** Writing `float(input())` without exception protection. This is an automatic penalty on SCSA assessments because typing alphabetical letters will crash the program instantly.
2.  **Hardcoding Limits:** Using numeric literals (e.g., `if height < 0.5 or height > 2.5`) directly in program structures instead of referencing declared constants (`MIN_BAR_HEIGHT`, `MAX_BAR_HEIGHT`). This makes code maintenance difficult if safety regulations change.
3.  **Low Modular Cohesion:** Creating a single function that validates height, appends to the list, finds the max, and prints the outputs. A separate module should be made for separate logical actions.

---

### Review and Connect
In this lesson, you mastered standard Good Programming Practices, which comprise up to 25% of SCSA practical assessment rubrics. In the next page, you will study the legal, ethical, and copyright frameworks that govern the code you write.

---

## Lesson 8.3: Ethical & Legal Software Development

### Your Goal
Analyze software scenarios to ensure compliance with Australian copyright laws, intellectual property rights, and open-source or proprietary licensing frameworks.

### Before You Start
Ensure you are comfortable with:
*   The general concept of software deployment and distribution.

### The Idea
If you spent three months writing a complex, innovative scoring database for the sports carnival, how would you feel if a rival school copied your file, changed the logo, and started selling it to other regions as their own creation? 

To protect innovation and assign responsibilities, developers must operate within strict legal boundaries. SCSA assesses your understanding of intellectual property, plagiarism, copyright, and software licensing:

```
┌────────────────────────────────────────────────────────┐
│               INTELLECTUAL PROPERTY (IP)               │
│         - Broad legal right over human creations       │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│              AUSTRALIAN COPYRIGHT ACT 1968             │
│  - Automatic legal protection of original source code   │
│  - Restricts unauthorized copying, sharing, or reuse   │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌───────────────────────────┴────────────────────────────┐
│                  SOFTWARE LICENSING                    │
│   - A legal agreement defining permissions of use      │
├────────────────────────────┬───────────────────────────┤
│    OPEN SOURCE LICENSES    │   PROPRIETARY LICENSES    │
│  - Source code is public   │  - Source code is private │
│  - Free modification       │  - Restrictive permissions│
│  - e.g., MIT, GNU GPL      │  - e.g., Commercial EULA  │
└────────────────────────────┴───────────────────────────┘
```

#### **SCSA Key Terms**
*   **Intellectual Property (IP):** The broad legal rights protecting creations of the mind (inventions, artistic works, designs, and source code).
*   **Copyright Act 1968 (Australia):** The statutory law protecting original literary, dramatic, musical, and artistic works. Under Australian law, software source code is protected automatically as a "literary work" the moment it is written down or saved.
*   **Plagiarism:** The unethical act of presenting someone else's work, code, or ideas as your own, without appropriate acknowledgement or citation.
*   **Software Licensing:** A legal agreement establishing terms and permissions under which a customer may use, modify, or redistribute a software application.
*   **Open-Source License:** A licensing model where the source code is freely available, allowing users to inspect, modify, and redistribute the software (e.g., MIT, GNU General Public License).
*   **Proprietary License:** A closed-source licensing model where the code remains private, and users are granted restricted rights to execute the program under a commercial End User License Agreement (EULA).

---

### See It Worked
#### **The Scenario**
A student developer at the junior sports carnival copies a Python array-sorting function from a public online forum. They paste it directly into the carnival's recording program without adding any comments or citations, and then attempt to sell the compiled software to the regional athletics association. 

Let's analyze this developer's actions across ethical and legal dimensions.

```
                  ┌──────────────────────────────┐
                  │   STUDENT COPIES FORUM CODE  │
                  └──────────────┬───────────────┘
                                 │
         ┌───────────────────────┴───────────────────────┐
         ▼                                               ▼
┌─────────────────────────────────┐             ┌─────────────────────────────────┐
│          ETHICAL CRITIQUE       │             │          LEGAL CRITIQUE         │
│  - Act of PLAGIARISM            │             │  - Code is copyrighted as a     │
│  - Claimed authorship of copy   │             │    "literary work" automatically│
│  - Violated academic integrity  │             │  - Commercial use requires      │
│  - Resolution: Add source link  │             │    an open-source or commercial │
│    and author credits in code   │             │    license permission           │
└─────────────────────────────────┘             └─────────────────────────────────┘
```

#### **SCSA-Style Case Analysis**
1.  **The Legal Violation:** 
    *   Under the **Australian Copyright Act 1968**, computer programs receive automatic copyright protection. By copying and selling the code without explicit permission or checking the host licensing terms, the student has committed **copyright infringement**.
2.  **The Ethical Violation (Plagiarism):** 
    *   The student committed **plagiarism** by submitting the code block to the regional association without citing the original programmer. 
3.  **The Professional Resolution:**
    *   To resolve this ethically, the developer must locate the code’s original license (e.g., an MIT license). They must keep the copyright notice intact within their source files and add explicit attribution:
    ```python
    # Helper Sorting Algorithm
    # Original Author: Jane Smith (2024)
    # Sourced From: stackoverflow.com/questions/12345
    # Licensed Under: MIT License (Permissions allow redistribution)
    ```

---

### Try It with Help
#### **The Problem**
A sports software company designs a proprietary database called "AthleticLog v1.0". They distribute the software to schools under a commercial license. One WA school purchases a single user license, copies the installer files onto ten local school computers, and decompiles the executable file to extract the database schema logic.

Analyze this situation using the SCSA licensing and copyright terminology, utilizing the guided table below.

#### **Guided License Analysis Matrix**

| Activity Checked | Legal or Illegal? | Terminology to Describe Violation | Logical Explanation |
| :--- | :--- | :--- | :--- |
| **Installing on 10 PCs** | **Illegal** | Software Piracy / EULA Breach | A single user license restricts installation to **one** designated computer. |
| **Decompiling Code** | **Illegal** (in most commercial EULAs) | Reverse Engineering / Copyright Infringement | Proprietary licenses restrict users from reading, extracting, or copying private, closed-source code. |
| **Plagiarism of Schema** | **Unethical** | Plagiarism | Reusing database designs and presenting them as the school's own original invention is plagiarism. |

*   *Hint:* Complete the table's explanations to justify why a school cannot claim "academic exemption" to distribute proprietary software files freely.

---

### Try It Yourself
#### **The Problem**
The WA Junior Sports Carnival committee wants to release their custom points system. They are debating between two options:
1.  **Option A:** Releasing the code under the **GNU General Public License (GPL)**, making it open source.
2.  **Option B:** Retaining closed-source control and requiring schools to sign a commercial **End User License Agreement (EULA)**, making it proprietary.

Write a technical comparison report that:
1.  Defines the **core technical and accessibility difference** between open source and proprietary models.
2.  Explains how **Australian copyright law** applies to the source code under *both* options.
3.  Recommends which option the committee should choose if their goal is to let country schools modify and customize the timing code for regional grass-track ovals.

---

### Check Your Reasoning
#### **The Answer**
```text
Textbook Comparison Report: Software Licensing Strategy

1. ACCESSIBILITY & SOURCE SYSTEM DIFFERENCE
   - Open Source (GPL): The underlying source code is made completely public. Anyone can download, read, modify, and re-compile the timing code. If a school customizes the code, the GPL requires them to also share their modified code under the same open terms.
   - Proprietary (EULA): The source code remains compiled and hidden from the public (closed-source). Users only receive a binary executable to run on their machines. The EULA strictly prohibits decompilation, unauthorized modification, or redistribution.

2. APPLICATION OF THE AUSTRALIAN COPYRIGHT ACT 1968
   - The Copyright Act 1968 applies AUTOMATICALLY to both models. 
   - Under Open Source (GPL), the developers do NOT give up their copyright; instead, they use their copyright to grant permission to modify and share the code under specific rules.
   - Under Proprietary (EULA), copyright is used to restrict access and protect the commercial value of the intellectual property.

3. STRATEGIC RECOMMENDATION
   - If the core goal is to allow rural schools to modify and customize the code for local track variations, the committee must choose Option A: Open Source (GPL). A proprietary license would legally prevent schools from editing the timing loops or adding hardware drivers to match their regional configurations.
```

#### **Common SCSA Student Errors**
1.  **Confusing Copyright and Licensing:** Believing that releasing code as "Open Source" means the developer loses their copyright. This is incorrect. An open-source license is a **grant of permissions** based on the author's automatic copyright ownership under the law.
2.  **Incorrect Plagiarism Boundaries:** Assuming that citing code online completely resolves copyright issues. A citation resolves plagiarism (the ethical issue) but does not resolve copyright infringement (the legal issue) if the host license does not permit commercial use or redistribution.
3.  **Vague Ownership Claims:** Stating that proprietary code is "more protected" than open-source code. Both receive identical legal protection under the Australian Copyright Act 1968; they simply distribute access differently.

---

### Review and Connect
In this chapter, you explored the complete lifecycle of software development—from Gantt scheduling charts in the **Investigate** phase, to clean formatting and commenting in **Develop**, to copyright compliance when releasing software. 

You have now completed the entire **Unit 1: Software Development & Design Foundations**. In the next chapter, you will transition to physical hardware networks and packet communication layers!

---

## Teacher Support Module (Chapter 8)

### **WA Syllabus Direct Mapping**
*   **Unit 1: Design and development of programming and networking solutions**
    *   **SD-01:** Framework for development: investigate (problem description, define requirements, development schedules, Gantt charts).
    *   **SD-02:** Framework for development: design (design data structures, design and test algorithm).
    *   **SD-03:** Framework for development: develop (develop and debug code, unit testing).
    *   **SD-04:** Framework for development: evaluate (user acceptance testing, developer retrospective).
    *   **GP-01 to GP-08:** Good programming practice (validate input, variable naming, constants, comments, control structures, indentation/white space, one task per module, module names).
    *   **EL-01:** Concepts associated with piracy and copyright: intellectual property, plagiarism in relation to acknowledgement of code, Australian copyright laws, purpose of software licensing, open source, proprietary.

### **Prerequisite Knowledge Checklist**
Before starting this chapter, students should be able to:
*   Write basic sequence, selection, and iteration structures in Python.
*   Identify high-level variable classifications (integers, strings, floats).
*   Trace basic program inputs and describe syntax errors.

### **Classroom Misconception Busters**
1.  **The GPL/Copyright Fallacy:** Students often write in exams that "open-source code is public domain and has no copyright." Correct this early: **Open source licenses rely completely on copyright law to enforce their open-source distribution rules.**
2.  **Coding in the Design Phase:** Students frequently start coding as soon as they receive a project brief. Emphasize that in SCSA practical projects, **writing design documentation (ERDs, structure charts, flowcharts, pseudocode) must precede code implementation.**
3.  **"Citing Code Prevents Piracy":** Ensure students understand that adding an attribution comment to a stolen proprietary block of code prevents plagiarism but **does not make the copying legal**. 

### **Suggested Assessment Tasks**

#### **Task 1: SCSA Project Schedule & Lifecycle Portfolio (15% Weight)**
*   **Format:** Project Portfolio.
*   **Description:** Students receive a client request for an interactive "WA Junior Sports Carnival Scoreboard Portal." 
    *   **Deliverable 1:** A technical requirements list and a 4-week Gantt planning chart showing key milestones.
    *   **Deliverable 2:** A pseudocode algorithm with input validation structures.
    *   **Deliverable 3:** A set of 5 unit test cases mapping normal, extreme, and boundary inputs.
    *   **Deliverable 4:** A reflective developer retrospective following testing.

#### **Task 2: Refactoring Lab and Style Audit (5% Weight)**
*   **Format:** Practical Code Audit.
*   **Description:** Provide students with a working but completely obfuscated Python file. The file must use global variables, cryptic single-letter names, have no indentation, contain no comments, and lack input validation. Students must refactor the file to conform to all 8 SCSA guidelines, earning marks for variable styling, comments, input handling, and modular decomposition.
