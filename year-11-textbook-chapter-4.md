# Unit 1 — Chapter 4: Modular Programming

This chapter introduces the power of modular design, subroutines, parameter passing, and variable scope in software development. By breaking down large, complex problems into small, self-contained units, we build software that is easy to write, test, debug, and maintain. 

---

## 4.1 Modular Design & Functions

### **Your Goal**
Deconstruct a complex programming problem into simple, single-purpose functions that perform exactly one logical task.

### **Before You Start**
- Check: Do you understand how variables hold data? (See **Lesson 1.4**)
- Check: Can you write basic conditional blocks to control execution? (See **Lesson 2.2**)

---

### **The Idea**
Imagine running a school sports carnival with 1,200 competitors. If a single coordinator tried to record every race time, calculate every house point, print every certificate, and sell food at the canteen simultaneously, the carnival would collapse into chaos. 

Instead, the coordinator delegates tasks:
*   **Person A** handles the stopwatch timing at the track.
*   **Person B** tallies the points at the main desk.
*   **Person C** prints the certificates.

In programming, this delegation of responsibility is called **modular decomposition**. We break a giant program into separate, independent blocks of code called **functions** (or subroutines). 

#### **Key SCSA Concepts**
*   **Modular Coding**: The practice of dividing a software solution into separate, independent subroutines.
*   **One Logical Task**: Each function should focus on doing exactly one job (e.g., *only* calculating speed, or *only* formatting a name). This is called high **cohesion**.
*   **Meaningful Naming**: Function names must use descriptive verbs indicating their job (e.g., `calculate_average_speed()`, not `thing()` or `do_stuff()`).

---

### **See It Worked**
Let's look at how to refactor a messy, sequential script into a clean, modular structure.

#### **The Messy Monolithic Script (No Modules)**
```python
# A flat, continuous script with no division of labor
print("--- WA Junior Sports Carnival ---")

# Task 1: Input and validation
distance_raw = input("Enter distance in meters: ")
if not distance_raw.isdigit():
    print("Invalid distance!")
    exit()
distance = float(distance_raw)

time_raw = input("Enter time in seconds: ")
if not time_raw.replace('.', '', 1).isdigit():
    print("Invalid time!")
    exit()
time = float(time_raw)

# Task 2: Calculation
speed = distance / time

# Task 3: Output Formatting
print(f"Athlete Speed: {speed:.2f} m/s")
```

#### **The Elegant Modular Design**
Here, we break the script into three distinct functions, each performing **one logical task**.

```python
def get_valid_input(prompt_text):
    """Task 1: Safely capture and return a positive decimal number."""
    while True:
        raw_val = input(prompt_text)
        try:
            val = float(raw_val)
            if val > 0:
                return val
            print("Value must be greater than zero.")
        except ValueError:
            print("Invalid input. Please enter a valid number.")

def calculate_speed(distance, time):
    """Task 2: Compute speed based on distance and time."""
    return distance / time

def display_results(speed):
    """Task 3: Display formatted speed to the operator."""
    print("---------------------------------")
    print(f"Calculated Speed: {speed:.2f} m/s")
    print("---------------------------------")

# Main Program Execution
print("--- WA Junior Sports Carnival ---")
run_distance = get_valid_input("Enter sprint distance (m): ")
run_time = get_valid_input("Enter runner time (s): ")

runner_speed = calculate_speed(run_distance, run_time)
display_results(runner_speed)
```

**Why this is better:** If the calculation rule for speed changes (e.g., converting to km/h), we only edit the `calculate_speed` function. The rest of the program remains untouched.

---

### **Try It with Help**
#### **The Scenario**
The timing desk wants a program that converts raw race times into points for the school house leaderboard. The points rule is:
*   Under 10 seconds: 10 points
*   10 to 12 seconds: 5 points
*   Over 12 seconds: 1 point

Below is a messy script. Your task is to refactor it by completing the scaffolded functions.

#### **The Buggy/Messy Script**
```python
# Refactor this!
time = float(input("Enter time: "))
if time < 10:
    pts = 10
elif time <= 12:
    pts = 5
else:
    pts = 1
print(f"Points Awarded: {pts}")
```

#### **Scaffolded Code (Fill in the blanks)**
```python
def get_athlete_time():
    # 1. Get user input, convert to float, and return it
    time_str = input("Enter race time (seconds): ")
    return float(time_str)

def calculate_house_points(seconds):
    # 2. Write the selection logic to evaluate 'seconds' and return the points
    if seconds < 10:
        return 10
    elif seconds <= 12:
        return 5
    else:
        return 1

def display_points(points_value):  
    # 3. Print the points awarded in a clean message
    print(f"Points Awarded: {points_value}")

# Main execution loop
time_taken = get_athlete_time()
points = calculate_house_points(time_taken)
display_points(points)
```

---

### **Try It Yourself**
#### **The Scenario**
The shot-put coordinator needs a clean modular system. Create a Python program that does the following:
1.  Defines a function `get_distance()` that prompts for, validates, and returns a single shot-put distance (float) in meters.
2.  Defines a function `is_new_record(distance, current_record)` that returns `True` if the distance is strictly greater than the current record, and `False` otherwise.
3.  Defines a main execution block that checks a throw of `14.2` meters against a school record of `13.8` meters, printing `"NEW RECORD!"` or `"Keep trying."` based on the outcome.

**Constraints:**
*   Do not combine inputs and comparisons in the same function.
*   Enforce descriptive naming conventions.

---

### **Check Your Reasoning**
Here is a complete, standard-compliant solution for the shot-put system:

```python
def get_distance():
    while True:
        try:
            val = float(input("Enter shot-put throw distance (m): "))
            if val >= 0:
                return val
            print("Distance cannot be negative.")
        except ValueError:
            print("Invalid numeric characters. Try again.")

def is_new_record(distance, current_record):
    return distance > current_record

# Main Block
school_record = 13.8
print(f"Current School Record: {school_record}m")

thrown_distance = get_distance()

if is_new_record(thrown_distance, school_record):
    print("★ NEW RECORD! ★")
else:
    print("Keep trying. Best of luck for the next throw.")
```

#### **Common SCSA Exam Pitfalls to Avoid:**
*   **The "Kitchen Sink" Function**: Writing functions that perform multiple unrelated tasks (e.g., reading an input and printing the output *inside* the calculation function). If an SCSA question asks for a calculation function, **do not write print statements inside it** unless explicitly asked. Use `return`.
*   **Generic naming**: Naming functions `fun1()`, `run()`, or `calc()`. Always use verb-noun pairs: `calculate_points()`, `validate_input()`.

---

### **Review and Connect**
*   **Recurrent Scenario Connect**: Organizing code into clean, modular components allows the WA Junior Sports Carnival developers to reuse the validation and calculation modules across sprint events, long jump, and high jump without duplicating code.
*   **Assessment Link**: Clean modular division of code is a fundamental requirement in **Assessment Task 1 (Programming Project)**. Up to 15% of your code quality marks depend on breaking your program down into logical, reusable functions instead of a long "spaghetti" script.

---
---

## 4.2 Parameters and Arguments

### **Your Goal**
Define, pass, and distinguish between parameters and arguments in modular Python programs.

### **Before You Start**
- Check: Can you define and call a basic function in Python? (See **Lesson 4.1**)
- Check: Do you know the difference between string and float variables? (See **Lesson 1.4**)

---

### **The Idea**
Imagine a school slip asking for permission to attend the sports carnival:
*   The blank form has a placeholder: `"Student Name: [               ]"`
*   When a parent fills it out, they write: `"Student Name: [ Sarah Jenkins ]"`

In programming:
*   The **placeholder** defined inside the function is called a **parameter** (or *formal parameter*).
*   The **actual value** you pass into the function when you call it is called an **argument** (or *actual argument*).

```
   def greet_athlete(athlete_name):  <--- 'athlete_name' is the PARAMETER (placeholder)
       print(f"Welcome, {athlete_name}!")
       
   greet_athlete("Sarah Jenkins")    <--- "Sarah Jenkins" is the ARGUMENT (actual value)
```

#### **Key SCSA Concepts**
*   **Parameter**: A variable listed in the function definition block. It acts as a local placeholder waiting for data.
*   **Argument**: The actual value or variable passed into the function when it is invoked (called).
*   **Parameter/Argument Alignment**: When calling a function, the arguments must match the parameters in **number**, **order**, and **data type**.

---

### **See It Worked**
Let's analyze a program that calculates a runner's velocity. We will map exactly how values travel from the main loop into the subroutine.

```python
def calculate_velocity(distance_m, time_s):
    # 'distance_m' and 'time_s' are formal parameters.
    # They only exist inside this function.
    if time_s == 0:
        return 0.0
    return distance_m / time_s

# MAIN PROGRAM
measured_distance = 100.0  # Float variable
measured_time = 12.5       # Float variable

# Invoking the function
runner_speed = calculate_velocity(measured_distance, measured_time)
# 'measured_distance' and 'measured_time' are the actual arguments.

print(f"Velocity: {runner_speed} m/s")
```

#### **Visualizing the Execution Trace:**
1.  The main program initializes `measured_distance` to `100.0` and `measured_time` to `12.5`.
2.  `calculate_velocity` is called.
3.  The value of the first argument (`measured_distance` -> `100.0`) is copied into the first parameter (`distance_m`).
4.  The value of the second argument (`measured_time` -> `12.5`) is copied into the second parameter (`time_s`).
5.  The calculation runs inside the function: `100.0 / 12.5 = 8.0`.
6.  The result (`8.0`) is returned and assigned to `runner_speed`.

---

### **Try It with Help**
#### **The Scenario**
The school database coordinator has built a function to format an athlete's certificate label. It must display their surname in ALL CAPS, followed by a comma, then their first name. 

Fill in the missing arguments and parameters below to complete the logic.

```python
# Definition Block
def format_certificate_name(first_name, surname):
    # Complete this function so it returns "SURNAME, Firstname"
    formatted_surname = surname.upper()
    return f"{formatted_surname}, {first_name}"

# Main Block
athlete_first = "Sarah"
athlete_last = "Jenkins"

# Call the function. Fill in the parameters/arguments correctly:
print("Printing certificate...")
display_name = format_certificate_name(athlete_first, athlete_last)

print(f"Certificate issued to: {display_name}")
```

---

### **Try It Yourself**
#### **The Scenario**
The WA Junior Sports Carnival uses "House Points" to determine the winning school. Write a Python program containing:
1.  A function named `calculate_bonus_points(base_points, places_won, is_champion_house)` that:
    *   Adds `base_points` and `(places_won * 2)`.
    *   If `is_champion_house` is `True`, adds an extra `50` points.
    *   Returns the total calculated points.
2.  A main program execution that calls this function for "Gold House", passing the following values as arguments:
    *   Base points: `450`
    *   Places won: `12`
    *   Is champion: `True`
3.  Prints the returned total points value with an appropriate label.

**SCSA Rules Check**: Ensure your variables are named meaningfully, and your function signature maps cleanly to the required parameters.

---

### **Check Your Reasoning**
Here is the correct Python structure to solve the sports points scenario:

```python
def calculate_bonus_points(base_points, places_won, is_champion_house):
    # Parameters: base_points (int), places_won (int), is_champion_house (bool)
    total = base_points + (places_won * 2)
    if is_champion_house:
        total += 50
    return total

# Main Program
gold_base = 450
gold_places = 12
gold_status = True

# Arguments passed in matching order, type, and count
final_points = calculate_bonus_points(gold_base, gold_places, gold_status)

print(f"Gold House Final Points Tally: {final_points}")
```

#### **Marking Guide (SCSA Style):**
*   **1 mark** for defining function `calculate_bonus_points` with exactly three parameters.
*   **1 mark** for implementing the correct mathematical evaluation inside the function.
*   **1 mark** for utilizing a conditional test based on the Boolean parameter.
*   **1 mark** for calling the function from the main script and passing matching arguments in the correct order.

---

### **Review and Connect**
*   **Recurrent Scenario Connect**: When we calculate values across 15 different regional schools in the Junior Sports Carnival, we don't write 15 different functions. We write *one* generic points function with parameters and pass each school's unique arguments into it dynamically.
*   **Assessment Link**: SCSA theory examinations almost always contain short-answer questions testing your ability to define the difference between a parameter and an argument. Remember: **Parameters** are defined; **arguments** are passed!

---
---

## 4.3 Scope of Variables (Global vs Local)

### **Your Goal**
Explain variable scope, trace local and global variable lifecycles, and fix variable namespace conflicts.

### **Before You Start**
- Check: Do you understand how variables hold values in memory? (See **Lesson 1.4**)
- Check: Are you comfortable writing functions that accept and return values? (See **Lesson 4.2**)

---

### **The Idea**
Imagine the rules at your school:
*   **The School Uniform Rule**: Only applies *inside* your school gates. If you walk down to the local shopping center on Sunday in casual clothes, the school principal cannot give you a detention. This rule has a **local scope**.
*   **WA Traffic Laws**: Apply *everywhere* in Western Australia—inside your school, outside your house, and at the beach. This law has a **global scope**.

In programming, the **scope** of a variable determines where in the code that variable is visible and can be accessed or modified.

```
                  GLOBAL SCOPE (Whole program)
     +-------------------------------------------------+
     |  global_points = 100                            |
     |                                                 |
     |        LOCAL SCOPE (Inside function)            |
     |       +----------------------------------+      |
     |       | def add_run():                   |      |
     |       |     local_score = 5              |      |
     |       |     print(local_score) # Works   |      |
     |       +----------------------------------+      |
     |                                                 |
     |  print(local_score) # CRASH! Cannot be seen.    |
     +-------------------------------------------------+
```

#### **Key SCSA Concepts**
*   **Global Variable**: A variable declared in the main body of a program. It is visible to the entire program, including inside all functions.
*   **Local Variable**: A variable declared inside a function. It is created when the function starts and is destroyed when the function exits (`returns`). It is completely invisible to the outside program.
*   **Namespace Collision**: Occurs when a local variable and a global variable share the exact same name, potentially leading to confusing bugs where local changes fail to affect the global state.

---

### **See It Worked**
Let's look at how local variables isolate memory. Observe how changes inside the function do not touch the main variable outside.

```python
# Global Variable
carnival_status = "Not Started"

def run_sprint_event():
    # Local Variable with the same name as the global variable!
    # This is called "shadowing".
    carnival_status = "Running Heats"
    print(f"Inside Function: Carnival status is '{carnival_status}' (Local)")

# Main Program
print(f"Start: Carnival status is '{carnival_status}' (Global)")
run_sprint_event()
print(f"End: Carnival status is '{carnival_status}' (Global)")
```

#### **Console Output:**
```text
Start: Carnival status is 'Not Started' (Global)
Inside Function: Carnival status is 'Running Heats' (Local)
End: Carnival status is 'Not Started' (Global)
```

**Why this happened**: The local variable `carnival_status` inside the function is a completely separate physical allocation in your computer's RAM. It exists only while `run_sprint_event` is running. When the function ends, the local variable is deleted from memory. The global variable remains unchanged at `"Not Started"`.

---

### **Try It with Help**
#### **The Scenario**
The timing coordinator attempted to write a score-tracking system. They wanted a button click to add `10` points to a school's overall score. However, their program output remains stuck at `0`!

Identify the bug in the code below and fix it by using returns instead of attempting to modify global scopes blindly.

#### **The Buggy Script**
```python
# Global Score Tracker
total_house_points = 0

def award_win_points():
    # Attempting to add 10 to the score
    total_house_points = total_house_points + 10  # This raises an UnboundLocalError!
    print(f"Points inside: {total_house_points}")

# Main execution
award_win_points()
print(f"Global points: {total_house_points}")
```

#### **The Fix (Using Return Scopes)**
Complete the clean, non-buggy code below by returning the modified value and assigning it back to the global tracker.

```python
# Clean Global Variable
total_house_points = 0

def award_win_points_clean(current_points):
    # 1. Take points as a parameter, calculate the new points locally, and return them
    new_points = current_points + 10
    return new_points

# Main execution
print(f"Starting Points: {total_house_points}")

# 2. Call the function, pass total_house_points, and re-assign the result to total_house_points
total_house_points = award_win_points_clean(total_house_points)

print(f"Updated Global Points: {total_house_points}")
```

---

### **Try It Yourself**
#### **The Scenario**
The WA Junior Sports Carnival's high-jump timing device logs variables. An external developer has supplied this buggy script:

```python
jump_height = 1.20 # Global variable

def set_target_height():
    jump_height = 1.45 # Local variable
    print(f"Local jump height set to: {jump_height}")

set_target_height()
print(f"Target is: {jump_height}") # Expecting 1.45, but it outputs 1.20!
```

**Your Task**:
Redesign this script in Python. Write a program that uses a function to calculate a new height (adding `0.05` meters to the current height passed as an argument) and updates the global variable `jump_height` cleanly in the main block *without* using the `global` keyword inside the subroutine.

---

### **Check Your Reasoning**
Here is the clean, structurally correct solution:

```python
# Main Global Variable
jump_height = 1.20

def calculate_next_increment(current_height):
    # Takes the current height as a parameter and returns a local increment
    incremented_height = current_height + 0.05
    return incremented_height

# Main Program Loop
print(f"Starting jump height: {jump_height}m")

# Clean update of global variable using functional parameters and returns
jump_height = calculate_next_increment(jump_height)

print(f"Next attempt target height: {jump_height}m")
```

#### **Trace Table of Variables:**
| Line # | Variable Name | Scope | Value | Action |
| :--- | :--- | :--- | :--- | :--- |
| 2 | `jump_height` | Global | `1.20` | Declared globally |
| 11 | `current_height` | Local | `1.20` | Parameter passed into function |
| 6 | `incremented_height` | Local | `1.25` | Calculated locally inside function |
| 11 | `jump_height` | Global | `1.25` | Updated globally via function return assignment |

---

### **Review and Connect**
*   **Recurrent Scenario Connect**: Keeping variables local prevents "cross-contamination" of runner times across different race lanes. If Lane 1 and Lane 2 timing systems both use local variables called `lap_time`, they will never overwrite each other's measurements.
*   **Assessment Link**: SCSA practical and theory exams penalize programs that rely heavily on global variables. Keeping variables locally scoped and using parameters is a key criterion for scoring full marks in the code development sections of **Assessment Task 2 (Practical Debugging Test)** and your semester exams.

---
---

## Teacher Guide & Chapter 4 Syllabus Mapping

This module contains curriculum-alignment strategies, pedagogical guidelines, and target diagnostic assessment protocols to support delivery of **Chapter 4: Modular Programming**.

### **SCSA Syllabus Alignment Matrix (Unit 1)**
*   **SCSA Core Concept**: *Modular coding using functions; one logical task per module; meaningful names for modules.*
    *   **Mapped Lesson**: **Lesson 4.1** (Modular Design & Functions) provides practical and conceptual scaffolding for converting monolithic logic blocks into high-cohesion functions.
*   **SCSA Core Concept**: *Modular coding using functions: parameters and arguments.*
    *   **Mapped Lesson**: **Lesson 4.2** (Parameters and Arguments) breaks down the physical and theoretical transport of data across subroutine boundaries.
*   **SCSA Core Concept**: *Modular coding using functions: scope of variables (Global, Local).*
    *   **Mapped Lesson**: **Lesson 4.3** (Scope of Variables) clarifies memory isolation, shadowing, and namespace conflict prevention.

---

### **Key Pedagogical Strategies**

#### **1. Addressing High-Frequency Misconceptions**
*   **The Parameter/Argument Conundrum**: Students often use the terms "parameter" and "argument" interchangeably. Use the "blank form vs. filled form" analogy. Test them continuously during desk checks: *"Is the variable inside this function header a parameter or an argument?"*
*   **The Global Keyword Trap**: Many students discover the `global` keyword in Python and use it as a shortcut to bypass returning values. **Establish a strict classroom ban on the global keyword.** Explain that in industrial software engineering, using global scope modification inside subroutines creates unpredictable dependency chains ("spaghetti code") and violates the principle of encapsulation.

#### **2. Formative Assessment Strategies**
*   **Code Refactoring Challenges**: Provide students with a long, unorganized text file containing 40 lines of sequential code. Task them with grouping sections into exactly four functions with named headers. 
*   **Trace Table Diagnostics**: Give students a function that shadows a global variable name (similar to Lesson 4.3) and ask them to complete a trace table. If they write down that the global variable changes value inside the function, you have identified a namespace scope misconception.

#### **3. SCSA Assessment Task Integration**
The modular principles learned in Chapter 4 are essential for success in **Assessment Task 1 (The Unit 1 Programming Project)**. 
*   **Project Integration**: When marking students' projects, check that their code is partitioned. For example, if they are building an interactive card game, check that they have separated the logic for shuffling the deck, scoring a hand, and printing the interface into distinct, single-purpose functions.
