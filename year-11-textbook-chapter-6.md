# Unit 1 — Chapter 6: Data Structures & Files

This chapter introduces the fundamental concepts of managing collections of data in active memory using **one-dimensional arrays (lists)** and storing data permanently in secondary storage using **sequential text files**. 

You will learn how to initialize arrays, traverse their elements, search for minimum and maximum values, accumulate sums, and interface with file streams to write, append, and read records. These computational patterns represent the backbone of **SCSA School-Based Assessment Projects (Assessment Task 1)** and practical examinations.

---

## Lesson 6.1: The 1D Array Structure

### Your Goal
Explain the memory structure of a one-dimensional array, declare arrays in Python, and access or modify specific elements using zero-indexed positions.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.4: Fundamental Data Types](./year-11-textbook-chapter-1.md#lesson-14-fundamental-data-types) (integers, floats, strings, Booleans).
*   [Lesson 2.1: Program Control Structures: Sequence](./year-11-textbook-chapter-2.md#lesson-21-program-control-structures-sequence).

### The Idea
Up to now, we have stored data in single variables. If we have 5 runners, we might write:
`runner1 = "Sarah"`, `runner2 = "Ben"`, and so on. But what if we have 500 runners? Creating 500 separate variables is practically impossible and makes processing data as a group extremely difficult.

To solve this, computer science uses a **Data Structure** called an array. 

**The Analogy:**
Imagine a long row of storage lockers at the **WA Junior Sports Carnival** equipment desk. 
*   The entire row is labeled **`lockers`**.
*   Each physical locker is an **element** of the array.
*   To keep things in order, the lockers are numbered consecutively starting at **`0`**. This number is the **index**.
*   If we put a shot-put ball in the first locker, we access it via `lockers[0]`.

In Python, we use a **list** to represent a one-dimensional array. While Python lists are dynamic (can change size), the SCSA syllabus focuses on the logical concepts of standard arrays, which historically have a fixed, static size in memory.

```
Index:       [0]        [1]        [2]        [3]        [4]
Element:  "Sarah"    "Ben"    "Kiran"    "Mei"     "Jack"
```

#### **SCSA Key Terms**
*   **Data Structure:** A specialized format for organizing, processing, retrieving, and storing data in a computer's memory.
*   **One-Dimensional (1D) Array:** A linear collection of elements, where each element is identified by at least one array index.
*   **Element:** An individual data item stored within an array.
*   **Index:** A numerical value representing the position of an element in an array (always starting at `0` in standard modern languages).
*   **Out of Bounds Error:** A runtime exception triggered when a program attempts to access an index that does not exist in the array (e.g., index `5` in a 5-element array).

---

### See It Worked
#### **The Scenario**
The high-jump coordinator wants to store the qualifying jump heights (in meters) of 5 athletes in a single data structure, access the first and last heights, modify one entry due to a recording error, and measure the list's size.

#### **The Solution Block (Python)**
```python
# 1. Declare and initialize a 1D array (list) of float values
heights = [1.45, 1.52, 1.48, 1.61, 1.55]

# 2. Access the first element (index 0) and the fourth element (index 3)
first_height = heights[0]
fourth_height = heights[3]

print("First jump height:", first_height, "m")
print("Fourth jump height:", fourth_height, "m")

# 3. Access the last element dynamically using a negative index
last_height = heights[-1]
print("Last jump height:", last_height, "m")

# 4. Modify an element (changing index 2 from 1.48 to 1.50)
print("\nOriginal heights:", heights)
heights[2] = 1.50
print("Corrected heights:", heights)

# 5. Determine the length (number of elements) in the array
num_jumps = len(heights)
print("Total records in array:", num_jumps)
```

#### **How the Logic Flows**
*   `heights = [1.45, 1.52, 1.48, 1.61, 1.55]` reserves a contiguous sequence of five memory slots under the variable name `heights`.
*   `heights[0]` retrieves the float value `1.45`.
*   `heights[2] = 1.50` locates index `2` (the third element) and replaces its existing contents (`1.48`) with `1.50`. This is an in-place modification.
*   `len(heights)` queries the array structure and returns an integer value of `5`.

---

### Try It with Help
#### **The Problem**
The volunteer coordinator has mapped out the names of four school sports houses in a 1D array. A school is renamed, and we need to correct their entry at index `2`. Fill in the missing code to initialize, access, and modify the array elements.

#### **Structural Hints**
*   The elements of the array are strings. Ensure they are enclosed in quotation marks.
*   Remember that index positions start counting at `0`.
*   Use the index position `2` to modify the third element of the array.

#### **Scaffolded Code Template**
```python
# Initialize the array of sports houses
houses = ["Blue", "Gold", "Red", "Green"]

# Access the first house in the array
first_house = houses[?]  # Replace ? with correct index
print("First house:", first_house)

# A correction is needed: "Red" house is renamed to "Scarlet"
# Modifying the element at index 2
houses[?] = "?"  # Replace ? with index and value

# Print the updated array to confirm the change
print("Updated sports houses:", houses)
print("Number of houses listed:", len(houses))
```

---

### Try It Yourself
#### **The Problem**
Write a complete, self-contained Python script that:
1.  Creates an array of 5 athlete names: `"Aisha"`, `"Caleb"`, `"Marcus"`, `"Chloe"`, and `"Daniel"`.
2.  Prints the name of the athlete in the middle of the array (the third element).
3.  Replaces the athlete at index `0` with the name `"Amara"`.
4.  Appends a 6th athlete, `"Eli"`, to the end of the array using Python's `.append()` method.
5.  Prints the total length of the array and the final state of the list.

---

### Check Your Reasoning
#### **The Answer**
```python
# 1. Create the initial list of 5 athletes
athletes = ["Aisha", "Caleb", "Marcus", "Chloe", "Daniel"]

# 2. Print the middle (third) element at index 2
print("Middle athlete:", athletes[2])

# 3. Replace index 0 with Amara
athletes[0] = "Amara"

# 4. Append Eli to the end of the list
athletes.append("Eli")

# 5. Print length and final list
print("Final size:", len(athletes))
print("Final list:", athletes)
```

#### **Common SCSA Student Errors**
1.  **Index Off-by-One:** Attempting to retrieve the third element by writing `athletes[3]`. Remember that `athletes[3]` actually returns the *fourth* element (`"Chloe"`), because index `0` is the first element.
2.  **Out of Bounds Crashing:** Trying to assign a value to a non-existent index (e.g., `athletes[5] = "Eli"` when the list only contains 5 elements). In Python, you must use `.append()` to expand a list dynamically; direct index assignment is only valid for indexes that already contain data.
3.  **Parentheses Confusion:** Writing `len[athletes]` with square brackets instead of round parentheses `len(athletes)`.

---

### Review and Connect
You have mastered the physical structure and indexing layout of 1D arrays. In the next lesson, we will explore how to write sequential loops that visit each of these index elements automatically, freeing us from writing manual index numbers.

---

## Lesson 6.2: Traversing and Printing

### Your Goal
Write and trace a loop that traverses (visits) every element in a 1D array to display its contents or perform checks.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 3.1: Definite Iteration (for loops)](./year-11-textbook-chapter-3.md#lesson-31-definite-iteration-for-loops).
*   [Lesson 6.1: The 1D Array Structure](#lesson-61-the-1d-array-structure).

### The Idea
To process elements in an array, our program must walk through them one by one. This process of visiting every element in a sequence is called **Traversal**.

**The Analogy:**
Imagine the carnival official walking down the row of equipment lockers. Starting at locker `0`, they open it, read the name written on the label inside, write it on a clipboard, close it, and move on to locker `1`. They repeat this process in sequence until they reach the end of the row.

In Python, we have two primary ways to write a loop to traverse an array:
1.  **Traversal by Element (Value Loop):** Simpler to write. Directly accesses the items inside.
    ```python
    for item in array:
        print(item)
    ```
2.  **Traversal by Index (Position Loop):** More powerful. Uses a counter to track the current index position, which is necessary if we need to modify values inside the array during the loop.
    ```python
    for i in range(len(array)):
        print(i, array[i])
    ```

#### **SCSA Key Terms**
*   **Traversal:** The process of accessing or visiting each element in a data structure exactly once.
*   **Loop Iterator:** The counter variable (typically `i` or `index`) that changes value with each pass of a loop to target sequential array positions.
*   **Sequential Processing:** Operating on data structures in a linear, predictable, element-by-element sequence.

---

### See It Worked
#### **The Scenario**
The track marshal needs to print a numbered list of the lanes and athlete names for a 100m sprint heat. The athlete names are stored in an array, and the lane assignments correspond to their index positions plus one (since lane numbers start at 1, but array indexes start at 0).

#### **The Solution Block (Python)**
```python
# Array of athletes assigned to lanes in order
runners = ["Aisha", "Caleb", "Marcus", "Chloe", "Daniel"]

print("--- 100m Sprint Lane Assignments ---")

# Traverse the array by index position using range()
for i in range(len(runners)):
    # Calculate lane number (index + 1)
    lane = i + 1
    # Retrieve athlete name at current index
    name = runners[i]
    
    print("Lane", lane, ":", name)
```

#### **How the Logic Flows**
*   `len(runners)` returns `5`. Thus, `range(5)` generates sequence values of `[0, 1, 2, 3, 4]`.
*   **First Pass:** `i` is `0`. `lane = 0 + 1 = 1`. `name = runners[0]` which is `"Aisha"`. Prints `Lane 1 : Aisha`.
*   **Second Pass:** `i` is `1`. `lane = 1 + 1 = 2`. `name = runners[1]` which is `"Caleb"`. Prints `Lane 2 : Caleb`.
*   The loop continues sequentially until `i` reaches `4` (the final index), printing `Lane 5 : Daniel`.

---

### Try It with Help
#### **The Problem**
The carnival results desk has an array containing recorded throwing distances for a shot-put round. They want a loop that prints out each throw distance, but flags an asterisk `(*)` next to any throw that exceeds the **15.0 meter** qualification limit. Complete the missing parts of the loop.

#### **Structural Hints**
*   Use a `for` loop to traverse the list of floats.
*   Inside the loop, use an `if-else` selection statement to check if the current value is greater than or equal to `15.0`.

#### **Scaffolded Code Template**
```python
throws = [14.2, 15.6, 13.8, 16.1, 14.9]

print("Shot-Put Qualifying Results:")

# Traverse the list using an element-by-element loop
for distance in ?:  # Replace ? with the array name
    if distance >= ?:  # Replace ? with threshold value
        print(distance, "m * [QUALIFIED]")
    else:
        print(distance, "m")
```

---

### Try It Yourself
#### **The Problem**
Write a Python script that:
1.  Defines an array of numbers representing school house points: `points = [120, 85, 150, 95]`.
2.  Defines a matching array of school house names: `names = ["Gold", "Blue", "Scarlet", "Green"]`.
3.  Uses a single `for` loop to traverse both arrays by index.
4.  For each pass, prints a combined sentence in the exact format: `"The Scarlet house has 150 points"`.

---

### Check Your Reasoning
#### **The Answer**
```python
points = [120, 85, 150, 95]
names = ["Gold", "Blue", "Scarlet", "Green"]

# Traverse by index since we must sync elements from two parallel lists
for i in range(len(names)):
    house_name = names[i]
    house_points = points[i]
    print("The " + house_name + " house has " + str(house_points) + " points")
```

#### **Common SCSA Student Errors**
1.  **Parallel Array Desynchronization:** Using two independent loops instead of a single, synchronized index loop. To read from parallel arrays (where elements at index `i` correspond to each other), you must use **Traversal by Index** (`i`) so the same index variable accesses both lists on the same loop iteration.
2.  **Using Element Traversals for Parallel Reading:** Writing `for name in names:` makes it very difficult to reference the matching numeric points array correctly.
3.  **Range Offset Mistakes:** Writing `range(len(names) + 1)`, which causes the index to run too far and trigger an `IndexError: list index out of range` on the final iteration.

---

### Review and Connect
Array traversal is the universal platform for almost all higher-level data algorithms. In the next lesson, we will build upon traversal loops to create an **Accumulator** algorithm, which sums values and calculates statistical averages across datasets.

---

## Lesson 6.3: Accumulating Data

### Your Goal
Implement and trace an accumulator algorithm to calculate the sum and mathematical average of numerical values stored in a 1D array.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 5.1: Arithmetic Operators and MOD](#lesson-51-arithmetic-operators-and-mod).
*   [Lesson 6.2: Traversing and Printing](#lesson-62-traversing-and-printing).

### The Idea
Often, we need to find total scores, aggregate point scores, or calculate average running splits. To achieve this, we use an **Accumulator Pattern**.

**The Analogy:**
Imagine a volunteer at the house point desk holding a hand-tally counter. 
*   Before starting, they clear the tally to read exactly **`0`**. This is our **initialization**.
*   They walk down a row of scorecards.
*   For each card they visit, they look at the score and add that exact number to their running total.
*   By the time they reach the end of the row, the counter contains the exact sum of all cards.

In computer science, an **Accumulator** is a variable that gathers value iteratively. Within an array traversal loop, we update the accumulator on each pass:
`total_points = total_points + current_item` (often abbreviated as `total_points += current_item`).

#### **SCSA Key Terms**
*   **Accumulator:** A variable used in a loop to accumulate a running total of values.
*   **Initialization:** The process of setting a starting value for a variable (crucial for accumulators to start at `0` before any looping begins).
*   **Average Calculation:** Dividing the accumulated sum by the total count of elements (retrieved via `len(array)`).

---

### See It Worked
#### **The Scenario**
The coordinator of the WA Junior Sports Carnival needs to sum up the house points scored by the Blue house across 4 different athletic events, then compute the average points scored per event.

#### **The Solution Block (Python)**
```python
# House points scored in each of the 4 events
blue_points = [85, 92, 78, 110]

# 1. Initialize the accumulator variable to 0
total_score = 0

# 2. Traverse the list, adding each score to the accumulator
for score in blue_points:
    # Add current element value to the running total
    total_score = total_score + score

# 3. Calculate the average by dividing sum by list size
num_events = len(blue_points)
average_score = total_score / num_events

print("--- Blue House Score Summary ---")
print("Total House Points:", total_score)
print("Average Points per Event:", average_score)
```

#### **How the Logic Flows**
Let's trace the state of the variables across each iteration of the traversal loop:

| Iteration | Current `score` | Math Operation | Resulting `total_score` |
| :---: | :---: | :--- | :---: |
| *(Start)* | — | *(Initialization)* | **`0`** |
| **Pass 1** | `85` | `0 + 85` | **`85`** |
| **Pass 2** | `92` | `85 + 92` | **`177`** |
| **Pass 3** | `78` | `177 + 78` | **`255`** |
| **Pass 4** | `110` | `255 + 110` | **`365`** |

*   After the loop completes, the total is `365`.
*   The divisor is calculated as `len(blue_points)` which equals `4`.
*   `365 / 4` evaluates to `91.25`. This is the calculated average.

---

### Try It with Help
#### **The Problem**
A timing official has collected split times (in seconds) for a runner over 5 laps: `[62.4, 60.1, 65.8, 61.2, 59.5]`. Complete the Python program below to calculate the total running time and the average lap time.

#### **Structural Hints**
*   Initialize your accumulator variable `total_time` to `0.0` (as we are dealing with floating-point split times).
*   Use a loop to traverse the list and add each lap time to `total_time`.
*   Calculate the average *after* the loop is completely finished.

#### **Scaffolded Code Template**
```python
laps = [62.4, 60.1, 65.8, 61.2, 59.5]

# Step 1: Initialize accumulator
total_time = ?  # Initialize to 0.0

# Step 2: Traverse and accumulate
for lap_time in laps:
    total_time = ? + ?  # Add lap_time to total_time

# Step 3: Calculate average
num_laps = len(laps)
avg_lap_time = ? / ?  # Divide sum by count

print("Total Track Time:", total_time, "seconds")
print("Average Lap Split:", avg_lap_time, "seconds")
```

---

### Try It Yourself
#### **The Problem**
Write a Python function named `calculate_team_average(scores)` that accepts an array of integer scores as its parameter. 
*   If the list is empty, the function should return `0.0` (to prevent division-by-zero crashes).
*   Otherwise, it should calculate, accumulate, and return the floating-point average of the scores.
*   Test your function with two input lists: `[12, 15, 10, 18]` and `[]`.

---

### Check Your Reasoning
#### **The Answer**
```python
def calculate_team_average(scores):
    # Guard clause: Check for empty array to prevent ZeroDivisionError
    if len(scores) == 0:
        return 0.0
    
    total = 0
    for score in scores:
        total += score  # Shorthand for total = total + score
        
    return total / len(scores)

# Test execution
print("Average 1:", calculate_team_average([12, 15, 10, 18]))  # Expected: 13.75
print("Average 2:", calculate_team_average([]))                # Expected: 0.0
```

#### **Common SCSA Student Errors**
1.  **Division-by-Zero Crashing:** Failing to check if the list is empty before dividing. If `len(scores)` is `0`, executing `total / 0` will crash the application with a `ZeroDivisionError`.
2.  **Accumulator Resetting inside the Loop:** Initializing the total variable *inside* the loop block (e.g., placing `total = 0` as the first line of the `for` loop). This resets the sum back to zero on every single pass, meaning the final total will simply equal the value of the very last element.
3.  **Premature Average Calculation:** Placing the division statement *inside* the loop. This calculates a series of intermediate averages unnecessarily, instead of summing all items first and dividing exactly once at the end.

---

### Review and Connect
The accumulator logic is standard for aggregating metrics. Now that we can find totals and averages, we will explore how to search through arrays to locate **extreme values** (the maximum and minimum elements) in Lesson 6.4.

---

## Lesson 6.4: Finding the Extremes

### Your Goal
Write and trace standard algorithms to locate the maximum or minimum value in a 1D array, and identify its corresponding index position.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 5.2: Relational Operators](#lesson-52-relational-operators) (specifically comparisons).
*   [Lesson 6.2: Traversing and Printing](#lesson-62-traversing-and-printing) (by index).

### The Idea
To find the gold-medal winning time or the longest javelin throw, our software must scan an array and extract the maximum or minimum value.

**The Analogy:**
Imagine looking at a row of closed lockers to find the heaviest equipment bag.
*   Since you cannot look at them all simultaneously, you open the first locker (`index 0`). You lift the bag and remember its weight: **"Heaviest so far is 12kg at locker 0."**
*   You walk to the second locker (`index 1`). If its bag weighs 15kg, you update your mental tally: **"Heaviest is now 15kg at locker 1."**
*   If the third locker has a bag weighing 10kg, you ignore it. The heaviest remains 15kg.
*   You repeat this process for every locker. By the end, you are holding the heaviest bag.

#### **The Golden Rule of SCSA Extremes**
Never initialize your tracking variable to a arbitrary number like `0` or `9999`. 
*   If you search for the maximum value in an array containing only negative temperature values `[-5, -12, -3]`, initializing `max_value = 0` will incorrectly report `0` as the maximum, even though `0` is not even in the array!
*   **Always initialize your tracking variable to the first element of the array (`array[0]`)** before beginning the loop.

#### **SCSA Key Terms**
*   **Extreme Value Tracking:** A logical pattern that compares sequential array elements against a running placeholder variable to find the highest or lowest value.
*   **Index Alignment:** Tracking the *index* of the extreme value so that matching details can be pulled from parallel arrays (e.g., getting the athlete name that goes with the winning score).

---

### See It Worked
#### **The Scenario**
The shot-put coordinator has an array containing recorded throwing distances in meters: `[14.2, 15.6, 13.8, 16.1, 14.9]`. They need to identify the **longest throw** in the set and report its value along with its matching array index.

#### **The Solution Block (Python)**
```python
throws = [14.2, 15.6, 13.8, 16.1, 14.9]

# 1. Initialize the running extreme to the first element (index 0)
max_throw = throws[0]
best_index = 0

# 2. Traverse the list starting from the second element (index 1)
for i in range(1, len(throws)):
    current_throw = throws[i]
    
    # 3. If we find a value greater than our current maximum, update
    if current_throw > max_throw:
        max_throw = current_throw
        best_index = i

print("--- Shot-Put Records ---")
print("Longest Throw Distance:", max_throw, "m")
print("Winning Record Position (Index):", best_index)
```

#### **How the Logic Flows**
Let's trace how the variables update as the algorithm scans the array:

*   **Initialization:** `max_throw = throws[0]` (`14.2`), `best_index = 0`.
*   **Pass 1 (`i = 1`):** `current_throw` is `15.6`. Is `15.6 > 14.2`? Yes. `max_throw` updates to `15.6`, `best_index` becomes `1`.
*   **Pass 2 (`i = 2`):** `current_throw` is `13.8`. Is `13.8 > 15.6`? No. No changes occur.
*   **Pass 3 (`i = 3`):** `current_throw` is `16.1`. Is `16.1 > 15.6`? Yes. `max_throw` updates to `16.1`, `best_index` becomes `3`.
*   **Pass 4 (`i = 4`):** `current_throw` is `14.9`. Is `14.9 > 16.1`? No. No changes occur.
*   **Final Output:** Longest Throw: `16.1 m`, located at Index `3`.

---

### Try It with Help
#### **The Problem**
The track coordinator wants to find the **fastest run time** (which is the **minimum value** in a list of splits) from a set of race times. Complete the missing comparison elements and initialization assignments in the Python script.

#### **Structural Hints**
*   Since we want the fastest (shortest) time, we initialize `min_time` to the first element in the array `times[0]`.
*   In our loop, we compare the current value to see if it is *less than* (`<`) our running `min_time`.
*   Track the index of the minimum time in `min_index`.

#### **Scaffolded Code Template**
```python
times = [12.8, 11.5, 13.1, 11.2, 11.8]

# Step 1: Initialize running minimum to the first element
min_time = ?  # Set to times[0]
min_index = 0

# Step 2: Traverse list from index 1 to the end
for i in range(1, len(times)):
    current_time = times[i]
    
    # Step 3: Check if current time is faster than minimum
    if current_time ? min_time:  # Replace ? with comparison operator
        min_time = ?  # Update min_time
        min_index = ? # Update min_index

print("Fastest time:", min_time, "seconds")
print("Fastest athlete index:", min_index)
```

---

### Try It Yourself
#### **The Problem**
Write a complete Python program that has:
1.  An array of athlete names: `names = ["Sarah", "Ben", "Kiran", "Mei", "Jack"]`.
2.  A parallel array of high-jump heights: `heights = [1.45, 1.52, 1.48, 1.61, 1.55]`.
3.  An algorithm that scans the heights array to find the maximum jump height and its corresponding index.
4.  Prints the name of the winning athlete and their jump height in the format: `"The winner is Mei with a jump of 1.61m"` (pulling the name from the parallel `names` list using the tracked index).

---

### Check Your Reasoning
#### **The Answer**
```python
names = ["Sarah", "Ben", "Kiran", "Mei", "Jack"]
heights = [1.45, 1.52, 1.48, 1.61, 1.55]

# 1. Initialize extreme tracker
max_height = heights[0]
winner_index = 0

# 2. Iterate by index across parallel arrays
for i in range(1, len(heights)):
    if heights[i] > max_height:
        max_height = heights[i]
        winner_index = i

# 3. Output result referencing parallel arrays
winning_name = names[winner_index]
print("The winner is " + winning_name + " with a jump of " + str(max_height) + "m")
```

#### **Common SCSA Student Errors**
1.  **Hardcoded Variable Initialization Failures:** Initializing `max_height = 0` or `min_height = 999`. SCSA markers explicitly check for this flaw. If an array contains values all below zero, or all above 999, the hardcoded starting values will corrupt the logic. **Always initialize to `array[0]`**.
2.  **Using Element Traversal for Parallel Alignment:** Writing `for height in heights:` makes it extremely difficult to update `winner_index` correctly. Traversing by index is mandatory for parallel data synchronization.
3.  **Off-by-One Range Omission:** Forgetting that lists are zero-indexed, or running loops beyond the final index.

---

### Review and Connect
Finding extremes is one of the most common exam questions in SCSA theory and practical tests. However, all data we have processed so far is stored in **volatile RAM**—which is completely wiped when our program exits. In the next lesson, we will explore how to write this data to permanent secondary storage using **sequential text files**.

---

## Lesson 6.5: Writing to Sequential Files

### Your Goal
Implement Python code to open, write data to, append data to, and safely close sequential text files.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.4: Fundamental Data Types](./year-11-textbook-chapter-1.md#lesson-14-fundamental-data-types) (specifically string parsing and escape characters like `\n`).
*   [Lesson 6.1: The 1D Array Structure](#lesson-61-the-1d-array-structure).

### The Idea
When we turn off a computer or close a Python program, all variables, arrays, and sports statistics in the random-access memory (RAM) disappear. To save athlete records permanently, we must store them in non-volatile secondary storage (such as a hard drive) using files.

The simplest file format is a **Sequential Text File**. In this format, data is written line-by-line in a sequential order, much like lines written in a physical notebook.

#### **The Three-Step File Lifecycle**
To interact with a file, a program must execute three clear logical steps:
1.  **Open:** Bind a file resource on disk to a program variable stream, specifying a mode:
    *   **Write Mode (`'w'`):** Creates a new file. *Warning:* If the file already exists, all existing content is erased.
    *   **Append Mode (`'a'`):** Opens an existing file and writes new data to the end without erasing old data.
2.  **Process (Write/Append):** Send string structures to the file stream.
3.  **Close:** Release the lock on the file. If you forget to close a file, data can be lost or remain locked in memory!

#### **SCSA Key Terms**
*   **Sequential Text File:** A file where characters are stored as a continuous sequence of lines, accessed in linear order.
*   **File Stream Mode:** A system permission parameter (`'w'` for write, `'a'` for append, `'r'` for read) defining the operation on the file resource.
*   **Newline Character (`\n`):** A special control character that tells the operating system to start a new line of text in the file.
*   **Resource Leak:** A system failure where a program opens a system resource (like a file) but fails to close it, consuming system memory.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival registration manager wants to write the names of three newly registered schools to a persistent text file named `registered_schools.txt`.

#### **The Solution Block (Python)**
```python
# 1. Open a text file in Write Mode ('w')
# This creates 'registered_schools.txt' on the disk.
file_stream = open("registered_schools.txt", "w")

# 2. Write three lines of text
# We must append '\n' explicitly to force each entry onto a new line!
file_stream.write("Scarlet House\n")
file_stream.write("Gold House\n")
file_stream.write("Blue House\n")

# 3. Close the file stream to release the disk lock and flush memory
file_stream.close()

print("File successfully created and written.")
```

#### **How the Logic Flows**
*   `open("registered_schools.txt", "w")` creates a blank file on the disk named `registered_schools.txt` and links it to our program variable `file_stream`.
*   `file_stream.write("Scarlet House\n")` writes the characters `'S', 'c', 'a', 'r', 'l', 'e', 't', ' ', 'H', 'o', 'u', 's', 'e'` followed by the special newline control signal. This places the blinking cursor on the next line down in the text file.
*   `file_stream.close()` informs the operating system that we are done. The data is safely committed to the disk storage sector.

---

### Try It with Help
#### **The Problem**
A timing volunteer wants to append a new record to the end of the existing timing file `registered_schools.txt` without erasing the school names already saved inside. Complete the program below by setting the correct file stream mode and writing the new entry.

#### **Structural Hints**
*   To add data to an existing file without wiping it, use **Append Mode (`'a'`)**.
*   Remember to add a newline character (`
`) to ensure the next entry added in the future starts on its own line.
*   Ensure the file is closed at the end of the script.

#### **Scaffolded Code Template**
```python
new_entry = "Green House"

# Step 1: Open the file in Append Mode
# Fill in the filename and correct mode character
file_stream = open("registered_schools.txt", "?")  # Use append mode

# Step 2: Write the new entry with a newline character
file_stream.write(new_entry + "?")  # Write string plus newline

# Step 3: Close the file stream safely
file_stream.?()  # Close the stream

print("New house appended successfully.")
```

---

### Try It Yourself
#### **The Problem**
Write a complete Python script that:
1.  Declares an array of 4 athlete registration numbers: `reg_numbers = [1042, 3081, 2099, 4012]`.
2.  Opens a file named `athlete_IDs.txt` in write mode (`'w'`).
3.  Uses a `for` loop traversal to write each registration number from the array to the text file on a new line.
    *   *Hint:* Since `write()` only accepts string types, you must cast the integer values using `str()` before writing.
4.  Safely closes the file stream when finished.

---

### Check Your Reasoning
#### **The Answer**
```python
reg_numbers = [1042, 3081, 2099, 4012]

# 1. Open file stream
file_stream = open("athlete_IDs.txt", "w")

# 2. Traverse and write
for num in reg_numbers:
    # Cast integer to string and add newline delimiter
    file_stream.write(str(num) + "\n")

# 3. Close the stream
file_stream.close()

print("Verification complete. 4 ID records written.")
```

#### **Common SCSA Student Errors**
1.  **Overwriting Existing Files Unintentionally:** Opening a file in `'w'` mode when you meant to add new data in `'a'` mode. A single open with `'w'` instantly wipes all prior contents of that file.
2.  **Type Errors (Writing Integers directly):** Writing `file_stream.write(num)` where `num` is an integer. Python's `file.write()` function *only* accepts strings. You must convert it using `str(num)`.
3.  **Forgetting Newlines:** Omitting the `+ "\n"` part when writing. This causes the file to become a single, long sequence of digits (e.g., `1042308120994012`), which is impossible to read correctly line-by-line later on.

---

### Review and Connect
You can now save data from RAM into persistent disk storage. In the final lesson of this chapter, we will learn the matching reverse operation: opening a file, reading its lines, stripping away formatting artifacts, and loading them back into 1D arrays for computation.

---

## Lesson 6.6: Reading and Processing Files

### Your Goal
Read text records from sequential files, parse them (cleaning newlines and casting data types), and load them into active 1D arrays for computational processing.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 6.1: The 1D Array Structure](#lesson-61-the-1d-array-structure).
*   [Lesson 6.5: Writing to Sequential Files](#lesson-65-writing-to-sequential-files).

### The Idea
Saving data to files is only useful if we can read it back. To run calculations or search lists, we must load the sequential lines of a file back into the fast, volatile RAM as arrays.

**The Analogy:**
Imagine the carnival coordinator opening a locked document file cabinet. They take out a sheet of paper containing student names, read the names line-by-line, and write them onto individual name tags laid out in order on a table (loading them into an active array) so they can easily sort or search through them.

In Python, we read a file line-by-line using **Read Mode (`'r'`)** and a sequential loop:
```python
file_stream = open("filename.txt", "r")
for line in file_stream:
    # Process each line
```

#### **The Newline Cleanup Trap (`.strip()`)**
When a program reads a line from a file, it reads the text *plus* the hidden newline control character `\n` at the end of that line!
*   If your file contains the name `"Aisha\n"`, reading it yields `"Aisha\n"`.
*   If we try to compare `if name == "Aisha"`, it will evaluate to `False` due to the hidden `\n`!
*   We must use Python's `.strip()` method to clean off these hidden whitespaces and newline characters before adding them to our memory structures.

---

### See It Worked
#### **The Scenario**
The sports scoring desk has a text file named `athlete_names.txt` containing athlete names written line-by-line. They need to read these names, strip out any trailing newline characters, append them into a blank 1D Python array in RAM, and display the final loaded list.

#### **The Solution Block (Python)**
```python
# Create a dummy names file first for simulation
temp_file = open("athlete_names.txt", "w")
temp_file.write("Sarah\nBen\nKiran\nMei\n")
temp_file.close()


# 1. Initialize a blank array to hold the loaded names
loaded_athletes = []

# 2. Open the sequential file in Read Mode ('r')
file_stream = open("athlete_names.txt", "r")

# 3. Sequential traversal: loop through each line of the file
for line in file_stream:
    # Strip away trailing newlines (
) and spaces
    clean_name = line.strip()
    
    # Append the clean string to our active memory array
    loaded_athletes.append(clean_name)

# 4. Close the file stream
file_stream.close()

print("--- Data Loading Phase Complete ---")
print("Array in RAM:", loaded_athletes)
print("Loaded Records Count:", len(loaded_athletes))
```

#### **How the Logic Flows**
*   `loaded_athletes` starts as an empty array: `[]`.
*   `open("athlete_names.txt", "r")` checks if the file exists and positions a read cursor at the very top of the document.
*   **Line 1:** Read `"Sarah\n"`. `line.strip()` trims off the `\n`, leaving the string `"Sarah"`. This is appended to the array: `["Sarah"]`.
*   **Line 2:** Read `"Ben\n"`. Strips to `"Ben"`, appends to array: `["Sarah", "Ben"]`.
*   This pattern continues until the end of the file (EOF) is reached.
*   `file_stream.close()` closes the read channel.

---

### Try It with Help
#### **The Problem**
The timing desk has a text file named `lap_splits.txt` containing numerical decimal values of race times on separate lines. They need to load these values into a numerical array. Complete the missing parsing steps to convert the text lines into **floats** before appending.

#### **Structural Hints**
*   Use `open()` with Read Mode (`'r'`).
*   Read each line, strip the newline character, and then convert (cast) the string to a `float` so we can do mathematical calculations with it.
*   Append the float value to the `loaded_splits` list.

#### **Scaffolded Code Template**
```python
# Create dummy split times file first for simulation
temp_file = open("lap_splits.txt", "w")
temp_file.write("12.4\n11.8\n13.1\n11.5\n")
temp_file.close()


loaded_splits = []

# Step 1: Open file in Read Mode
file_stream = open("lap_splits.txt", "?")  # Use read mode

# Step 2: Loop through file lines sequentially
for line in file_stream:
    # Clean the line text
    clean_line = line.?()  # Use strip to clean whitespace
    
    # Cast string value to a float
    numeric_time = ?(clean_line)  # Cast to float
    
    # Append to array in RAM
    loaded_splits.append(?)

# Step 3: Close the stream
file_stream.close()

print("Array in RAM:", loaded_splits)
```

---

### Try It Yourself
#### **The Problem**
Write a Python script that reads integer point totals from a sequential file named `house_points.txt` and performs calculations.
*   *Setup:* Create a dummy file `house_points.txt` first containing:
    ```
    120
    85
    150
    95
    ```
*   Your program must read each line, strip it, and cast it to an **integer** value.
*   Load these integers into a 1D array in RAM.
*   Using the **accumulator** logic from Lesson 6.3, compute and print the total house points and the average points per event from the loaded array.

---

### Check Your Reasoning
#### **The Answer**
```python
# Setup dummy file
temp_file = open("house_points.txt", "w")
temp_file.write("120\n85\n150\n95\n")
temp_file.close()

# 1. Read and load phases
points_array = []
file_stream = open("house_points.txt", "r")

for line in file_stream:
    # Strip and cast to integer
    clean_val = int(line.strip())
    points_array.append(clean_val)

file_stream.close()

# 2. Computational processing phase (using RAM array)
total_points = 0
for score in points_array:
    total_points += score

average_points = total_points / len(points_array)

print("Points Array in RAM:", points_array)
print("Calculated Total Sum:", total_points)
print("Calculated Class Average:", average_points)
```

#### **Common SCSA Student Errors**
1.  **Forgetting to Typecast String Lines:** Attempting to sum the lines directly (e.g., `total_points += line`). This causes a `TypeError` because data read from files is *always* stored as strings. Trying to add strings mathematically (e.g., `"120" + "85"`) will concatenate them into `"12085"`.
2.  **Processing Inside the File Loop Excessively:** It is good architectural practice to **load the data first, close the file, and then perform calculations** on the array in RAM. This keeps file lock times minimal, protecting data integrity.
3.  **Forgetting to call `.strip()`:** Reading lines and forgetting to strip trailing spaces/newline, leading to casting errors when converting to integers or floats (e.g., `int("120\n")` may crash depending on the language parser environment, though Python's parser is forgiving, other SCSA assessed environments are not).

---

## Chapter 6 Teacher Notes & SCSA Assessment Mapping

### **WA Syllabus Direct Mapping**
*   **Unit 1 Practical Concepts:** Data types used in solutions, including integer, float, string, Boolean. One-dimensional arrays (data structures). Array operations: loading, printing, summing, finding the minimum or maximum value.
*   **Unit 1 File Concepts:** Sequential text files: reading, writing, appending, closing.

### **Misconception Busters**
1.  **"Lists are Arrays"**: Remind students that while Python lists are dynamic, SCSA theory questions assess **static-size arrays**. Emphasize that in an array, all elements are traditionally of the *same* data type and contiguous in memory.
2.  **File Operations vs. RAM Operations**: Students often confuse changing a variable in Python with changing it in the file. Explain that `file.write()` is a one-way export; updating `points_array[2] = 200` in Python has zero effect on the text file until the program explicitly writes the entire list back to the disk.
3.  **The Trailing Newline Pitfall**: Emphasize that every write operation should have `\n` to separate records, but every read operation must use `.strip()` to clean them.

### **Classroom Discussion Prompts**
*   *"Why does SCSA enforce closing files at the end of a program? What would happen if a system ran 10,000 file-open procedures without closing them?"* (Focus on **Resource Leaks** and locking out other users or applications).
*   *"When compiling sports result data, why might we load data into an array first before calculating averages instead of calculating the average directly line-by-line while reading?"* (Focus on separating **I/O operations** from **business logic** and minimizing disk activity).

### **Interlocking with SCSA School-Based Assessments**
*   **Assessment Task 1 (Programming Project - 20%):** Students must use arrays to hold game states (e.g., a leaderboard or grid coordinates) and save game states permanently to a sequential text file so players can resume later.
*   **Assessment Task 2 (Practical Debugging Test - 5%):** Students will be given a file with common file processing bugs (e.g., missing `.close()`, missing cast to `int`/`float`, or incorrect array index counters) and must correct them under test conditions using trace tables.
