# Year 11 CS ATAR — Interactive Quizzes

Welcome to the **Interactive Quiz Center**! Test your understanding of each lesson mapped to the Western Australian SCSA syllabus. 

These self-correcting quizzes provide instant feedback, detailed scoring, and explanations designed to help you master syllabus concepts and identify common exam pitfalls.

Select a chapter from the menu below to start testing:

---

## 🧭 Quick Jump
* **Unit 1: Software & Networks**
  * [Chapter 1: Foundations Quiz](#chapter-1-programming-foundations-quiz)
  * [Chapter 2: Control Structures Quiz](#chapter-2-control-structures-quiz)
  * [Chapter 3: Iteration Quiz](#chapter-3-iteration-loops-quiz)
  * [Chapter 4: Modular Programming Quiz](#chapter-4-modular-programming-quiz)
  * [Chapter 5: Operators & Logic Quiz](#chapter-5-operators-logical-precedence-quiz)
  * [Chapter 6: Lists & Files Quiz](#chapter-6-lists-file-io-quiz)
  * [Chapter 7: Algorithm Development Quiz](#chapter-7-algorithmic-design-quiz)
  * [Chapter 8: Technology Process Quiz](#chapter-8-project-development-lifecycles-quiz)
  * [Chapter 9: Networks & Topologies Quiz](#chapter-9-network-foundations-quiz)
* **Unit 2: Databases & Cybersecurity**
  * [Chapter 10: Ethics & Privacy Quiz](#chapter-10-ethics-law-security-frameworks-quiz)
  * [Chapter 11: Cyber Threats Quiz](#chapter-11-cyber-threats-malware-quiz)
  * [Chapter 12: Cryptography Quiz](#chapter-12-defensive-security-cryptography-quiz)
  * [Chapter 13: Database Foundations Quiz](#chapter-13-database-foundations-quiz)
  * [Chapter 14: Relational Modelling Quiz](#chapter-14-database-design-modelling-quiz)
  * [Chapter 15: Normalisation Quiz](#chapter-15-database-normalisation-integrity-quiz)
  * [Chapter 16: SQL & Backups Quiz](#chapter-16-sql-implementation-quiz)

---

## Unit 1: Design & Development of Programming & Networking Solutions

### Chapter 1: Programming Foundations Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Byte Character Encoding</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Under the standard 8-bit ASCII mapping, the character 'A' is represented by decimal 65. What is the correct binary byte representation of the character 'D'?</p>
  
  <form id="quiz-ch1" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch1" value="A" style="accent-color: #1e3a8a;"> <code>01000010</code>
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch1" value="B" style="accent-color: #1e3a8a;"> <code>01000011</code>
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch1" value="C" style="accent-color: #1e3a8a;"> <code>01000100</code>
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch1" value="D" style="accent-color: #1e3a8a;"> <code>01000101</code>
    </label>
    
    <button type="button" onclick="checkAnswerCh1()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch1" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh1() {
    var selected = document.querySelector('input[name="qch1"]:checked');
    var feedback = document.getElementById('feedback-ch1');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "C") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> Since 'A' is 65, 'D' maps to decimal 68. Under our place-value binary columns: $68 = 64 + 4$, which corresponds directly to <code>01000100</code>.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Let's recalculate: 'A' (65) -> 'B' (66) -> 'C' (67) -> 'D' (68). Convert 68 into binary using powers of 2 columns ($68 - 64 = 4$, then $4 - 4 = 0$), which makes the 64 and 4 columns equal to 1.";
    }
  }
</script>

---

### Chapter 2: Control Structures Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Sequential execution paths</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Consider a script where <code>x = 10</code>. If we execute the following logic sequence:
  <pre style="background: #1e293b; color: #f8fafc; padding: 10px; border-radius: 4px;">IF x >= 10 THEN
  x = x + 5
ENDIF
IF x > 12 THEN
  x = x * 2
ENDIF</pre>
  What is the final value of <code>x</code>?</p>
  
  <form id="quiz-ch2" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch2" value="A" style="accent-color: #1e3a8a;"> 10
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch2" value="B" style="accent-color: #1e3a8a;"> 15
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch2" value="C" style="accent-color: #1e3a8a;"> 20
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch2" value="D" style="accent-color: #1e3a8a;"> 30
    </label>
    
    <button type="button" onclick="checkAnswerCh2()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch2" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh2() {
    var selected = document.querySelector('input[name="qch2"]:checked');
    var feedback = document.getElementById('feedback-ch2');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "D") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> Step 1: <code>x = 10</code>. Step 2: The first IF condition (<code>x >= 10</code>) is TRUE, so <code>x</code> increases to 15. Step 3: The second sequential IF condition (<code>x > 12</code>) is evaluated immediately using the *updated* value 15. This is also TRUE, so <code>x</code> is multiplied by 2, resulting in 30.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Remember that sequential IF structures execute one after the other. The output of the first statement becomes the input to the next!";
    }
  }
</script>

---

### Chapter 3: Iteration Loops Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Definite Loop Bounds</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">How many times will the body of the following loop execute?
  <pre style="background: #1e293b; color: #f8fafc; padding: 10px; border-radius: 4px;">FOR i FROM 2 TO 8 STEP 2
  OUTPUT i
ENDFOR</pre></p>
  
  <form id="quiz-ch3" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch3" value="A" style="accent-color: #1e3a8a;"> 3 times
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch3" value="B" style="accent-color: #1e3a8a;"> 4 times
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch3" value="C" style="accent-color: #1e3a8a;"> 6 times
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch3" value="D" style="accent-color: #1e3a8a;"> 7 times
    </label>
    
    <button type="button" onclick="checkAnswerCh3()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch3" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh3() {
    var selected = document.querySelector('input[name="qch3"]:checked');
    var feedback = document.getElementById('feedback-ch3');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "B") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> The counter <code>i</code> takes the values <code>2</code>, <code>4</code>, <code>6</code>, and <code>8</code>. Because the upper limit of an SCSA FOR loop is inclusive, the loop executes exactly 4 times.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Let's count the loop steps manually: Iteration 1: <code>i = 2</code>, Iteration 2: <code>i = 4</code>, Iteration 3: <code>i = 6</code>, Iteration 4: <code>i = 8</code>. Once <code>i</code> steps to 10, the loop boundaries are exceeded and execution halts.";
    }
  }
</script>

---

### Chapter 4: Modular Programming Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Global vs Local variable scopes</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Review the following pseudocode sequence:
  <pre style="background: #1e293b; color: #f8fafc; padding: 10px; border-radius: 4px;">DECLARE score : INTEGER
score <- 10

BEGIN SUBROUTINE updateScore()
  DECLARE score : INTEGER
  score <- 20
END SUBROUTINE

updateScore()
OUTPUT score</pre>
  What does the program output?</p>
  
  <form id="quiz-ch4" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch4" value="A" style="accent-color: #1e3a8a;"> 10
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch4" value="B" style="accent-color: #1e3a8a;"> 20
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch4" value="C" style="accent-color: #1e3a8a;"> None
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch4" value="D" style="accent-color: #1e3a8a;"> Crashes with compilation error
    </label>
    
    <button type="button" onclick="checkAnswerCh4()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch4" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh4() {
    var selected = document.querySelector('input[name="qch4"]:checked');
    var feedback = document.getElementById('feedback-ch4');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "A") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> This highlights the concept of **variable shadowing**. Inside the subroutine, declaring <code>score</code> creates a completely separate, local variable. When <code>score <- 20</code> is run, it only updates the local variable, leaving the global <code>score</code> unchanged at 10.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Declaring the variable inside the subroutine creates a distinct local variable with limited scope. The global variable's value of 10 remains unaffected.";
    }
  }
</script>

---

### Chapter 5: Operators & Logical Precedence Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Operator Precedence Evaluation</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">What is the Boolean result of the following logical expression?
  <pre style="background: #1e293b; color: #f8fafc; padding: 10px; border-radius: 4px;">True OR False AND NOT True</pre></p>
  
  <form id="quiz-ch5" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch5" value="A" style="accent-color: #1e3a8a;"> True
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch5" value="B" style="accent-color: #1e3a8a;"> False
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch5" value="C" style="accent-color: #1e3a8a;"> Error
    </label>
    
    <button type="button" onclick="checkAnswerCh5()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch5" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh5() {
    var selected = document.querySelector('input[name="qch5"]:checked');
    var feedback = document.getElementById('feedback-ch5');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "A") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> Under the standard order of logical precedence: 1. `NOT` (evaluates `NOT True` to `False`), 2. `AND` (evaluates `False AND False` to `False`), 3. `OR` (evaluates `True OR False` to **`True`**).";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Let's trace using precedence rules: Step 1: `NOT True` becomes `False`. Step 2: `False AND False` becomes `False`. Step 3: `True OR False` evaluates to `True`. Remember, `NOT` runs first, followed by `AND`, then `OR`.";
    }
  }
</script>

---

### Chapter 6: Lists & File I/O Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: 1D Array Off-By-One Errors</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Consider a 1-D array named <code>times</code> containing exactly 5 competitor sprint times. Which line of code executes a complete traversal without throwing an index bounds error?</p>
  
  <form id="quiz-ch6" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch6" value="A" style="accent-color: #1e3a8a;"> <code>FOR i FROM 1 TO 5 OUTPUT times[i] ENDFOR</code>
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch6" value="B" style="accent-color: #1e3a8a;"> <code>FOR i FROM 0 TO 5 OUTPUT times[i] ENDFOR</code>
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch6" value="C" style="accent-color: #1e3a8a;"> <code>FOR i FROM 0 TO 4 OUTPUT times[i] ENDFOR</code>
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch6" value="D" style="accent-color: #1e3a8a;"> <code>FOR i FROM 0 TO length(times) OUTPUT times[i] ENDFOR</code>
    </label>
    
    <button type="button" onclick="checkAnswerCh6()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch6" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh6() {
    var selected = document.querySelector('input[name="qch6"]:checked');
    var feedback = document.getElementById('feedback-ch6');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "C") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> In computer science, arrays use **zero-based indexing**. For an array with 5 elements, the valid indices are <code>0, 1, 2, 3, 4</code>. Traversing from 0 to 4 covers every element perfectly without throwing an out-of-bounds crash.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Since arrays start at index <code>0</code>, an array with 5 elements does not contain an element at index <code>5</code>. Stepping to 5 throws an index crash!";
    }
  }
</script>

---

### Chapter 7: Algorithmic Design Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Modular Flowcharts</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">In a standard system flowchart, which symbol is used to represent a predefined call to a modular sub-process (such as a separate subroutine)?</p>
  
  <form id="quiz-ch7" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch7" value="A" style="accent-color: #1e3a8a;"> Ovals (Terminator)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch7" value="B" style="accent-color: #1e3a8a;"> Rhombus (Decision block)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch7" value="C" style="accent-color: #1e3a8a;"> Plain Rectangle (Process block)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch7" value="D" style="accent-color: #1e3a8a;"> Rectangle with double vertical borders (Predefined Process)
    </label>
    
    <button type="button" onclick="checkAnswerCh7()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch7" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh7() {
    var selected = document.querySelector('input[name="qch7"]:checked');
    var feedback = document.getElementById('feedback-ch7');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "D") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> A rectangle with double vertical borders denotes a **Predefined Process**. It lets system architects draw complex algorithms cleanly by hiding sub-process details inside a separate diagram.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> An oval is for start/end points, a rhombus is for branching logic, and a standard rectangle is for a basic process. To show a modular call, use a rectangle with double vertical side borders.";
    }
  }
</script>

---

### Chapter 8: Project Development Lifecycles Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: SDLC Implementation Strategies</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">A school wants to replace its old gradebook software with a brand-new cloud portal. If they disable the old portal completely on Friday night and boot up the new software on Monday morning, which implementation strategy is being used?</p>
  
  <form id="quiz-ch8" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch8" value="A" style="accent-color: #1e3a8a;"> Parallel
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch8" value="B" style="accent-color: #1e3a8a;"> Direct cut-over (Abrupt)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch8" value="C" style="accent-color: #1e3a8a;"> Phased
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch8" value="D" style="accent-color: #1e3a8a;"> Pilot
    </label>
    
    <button type="button" onclick="checkAnswerCh8()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch8" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh8() {
    var selected = document.querySelector('input[name="qch8"]:checked');
    var feedback = document.getElementById('feedback-ch8');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "B") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> This represents a **Direct Cut-Over** (also known as abrupt cut-over). It is high-risk because there is no fallback safety net if the new system fails, but it is fast and minimizes data synchronization costs.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Parallel runs both systems side-by-side, phased rolls it out feature-by-feature, and pilot runs the whole system in one department first. Replacing it instantly over a weekend is a Direct Cut-Over.";
    }
  }
</script>

---

### Chapter 9: Network Foundations Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Subnet Host Calculations</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Under the IPv4 classless routing structure, how many usable host IP addresses are available within a subnet masked with <code>/24</code>?</p>
  
  <form id="quiz-ch9" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch9" value="A" style="accent-color: #1e3a8a;"> 256
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch9" value="B" style="accent-color: #1e3a8a;"> 255
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch9" value="C" style="accent-color: #1e3a8a;"> 254
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch9" value="D" style="accent-color: #1e3a8a;"> 128
    </label>
    
    <button type="button" onclick="checkAnswerCh9()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch9" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh9() {
    var selected = document.querySelector('input[name="qch9"]:checked');
    var feedback = document.getElementById('feedback-ch9');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "C") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> While a `/24` mask yields $2^8 = 256$ total binary combinations, we **must subtract exactly 2 addresses**: the first address (network identifier) and the last address (broadcast address). This leaves 254 assignable host IPs.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> High-frequency exam error! Although there are 256 addresses total, you cannot assign the network address (typically `.0`) or the broadcast address (typically `.255`) to devices. Always subtract 2!";
    }
  }
</script>

---

## Unit 2: Design & Development of Database Solutions & Cyber Security Considerations

### Chapter 10: Ethics, Law & Security Frameworks Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Privacy Act & APP 11 Compliance</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Under the Australian Privacy Principles (APPs), which specific guideline dictates that software developers and organizations must take active, reasonable steps to protect personal, sensitive customer data from breach or unauthorized modification?</p>
  
  <form id="quiz-ch10" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch10" value="A" style="accent-color: #1e3a8a;"> APP 1 (Open management)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch10" value="B" style="accent-color: #1e3a8a;"> APP 5 (Notification of collection)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch10" value="C" style="accent-color: #1e3a8a;"> APP 11 (Security of personal information)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch10" value="D" style="accent-color: #1e3a8a;"> APP 13 (Correction of records)
    </label>
    
    <button type="button" onclick="checkAnswerCh10()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch10" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh10() {
    var selected = document.querySelector('input[name="qch10"]:checked');
    var feedback = document.getElementById('feedback-ch10');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "C") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> **APP 11 (Security of personal information)** explicitly mandates that organisations protect data from misuse, loss, interference, and unauthorised access or modification. This is the most critical principle for database designers.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> While APP 1 covers general management policies and APP 5 concerns data disclosure, it is **APP 11** that legally forces database developers to implement active technical protections like passwords and database encryption.";
    }
  }
</script>

---

### Chapter 11: Cyber Threats & Malware Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Malware propagation vectors</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">What is the primary operational difference between a computer virus and a computer worm?</p>
  
  <form id="quiz-ch11" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch11" value="A" style="accent-color: #1e3a8a;"> A virus is more destructive than a worm.
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch11" value="B" style="accent-color: #1e3a8a;"> A virus self-replicates across networks automatically, whereas a worm requires a host file.
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch11" value="C" style="accent-color: #1e3a8a;"> A virus requires human/host file activation to propagate, whereas a worm self-replicates across network connections independently.
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch11" value="D" style="accent-color: #1e3a8a;"> A virus is software, whereas a worm is a physical hardware exploit.
    </label>
    
    <button type="button" onclick="checkAnswerCh11()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch11" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh11() {
    var selected = document.querySelector('input[name="qch11"]:checked');
    var feedback = document.getElementById('feedback-ch11');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "C") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> This is a core SCSA classification standard. A **virus** requires a human host action to run/spread (such as double-clicking an infected email attachment), whereas a **worm** replicates across open network nodes automatically without any human interaction.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Don't make the common mistake of reversing the definitions! Viruses are host-dependent and require activation, while worms are network-dependent and self-propagate.";
    }
  }
</script>

---

### Chapter 12: Defensive Security & Cryptography Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Substitution Cipher Modulo</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Under a Caesar rotation cipher with a key shift of <code>+5</code>, what is the encrypted ciphertext character corresponding to the plaintext letter <code>'Y'</code> (Index 24)?</p>
  
  <form id="quiz-ch12" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch12" value="A" style="accent-color: #1e3a8a;"> <code>'C'</code> (Index 2)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch12" value="B" style="accent-color: #1e3a8a;"> <code>'D'</code> (Index 3)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch12" value="C" style="accent-color: #1e3a8a;"> <code>'E'</code> (Index 4)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch12" value="D" style="accent-color: #1e3a8a;"> <code>'F'</code> (Index 5)
    </label>
    
    <button type="button" onclick="checkAnswerCh12()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch12" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh12() {
    var selected = document.querySelector('input[name="qch12"]:checked');
    var feedback = document.getElementById('feedback-ch12');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "B") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> The math works as follows: $(24 + 5) \pmod{26} = 29 \pmod{26} = 3$. Index 3 corresponds directly to the character **'D'** (where A=0, B=1, C=2, D=3).";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Recall how standard modulo-26 wrapping handles boundaries: $(24 + 5) = 29$. Since 29 is greater than 25, wrap it back around by subtracting 26: $29 - 26 = 3$. This maps directly to index 3 ('D').";
    }
  }
</script>

---

### Chapter 13: Database Foundations Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Database structural hierarchy</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Which option correctly displays the hierarchical organization of data inside an RDBMS from smallest/lowest to largest/highest entity block?</p>
  
  <form id="quiz-ch13" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch13" value="A" style="accent-color: #1e3a8a;"> Database &rarr; Table &rarr; Field &rarr; Record
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch13" value="B" style="accent-color: #1e3a8a;"> Field/Attribute &rarr; Record/Row &rarr; Table/Entity &rarr; Database
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch13" value="C" style="accent-color: #1e3a8a;"> Table &rarr; Database &rarr; Record &rarr; Field
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch13" value="D" style="accent-color: #1e3a8a;"> Record &rarr; Field &rarr; Table &rarr; Database
    </label>
    
    <button type="button" onclick="checkAnswerCh13()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch13" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh13() {
    var selected = document.querySelector('input[name="qch13"]:checked');
    var feedback = document.getElementById('feedback-ch13');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "B") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> In RDBMS, the structural hierarchy of data begins with the **Field/Attribute** (the raw column datum), which clusters together to form a **Record/Row**, which stacks to compile a **Table/Entity**, all governed under a unified **Database**.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Let's look at the structure: Attributes (fields) represent individual data fields. Combining them horizontally creates a single transaction row (record). Placing multiple rows together forms an entity (table), and all tables live within the database.";
    }
  }
</script>

---

### Chapter 14: Database Design & Modelling Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: ERD Crow's Foot cardinalities</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">You are mapping a database ERD for a local school where each class has exactly one teacher, but a teacher can run multiple classes. What is the correct cardinality connector line touching the 'Class' entity box?</p>
  
  <form id="quiz-ch14" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch14" value="A" style="accent-color: #1e3a8a;"> One and Only One (double lines: <code>-||-</code>)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch14" value="B" style="accent-color: #1e3a8a;"> Zero or One (circle and line: <code>-o|-</code>)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch14" value="C" style="accent-color: #1e3a8a;"> One or Many (line and three-prong fork: <code>-|-&lt;</code>)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch14" value="D" style="accent-color: #1e3a8a;"> Zero or Many (circle and three-prong fork: <code>-o-&lt;</code>)
    </label>
    
    <button type="button" onclick="checkAnswerCh14()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch14" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh14() {
    var selected = document.querySelector('input[name="qch14"]:checked');
    var feedback = document.getElementById('feedback-ch14');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "C") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> In ERDs, we read the cardinality *away* from the starting point. Since one teacher can run *one or many* classes, the **One or Many** connector (line + split three-prong crow's foot) must touch the 'Class' entity box.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Ensure you aren't drawing the relationship backward! The double lines (One and Only One) represent how 'Class' links to 'Teacher'. But the 'Teacher' can manage *one-or-many* classes, so the crow's foot touches 'Class'.";
    }
  }
</script>

---

### Chapter 15: Database Normalisation & Integrity Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Functional Dependencies</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">During database normalisation, what type of dependency has been successfully resolved when we transition a schema from 2NF to 3NF?</p>
  
  <form id="quiz-ch15" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch15" value="A" style="accent-color: #1e3a8a;"> Repeating multi-value groups
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch15" value="B" style="accent-color: #1e3a8a;"> Partial dependency (non-key columns depending on a portion of a composite key)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch15" value="C" style="accent-color: #1e3a8a;"> Transitive dependency (non-key columns depending on other non-key columns)
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch15" value="D" style="accent-color: #1e3a8a;"> Referential integrity keys
    </label>
    
    <button type="button" onclick="checkAnswerCh15()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch15" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh15() {
    var selected = document.querySelector('input[name="qch15"]:checked');
    var feedback = document.getElementById('feedback-ch15');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "C") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> Transitive dependencies occur when non-key fields depend on other non-key fields (e.g. `SchoolName` depending on `SchoolID`, which is not the table's primary key). Removing these transitive links is the core objective when normalizing from **2NF to 3NF**.";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Let's review normalisation definitions: 1NF eliminates repeating groups. 2NF resolves partial dependencies. **3NF resolves transitive dependencies**.";
    }
  }
</script>

---

### Chapter 16: SQL Implementation Quiz

<div class="interactive-quiz" style="border: 1px solid #cbd5e1; border-left: 6px solid #1e3a8a; padding: 20px; border-radius: 6px; margin: 25px 0; background-color: #f8fafc;">
  <h4 style="margin-top: 0; color: #0f172a;">⚡ SCSA Challenge: Multi-Table Joins</h4>
  <p style="font-weight: 500; margin-bottom: 15px;">Consider an <code>ATHLETE</code> table (with <code>SchoolID</code> as a foreign key) and a <code>SCHOOL</code> table (with <code>SchoolID</code> as its primary key). Which SQL query correctly lists each athlete's name alongside their school name?</p>
  
  <form id="quiz-ch16" style="display: flex; flex-direction: column; gap: 10px;">
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch16" value="A" style="accent-color: #1e3a8a;"> <pre style="background:none; border:none; padding:0; margin:0; font-size:12px;">SELECT AthleteName, SchoolName FROM ATHLETE, SCHOOL;</pre>
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch16" value="B" style="accent-color: #1e3a8a;"> <pre style="background:none; border:none; padding:0; margin:0; font-size:12px;">SELECT AthleteName, SchoolName FROM ATHLETE 
INNER JOIN SCHOOL ON ATHLETE.SchoolID = SCHOOL.SchoolID;</pre>
    </label>
    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
      <input type="radio" name="qch16" value="C" style="accent-color: #1e3a8a;"> <pre style="background:none; border:none; padding:0; margin:0; font-size:12px;">SELECT AthleteName, SchoolName FROM ATHLETE 
WHERE SCHOOL ON SchoolID;</pre>
    </label>
    
    <button type="button" onclick="checkAnswerCh16()" style="margin-top: 15px; width: fit-content; background-color: #1e3a8a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: 600; cursor: pointer;">Check Answer</button>
  </form>
  
  <div id="feedback-ch16" style="margin-top: 15px; padding: 12px; border-radius: 4px; display: none;"></div>
</div>

<script>
  function checkAnswerCh16() {
    var selected = document.querySelector('input[name="qch16"]:checked');
    var feedback = document.getElementById('feedback-ch16');
    if (!selected) {
      feedback.style.display = "block"; feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "⚠️ Please select an answer first!"; return;
    }
    feedback.style.display = "block";
    if (selected.value === "B") {
      feedback.style.backgroundColor = "#f0fdf4"; feedback.style.color = "#166534";
      feedback.innerHTML = "<strong>Correct! 🎉</strong> To query data across two tables, use the standard SQL <code>INNER JOIN</code> syntax, matching rows using the <code>ON</code> clause on their common key field (<code>ATHLETE.SchoolID = SCHOOL.SchoolID</code>).";
    } else {
      feedback.style.backgroundColor = "#fef2f2"; feedback.style.color = "#991b1b";
      feedback.innerHTML = "<strong>Incorrect ❌</strong> Option A creates a cross product of rows (which duplicates data), and Option C uses completely invalid SQL syntax. To join relational tables, always use <code>INNER JOIN ... ON TableA.Key = TableB.Key</code>.";
    }
  }
</script>
