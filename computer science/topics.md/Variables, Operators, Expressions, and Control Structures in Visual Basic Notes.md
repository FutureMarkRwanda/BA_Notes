# Unit 9: Variables, Operators, Expressions, and Control Structures in Visual Basic

## 9.1 Types of Visual Basic Data
Data types in Visual Basic define the kind of data a variable can hold, determining its size and operations.

- **What is a Data Type?**
  - A data type specifies the type of value (e.g., number, text) a variable can store.
  - Helps ensure correct operations and memory usage.
- **Common VB6 Data Types**:
  - **Integer**: Whole numbers (e.g., 5, -10), 2 bytes, range: -32,768 to 32,767.
  - **Long**: Larger whole numbers, 4 bytes, range: -2,147,483,648 to 2,147,483,647.
  - **Single**: Floating-point numbers (e.g., 3.14), 4 bytes.
  - **Double**: Higher-precision floating-point numbers, 8 bytes.
  - **String**: Text (e.g., "Hello"), variable length.
  - **Boolean**: True or False, 2 bytes.
  - **Variant**: Can hold any data type, but less efficient (use sparingly).
- **Example**:
  ```vb
  Dim age As Integer
  Dim name As String
  Dim salary As Double
  Dim isStudent As Boolean
  age = 20
  name = "Alice"
  salary = 50000.75
  isStudent = True
  MsgBox "Age: " & age & ", Name: " & name, 0, "Data Types"
  ```
- **Self-Study Tip**:
  - Think of data types as different containers: a small box (Integer) for whole numbers, a large box (String) for text, and a flexible box (Variant) for anything, but heavier to carry.

## 9.2 Variables
Variables are named storage locations in memory that hold data values.

- **What is a Variable?**
  - A variable is a name assigned to a memory location to store data.
  - Must be declared with a data type before use in VB6.
- **Declaring Variables**:
  - Syntax: `Dim variableName As DataType`
  - Example: `Dim count As Integer`
- **Assigning Values**:
  - Use `=` to assign a value: `count = 10`
- **Rules for Variable Names**:
  - Start with a letter, not a number.
  - No spaces or special characters (except underscore `_`).
  - Meaningful names (e.g., `studentAge` instead of `x`).
- **Example**:
  ```vb
  Private Sub Command1_Click()
      Dim score As Integer
      Dim playerName As String
      score = 95
      playerName = "Bob"
      MsgBox playerName & " scored " & score, 0, "Score"
  End Sub
  ```
- **Self-Study Tip**:
  - Variables are like labeled drawers in a desk. You choose the drawer’s type (e.g., Integer) and store specific items (values) in it.

## 9.3 Scope of a Variable
The scope of a variable determines where it can be accessed in a program.

- **What is Scope?**
  - Scope defines the visibility and lifetime of a variable (where and how long it exists).
- **Types of Scope in VB6**:
  - **Local Scope**:
    - Declared inside a procedure (e.g., Sub or Function) using `Dim`.
    - Accessible only within that procedure.
    - Destroyed when the procedure ends.
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim temp As Integer
          temp = 10
          MsgBox "Temp: " & temp, 0, "Local"
      End Sub
      ```
  - **Module Scope**:
    - Declared at the top of a form/module using `Dim` or `Private`.
    - Accessible to all procedures in that form/module.
    - Example:
      ```vb
      Dim counter As Integer ' Module-level
      Private Sub Command1_Click()
          counter = counter + 1
          MsgBox "Counter: " & counter, 0, "Module Scope"
      End Sub
      ```
  - **Global Scope**:
    - Declared in a standard module using `Public`.
    - Accessible across all forms/modules in the project.
    - Example:
      ```vb
      ' In a standard module (e.g., Module1.bas)
      Public appName As String
      ' In a form
      Private Sub Form_Load()
          appName = "MyApp"
          MsgBox "App: " & appName, 0, "Global"
      End Sub
      ```
- **Self-Study Tip**:
  - Scope is like access to a room. Local variables are locked in one room (procedure), module variables are shared in a house (form), and global variables are available to the entire neighborhood (project).

## 9.4 Operators and Expressions in Visual Basic
Operators perform operations on variables/values, and expressions combine them to produce results.

- **What are Operators and Expressions?**
  - **Operators**: Symbols that perform operations (e.g., `+`, `-`, `=`).
  - **Expressions**: Combinations of variables, values, and operators that evaluate to a result (e.g., `x + 5`).
- **Types of Operators**:
  - **Arithmetic**: `+` (add), `-` (subtract), `*` (multiply), `/` (divide), `\` (integer divide), `Mod` (remainder), `^` (exponent).
    - Example: `5 + 3` evaluates to 8.
  - **Comparison**: `=` (equal), `<>` (not equal), `<`, `>`, `<=`, `>=`.
    - Example: `x > 10` returns True or False.
  - **Logical**: `And`, `Or`, `Not`.
    - Example: `x > 5 And y < 10` checks both conditions.
  - **Concatenation**: `&` (joins strings).
    - Example: `"Hello" & " World"` results in "Hello World".
- **Example**:
  ```vb
  Private Sub Command1_Click()
      Dim a As Integer, b As Integer, result As Integer
      a = 10
      b = 3
      result = a + b * 2 ' Expression: 10 + (3 * 2) = 16
      MsgBox "Result: " & result, 0, "Arithmetic"
      If a > b Then
          MsgBox a & " is greater than " & b, 0, "Comparison"
      End If
      MsgBox "Name: " & "Alice" & " Smith", 0, "Concatenation"
  End Sub
  ```
- **Self-Study Tip**:
  - Operators are like tools (e.g., a hammer for adding numbers), and expressions are like building a small structure (e.g., `x + y`) using those tools.

## 9.5 Decision Structures in Visual Basic
Decision structures control program flow based on conditions.

- **What are Decision Structures?**
  - Code blocks that execute different actions based on conditions (e.g., if a number is positive).
- **Types**:
  - **If…Then**:
    - Executes code if a condition is True.
    - Syntax: `If condition Then statement`
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim num As Integer
          num = 10
          If num > 0 Then
              MsgBox "Number is positive", 0, "Check"
          End If
      End Sub
      ```
  - **If…Then…Else**:
    - Handles two outcomes (True or False).
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim age As Integer
          age = Val(InputBox("Enter age:"))
          If age >= 18 Then
              MsgBox "Adult", 0, "Age Check"
          Else
              MsgBox "Minor", 0, "Age Check"
          End If
      End Sub
      ```
  - **If…Then…ElseIf**:
    - Handles multiple conditions.
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim score As Integer
          score = Val(InputBox("Enter score:"))
          If score >= 90 Then
              MsgBox "Grade A", 0, "Result"
          ElseIf score >= 80 Then
              MsgBox "Grade B", 0, "Result"
          Else
              MsgBox "Below B", 0, "Result"
          End If
      End Sub
      ```
  - **Select Case**:
    - Simplifies multiple conditions for a single variable.
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim day As Integer
          day = Val(InputBox("Enter day (1-7):"))
          Select Case day
              Case 1
                  MsgBox "Monday", 0, "Day"
              Case 2
                  MsgBox "Tuesday", 0, "Day"
              Case Else
                  MsgBox "Other day", 0, "Day"
          End Select
      End Sub
      ```
- **Self-Study Tip**:
  - Decision structures are like choosing a path at a fork in the road. Based on a condition (e.g., “Is it raining?”), you pick one route (e.g., take an umbrella) or another (e.g., go without).

## 9.6 Repetition Structures
Repetition structures (loops) execute code multiple times based on a condition or count.

- **What are Repetition Structures?**
  - Code blocks that repeat until a condition is met or a set number of times.
- **Types**:
  - **For…Next**:
    - Loops a fixed number of times using a counter.
    - Syntax: `For counter = start To end [Step increment]`
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim i As Integer
          For i = 1 To 5
              MsgBox "Count: " & i, 0, "Loop"
          Next i
      End Sub
      ```
  - **Do While…Loop**:
    - Loops while a condition is True (checks condition first).
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim count As Integer
          count = 1
          Do While count <= 3
              MsgBox "Count: " & count, 0, "Loop"
              count = count + 1
          Loop
      End Sub
      ```
  - **Do…Loop While**:
    - Loops at least once, checks condition at the end.
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim num As Integer
          num = 0
          Do
              num = num + 1
              MsgBox "Number: " & num, 0, "Loop"
          Loop While num < 2
      End Sub
      ```
  - **Do Until…Loop**:
    - Loops until a condition is True.
    - Example:
      ```vb
      Private Sub Command1_Click()
          Dim value As Integer
          value = 1
          Do Until value > 3
              MsgBox "Value: " & value, 0, "Loop"
              value = value + 1
          Loop
      End Sub
      ```
- **Self-Study Tip**:
  - Loops are like doing push-ups. You repeat an action (e.g., one push-up) a set number of times (For loop) or until you’re tired (While/Until loop).