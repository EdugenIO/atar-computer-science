# Unit 1 — Chapter 3: Iteration & Looping

This chapter details the mechanics, logic, and implementations of program repetition structures in Python. Under the Western Australian SCSA Computer Science ATAR syllabus, mastering loop-based execution and input validation is critical for designing efficient algorithms and completing **Assessment Task 1 (the Programming Project)**.

---

## 3.1 Definite Iteration (for loops)

### **Your Goal**
Write and trace definite iteration loops using controlled iterators in Python, predicting outcomes and managing loop boundaries precisely.

### **Before You Start**
- [x] **Chapter 1.4**: Understand basic integer variables.
- [x] **Chapter 2.1**: Master sequential line execution.

### **The Idea**
Imagine a track coach telling an athlete, *"Run exactly 4 laps of the oval."* Before the run begins, the total number of repetitions (4) is known. The runner keeps track of which lap they are on, starting at Lap 1, increments the count after each lap, and stops as soon as Lap 4 is completed.

This is **definite iteration**. In computer science, definite iteration is used when the number of times a block of code must execute is determined *before* the loop starts running. 

In Python, definite iteration is implemented using the `for` loop, typically combined with the `range()` function. The loop variable (the iterator) changes value on each repetition, serving as a counter.

#### **Key Terms**
*   **Definite Iteration**: A loop structure that executes a block of code a predetermined number of times.
*   **Loop Control Variable (Iterator)**: The variable that tracks the current repetition number or item in a sequence.
*   **Range Boundary**: The start, stop, and step parameters that define the limits of loop execution.

---

### **See It Worked**
#### **The Scenario**
The WA Junior Sports Carnival uses a digital timing system. We need a program to count down from 5 to 1 to signal the start of a sprint event, followed by a "Go!" message.

#### **The Implementation (Python)**
```python
# Countdown timer for sprint start
print("Sprinters to your marks...")

# range(start, stop, step)
# Starts at 5, stops BEFORE 0 (i.e. at 1), stepping down by -1 each time
for count in range(5, 0, -1):
    print(f"{count}...")

print("GO! 🏃💨")
```

#### **How It Executes (The Trace Table)**
To verify this algorithm, we perform a **desk check** using a trace table. This tracks the state of variables at each line of execution.

| Iteration | Line Number | Variable: `count` | Output | Notes |
| :--- | :--- | :--- | :--- | :--- |
| Initial | 2 | - | *None* | Prints "Sprinters to your marks..." |
| 1 | 6 | `5` | `5...` | Loop starts; `count` initialized to 5. |
| 2 | 6 | `4` | `4...` | `count` decrements by 1. |
| 3 | 6 | `3` | `3...` | `count` decrements by 1. |
| 4 | 6 | `2` | `2...` | `count` decrements by 1. |
| 5 | 6 | `1` | `1...` | `count` decrements to 1. Stop value (0) reached next, exiting loop. |
| Exit | 9 | - | `GO! 🏃💨` | Prints launch statement. |

---

### **Try It with Help**
#### **The Problem**
Write an algorithm using a `for` loop that calculates and prints the cumulative score of a school house ("Gold") over 4 events. In each round of the loop, the program should ask for the score earned in that event and add it to a running total.

#### **Structural Hint**
You must initialize a accumulator variable (e.g. `total_score = 0`) *before* the loop starts. If you initialize it inside the loop, it will reset to `0` on every iteration!

```python
# Initialize the accumulator variable
total_score = 0

# Loop exactly 4 times (0, 1, 2, 3)
for round_num in range(1, 5): 
    # Prompt the user with a dynamic string indicating the round number
    score_input = int(input(f"Enter points won in Event {round_num}: "))
    
    # Add input to your running total
    total_score = total_score + score_input

# Output the final accumulated score
print(f"Total accumulated points: {total_score}")
```

---

### **Try It Yourself**
#### **The Problem**
Write a Python program that calculates the average run time of exactly 5 sprinters. Your program should:
1.  Set up an accumulator for total seconds.
2.  Use a `for` loop to capture each athlete's run time (as a decimal float).
3.  Calculate the final average.
4.  Print the average rounded to two decimal places.

---

### **Check Your Reasoning**
#### **The Correct Solution**
```python
total_time = 0.0

for runner in range(1, 6):
    time_entry = float(input(f"Enter time for Runner {runner} (sec): "))
    total_time += time_entry

average_time = total_time / 5
print(f"Average timing: {round(average_time, 2)} seconds.")
```

#### **Marking Criteria (SCSA Practical Test Style)**
*   **[1 Mark]**: Correct initialization of accumulator variable (`total_time = 0.0`) outside the loop.
*   **[1 Mark]**: Implement `for` loop with correct execution range (exactly 5 times, e.g. `range(1, 6)` or `range(5)`).
*   **[1 Mark]**: Capture runtime decimal entries as `float` inputs.
*   **[1 Mark]**: Accumulate inputs correctly inside the loop body (`total_time += time_entry`).
*   **[1 Mark]**: Correctly calculate average (divide by 5) and display output to 2 decimal places.

#### **Common SCSA Exam Pitfall**
*   **The Off-by-One Range Error**: Writing `range(1, 5)` expecting it to run 5 times. Remember, `range(start, stop)` stops *before* reaching the `stop` value. `range(1, 5)` only iterates for values `1, 2, 3, 4` (4 iterations). To iterate 5 times, use `range(1, 6)` or `range(5)`.

---

### **Review and Connect**
Definite iteration allows us to process structured sequences where the quantity is known. When we move to **Chapter 6 (Data Structures)**, we will use `for` loops to iterate over 1D arrays of athlete data.

---
---

## 3.2 Indefinite Iteration (while loops)

### **Your Goal**
Implement event-driven indefinite loops using logical conditional expressions in Python, ensuring correct termination conditions.

### **Before You Start**
- [x] **Chapter 2.2**: Master relational and conditional operators.
- [x] **Chapter 3.1**: Understand loop structures and iterators.

### **The Idea**
Imagine a high-jump official telling an athlete, *"Keep attempting to clear this bar height until you either clear it or use up all 3 attempts."* Before starting, the official does not know exactly how many attempts the athlete will make. They might clear it on the 1st attempt, or fail three times.

This is **indefinite iteration**. In computer science, indefinite loops repeat a block of code as long as a specified logical condition remains `True`. Because we do not know how many times the loop will execute, we must design a clear termination trigger to prevent the system from looping forever.

#### **Key Terms**
*   **Indefinite Iteration**: A loop structure that executes a block of code an unknown number of times, continuing until a logical condition changes state.
*   **Pre-Test Loop**: A loop that evaluates its conditional expression *before* executing the loop body (e.g. standard `while` loop).
*   **Infinite Loop**: A structural bug where the loop conditional never becomes `False`, freezing the system.

---

### **See It Worked**
#### **The Scenario**
At the WA Junior Sports Carnival timing booth, administrators enter the house names of winning relay squads. Because races occur throughout the day, the timing program needs to run indefinitely, capturing names until the user types `"DONE"`.

#### **The Implementation (Python)**
```python
# Event tracker with sentinel termination
print("Enter relay squad house names. Type 'DONE' to close today's log.")

# Initialize the loop control variable (sentinel variable)
house_name = input("First entry: ")

# Pre-test loop: check condition before executing block
while house_name != "DONE":
    print(f"Log updated: {house_name} registered.")
    
    # MUST update the loop control variable inside the loop body
    house_name = input("Next entry (or 'DONE'): ")

print("Relay tracking session terminated. Data synchronized.")
```

#### **How It Executes (The Trace Table)**
Let's desk-check the execution with input entries: `Gold`, `Red`, `DONE`.

| Iteration | Line Number | Variable: `house_name` | Relational Check: `house_name != "DONE"` | Output / Action |
| :--- | :--- | :--- | :--- | :--- |
| Entry | 5 | `"Gold"` | - | Takes input. |
| 1 | 8 | `"Gold"` | `"Gold" != "DONE"` (True) | Prints log update; prompts for next input. |
| 2 | 11 | `"Red"` | `"Red" != "DONE"` (True) | Prints log update; prompts for next input. |
| 3 | 11 | `"DONE"` | `"DONE" != "DONE"` (False) | Loop condition fails; loop terminates. |
| Exit | 13 | - | - | Prints final termination message. |

---

### **Try It with Help**
#### **The Problem**
A security lock for the timing console requires users to enter a numeric passcode. The user gets up to 3 attempts. Write a program using a `while` loop that locks the console out if 3 failed attempts are reached.

#### **Structural Hint**
You must track two conditions: whether the passcode entered is incorrect, and whether the attempt count is less than 3. Use a logical `and` operator to combine these conditions in your pre-test check.

```python
CORRECT_PIN = 1234
attempts = 0
access_granted = False

# Loop while access is not granted AND attempts are less than 3
while not access_granted and attempts < 3:
    pin_guess = int(input("Enter timing console PIN: "))
    
    if pin_guess == CORRECT_PIN:
        access_granted = True
        print("Console unlocked. Live timing activated.")
    else:
        attempts += 1 # Increment attempt counter
        remaining = 3 - attempts
        print(f"Incorrect PIN. Attempts remaining: {remaining}")

if not access_granted:
    print("TIMING SYSTEM LOCKED. Contact ATAR administrator.")
```

---

### **Try It Yourself**
#### **The Problem**
Write an indefinite timing-desk program that tracks high jump failures. 
1.  Initialize a variable tracking consecutive missed jumps to `0`.
2.  Use a `while` loop that keeps running as long as consecutive misses are fewer than 3.
3.  Inside the loop, prompt the operator to enter whether the athlete cleared the current bar (`"y"` or `"n"`).
4.  If they clear (`"y"`), reset consecutive misses to `0`. If they miss (`"n"`), add `1` to consecutive misses.
5.  If consecutive misses hit 3, exit the loop and print `"Competitor eliminated."`

---

### **Check Your Reasoning**
#### **The Correct Solution**
```python
consecutive_misses = 0

while consecutive_misses < 3:
    jump_result = input("Did the athlete clear the bar? (y/n): ")
    
    if jump_result == "y":
        consecutive_misses = 0 # reset tracking
        print("Success! High jump continues.")
    elif jump_result == "n":
        consecutive_misses += 1
        print(f"Miss registered! (Miss {consecutive_misses}/3)")
    else:
        print("Invalid entry. Use 'y' or 'n'.")

print("Competitor eliminated.")
```

#### **Common SCSA Exam Pitfall**
*   **The Infinite Loop (No Update)**: Forgetting to modify the loop control variable within the loop body. For example, if you checked `while consecutive_misses < 3` but never ran `consecutive_misses += 1` inside the loop, the check would always remain `0 < 3` (True) forever, crashing the computer.

---

### **Review and Connect**
Indefinite iteration is crucial when program execution depends on external, real-world events. We will build on this structural logic in **Chapter 5 (Testing & Debugging)** when designing system stress tests.

---
---

## 3.3 Loop-Based Input Validation

### **Your Goal**
Design and implement robust loop-based input validation routines in Python to protect program logic from corrupt or out-of-bounds input.

### **Before You Start**
- [x] **Chapter 2.4**: Master Python error handling blocks (`try/except`).
- [x] **Chapter 3.2**: Understand `while` loop syntax and execution.

### **The Idea**
Imagine a timing coordinator accidentally typing `122.5` seconds for an athlete's 100m sprint run time, or typing `"ten"` instead of `10.0`. If a program processes these invalid entries, it could calculate impossible averages, corrupt files, or crash completely.

In professional software development, you **never trust user input**. Input validation is a programming technique that acts like an entry guard: it checks all user data against logical rules *before* allowing the program to process that data. If the user inputs an invalid value, the program uses an indefinite loop to repeatedly prompt them until they enter clean, safe data.

#### **Key Terms**
*   **Input Validation**: Checking incoming data against range, type, or format constraints before processing.
*   **Boundary Checking**: Verifying if numerical data falls within logical, realistic constraints (minimum/maximum limits).
*   **Validation Loop**: A loop structure that forces a user to stay in a repetition block until input matches requirements.

---

### **See It Worked**
#### **The Scenario**
At the registration booth, clerks enter competitor age divisions. An age division must be an integer between 7 and 17 inclusive. We need an input validation loop that refuses out-of-bounds integers.

#### **The Implementation (Python)**
```python
# Initialize variable with an out-of-bounds value to force the loop entry
age_input = -1

# Validation loop: runs while age_input is outside the legal range [7, 17]
while age_input < 7 or age_input > 17:
    try:
        age_input = int(input("Enter competitor age (7 to 17): "))
        
        # Explicitly check range to prompt helpful error messaging
        if age_input < 7 or age_input > 17:
            print("Logical Error: Age must be between 7 and 17.")
            
    except ValueError:
        print("Type Error: Please enter a whole number (digits only).")
        # Ensure age_input remains out-of-bounds to keep loop active
        age_input = -1

# Input is confirmed valid at this point
print(f"Competitor registration validated. Assigned to Under {age_input + 1} division.")
```

#### **How It Executes (Logical Walkthrough)**
1.  **Loop Setup**: `age_input` is initialized to `-1`. Since `-1 < 7` is `True`, the `while` loop condition (`age_input < 7 or age_input > 17`) is met, and the loop starts.
2.  **Scenario A (User types `"ten"`)**:
    *   `int("ten")` throws a `ValueError`.
    *   The `except ValueError` block catches the crash.
    *   `age_input` resets to `-1`, loop condition remains `True`, and user is re-prompted.
3.  **Scenario B (User types `25`)**:
    *   `try` succeeds. `age_input` becomes `25`.
    *   The conditional checks `25 < 7 or 25 > 17` (True) and displays the range error message.
    *   The loop condition evaluates to `True`, keeping the user trapped.
4.  **Scenario C (User types `14`)**:
    *   `try` succeeds. `age_input` becomes `14`.
    *   The conditional checks `14 < 7 or 14 > 17` (False). No error printed.
    *   The loop condition evaluates to `False`, the loop exits, and execution proceeds cleanly.

---

### **Try It with Help**
#### **The Problem**
Write an input validation program for the shot-put event recording desk. High-school shot-put throws must be recorded as floats, and must be logically between 1.0 meters and 25.0 meters inclusive. 

#### **Structural Hint**
Use a `while True` loop structure combined with an internal `break` statement. This is an elegant, alternative SCSA-supported technique to validate inputs, mimicking a "post-test" loop.

```python
while True:
    try:
        # Prompt user to input distance
        distance = float(input("Enter shot-put distance (m): "))
        
        # Check boundary rules (1.0 to 25.0 inclusive)
        if 1.0 <= distance <= 25.0:
            # Input is valid! Break out of the infinite loop
            break
        else:
            print("Logical Error: Distance must be between 1.0m and 25.0m.")
            
    except ValueError:
        print("Type Error: Enter a decimal number.")

# Safe execution proceeds
print(f"Official distance saved: {distance}m.")
```

---

### **Try It Yourself**
#### **The Problem**
Design a validation loop for registration codes. A registration code must match one of the three legal house colors: `"RED"`, `"BLUE"`, or `"GREEN"`. Your program must:
1.  Prompt the user to enter a house color.
2.  Force uppercase comparison to prevent case issues.
3.  Loop indefinitely until the user enters one of the three verified strings.

---

### **Check Your Reasoning**
#### **The Correct Solution**
```python
valid_houses = ["RED", "BLUE", "GREEN"]

# Prompt initial input
house_choice = input("Enter house color (Red/Blue/Green): ").upper()

# Check containment in validation list
while house_choice not in valid_houses:
    print("Invalid house choice. Registration denied.")
    house_choice = input("Enter house color (Red/Blue/Green): ").upper()

print(f"Successfully registered competitor to {house_choice} house.")
```

#### **Common SCSA Exam Pitfall**
*   **The Ineffective Logical OR**: A common mistake is writing the conditional checking as `while house_choice != "RED" or house_choice != "BLUE"`. This creates an infinite loop! If a user inputs `"RED"`, it is true that `"RED" != "BLUE"`, so the overall evaluation is `True` and the loop repeats. When checking inequality exclusions, you must use `and` (e.g. `while house_choice != "RED" and house_choice != "BLUE"`) or use containment checking (`while house_choice not in ["RED", "BLUE"]`).

---

### **Review and Connect**
By utilizing loop-based validation, you guarantee **data integrity** at the software entry point. When you start building databases in **Unit 2 (Chapters 13-16)**, you will see how these validation principles translate into SQL schema constraints (`CHECK`, `NOT NULL`).

---
---

## Teacher Guide & Lesson Resources

### **WA Syllabus Links**
*   **Unit 1 (Programming)**: Program control structures: iteration.
*   **Unit 1 (Programming)**: Good programming practice: validate input before processing, exception handling.

### **Misconception Busters**
1.  **Pre-test vs. Post-test Iteration**: Explain to students that Python does not support a native `do-while` or `repeat-until` loop structure (post-test loops, which guarantee the loop body runs at least once before testing the condition). To emulate this in Python, developers use the `while True:` structure paired with a conditional `break` statement inside.
2.  **Scope of Loop Variables**: Clarify that unlike some high-level languages, variables initialized inside loop bodies or used as `for` iterators remain accessible in scope *after* the loop terminates in Python.

### **In-Class Discussion Prompts**
*   *Why is input validation considered a critical component of cybersecurity?* (Connect to how SQL injection attacks and buffer overflows rely on application layers blindly executing unvalidated input).
*   *If we have range bounds, do we need type checks?* (Yes, integer checks protect against numerical system crashes, while boundary range limits guarantee semantic accuracy).

### **Classroom Diagnostic Questions (Exit Tickets)**
1.  How many times does the loop body execute in `for i in range(2, 10, 3)`?
    *   *Answer*: 3 times (i takes values 2, 5, 8).
2.  What is the final value of `count` after this loop finishes?
    ```python
    count = 0
    while count < 5:
        count += 2
    ```
    *   *Answer*: 6 (Since 4 is less than 5, the loop executes one last time to increment count to 6).
