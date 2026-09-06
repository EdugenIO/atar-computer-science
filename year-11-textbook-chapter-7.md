# Unit 1 — Chapter 7: Developing Algorithms

This chapter introduces the structural design and planning tools that computer scientists use to draft logic before writing formal code. You will explore the architectural benefits of structured algorithms, learn to write and read SCSA-compliant pseudocode, and design modular blueprints using structure charts and program stubs.

These systematic modeling skills are crucial for designing, documenting, and debugging complex solutions, forming the cornerstone of **SCSA School-Based Assessment Projects (Assessment Task 1)** and written theory examinations.

---

## Lesson 7.1: Benefits of Structured Algorithms

### Your Goal
Explain the specific architectural benefits of structured algorithms—including readability, modularity, ease of debugging, and code reusability—over monolithic design structures.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 4.1: Modular Design & Functions](./year-11-textbook-chapter-4.md#lesson-41-modular-design--functions).
*   [Lesson 4.3: Scope of Variables (Global vs Local)](./year-11-textbook-chapter-4.md#lesson-43-scope-of-variables-global-vs-local).

### The Idea
When building software, it is tempting to start writing code immediately. However, writing a program as one continuous sequence of instructions—known as a **monolithic** or "spaghetti" program—leads to massive complications as the project grows.

**The Analogy:**
Imagine organizing the **WA Junior Sports Carnival** with a team of 10 volunteers. 
*   **The Monolithic Way:** You write a single, massive 15-page instruction manual. Every volunteer must read the entire document, and if a rule changes for the shot-put sector, you have to rewrite and re-distribute the entire manual, hoping nobody gets confused by page references.
*   **The Structured Way:** You break the day into discrete, independent jobs: a "Ticketing Guide," a "Timing Gate Guide," and a "Catering Guide." If the timing gate system changes, you only update the Timing Gate Guide. The ticketing team continues working without interruption, completely unaffected by the update.

Structured programming is an approach where a complex problem is broken down into small, self-contained, logical modules (subroutines or functions), each performing a single, well-defined task.

#### **SCSA Key Terms**
*   **Structured Algorithm:** An algorithm design divided into distinct, independent subroutines, each with a single entry and exit point, using structured control paths (sequence, selection, and iteration).
*   **Monolithic Code:** A program written as a single, continuous stream of execution without modular divisions, relying heavily on global state.
*   **Modularity:** The degree to which a system's components may be separated and recombined, allowing independent development of separate modules.
*   **Readability:** The ease with which a human reader can comprehend the purpose, control flow, and logic of an algorithm.
*   **Ease of Debugging:** The ability to isolate, identify, and repair logical errors within a specific, localized module without affecting the rest of the system.
*   **Code Reusability:** The practice of writing a module once and invoking it multiple times across different parts of the system (or in future projects) rather than rewriting the code.

#### **Comparison Table: Monolithic vs. Structured Design**

| Metric | Monolithic Design | Structured Design |
| :--- | :--- | :--- |
| **Organization** | One giant main script. | Divided into small, single-purpose functions. |
| **Variable Scope** | Heavy reliance on global variables. | Local variables with strict parameter passing. |
| **Testing** | Must run and test the entire program at once. | Modules can be tested individually (unit testing). |
| **Debugging** | Extremely difficult; a change in line 20 can break line 300. | Errors are isolated within a single function. |
| **Team Collaboration** | Hard; programmers overwrite each other's work in the same file. | Programmers can work on different modules simultaneously. |

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival coordinators want to process an athlete's trial runs: get their three sprint times, compute the average, and save the result to a database file. 

Let's contrast the design of a **monolithic script** with a **structured design** to see the differences in readability and maintenance.

#### **Monolithic Implementation (Avoid This!)**
```python
# One long, unstructured block
print("WA Junior Sports Carnival Timing Desk")
times = []
for i in range(3):
    while True:
        try:
            val = float(input(f"Enter sprint time {i+1}: "))
            if val > 0:
                times.append(val)
                break
            print("Time must be positive!")
        except ValueError:
            print("Invalid input!")

total = 0
for t in times:
    total += t
avg = total / len(times)

file = open("carnival_results.txt", "a")
file.write(f"Average: {avg:.2f}\n")
file.close()
print("Saved successfully.")
```

#### **Structured Implementation (The Professional Way)**
```python
def capture_positive_float(prompt):
    """Module 1: Focuses solely on safe user input."""
    while True:
        try:
            val = float(input(prompt))
            if val > 0:
                return val
            print("Value must be positive.")
        except ValueError:
            print("Invalid numeric characters. Try again.")

def calculate_average(numbers_list):
    """Module 2: Focuses solely on mathematical average calculation."""
    if not numbers_list:
        return 0.0
    total = 0
    for num in numbers_list:
        total += num
    return total / len(numbers_list)

def append_to_file(filename, data_string):
    """Module 3: Focuses solely on writing to external storage."""
    file = open(filename, "a")
    file.write(data_string + "\n")
    file.close()

def main():
    """Main control module organizing the program flow."""
    print("WA Junior Sports Carnival Timing Desk")
    
    # 1. Capture 3 trials using Module 1
    sprint_times = []
    for i in range(3):
        time_entry = capture_positive_float(f"Enter sprint time {i+1}: ")
        sprint_times.append(time_entry)
        
    # 2. Compute average using Module 2
    avg_sprint = calculate_average(sprint_times)
    
    # 3. Save average using Module 3
    append_to_file("carnival_results.txt", f"Average: {avg_sprint:.2f}")
    print("Saved successfully.")

# Execute Main Program
if __name__ == "__main__":
    main()
```

#### **How the Logic Decisions Excel in the Structured Version**
1.  **Readability:** Look at the `main()` function in the structured code. You can understand the entire program flow in 4 lines of clear, self-documenting code, without wading through input loops or file operations.
2.  **Code Reusability:** If we later need to capture field event distances (like shot-put throws), we can reuse the `capture_positive_float()` function without copying and pasting validation loops.
3.  **Ease of Debugging:** If the program fails when saving files, we know immediately that the error lies inside `append_to_file()`. We can debug that single function in isolation without touching our mathematical or input validation logic.

---

### Try It with Help
#### **The Problem**
A student is explaining structured programming in their semester exam. They write: *"Structured programming is better because you can use GOTO statements to jump around code and make files smaller."* 

Rewrite this response to provide a correct, high-scoring SCSA explanation of **why** structured programming is superior to monolithic design, referencing the core benefits of readability and modularity.

#### **Structural Hints**
*   Explain how breaking programs into subroutines improves **readability** (makes code easier to read for external programmers).
*   Describe how **modularity** supports collaborative development (multiple programmers working on different subroutines).
*   Address how localized scopes make **debugging** faster and safer.

#### **Scaffolded Response Template**
> "Structured programming is superior because it replaces a single, continuous, monolithic block of code with distinct, single-purpose ______________. 
>
> Firstly, this dramatically improves **readability** by allowing a developer to look at a high-level control routine (like `main()`) and instantly comprehend the control flow without being distracted by operational details. 
>
> Secondly, it introduces **modularity**, which is highly beneficial for teams because programmers can build and test individual functions like ______________ and ______________ at the same time. 
>
> Finally, structured programming makes **debugging** far easier because errors are confined to localized modules, reducing the risk that a code modification in one section of the program will accidentally ______________."

---

### Try It Yourself
#### **The Problem**
A volunteer at the WA Junior Sports Carnival timing office has written a python script that calculates race speeds and updates a global scoreboard. The script is entirely monolithic, containing over 400 lines of unorganized instructions, global lists, and input loops.

The school's IT support officer refuses to host the program, citing a lack of structured design. 

**Your Task:** Write a technical memo to the volunteer explaining **four distinct operational risks** of maintaining their monolithic program, and justify why converting it to a structured algorithm will save time during the live sports event.

---

### Check Your Reasoning
#### **The Answer**
A high-scoring SCSA-style memo should clearly identify and explain four key concepts (Modularity, Readability, Debugging, Reusability):

```
TECHNICAL MEMORANDUM
TO: Timing Office Volunteer
FROM: Lead IT Systems Administrator
SUBJECT: Monolithic Code Operational Risks and Structured Migration

Maintaining the current 400-line monolithic results script presents significant operational risks during the live carnival:

1. High Debugging Latency (Lack of Isolation):
   Because the program is monolithic and uses global lists, a logical error in the scoreboard update logic could corrupt the global timing variable. This makes isolating the bug during live races extremely slow, as the entire 400-line script must be analysed.

2. Fragile Code Modification (Coupling Errors):
   Changing how race inputs are structured (e.g., adding milliseconds to the data format) will require manually scouring and editing multiple locations throughout the script, increasing the risk of introducing syntax or logic errors.

3. Complete Loss of Reusability:
   The validation loops and formatting logic are bound inside the main thread. If we decide to launch a secondary field-event track system, we cannot reuse those validated blocks without copying code, which multiplies the maintenance effort.

4. Collaborative Bottlenecks:
   Only one developer can safely edit the file at a time. In a structured design, different volunteers could independently develop and test modules like 'sort_leaderboard()' and 'validate_times()' in isolation.

By converting the program to a structured design with independent functions, we can easily run unit tests on each subroutine and guarantee a stable system for the carnival.
```

#### **Common SCSA Student Errors**
1.  **Vague Descriptions:** Saying structured code is "easier" or "faster" without explaining *why* (e.g., failing to link modularity to collaborative development or isolated variables).
2.  **Confusing Structure with Performance:** Believing structured code runs faster on computer hardware. (In reality, modern processors do not care about modular division; structured programming is a design choice that benefits *humans*).
3.  **Proposing "Global" Solutions:** Suggesting structured code should use more global variables. SCSA markers reward the containment of data through local scope and parameter passing.

---

### Review and Connect
By structuring your algorithms, you make your programs highly maintainable and clean. In the next lesson, we will explore the formal language used to design and draft these structured algorithms before writing any actual code: **SCSA-Standard Pseudocode**.

---

## Lesson 7.2: Pseudocode Representation

### Your Goal
Read and write SCSA-Standard pseudocode using correct algorithmic notation, assignment indicators, selection structures, and loop constructs.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 2.2: Selection (if, else)](./year-11-textbook-chapter-2.md#lesson-22-selection-if-else).
*   [Lesson 3.1: Definite Iteration (for loops)](./year-11-textbook-chapter-3.md#lesson-31-definite-iteration-for-loops).
*   [Lesson 3.2: Indefinite Iteration (while loops)](./year-11-textbook-chapter-3.md#lesson-32-indefinite-iteration-while-loops).

### The Idea
Before coding a structured algorithm in a specific language (like Python, Java, or C++), computer scientists must map out the logical steps in a language-independent format. 

**Pseudocode** is a text-based, structured method used to represent algorithms. It uses a combination of natural language (English) and structured programming constructs (like loops and branches) to map logical flows.

The Western Australian **School Curriculum and Standards Authority (SCSA)** enforces a specific, rigid pseudocode standard in all ATAR exams. To secure maximum marks, you must understand SCSA syntax conventions.

#### **The Golden Rules of SCSA Pseudocode Syntax**
1.  **CAPITALIZE All Keywords:** Control structures and logical operators must always be written in uppercase (e.g., `IF`, `THEN`, `ELSE`, `ENDIF`, `WHILE`, `FOR`, `AND`, `OR`, `NOT`).
2.  **The Left-Pointing Arrow for Assignment:** You must never use the `=` sign to assign values to variables. SCSA pseudocode reserves the single equals sign strictly for comparison. For variable assignment, you must write a left-pointing arrow: `<-` (or `←`).
    *   *SCSA Standard:* `points <- 10`
    *   *Incorrect:* `points = 10`
3.  **Indentation:** Indent all nested statements within selection blocks (`IF`) and loops (`WHILE`, `FOR`) to visually display structural hierarchy.
4.  **End Your Structures:** Always close control structures explicitly (e.g., `ENDIF`, `ENDWHILE`, `ENDFOR`).

#### **SCSA Standard Control Block Templates**

##### **1. Assignment**
```text
variable <- expression
```

##### **2. Selection (Branching Decisions)**
```text
IF condition THEN
    statements
ELSE
    statements
ENDIF
```

##### **3. Definite Loop (Count-Controlled)**
```text
FOR iterator <- start_value TO end_value
    statements
ENDFOR
```

##### **4. Indefinite Loop (Pre-Test Conditional)**
```text
WHILE condition
    statements
ENDWHILE
```

##### **5. Subroutine Definition & Return**
```text
MODULE calculate_average(numbers)
    statements
    RETURN value
ENDMODULE
```

---

### See It Worked
#### **The Scenario**
At the WA Junior Sports Carnival, we need to design an algorithm that searches an array of 5 runner times, counts how many times were under 12.0 seconds, and returns the final count.

Let's look at how we write this algorithm in **SCSA-Standard Pseudocode** versus how we write it in **Python**.

#### **SCSA Pseudocode Version**
```text
MODULE count_fast_runners(times_array)
    count <- 0
    
    FOR i <- 0 TO 4
        IF times_array[i] < 12.0 THEN
            count <- count + 1
        ENDIF
    ENDFOR
    
    RETURN count
ENDMODULE
```

#### **Equivalent Python Implementation**
```python
def count_fast_runners(times_array):
    count = 0
    
    for i in range(5):
        if times_array[i] < 12.0:
            count = count + 1
            
    return count
```

#### **Key Syntax Transitions to Observe**
*   **Module Enclosure:** The pseudocode uses `MODULE ... ENDMODULE` instead of Python's `def`.
*   **Variable Assignments:** In pseudocode, we write `count <- 0` and `count <- count + 1`. In Python, we write `=` or `+=`.
*   **Loop Boundary:** The pseudocode loop runs `FOR i <- 0 TO 4`, explicitly declaring the inclusive loop bounds. Python uses `range(5)`, which implicitly generates sequence values from `0` to `4`.
*   **Explicit Structure Closures:** Notice `ENDIF` and `ENDFOR` in the pseudocode. Python relies solely on indentation whitespaces to determine where loops and blocks end.

---

### Try It with Help
#### **The Problem**
Write an SCSA-Standard pseudocode algorithm for an indefinite loop that validates user PIN inputs. 
The program must prompt the user for their registration code, check if it matches the master key `941`, and repeatedly lock out the user, prompting them again until they enter the correct code.

#### **Structural Hints**
*   Use `INPUT` to capture user data.
*   Store the input in a variable `user_input` using the `<-` assignment operator.
*   Structure an indefinite loop using `WHILE user_input != 941`. (Remember to write `WHILE` in uppercase!).
*   Inside the loop, prompt for input again so the value changes.
*   Don't forget to close your loop with `ENDWHILE` and capitalize all control terms!

#### **Scaffolded Pseudocode Template**
```text
MODULE validate_registration()
    master_key <- 941
    
    DISPLAY "Enter your registration access PIN: "
    INPUT user_input
    
    WHILE user_input != master_key
        DISPLAY "Access denied. PIN incorrect."
        DISPLAY "Enter PIN again: "
        INPUT user_input
    ENDWHILE
    
    DISPLAY "Access granted."
ENDMODULE
```

---

### Try It Yourself
#### **The Problem**
Review the following Python function, which iterates through an array of 10 shot-put throw distances, determines the maximum throw distance, and returns it.

```python
def find_maximum_throw(throws):
    max_throw = throws[0]
    for idx in range(1, 10):
        if throws[idx] > max_throw:
            max_throw = throws[idx]
    return max_throw
```

Write an equivalent algorithm written strictly in **SCSA-Standard Pseudocode**. Ensure all assignment operators, loops, selection structures, and module declarations follow exam conventions perfectly.

---

### Check Your Reasoning
#### **The Answer**
Below is the SCSA-Standard pseudocode translation. Note the uppercase syntax, correct assignment arrows, and explicit end clauses:

```text
MODULE find_maximum_throw(throws)
    max_throw <- throws[0]
    
    FOR idx <- 1 TO 9
        IF throws[idx] > max_throw THEN
            max_throw <- throws[idx]
        ENDIF
    ENDFOR
    
    RETURN max_throw
ENDMODULE
```

#### **SCSA Exam Grading Scheme (3 Marks)**
*   **1 Mark:** For declaring the module correctly with `MODULE` / `ENDMODULE` and capturing parameters.
*   **1 Mark:** For implementing correct assignment structures (using `<-`, specifically initialization `max_throw <- throws[0]` and loop update `max_throw <- throws[idx]`).
*   **1 Mark:** For writing correct loops and selections with explicit structures (`FOR idx <- 1 TO 9 ... ENDFOR` and `IF ... THEN ... ENDIF`).

#### **Common SCSA Student Errors**
1.  **Using Python Syntax in Exams:** Writing `def` instead of `MODULE`, or leaving out `THEN` on the `IF` line. SCSA markers actively dock points for language leaks.
2.  **Off-by-One Loop Bounds:** Writing `FOR idx <- 1 TO 10`. Because the array has 10 elements and indices run from `0` to `9`, checking index `10` will cause an index-out-of-bounds crash in pseudo-execution!
3.  **No Assignment Arrows:** Writing `max_throw = throws[0]`. In ATAR examinations, utilizing the `=` symbol for assignment is a high-frequency error that directly results in lost marks.

---

### Review and Connect
Using SCSA pseudocode allows you to represent any algorithm's logical details cleanly. But how do we visualize high-level program architectures and show the flow of parameters between our modules? In the next page, we learn about **Structure Charts and Program Stubs**.

---

## Lesson 7.3: Structure Charts & Stubs

### Your Goal
Construct and interpret structure charts displaying module relationships, data couples, and control flags, and implement code stubs to test modular integration.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 4.2: Parameters and Arguments](./year-11-textbook-chapter-4.md#lesson-42-parameters-and-arguments) (scoping data exchanges).
*   [Lesson 7.1: Benefits of Structured Algorithms](#lesson-71-benefits-of-structured-algorithms).

### The Idea
When designing a complex program, we need a visual way to show the hierarchy of modules and how data is shared between them. We use a **Structure Chart** as our primary visual design tool.

**The Analogy:**
Imagine looking at a corporate chart for the **WA Junior Sports Carnival Committee**:
*   The **Carnival Coordinator** (Main Module) sits at the top.
*   They delegate tasks down to the **Timing Desk Manager** and **Scoreboard Writer** (Subroutines).
*   The Coordinator passes a physical clipboard of raw race times down to the Timing Manager. (This is a **parameter / argument** pass).
*   The Timing Manager processes the numbers and hands back a neat average score card. (This is a **return value**).
*   If a problem occurs (like a timing sensor failure), the Timing Manager raises a red flag to notify the Coordinator. (This is a **control flag**).

A Structure Chart displays this exact modular relationships, showing how variables flow up and down the system.

#### **Structure Chart Anatomy and Symbols**
A structure chart consists of boxes representing modules, connected by arrows showing execution pathways.

```text
                      [ Main Control Module ]
                                 │
                 ┌───────────────┴───────────────┐
                 │ (Data Out)                    │ (Data In)
                 ▼ ◯                             ▼ ◯
           ┌───────────┐                   ┌───────────┐
           │ Module A  │                   │ Module B  │
           └───────────┘                   └───────────┘
```

1.  **Module Boxes:** Rectangular boxes labeled with the module's name, representing a self-contained function.
2.  **Connection Lines:** Solid lines showing which modules call other modules (called from top to bottom).
3.  **Data Couples (◯──►):** Arrows with an **open circle** on the tail. They represent variables containing raw data passed between modules (e.g., passing a list of times or an athlete's age).
4.  **Control Flags (●──►):** Arrows with a **filled (solid black) circle** on the tail. They represent control signals, states, or status flags used to control logical branching (e.g., an `is_valid` flag, a `success_status`, or an `end_of_file` warning).
5.  **Iteration Arc (↻):** A curved arrow sweeping across connection lines, indicating that those module calls run repeatedly inside a loop.
6.  **Decision Diamond (♦):** A diamond drawn over connection lines, indicating that calling the connected sub-modules is conditional (occurs inside an `IF` statement).

#### **What is a Program Stub?**
When building a structured system with multiple modules, you cannot write everything at once. If you wait until every function is 100% finished before running your program, finding integration bugs becomes a nightmare.

Instead, we write **Program Stubs** (or mock subroutines).
A **stub** is a simple, temporary placeholder function that mimics a completed module by returning hardcoded test values. This allows developers to test the overarching high-level program control flow and parameter exchanges before implementing the underlying algorithms.

---

### See It Worked
#### **The Scenario**
We are designing a timing system dashboard. The program structure chart looks like this:

```text
                            [ main ]
                                │
          ┌─────────────────────┼─────────────────────┐
          │                     │                     │
      (prompt)                  │ (times)             │ (average)
       ◯──►                     ▼ ◯                   ▼ ◯
    ┌─────────────┐       ┌─────────────┐       ┌─────────────┐
    │  get_times  │       │ calculate_  │       │   display_  │
    │             │       │   average   │       │  dashboard  │
    └─────────────┘       └─────────────┘       └─────────────┘
          ▲ ◯                     ▲ ◯
       (time_val)             (avg_val)
```

We want to build this program. However, our database calculations for `calculate_average` are extremely complex and still being drafted by another developer. 

To prevent development bottlenecks, we construct a **program stub** in Python to test if `main()` passes variables and handles returns correctly.

#### **Python Implementation with a Program Stub**
```python
def get_times(prompt):
    """A fully operational input module."""
    print("Simulating timing capture...")
    return [11.5, 12.1, 10.9]

def calculate_average(times_list):
    """
    PROGRAM STUB
    The mathematical average logic is not implemented yet.
    We return a hardcoded value (11.5) to verify data flow.
    """
    print(f"[STUB] Received list: {times_list}. Returning mock value 11.5")
    return 11.5

def display_dashboard(average):
    """A fully operational display module."""
    print(f"=== CARNIVAL DASHBOARD ===")
    print(f"Average Field Sprint Time: {average} seconds")

def main():
    print("Initializing Timing Dashboard...")
    # 1. Fetch raw timing array
    captured_times = get_times("Enter data:")
    
    # 2. Call the STUB module to test parameter flow
    mock_avg = calculate_average(captured_times)
    
    # 3. Print out result to test communication chain
    display_dashboard(mock_avg)

if __name__ == "__main__":
    main()
```

#### **How the Stub Resolves Development Barriers**
*   Running this script outputs `=== CARNIVAL DASHBOARD === Average Field Sprint Time: 11.5 seconds`.
*   Even though our actual mathematical code is empty, we have proven that `main()` successfully passes `captured_times` down to `calculate_average`, captures the returned value, and feeds it into the display dashboard. 
*   Once the math formulas are ready, we can swap out the stub contents with the actual arithmetic loops, confident that the high-level program structure is 100% bug-free.

---

### Try It with Help
#### **The Problem**
Consider a student enrollment module at the carnival desk. A structure chart shows a parent module `enroll_student` calling a sub-module `validate_age`. 
*   `enroll_student` passes `birth_year` (an integer) down to `validate_age`.
*   `validate_age` checks the age limit and sends a boolean status flag named `is_allowed` back up.

Identify which variables represent the **Data Couple** and which represent the **Control Flag**, and match them to their correct visual symbol representation.

#### **Structural Hints**
*   **Data Couple:** Relates to raw numeric or text data parameters. Symbol: Arrow with an **open** circle base (◯──►).
*   **Control Flag:** Relates to logical states, decisions, or system checks. Symbol: Arrow with a **solid** black circle base (●──►).

#### **Matching Activity Sheet**
1.  **The parameter `birth_year` flowing down is a:** ________________________
    *   *Visual Symbol:* ________________________
2.  **The return flag `is_allowed` flowing up is a:** ________________________
    *   *Visual Symbol:* ________________________

---

### Try It Yourself
#### **The Problem**
Draw or map out a Structure Chart representing an authentication and login program for the WA Junior Sports Carnival administration desk. 

The structure has three layers:
1.  **Main Module:** `admin_portal`
2.  `admin_portal` calls `capture_login_details`, which prompts the user and returns `username` and `password` to the main module.
3.  `admin_portal` then calls `authenticate_user`, passing `username` and `password` down. 
4.  `authenticate_user` checks the credentials and returns a status flag `is_authorised` back up.
5.  If `is_authorised` is true, the main module calls `display_welcome_banner`, passing `username` down.

**Your Tasks:**
1.  Write a detailed text description detailing every module box, describing the arrows, data couples, and control flags flowing between them.
2.  Write a complete, executable Python program representing this flow, implementing `capture_login_details` and `display_welcome_banner` fully, but using a **program stub** for the complex database-dependent `authenticate_user` module.

---

### Check Your Reasoning
#### **The Answer**
##### **1. Structure Chart Flow Architecture**
```
                    [ admin_portal ]
                    /       │      \
     (username,     /        │       \  (username)
      password)    /         │        \  ◯──►
        ▲ ◯       /          │         \
                 /    (username,        ▼
                ▼      password)    [ display_welcome_banner ]
 [ capture_login_details ]  ◯──►
                             ▼
                    [ authenticate_user ]
                             ▲
                             │ ● (is_authorised)
```

##### **Detailed Mapping Description:**
*   **Sub-Module Calling Hierarchy:** `admin_portal` sits at the top, calling three children: `capture_login_details`, `authenticate_user`, and `display_welcome_banner`.
*   **Connection 1 (capture_login_details):** No data flows down. A **Data Couple** (◯──►) containing `username` and `password` flows up to `admin_portal`.
*   **Connection 2 (authenticate_user):** A **Data Couple** (◯──►) containing `username` and `password` flows down from `admin_portal`. A **Control Flag** (●──►) named `is_authorised` flows up to `admin_portal`.
*   **Conditional Execution:** The line calling `display_welcome_banner` is marked with a **Decision Diamond** (♦) because it is conditional upon `is_authorised` being true.
*   **Connection 3 (display_welcome_banner):** A **Data Couple** (◯──►) containing `username` flows down from `admin_portal`. No data is returned.

##### **2. Python Implementation with Mock Stub**
```python
def capture_login_details():
    """Captures input details."""
    print("=== Carnival Portal Login ===")
    user = input("Enter admin username: ")
    passwd = input("Enter password: ")
    return user, passwd

def authenticate_user(user, passwd):
    """
    PROGRAM STUB
    Mocking database connection logic. Checks if user is "admin" with "sports123".
    """
    print(f"[STUB] Authenticating user: '{user}'")
    if user == "admin" and passwd == "sports123":
        # Returns True and a control flag
        return True
    return False

def display_welcome_banner(user):
    """Displays welcome dashboard."""
    print(f"\n===========================")
    print(f"WELCOME BACK, {user.upper()}!")
    print(f"WA Junior Sports Carnival Admin Dashboard.")
    print(f"===========================")

def main():
    # 1. Fetch details
    username, password = capture_login_details()
    
    # 2. Authenticate using the STUB module
    is_authorised = authenticate_user(username, password)
    
    # 3. Branch conditionally based on return flag
    if is_authorised:
        display_welcome_banner(username)
    else:
        print("Access Denied. Invalid credentials.")

if __name__ == "__main__":
    main()
```

#### **Common SCSA Student Errors**
1.  **Confusing Data Couples and Control Flags:** Drawing an open circle for `is_authorised`. Since `is_authorised` is a boolean condition that dictates program logic, it *must* have a solid circle (●) tail.
2.  **Missing arrows or directions:** Leaving out direction arrows on connection blocks. Structure charts must show the direction of flow (down or up) explicitly.
3.  **No Stub Printing:** Writing a stub that does not print a placeholder message (e.g., `print("[STUB]...")`). SCSA assessors look for stubs that actively log execution traces during debugging tests.

---

### Review and Connect
In this lesson, you mastered visualizing software structures using SCSA-compliant structure charts and verified logical designs using program stubs. 

These architectural techniques are highly examinable and will prove invaluable when designing and developing your multi-module interactive game project for SCSA Assessment Task 1.

---

## Unit 1 — Chapter 7: Teacher Support Module

### **WA Syllabus Curriculum Mapping**
*   **SCSA Syllabus Link:** Benefits of structured algorithms (readability, modularity, ease of debugging, code reusability).
*   **SCSA Syllabus Link:** Software representation and modeling tools: pseudocode and structure charts (modules, parameters, returns, loops, decisions).
*   **SCSA Syllabus Link:** Testing and implementation strategies: program stubs.

### **Prerequisite Knowledge Checklist**
Students must be comfortable with the following before beginning Chapter 7:
1.  Creating user-defined subroutines with arguments and return statements in Python ([Chapter 4](./year-11-textbook-chapter-4.md)).
2.  Understanding how local scopes protect variables from being mutated globally ([Chapter 4](./year-11-textbook-chapter-4.md)).
3.  Mapping simple selections and comparisons using relational syntax ([Chapter 5](./year-11-textbook-chapter-5.md)).

### **High-Frequency Student Misconceptions**
*   **The Equivalence Symbol Trap:** Students consistently write standard math equality blocks (`=`) when performing variable assignments in exam pseudocode. Reinforce: `<-` is for saving data, and `=` is for comparing.
*   **The Global Scope Crutch:** Students transitioning from small scripts often struggle to pass arguments, reverting to making all variables global. Show them how global dependencies break structure charts and make isolated unit testing impossible.
*   **Solid vs. Open Circle Confusion:** Students frequently mistake the visual distinction between data parameters (data couples, open circles) and boolean conditions (control flags, solid circles). Ensure they trace variable types: if it is a boolean used for switching code branches, it is a control flag.

### **Suggested Assessment Tasks**
*   **SCSA Project Connection (Task 1):** Require students to submit a complete SCSA Structure Chart and Pseudocode draft for their interactive Python game's scoring and validation routines *before* they are permitted to write code.
*   **Practical Debugging Test (Task 2):** Provide students with an executable program that crashes due to scope coupling. Task them with redesigning the code using isolated modules and stub-testing.
*   **Theory Examination (Task 8):** Design a 10-mark examination paper containing a structure chart diagram with missing arrows, requiring students to translate the chart into complete, syntax-compliant SCSA Pseudocode.
