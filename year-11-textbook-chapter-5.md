# Unit 1 — Chapter 5: Operators & Complex Expressions

This chapter explores how to perform calculations and make logical decisions in computer science using standard operator types. You will learn to use mathematical operators (including modulo and floor division), construct comparisons using relational operators, and combine multiple logical conditions using Boolean algebra with correct order of precedence.

These skills are essential for processing scores, validating entries, and routing program logic in your **SCSA School-Based Assessment Projects (Assessment Task 1)** and practical examinations.

---

## Lesson 5.1: Arithmetic Operators and MOD

### Your Goal
Apply arithmetic operators, specifically modulo (`%` or `MOD`) and floor division (`//` or `DIV`), to solve cyclical, timing, and grouping problems in software solutions.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.4: Fundamental Data Types](./year-11-textbook-chapter-1.md#lesson-14-fundamental-data-types) (specifically `int` and `float` variables).
*   [Lesson 2.1: Program Control Structures: Sequence](./year-11-textbook-chapter-2.md#lesson-21-program-control-structures-sequence).

### The Idea
In everyday life, we often perform calculations where the remainder of a division is more important than the decimal result. 

**The Analogy:**
Suppose a volunteer at the **WA Junior Sports Carnival** has a box of 38 timing cones and needs to place them in groups of 8 to mark out a shot-put sector. 
*   If they divide 38 by 8 mathematically, they get $4.75$ groups. But you cannot have $0.75$ of a group of cones!
*   Instead, they have **4 full groups** of 8 cones, with **6 leftover cones** that cannot form a complete group.

In computer science, we use two special operators to perform this exact division:
1.  **Floor Division (`//` in Python, often called `DIV` in pseudocode):** Performs division and rounds down to the nearest whole integer, discarding the decimal fraction.
    *   `38 // 8` results in `4` (the number of full groups).
2.  **Modulo (`%` in Python, written as `MOD` in pseudocode):** Performs division and returns *only* the remainder.
    *   `38 % 8` results in `6` (the remaining leftovers).

#### **SCSA Key Terms**
*   **Arithmetic Operators:** Symbols that perform mathematical operations on numerical values (operands).
*   **Modulo (`%` / `MOD`):** An operator that returns the integer remainder of a division.
*   **Floor Division (`//` / `DIV`):** An operator that returns the largest integer less than or equal to the algebraic quotient.
*   **Exponentiation (`**`):** Raises a base number to a power (e.g., $2^3$ is written as `2 ** 3`).

| Operator (SCSA Pseudocode) | Operator (Python) | Description | Example | Python Output |
| :--- | :--- | :--- | :--- | :--- |
| `+` | `+` | Addition | `12 + 5` | `17` |
| `-` | `-` | Subtraction | `12 - 5` | `7` |
| `*` | `*` | Multiplication | `12 * 5` | `60` |
| `/` | `/` | Real/Float Division | `12 / 5` | `2.4` |
| `DIV` | `//` | Floor/Integer Division | `12 // 5` | `2` |
| `MOD` | `%` | Modulo (Remainder) | `12 % 5` | `2` |
| `^` or `**` | `**` | Exponentiation (Power) | `2 ** 3` | `8` |

---

### See It Worked
#### **The Scenario**
The timing desk at the athletics field captures a runner's 1500m finish time in **total seconds** (e.g., `325` seconds). The leaderboard screen needs to display this time in a human-readable format: **minutes and seconds** (e.g., `5 minutes and 25 seconds`).

#### **The Solution Block (Python)**
```python
# Timing desk input (total seconds)
total_seconds = 325

# 1. Calculate the whole minutes using floor division (60 seconds per minute)
minutes = total_seconds // 60

# 2. Calculate the leftover seconds using modulo (the remainder)
seconds = total_seconds % 60

# Display the formatted output
print(total_seconds, "seconds is equivalent to:")
print(minutes, "minutes and", seconds, "seconds")
```

#### **How the Logic Flows**
*   `total_seconds // 60` $ightarrow$ `325 // 60` evaluates to **`5`** because $60 	imes 5 = 300$, and the remaining fraction ($0.416$) is discarded.
*   `total_seconds % 60` $ightarrow$ `325 % 60` evaluates to **`25`** because $325 - (60 	imes 5) = 25$. This is the mathematical remainder.

---

### Try It with Help
#### **The Problem**
The carnival marshall needs to organize **53 track athletes** into qualifying sprint heats. Each heat has a maximum capacity of **8 lanes**. Write a program block that calculates:
1.  How many **full heats** of 8 runners will run.
2.  How many athletes are left over to run in a **final, partially filled heat**.

#### **Structural Hints**
*   Create a variable `total_athletes` and assign it the value `53`.
*   Create a variable `lane_capacity` and set it to `8`.
*   Use floor division (`//`) to find the number of full heats.
*   Use modulo (`%`) to find the remaining runners.

#### **Scaffolded Code Template**
```python
total_athletes = 53
lane_capacity = 8

# Fill in the operators below
full_heats = total_athletes  # ??? calculation here
leftover_athletes = total_athletes  # ??? calculation here

print("Number of full heats:", full_heats)
print("Athletes in the final heat:", leftover_athletes)
```

---

### Try It Yourself
#### **The Problem**
Write a complete, robust Python function named `format_milliseconds(ms)` that takes a single integer representing an interval in **milliseconds** and returns a string in the format: `"S seconds and MS milliseconds"`. 
*   *Note:* There are 1000 milliseconds in one second.
*   *Example input:* `4520` milliseconds should yield: `"4 seconds and 520 milliseconds"`.
*   Test your function with the input values: `8050` and `900`.

---

### Check Your Reasoning
#### **The Answer**
```python
def format_milliseconds(ms):
    # Calculate whole seconds
    seconds = ms // 1000
    # Calculate remaining milliseconds
    milliseconds = ms % 1000
    
    return str(seconds) + " seconds and " + str(milliseconds) + " milliseconds"

# Test cases
print(format_milliseconds(8050))  # Expected: "8 seconds and 50 milliseconds"
print(format_milliseconds(900))   # Expected: "0 seconds and 900 milliseconds"
```

#### **Common SCSA Student Errors**
1.  **Using standard division (`/`) instead of floor division (`//`):** Writing `seconds = ms / 1000` will store a floating-point number (e.g., `4.52`), causing a syntax or type error when concatenated as an integer.
2.  **Order Confusion:** Reversing the calculations (e.g., using modulo for seconds and floor division for milliseconds). Remember: **Floor division yields the whole quotients; Modulo yields the leftovers.**
3.  **String Concatenation Crashes:** Attempting to join integers and strings directly without type conversion (e.g., `return seconds + " seconds"`). You must wrap the variables in `str()`.

---

### Review and Connect
In this lesson, you mastered basic arithmetic operators and the critical integer division pair: `//` (DIV) and `%` (MOD). In the next page, we will learn how to compare these calculated values to check if an athlete has successfully broken a record.

---

## Lesson 5.2: Relational Operators

### Your Goal
Construct logical comparison expressions using relational operators to evaluate numerical and text data in software solutions.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 2.2: Selection (if, else)](./year-11-textbook-chapter-2.md#lesson-22-selection-if-else) and structural indentation blocks.

### The Idea
Programs cannot make decisions without comparing values. If we want to check if a student has qualified for a race final, we must compare their race time against a qualifying threshold.

We use **Relational Operators** to establish relationships between two values. Every relational expression resolves to a single Boolean value: either **`True`** or **`False`**.

**The Analogy:**
Imagine a high-jump official holding a measuring stick set exactly at 1.45 meters. 
*   If an athlete clears **1.48m**, their height is *greater than* the stick ($1.48 > 1.45$). Result: **`True`** (Success).
*   If an athlete clears **1.42m**, their height is *not greater than* the stick ($1.42 > 1.45$). Result: **`False`** (Fail).

#### **SCSA Key Terms**
*   **Relational Operator:** An operator that compares two values (operands) and evaluates to a Boolean value (`True` or `False`).
*   **Boolean Expression:** A statement that evaluates to either `True` or `False`.
*   **Equivalency (`==`):** Checks if the left side is exactly equal to the right side. Note the double equals sign!
*   **Inequality (`!=`):** Checks if the left side is *not* equal to the right side.

| SCSA Pseudocode | Python Operator | Description | Example | Evaluation |
| :--- | :--- | :--- | :--- | :--- |
| `=` | `==` | Equal to | `15 == 15` | `True` |
| `≠` or `!=` | `!=` | Not equal to | `15 != 10` | `True` |
| `>` | `>` | Greater than | `12 > 15` | `False` |
| `<` | `<` | Less than | `8 < 10` | `True` |
| `≥` or `>=` | `>=` | Greater than or equal to | `15 >= 15` | `True` |
| `≤` or `<=` | `<=` | Less than or equal to | `14 <= 12` | `False` |

---

### See It Worked
#### **The Scenario**
The high-jump recorder needs a Python script that takes a student's jump height and checks if it is high enough to break the **current school record of 1.62 metres**. 

#### **The Solution Block (Python)**
```python
school_record = 1.62
athlete_jump = 1.65

# Relational evaluation
is_new_record = athlete_jump > school_record

if is_new_record == True:
    print("Congratulations! You broke the school record of", school_record, "metres.")
else:
    print("Good attempt, but the school record remains at", school_record, "metres.")
```

#### **How the Logic Flows**
*   The expression `athlete_jump > school_record` evaluates to `1.65 > 1.62`.
*   Because 1.65 is larger than 1.62, the expression resolves to the Boolean value **`True`**.
*   The variable `is_new_record` is assigned **`True`**, triggering the primary branch of the `if` statement.

---

### Try It with Help
#### **The Problem**
Write a Python script that evaluates a competitor's **sprint start time** (reaction time) captured by a pressure pad. 
*   If the runner's reaction time is **less than 0.10 seconds**, they have triggered a **false start** and must be flagged for disqualification.
*   Otherwise, their start is clean.

#### **Structural Hints**
*   The reaction time threshold is `0.10`.
*   Use the "less than" operator (`<`) to evaluate the reaction time.
*   Complete the conditional block below.

#### **Scaffolded Code Template**
```python
reaction_time = 0.08  # Example reaction time in seconds
threshold = 0.10

# Compare reaction_time with threshold
has_false_started = reaction_time  # ??? add comparison operator here

if has_false_started:
    print("WARNING: False start detected! Runner is disqualified.")
else:
    print("Clean start. Race is live.")
```

---

### Try It Yourself
#### **The Problem**
Write an entry-verification program for the **WA Junior Sports Carnival**. The system takes two pieces of data:
1.  The school house name of an athlete (e.g., `"Gold"`, `"Blue"`, `"Red"`).
2.  The maximum points scored by that house so far (an integer).

Write a Python script that checks:
*   If the athlete's house is **not** equal to `"Gold"`.
*   If their points are **greater than or equal to** `150`.
Assign these comparisons to Boolean variables and print their status.

---

### Check Your Reasoning
#### **The Answer**
```python
athlete_house = "Blue"
house_points = 165

# 1. Inequality check (not equal to Gold)
not_gold = athlete_house != "Gold"

# 2. Comparison check (greater than or equal to 150)
meets_points_threshold = house_points >= 150

print("Is the athlete NOT in Gold house?", not_gold)
print("Does the house meet the 150 points threshold?", meets_points_threshold)
```

#### **Common SCSA Student Errors**
1.  **Using `=` instead of `==` for equality checking:** Writing `if athlete_house = "Gold"` in Python results in a `SyntaxError: invalid syntax` because `=` is exclusively used for variable assignment.
2.  **Reversing compound operators:** Writing `=>` or `=<` instead of `>=` or `<=`. The equals sign must *always* come second in comparison operators.
3.  **Data type mismatches in comparison:** Attempting to compare a string number with an integer (e.g., `"150"` >= `150`). This will throw a `TypeError` in Python. Always cast user input to integers or floats before comparison.

---

### Review and Connect
Relational operators allow us to evaluate single statements. However, in real-world scenarios, decisions are rarely based on a single factor. In the next lesson, we will explore how to chain multiple relational expressions together using logical operators.

---

## Lesson 5.3: Logical Expressions & Precedence

### Your Goal
Construct, evaluate, and simplify complex compound logical expressions using the logical operators `AND`, `OR`, and `NOT` while respecting SCSA logical order of precedence.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 5.1: Arithmetic Operators and MOD](#lesson-51-arithmetic-operators-and-mod).
*   [Lesson 5.2: Relational Operators](#lesson-52-relational-operators).

### The Idea
What if an athlete needs to meet *multiple* conditions to qualify for an elite final? For example, they must be in the **Under 16 Division** AND have a **sprint time under 12 seconds**, OR hold a **special wild-card entry token**.

To evaluate multiple conditions, we use **Logical Operators** (`AND`, `OR`, `NOT`) to construct compound logical expressions.

**The Analogy:**
Imagine an entry gate staffed by a marshal checking registration badges:
*   **`AND` (Conjunction):** The marshal says: "To pass, you must have your badge **AND** be wearing running spikes." (Both must be True).
*   **`OR` (Disjunction):** The marshal says: "To pass, you must show a student ID card **OR** a volunteer pass." (At least one must be True).
*   **`NOT` (Negation):** The marshal says: "You cannot pass if you are on the **NOT** cleared list." (Inverts the outcome).

#### **Truth Tables**
A **Truth Table** is a mathematical table used in logic to determine whether a compound expression is true or false.

##### **Conjunction (AND)**
*Both operands must be True for the result to be True.*
| Operand A | Operand B | A AND B |
| :--- | :--- | :--- |
| `False` | `False` | `False` |
| `False` | `True` | `False` |
| `True` | `False` | `False` |
| `True` | `True` | `True` |

##### **Disjunction (OR)**
*At least one operand must be True for the result to be True.*
| Operand A | Operand B | A OR B |
| :--- | :--- | :--- |
| `False` | `False` | `False` |
| `False` | `True` | `True` |
| `True` | `False` | `True` |
| `True` | `True` | `True` |

##### **Negation (NOT)**
*Inverts the input value.*
| Operand A | NOT A |
| :--- | :--- |
| `False` | `True` |
| `True` | `False` |

#### **Logical Order of Precedence**
When you write an expression containing multiple arithmetic, relational, and logical operators, the computer must evaluate them in a strict, deterministic sequence. 

**The SCSA Order of Precedence (highest priority to lowest):**
1.  **Parentheses / Brackets `()`** (Explicitly groups expressions first)
2.  **Arithmetic Operators** (`**`, then `*`, `/`, `//`, `%`, then `+`, `-`)
3.  **Relational Operators** (`==`, `!=`, `>`, `<`, `>=`, `<=`)
4.  **Logical `NOT`**
5.  **Logical `AND`**
6.  **Logical `OR`**

*Memory Trick:* **N-A-O** (Not, And, Or) is the order of evaluation for logical operations after comparisons are resolved.

---

### See It Worked
#### **The Scenario**
An athlete's performance log needs to be assessed to see if they qualify for the **WA State Junior Championships**. The rules state:
An athlete qualifies if they:
*   Are registered under the `"WA"` division.
*   **AND** either score above `180` points **OR** run a sprint under `11.5` seconds.
*   **AND** do not have any active doping or code-of-conduct disqualification flags (`NOT has_fouls`).

Let's evaluate this logic for an athlete with the following attributes:
*   `division = "WA"`
*   `points = 185`
*   `sprint_time = 12.1`
*   `has_fouls = False`

#### **The Compound Expression (Python)**
```python
division = "WA"
points = 185
sprint_time = 12.1
has_fouls = False

# Evaluate qualification
is_qualified = (division == "WA") and (points > 180 or sprint_time < 11.5) and not has_fouls

print("Championship qualification status:", is_qualified)
```

#### **Step-by-Step Precedence Evaluation Trace**
Let's resolve the expression mathematically using the order of precedence:
`is_qualified = (division == "WA") and (points > 180 or sprint_time < 11.5) and not has_fouls`

1.  **Step 1: Evaluate expressions inside Parentheses first.**
    *   `(division == "WA")` $ightarrow$ `("WA" == "WA")` $ightarrow$ **`True`**
    *   `(points > 180 or sprint_time < 11.5)` contains two comparisons. Let's evaluate them:
        *   `points > 180` $ightarrow$ `185 > 180` $ightarrow$ `True`
        *   `sprint_time < 11.5` $ightarrow$ `12.1 < 11.5` $ightarrow$ `False`
        *   Now resolve the `or` inside: `True or False` $ightarrow$ **`True`**
2.  **Substitute back into the expression:**
    *   `is_qualified = True and True and not has_fouls`
3.  **Step 2: Evaluate logical `NOT`.**
    *   `not has_fouls` $ightarrow$ `not False` $ightarrow$ **`True`**
4.  **Substitute back into the expression:**
    *   `is_qualified = True and True and True`
5.  **Step 3: Evaluate logical `AND` left-to-right.**
    *   `True and True` $ightarrow$ `True`
    *   `True and True` $ightarrow$ **`True`**

The athlete qualifies! Output: `Championship qualification status: True`.

---

### Try It with Help
#### **The Problem**
Evaluate the Boolean output of the following expression using SCSA logical precedence rules:
`result = NOT 15 > 12 AND 10 == 10 OR 5 < 8`

#### **Structural Hints**
*   There are no parentheses. Follow the **N-A-O** (NOT, then AND, then OR) rule.
*   First, evaluate all **relational operators** ($>$, $==$, $<$):
    *   `15 > 12` $ightarrow$ ???
    *   `10 == 10` $ightarrow$ ???
    *   `5 < 8` $ightarrow$ ???
*   Next, apply the **`NOT`** operator to its direct operand.
*   Next, resolve the **`AND`** statement.
*   Finally, resolve the **`OR`** statement to yield your final Boolean value.

#### **Fill in the Blanks**
```
1. Comparisons:  result = NOT (True) AND (???) OR (???)
2. Apply NOT:    result = (???) AND True OR True
3. Apply AND:    result = (???) OR True
4. Apply OR:     result = ???
```

---

### Try It Yourself
#### **The Problem**
An athletics program assigns athletes to the **Gold Championship Finals** based on three inputs:
1.  `sprint_time` (float)
2.  `house_points` (integer)
3.  `is_disqualified` (Boolean)

The rules state:
An athlete is eligible for the Gold Finals if they have a `sprint_time` of **less than 12.0 seconds** OR a `house_points` tally of **more than 200**, and they are **NOT disqualified**.

Write a Python program that:
*   Asks the user to input the three fields.
*   Constructs a single, compound Boolean expression to evaluate eligibility.
*   Prints whether the athlete is eligible or not.
*   Test your code using two athletes:
    *   *Athlete A:* Time = `11.8`, Points = `150`, Disqualified = `True`.
    *   *Athlete B:* Time = `13.5`, Points = `250`, Disqualified = `False`.

---

### Check Your Reasoning
#### **The Answer**
```python
# Athlete Input variables (Simulating inputs for testing)
# Test Athlete A
sprint_time_A = 11.8
house_points_A = 150
is_disqualified_A = True

# Test Athlete B
sprint_time_B = 13.5
house_points_B = 250
is_disqualified_B = False

# Complex Boolean expression
# Parentheses are critical around the 'or' block to ensure the 'and not' applies to the entire outcome!
eligible_A = (sprint_time_A < 12.0 or house_points_A > 200) and not is_disqualified_A
eligible_B = (sprint_time_B < 12.0 or house_points_B > 200) and not is_disqualified_B

print("Athlete A Eligibility:", eligible_A)  # Expected: False (due to disqualification)
print("Athlete B Eligibility:", eligible_B)  # Expected: True (points > 200, clean record)
```

#### **Common SCSA Student Errors**
1.  **Omitting parenthetical groupings:** Writing `sprint_time < 12.0 or house_points > 200 and not is_disqualified` without brackets around the `or` block. Due to precedence rules, the computer evaluates `house_points > 200 and not is_disqualified` first, then `or`s the result with `sprint_time < 12.0`. This would mean Athlete A would incorrectly qualify because their `sprint_time < 12.0` is `True`, bypasses the disqualification check, and evaluates to `True` overall!
2.  **Negation Misuse:** Writing `not is_disqualified == True`. While syntactically correct, it is logically redundant. `is_disqualified` is already a Boolean variable. Writing `not is_disqualified` is the clean, correct SCSA standard.
3.  **Confusing `and` / `or` in English vs. Logic:** Students often write `if division == "WA" and division == "VIC"` hoping to catch athletes from either WA or VIC. However, a single variable can never hold two values simultaneously! They must use the logical `or` operator instead.

---

### Review and Connect
In this chapter, you mastered the mathematical and logical operations that control program execution. By combining arithmetic division (`DIV` and `MOD`), comparison checks (`>`, `<`, `==`), and compound logic (`AND`, `OR`, `NOT`), you can now write complex programs that handle data and make decisions automatically.

On the next page, you will apply these tools to construct and manipulate **one-dimensional arrays** and manage raw text files for storing performance histories.

---

## Unit 1 — Chapter 5: Teacher Guide

### **WA Syllabus Mapping**
This chapter covers the following explicit content lines from the **SCSA Computer Science ATAR Year 11 Syllabus (for teaching from 2026)**:
*   **Types of operators:** arithmetic operators (`+`, `-`, `*`, `/`, `%` or `MOD`).
*   **Types of operators:** relational operators (`==`, `!=`, `>`, `<`, `>=`, `<=`).
*   **Types of operators:** logical operators (`AND`, `OR`, `NOT`).
*   Read and write complex logical expressions, including Boolean operators.
*   Logical order of precedence.

### **Misconception Busters & Diagnostic Tips**
1.  **The Double Equals Trap:** Year 11 students repeatedly write `=` instead of `==` in relational expressions. 
    *   *Diagnostic check:* Give students a code snippet containing `if value = 10:` and ask them to spot the syntax error before running it.
2.  **Order of Precedence Blindness:** Many students assume code is evaluated strictly from left to right.
    *   *Teaching strategy:* Write `True or False and False` on the whiteboard. Most students will guess `False` (evaluating left-to-right: `True or False` $ightarrow$ `True`; then `True and False` $ightarrow$ `False`). Explain that because `and` takes priority, it is evaluated as `True or (False and False)` $ightarrow$ `True or False` $ightarrow$ `True`.
3.  **The Modular Arithmetic Barrier:** Modulo (`%`) is highly abstract for students who haven't encountered it outside algebra. 
    *   *Visualization tool:* Use a circular clock analogy. `13 % 12` is `1` o'clock. `25 % 12` is also `1` o'clock. Modulo is "wrapping around" a boundary.

### **Classroom Discussion Starters**
*   **Theme - Algorithmic Fairness in Sports:** "If we use compound logical criteria to screen athletes for state selections, could small logical discrepancies in the code (e.g., an off-by-one bracket error in qualification age) accidentally lock out a deserving athlete? Why must developers test edge-case data?"
*   **Theme - Legacy Encodings in Modern Timing Equipment:** "Why do older Olympic and timing boards still use strict, truncated ASCII byte displays instead of rich Unicode configurations? (Hint: physical chip memory limits and transmission latency over old serial connections)."

### **Assessment Integration (Task 1 & Task 2)**
*   **SCSA Assessment Task 1 (Programming Project):** Direct students to use modulo (`%`) to manage cyclical states in their games (e.g., swapping turns between Player 1 and Player 2: `current_player = turn % 2`).
*   **SCSA Assessment Task 2 (Practical Debugging Test):** Include logic errors in test-ready code where brackets have been left out of compound conditions, forcing students to construct a formal SCSA trace table to isolate and correct the validation failure.
