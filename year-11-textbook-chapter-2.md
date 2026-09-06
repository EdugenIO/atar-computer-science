# Unit 1 — Chapter 2: Control Structures & Selection

This chapter covers program control structures (sequence, selection), multi-way selection, and robust input handling through exception structures, in direct alignment with the Western Australian SCSA Computer Science ATAR syllabus for Year 11 (effective from 2026).

---

## 2.1 Program Control Structures: Sequence

### **Your Goal**
Trace and predict the logical outcomes of a sequential program block where instructions execute synchronously line-by-line, explaining how variable states change in memory.

### **Before You Start**
- [ ] I understand how variables store basic data types (integers, floats, strings, Booleans) [Ref: Lesson 1.4].
- [ ] I can perform basic arithmetic calculations using standard Python operators [Ref: Lesson 1.4].

### **The Idea**
Imagine following a strict recipe for baking a cake. You cannot pre-heat the oven *after* you have already baked the batter; you must complete each step in order from top to bottom. 

In programming, this linear execution is called **sequence**. It is the most fundamental program control structure. 

#### **Key Terminology**
*   **Sequence:** The execution of statements one after another in the order they are written in the source code.
*   **Program Counter (PC):** A specialized processor register that tracks the memory address of the next instruction to be executed, ensuring synchronous, sequential progression.
*   **Synchronous Execution:** A model of execution where instructions are completed one at a time, blocking subsequent instructions until the current line is fully executed.
*   **Variable Swap:** A standard sequence algorithm used to exchange the values of two memory locations, usually requiring a third "temporary" location to prevent data loss.

---

### **See It Worked**
#### **The Scenario: Swapping Finish Line Sensor Readings**
At the finish line of the WA Junior Sports Carnival, two laser-gate timing systems record sensor IDs. Gate A (`sensor_A`) is mistakenly swapped with Gate B (`sensor_B`) during physical setup. We must write a sequential algorithm to correct this in the software.

#### **Annotated Python Code**
```python
# Step 1: Initialise the sensor variables in memory
sensor_A = "LASER_GATE_01"  # Target value for Gate B
sensor_B = "LASER_GATE_02"  # Target value for Gate A

# Step 2: Store the value of sensor_A in a temporary variable (temp)
# This prevents LASER_GATE_01 from being overwritten and lost
temp = sensor_A             

# Step 3: Copy the value of sensor_B into sensor_A
sensor_A = sensor_B         

# Step 4: Copy the temporary variable (holding original sensor_A) into sensor_B
sensor_B = temp             

# Print the corrected values
print("A:", sensor_A)
print("B:", sensor_B)
```

#### **Visual State Trace Diagram**
Below is the memory state at each line of execution:
```
Line Number   | sensor_A       | sensor_B       | temp
--------------|----------------|----------------|-------------
Initial State | LASER_GATE_01  | LASER_GATE_02  | None (Undefined)
Line 6        | LASER_GATE_01  | LASER_GATE_02  | LASER_GATE_01
Line 9        | LASER_GATE_02  | LASER_GATE_02  | LASER_GATE_01
Line 12       | LASER_GATE_02  | LASER_GATE_01  | LASER_GATE_01
```

---

### **Try It with Help**
#### **The Problem: Tracing a Running Speed Calculation**
An athlete passes the starting gate at $t_1 = 12.4$ seconds, and the finish gate at $t_2 = 14.8$ seconds. The measured track distance is exactly $15.0$ metres. We must write a sequential script that calculates the split duration and average running speed ($	ext{Speed} = rac{	ext{Distance}}{	ext{Duration}}$).

**Your task:** Complete the missing code lines and trace the values in the grid below.

```python
# 1. Define initial physical measurements
time_start = 12.4
time_finish = 14.8
distance = 15.0

# 2. Calculate the total duration of the sprint
# HINT: Subtract start time from finish time
duration = _________ - time_start

# 3. Compute the speed (Distance divided by Duration)
# HINT: Ensure you use the newly calculated duration variable
speed = distance / _________

# 4. Output the results
print("Duration:", duration, "seconds")
print("Average Speed:", speed, "m/s")
```

#### **Memory Trace Grid**
Fill in the blanks as the Program Counter moves through each step:
*   At Line 3: `time_start` = `12.4`, `time_finish` = `14.8`, `distance` = `15.0`, `duration` = `Undefined`, `speed` = `Undefined`
*   At Line 7: `duration` = `__________`
*   At Line 10: `speed` = `__________`

---

### **Try It Yourself**
#### **The Problem: Adjusting Times for Wind Resistance**
WA SCSA exam questions often ask you to calculate and adjust values sequentially. Write a short Python script to adjust a runner's raw sprint time based on a wind assistance penalty.
*   Input values: Raw sprint time is `11.25` seconds. Wind vector is positive `2.4` m/s (tailwind).
*   Formula: If there is a positive wind, you must add an adjustment penalty of `0.05` seconds for every complete `1.0` m/s of wind to make the time fair. (Use integer division `//` to find complete m/s).
*   Compute: Calculate the adjusted time (`raw_time + adjustment`). Output the raw wind vector, the total time adjustment, and the final adjusted time.

---

### **Check Your Reasoning**
#### **Try It with Help Solution**
*   `duration = time_finish - time_start` ($14.8 - 12.4 = 2.4$ seconds)
*   `speed = distance / duration` ($15.0 / 2.4 = 6.25$ m/s)
*   **Trace values:** `duration` at line 7 is `2.4`. `speed` at line 10 is `6.25`.

#### **Try It Yourself Solution**
```python
raw_time = 11.25
wind_speed = 2.4

# Perform calculations in strict sequential order
wind_complete_units = wind_speed // 1.0  # Returns 2.0
adjustment = wind_complete_units * 0.05  # Returns 0.10
adjusted_time = raw_time + adjustment   # Returns 11.35

print("Wind Speed:", wind_speed)
print("Adjustment:", adjustment)
print("Adjusted Time:", adjusted_time)
```

#### **SCSA Exam Trap: Retroactive Variable Fallacy**
> **SCSA Examiner Note:** Students frequently assume variables are mathematically "linked." For example, writing:
> ```python
> x = 10
> y = x * 2  # y is 20
> x = 15     # Students wrongly assume y updates to 30!
> ```
> Remember, in sequential execution, the computer reads the value in memory *at the exact millisecond* that line runs. Future updates to `x` have zero impact on previous values calculated for `y`.

---

### **Review and Connect**
You have now verified that sequential execution runs from top to bottom. At the WA Junior Sports Carnival timing desk, this sequence acts as the primary pipeline for processing raw sensor times before we apply filters. In the next lesson, we will see how to break this simple straight line using selection statements.

---
---

## 2.2 Selection (if, else)

### **Your Goal**
Write, trace, and explain selection statements (`if` and `else` blocks) that evaluate single logical conditions to branch execution flow in Python.

### **Before You Start**
- [ ] I can write sequential scripts in Python [Ref: Lesson 2.1].
- [ ] I can use relational operators (`==`, `!=`, `>`, `<`, `>=`, `<=`) to compare numeric values [Ref: Lesson 1.4].

### **The Idea**
In sequential programming, every single line of code runs. But real-world systems must make decisions. Imagine approaching a railway switch: if the track is clear, you go straight; if it is blocked, you divert to the siding. 

This branch pathway in programming is called **selection**. It allows a program to execute certain lines of code *only* when a specific condition is met, bypassing them completely if it is not.

#### **Key Terminology**
*   **Selection:** A program control structure that directs the flow of execution along one of two or more pathways depending on the evaluation of a Boolean (True/False) condition.
*   **Branching:** The pathway taken by the execution flow when a condition evaluates to True or False.
*   **Code Block:** A group of statements grouped together. In Python, code blocks are defined by their **indentation level** (traditionally 4 spaces).
*   **Relational Expression:** An expression that compares two values and returns a Boolean result (`True` or `False`).

---

### **See It Worked**
#### **The Scenario: Verifying Athlete Finals Qualification**
An athlete at the carnival qualifies for the 100m sprint finals if their run time is less than or equal to $12.5$ seconds. If they qualify, we print a congratulations message and set their qualification status to `True`. Otherwise, we print a encouragement message and set status to `False`.

#### **Annotated Python Code**
```python
run_time = 12.3  # Input runner time
qualified = False # Default status in memory

# Evaluates if run_time is less than or equal to 12.5
if run_time <= 12.5:  
    # This indented block runs ONLY if the condition is True
    print("Congratulations! You qualified.")
    qualified = True
else:
    # This indented block runs ONLY if the condition is False
    print("Keep training! Qualification threshold is 12.5s.")
    qualified = False

print("Qualification status:", qualified)
```

#### **Visual Control Flow Diagram**
```
           [ Start: run_time = 12.3 ]
                       │
                       ▼
           Is run_time <= 12.5? ───────────────────┐
                       │ (Yes / True)              │ (No / False)
                       ▼                           ▼
          [ Print: Congratulations ]     [ Print: Keep training ]
          [ Set: qualified = True  ]     [ Set: qualified = False ]
                       │                           │
                       └─────────────┬─────────────┘
                                     │
                                     ▼
                      [ Print: Qualification status ]
```

---

### **Try It with Help**
#### **The Problem: High Jump Bar Clearance Evaluator**
At the high jump event, an athlete's jump is recorded as a clearance if the `jump_height` is greater than or equal to the `bar_height`. If cleared, the program increases their jump count attempt and records their status.

**Your task:** Complete the syntax blanks and trace the path of execution for a competitor whose jump is $1.65$m against a bar height of $1.68$m.

```python
bar_height = 1.68
jump_height = 1.65
attempts = 0

# Check if jump height is enough to clear the bar
if jump_height ____ bar_height_height_height_height:  # <-- HINT: What relational operator checks "greater than or equal to"?
    print("CLEARED!")
    attempts = attempts + 1
    cleared_status = True
____:  # <-- HINT: What keyword represents "otherwise"?
    print("KNOCK DOWN!")
    attempts = attempts + 1
    cleared_status = False

print("Cleared status:", cleared_status)
```

#### **Execution Trace Checklist**
*   What is the Boolean result of `1.65 >= 1.68`? (`True` / `False`)
*   Does the computer execute the lines inside the `if` block, or the `else` block?
*   What is the final value of `cleared_status` printed to the terminal?

---

### **Try It Yourself**
#### **The Problem: Age Division Checker**
Write a Python selection algorithm to verify if a student's age qualifies them for the **Senior Division** of the carnival.
*   A student is classified as a "Senior" if their age is `16` or older.
*   Input variable: `student_age` (e.g. `15`).
*   Your program must check the age. If they are $16$ or older, output "Division: Senior" and set a variable `is_senior` to `True`. Otherwise, output "Division: Junior" and set `is_senior` to `False`.

---

### **Check Your Reasoning**
#### **Try It with Help Solution**
*   Relational operator blank: `>=`
*   Otherwise keyword blank: `else:` (Note the mandatory colon!)
*   **Trace Analysis:** The condition evaluates `1.65 >= 1.68`, which is `False`. The program skips the `if` block entirely and jumps to the `else` block. It prints "KNOCK DOWN!" and sets `cleared_status` to `False`.

#### **Try It Yourself Solution**
```python
student_age = 15

if student_age >= 16:
    print("Division: Senior")
    is_senior = True
else:
    print("Division: Junior")
    is_senior = False

print("Senior Status:", is_senior)
```

#### **SCSA Exam Trap: Syntax and Indentation Pitfalls**
> **SCSA Examiner Note:** SCSA practical exams assess precise syntactic logic. In Python, you *must* include:
> 1.  The colon (`:`) at the end of every `if` and `else` statement header. Forgetting this is a standard mark loss.
> 2.  Consistent indentation. The lines inside the block must be indented. Mixing tab spaces and raw spaces will trigger an `IndentationError` and cause your code to fail to compile.

---

### **Review and Connect**
Selection enables dynamic branching based on singular conditions. In our WA Junior Sports Carnival registration suite, this logic allows us to instantly classify and separate athletes. However, what happens when we have *three or more* pathways—such as sorting runners into Gold, Silver, and Bronze rankings? In the next page, we will implement multi-way selection.

---
---

## 2.3 Multi-Way Selection (if, elif, else)

### **Your Goal**
Design, write, and trace multi-way selection structures using Python's `if-elif-else` constructs to evaluate multiple sequential, mutually exclusive criteria.

### **Before You Start**
- [ ] I can implement basic binary branching using `if` and `else` [Ref: Lesson 2.2].
- [ ] I understand the precedence of logical and relational expressions [Ref: Lesson 1.4].

### **The Idea**
Think of an automatic sorting machine at a postal depot. Packages are checked sequentially: is it over 10kg? (Route to heavy bin). Otherwise, is it over 5kg? (Route to medium bin). Otherwise, route to light bin. 

This multi-path routing is called **multi-way selection**. In Python, we implement this using the `elif` (short for "else if") keyword. 

It is crucial to understand that multi-way selection is **sequentially evaluated** and **mutually exclusive**. The moment the computer finds *one* condition that is True, it executes that block, ignores all other subsequent evaluations, and exits the entire selection structure.

```
       [ Input Value ] ───► [ Condition 1 ] ───(True)───► [ Execute Block 1 ] ───► [ Exit Selection ]
                                │
                             (False)
                                ▼
                            [ Condition 2 ] ───(True)───► [ Execute Block 2 ] ───► [ Exit Selection ]
                                │
                             (False)
                                ▼
                            [ default / else ] ─────────► [ Execute Block 3 ] ───► [ Exit Selection ]
```

---

### **See It Worked**
#### **The Scenario: Calculating Carnival Entry Fees**
The WA Junior Sports Carnival charges entry fees dynamically based on the competitor's age bracket:
*   Under 12 years old: `$10.00`
*   Under 16 years old: `$15.00`
*   Open division (16 and over): `$25.00`

#### **Annotated Python Code**
```python
age = 14  # Competitor age input
fee = 0.0 # Initialise empty fee tracker

# Check 1: Is age strictly less than 12?
if age < 12:
    fee = 10.00
    print("Under 12 Division")

# Check 2: If Check 1 was False, is age strictly less than 16?
elif age < 16:
    fee = 15.00
    print("Under 16 Division")

# Catch-all: If all prior checks were False, execute default
else:
    fee = 25.00
    print("Open Division")

print("Entry Fee: $", fee)
```

#### **How the Computer Evaluates This**
1.  It checks `age < 12`. Since `14 < 12` is `False`, it ignores the `$10.00` block.
2.  It moves to `elif age < 16`. Since `14 < 16` is `True`, it runs this block: `fee = 15.00` and prints "Under 16 Division".
3.  **Crucial Step:** It now completely ignores the `else` block! It exits the selection structure and prints `Entry Fee: $ 15.0`.

---

### **Try It with Help**
#### **The Problem: Automating Medal Allocations**
The carnival committee wants to automatically assign medal titles based on race rankings:
*   Rank `1` receives "Gold Medal"
*   Rank `2` receives "Silver Medal"
*   Rank `3` receives "Bronze Medal"
*   Any other rank receives "Participation Ribbon"

**Your task:** Complete the syntax gaps below to construct this multi-way evaluation.

```python
competitor_rank = 3
medal_type = "None"

if competitor_rank == 1:
    medal_type = "Gold Medal"
____ competitor_rank == 2:  # <-- HINT: What keyword checks "otherwise, if"?
    medal_type = "Silver Medal"
elif competitor_rank ____ 3:  # <-- HINT: What operator checks absolute equivalence?
    medal_type = "Bronze Medal"
____:  # <-- HINT: What is the default catch-all keyword?
    medal_type = "Participation Ribbon"

print("Awarded:", medal_type)
```

#### **Tracing Analysis**
*   If `competitor_rank` is updated to `2`, list the exact checks the computer performs before printing.
*   Why would it be bad practice to write this as four independent `if` statements instead of a linked `if-elif-else` structure?

---

### **Try It Yourself**
#### **The Problem: Athletic House Points Allocator**
Write a Python script to allocate overall points to a school's Sports House based on the finishing position of their relay team:
*   First place (`1`): `10` points
*   Second place (`2`): `8` points
*   Third place (`3`): `5` points
*   Fourth place (`4`): `2` points
*   Any other finish position: `0` points
*   Input variable: `finish_place` (e.g. `2`). Output: "Points Earned: X".

---

### **Check Your Reasoning**
#### **Try It with Help Solution**
*   First blank keyword: `elif`
*   Equivalence operator: `==`
*   Default catch-all: `else:`
*   **Trace Analysis:** For `competitor_rank = 3`, Check 1 (`3 == 1`) is `False`. Check 2 (`3 == 2`) is `False`. Check 3 (`3 == 3`) is `True`. The program sets `medal_type = "Bronze Medal"`, skips the remaining lines, and prints "Awarded: Bronze Medal".

#### **Try It Yourself Solution**
```python
finish_place = 2
points = 0

if finish_place == 1:
    points = 10
elif finish_place == 2:
    points = 8
elif finish_place == 3:
    points = 5
elif finish_place == 4:
    points = 2
else:
    points = 0

print("Points Earned:", points)
```

#### **SCSA Exam Trap: The Multi-`if` Inefficiency and Logical Bug**
> **SCSA Examiner Note:** Beginners often make the error of writing multiple isolated `if` blocks instead of a cohesive `if-elif-else` structure:
> ```python
> # INEFFICIANT AND BUGGY EXAMPLE:
> score = 85
> if score >= 50:
>     grade = "Pass"
> if score >= 80:
>     grade = "Distinction"  
> ```
> In this buggy version, even if `score` is `85`, the computer evaluates *both* conditions separately. If we write it this way, we waste processor cycles because the PC has to evaluate every comparison. More importantly, if we arrange the conditions in the wrong order without `elif`, one block might overwrite a correct calculation! Always link related sequential decisions using `elif`.

---

### **Review and Connect**
Multi-way selection enables robust, efficient sorting of complex, tiered data such as race placings and house point distributions. Up to this point, our code has assumed that inputs entered by users (such as age or ranking) are mathematically perfect. But what if a user inputs alphabetical letters like "four" instead of numeric digits? To prevent our programs from crashing during live use, we must implement robust exception handling, which we cover next.

---
---

## 2.4 Exception Handling (try/except)

### **Your Goal**
Apply and write Python `try-except` blocks to detect, intercept, and gracefully handle runtime entry errors (such as mismatched data types) without causing the software application to crash.

### **Before You Start**
- [ ] I can write structured sequential and conditional code [Ref: Lesson 2.2, 2.3].
- [ ] I understand the critical difference between syntax errors and runtime exceptions [Ref: Chapter 1].

### **The Idea**
Imagine walking on a tightrope. A professional performer walks carefully (the logic). But just in case they lose their footing, we stretch a safety net underneath them (the exception handler). If they slip, they hit the net safely instead of falling to the ground.

In programming, if a user enters invalid data (such as typing their name into a field that expects their run speed), Python cannot perform the mathematical processing. Normally, the execution halts instantly, showing a cryptic system error—meaning your program has crashed.

To prevent this, we wrap risky operations in a **`try-except` block**. If a runtime exception occurs inside the `try` block, Python immediately arrests the crash and routes execution into the `except` block, allowing the program to remain active.

```
                  [ Run Block inside "try" ]
                             │
            ┌────────────────┴────────────────┐
            ▼ (No Errors Occur)               ▼ (Exception Triggered)
      [ Finish Block ]               [ Instantly Jump to "except" ]
            │                                 │
            │                                 ▼
            │                        [ Execute Recovery Code ]
            │                                 │
            └────────────────┬────────────────┘
                             ▼
                 [ Continue Main Program ]
```

#### **Key Terminology**
*   **Syntax Error:** An error in the program's structural writing (e.g. missing colons or parentheses) that prevents the code from compiling in the first place.
*   **Runtime Error (Exception):** An error that occurs while the program is actively executing (e.g., dividing by zero or attempting to convert a letter string into an integer).
*   **ValueError:** A standard built-in exception raised when a system function receives an argument of the correct data type but an inappropriate value (e.g., passing `"apple"` to `int()`).
*   **Graceful Recovery:** The capability of software to intercept an execution failure, display a user-friendly error warning, and reset without crashing the host operating system.

---

### **See It Worked**
#### **The Scenario: Guarding the Stopwatch Input Terminal**
At the finish gate of the sports carnival, the timing official enters athlete run times. If they accidentally key in a typo containing letters (e.g. `"12..4"` or `"twelve"`), we must catch the exception, print an error warning, and set a default fallback time of `99.9` seconds rather than crashing the timer screen.

#### **Annotated Python Code**
```python
# Mismatched user input string
raw_input_time = "twelve"  

try:
    # 1. The computer attempts to run this block.
    # Passing "twelve" to float() is impossible, so this raises a ValueError.
    processed_time = float(raw_input_time)
    
    # 2. This print line is completely skipped because line 6 raised an error.
    print("Time saved successfully:", processed_time)

except ValueError:
    # 3. Execution jumps straight here. The crash is safely intercepted.
    print("INPUT ERROR: Please enter numeric digits only (e.g. 12.4).")
    processed_time = 99.99  # Fallback default applied

# 4. The program continues running normally instead of crashing!
print("Stored competitor time is:", processed_time)
```

---

### **Try It with Help**
#### **The Problem: Securing the Shot-Put Distance Recorder**
The field referee logs shot-put throws in metres. Throw distances must be processed as decimal floats (e.g. `14.25`). If the input contains corrupt data characters, the script must intercept the error and reset the entry value to `0.0` so that school point totals are not corrupted.

**Your task:** Fill in the code blocks below to implement exception trapping.

```python
raw_throw_distance = "15.4m"  # Contains illegal character "m"
processed_distance = 0.0

____:  # <-- HINT: What keyword begins our protected execution block?
    # Convert string to float
    processed_distance = float(raw_throw_distance)
    print("Throw logged:", processed_distance)

____ ValueError:  # <-- HINT: What keyword intercepts the specific error?
    print("ERROR: Invalide characters in measurement!")
    # Reset to baseline default
    processed_distance = 0.0

print("Final logged throw distance:", processed_distance)
```

#### **Conceptual Check**
*   Why does line 6 trigger a `ValueError` in Python?
*   Trace the exact sequence of code lines that execute when this program runs.

---

### **Try It Yourself**
#### **The Problem: Competitor Registration Age Intake**
Design a complete, robust terminal input block in Python for processing the registered age of an incoming athlete.
*   The raw input to evaluate is stored in a variable: `raw_age = "14.5"` (a float representation, which cannot be converted directly into an integer `int()` without raising an error).
*   Wrap the conversion of `raw_age` to an integer variable `final_age = int(raw_age)` in a try-except structure.
*   If the conversion raises a `ValueError`, print a warning: "Age must be a whole number!" and assign `final_age = 0`.
*   If successful, print: "Age logged: X".

---

### **Check Your Reasoning**
#### **Try It with Help Solution**
*   First keyword: `try:`
*   Second keyword: `except`
*   **Trace Analysis:** Line 6 attempts `float("15.4m")`. The character `"m"` cannot be parsed as a decimal. Python immediately halts execution in the `try` block, ignores line 7, and transfers control to the `except ValueError:` block. Line 10 and 12 execute, resetting the distance to `0.0`. The program then moves to line 14, outputting: `"Final logged throw distance: 0.0"`.

#### **Try It Yourself Solution**
```python
raw_age = "14.5"
final_age = 0

try:
    # Converting a decimal string directly to an int raises a ValueError
    final_age = int(raw_age)
    print("Age logged:", final_age)
except ValueError:
    print("Age must be a whole number!")
    final_age = 0

print("Registered age:", final_age)
```

#### **SCSA Exam Trap: The "Blind Exception" Anti-Pattern**
> **SCSA Examiner Note:** Students frequently write a generic `except:` block without specifying the type of error they are catching (e.g. `except:` vs `except ValueError:`). This is bad programming practice. A generic exception block catches *everything*, including keyboard break interruptions (`Ctrl+C`) or system memory allocation faults, which makes troubleshooting your code nearly impossible. In ATAR examinations, always specify the exact exception you intend to capture, such as `ValueError`.

---

### **Review and Connect**
By wrapping input logic in `try-except` blocks, you guarantee that physical operator typos do not crash our sports entry system. This exception safety, combined with sequential calculations and multi-way selection systems, forms the logical core of SCSA **Assessment Task 1 (the Python Programming Project)**. In the next chapter, we will build on this to create repeating loops (iteration) to automatically process whole squads of runners.

---
---

## Chapter 2: Teacher Guide & Assessment Mapping

This professional guide is designed to assist Western Australian educators in delivering Chapter 2 content to meet Year 11 Computer Science ATAR standards.

### **SCSA Syllabus Mapping**
*   **Programming Concepts (Unit 1)**: Covers "program control structures: sequence, selection" and "good programming practice: exception handling" under the theoretical and practical skill guidelines of the Unit 1 syllabus.
*   **WACE Grade A Standard Indicators**:
    *   **Programming Skills**: Consistently and accurately applies programming control structures in pseudocode and a programming language to develop efficient solutions.
    *   **Good Programming Practice**: Correctly designs and implements exception handling blocks targeting specific error streams.

### **Misconception Busters & Diagnostic Interventions**

#### **1. The Colon and Indentation Standard**
*   **The Issue:** Students transitioning from block-based programming (such as Scratch) or text-based languages like Javascript often write selection structures without colons or indentations:
    ```python
    # SYNTAX ERROR
    if student_age >= 16
    print("Senior")
    ```
*   **The Intervention:** Have students highlight the colon at the end of every header block. Explain that in Python, the colon represents the "start of the pathway," and the 4-space indentation is the "safety gate" keeping those instructions inside that pathway.

#### **2. Multi-Way Mutual Exclusivity**
*   **The Issue:** Students assume that if they meet multiple conditions in an `if-elif` chain, all matching blocks will execute.
*   **The Intervention:** Present this code snippet to the class:
    ```python
    num = 15
    if num > 10:
        print("Greater than 10")
    elif num > 5:
        print("Greater than 5")
    ```
    Have them predict the output. Many will assume it prints both lines. Run the code to demonstrate that once "Greater than 10" evaluates to `True`, the program exits the structure, skipping "Greater than 5" entirely.

### **Classroom Discussion Starters**
1.  *Why is it critical for public registration systems—such as the Western Australian Department of Transport vehicle registration database—to use robust exception handling? What could happen if a database system crashed every time an operator made a physical typo?*
2.  *When designing software, why should we try to avoid using generic `except:` blocks? How does identifying specific errors (like `ValueError` vs `ZeroDivisionError`) make our code cleaner and safer to modify?*

### **Suggested School-Based Assessment Alignment**
*   **Task 1: Python Programming Project (20%)**: Direct students to integrate at least three `if-elif-else` control blocks and two distinct `try-except` validation routines into their interactive text-based game. This satisfies the SCSA requirements for complex control structures and good programming practices.
*   **Task 2: Practical Debugging Test (5%)**: Include a tracing question where a program fails due to a `ValueError` caused by converting textual input to an integer. Students must locate the error and repair the code by adding an appropriate `try-except` block.
