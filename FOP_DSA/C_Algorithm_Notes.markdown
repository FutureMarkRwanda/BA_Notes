# Chapter 2: Algorithms

## Overview of Algorithms
- **Definition**: A series of steps to perform a computation or task, providing a step-by-step procedure to solve a problem.
- **Origin**: Derived from the work of Arabic mathematician Muḥammad ibn Mūsā al-Khwārizmī; now central to computer science.
- **Good Algorithm**: Efficient, clear, unambiguous, human-readable, programming language-independent, with well-defined inputs and outputs.

## Representing Algorithms
- **Two Main Methods**:
  - **Pseudocode**: A simplified, non-executable description of instructions without strict syntax.
  - **Flowcharts**: Graphical representations of steps using standardized symbols connected by arrows.

### Pseudocode
- **Characteristics**:
  - Not a programming language; mimics programming structure.
  - Instructions in uppercase, variables in lowercase, messages in sentence case.
  - Uses `INPUT` for questions, `OUTPUT` for screen messages.
- **Example 1**: Ask for name and age, comment based on age.
  ```pseudocode
  START
  DECLARE name, age
  OUTPUT 'What is your name?'
  INPUT name
  STORE the user's input in the name variable
  OUTPUT 'Hello' + name
  OUTPUT 'How old are you?'
  INPUT age
  STORE the user's input in the age variable
  IF age >= 70 THEN
      OUTPUT 'You are aged to perfection!'
  ELSE
      OUTPUT 'You are a spring chicken!'
  END
  ```
  
## Qualities of a Good Algorithm
- Well-defined input and output.
- Clear, unambiguous steps.
- Most effective solution among alternatives.
- Human-readable, not computer code.
- Programming language-independent.

### Flowcharts
- **Definition**: Graphical representation of algorithm steps using standardized symbols (e.g., ovals for start/end, rectangles for processes, diamonds for decisions) connected by arrows.
- **Example**: Sum of 529 and 256.
  - Steps: Start → Compute 529 + 256 → Sum = 875 → Stop.


---
#### Pseudocode Syntax Guide
- **Expressions**:
  - `IntExp`, `BoolExp`, `CharExp`, `StringExp`: Expressions evaluating to integer, boolean, character, or string.
  - `Exp`: Any expression.
- **Indexing**: Arrays and strings start at index 0 unless specified.
- **Variable Assignment**:
  ```pseudocode
  Identifier ← Exp
  a ← 3
  a ← a + 1
  ```
- **Constant Assignment**:
  ```pseudocode
  constant IDENTIFIER ← Exp
  constant PI ← 3.141
  ```
- **Arithmetic Operations**:
  - Standard: `+`, `-`, `*`, `/` (division uses `/` instead of `÷`).
  - Integer Division: `IntExp DIV IntExp` (e.g., `9 DIV 5` = 1).
  - Modulus: `IntExp MOD IntExp` (e.g., `9 MOD 5` = 4).
- **Relational Operators**:
  - `<`, `>`, `=`, `≠`, `≤`, `≥` (e.g., `4 < 6`, `3 ≤ 4`).
- **Boolean Operations**:
  - `AND`, `OR`, `NOT` (e.g., `(3 = 3) AND (3 ≤ 4)`).
- **Condition-Controlled Iteration**:
  - **Repeat-Until**:
    ```pseudocode
    REPEAT
        # statements
    UNTIL BoolExp
    ```
  - **While**:
    ```pseudocode
    WHILE BoolExp
        # statements
    ENDWHILE
    ```
- **Count-Controlled Iteration (For Loop)**:
  ```pseudocode
  FOR Identifier ← IntExp TO IntExp
      # statements
  ENDFOR
  ```
- **Selection**:
  - **If**:
    ```pseudocode
    IF BoolExp THEN
        # statements
    ENDIF
    ```
  - **If-Else**:
    ```pseudocode
    IF BoolExp THEN
        # statements
    ELSE
        # statements
    ENDIF
    ```
  - **Else-If**:
    ```pseudocode
    IF BoolExp THEN
        # statements
    ELSE IF BoolExp THEN
        # statements
    ELSE
        # statements
    ENDIF
    ```
- **Arrays**:
  - **Assignment**:
    ```pseudocode
    Identifier ← [Exp, Exp, …, Exp]
    primes ← [2, 3, 5, 7, 11, 13]
    ```
  - **Accessing Elements**:
    ```pseudocode
    Identifier[IntExp]
    primes[0]  # evaluates to 2
    ```
  - **Updating Elements**:
    ```pseudocode
    Identifier[IntExp] ← Exp
    primes[5] ← 17
    ```
  - **2D Arrays**:
    ```pseudocode
    Identifier[IntExp][IntExp]
    tables ← [[1, 2, 3], [2, 4, 6], [3, 6, 9], [4, 8, 12]]
    tables[3][1]  # evaluates to 8
    ```
  - **Array Length**:
    ```pseudocode
    LEN(Identifier)
    LEN(primes)  # evaluates to 6
    ```
- **Comments**:
  - Single-line: `# comment`
  - Multi-line: `# comment # comment`

## Real-Life Example: Baking Bread
```pseudocode
START
Preheat the oven
Mix flour, sugar, and other ingredients
Pour into a baking pan
Heat for some time
Get the bread out of the baking pan
STOP
```

## Programming Examples

### 1. Calculate Sum of Two Numbers
```pseudocode
START
VAR A, B, Sum
GET A
GET B
Sum ← A + B
PRINT Sum
STOP
```

### 2. Find Maximum Number in a List
```pseudocode
START
DECLARE C, max, i
C ← [val1, val2, ..., valn]
max ← C[0]
FOR i ← 1 TO n-1
    IF C[i] > max THEN
        max ← C[i]
    ENDIF
ENDFOR
PRINT max
STOP
```

### 3. Sum and Average of Even Numbers (1 to n)
```pseudocode
START
VAR sum ← 0, average, i
INPUT n
FOR i ← 1 TO n
    IF i MOD 2 = 0 THEN
        sum ← sum + i
    ENDIF
ENDFOR
average ← sum / n
PRINT average
END
```

### 4. Find Largest of Three Numbers
```pseudocode
START
DECLARE n1, n2, n3, largest
INPUT n1, n2, n3
IF n1 > n2 THEN
    IF n1 > n3 THEN
        largest ← n1
    ELSE IF n3 > n1 THEN
        largest ← n3
    ENDIF
ELSE IF n2 > n1 THEN
    largest ← n2
ENDIF
PRINT largest
END
```

### 5. Check if a Number is Prime
```pseudocode
START
DECLARE n, lv, flag ← 1
INPUT n
FOR lv ← n-1 TO 3
    IF n % lv = 0 THEN
        flag ← 0
        BREAK
    ENDIF
ENDFOR
IF flag = 0 THEN
    PRINT "n is not prime"
ELSE
    PRINT "n is prime"
ENDIF
STOP
```

### 6. Count Digits in a Positive Integer
```pseudocode
START
VAR n, counter ← 0
INPUT n
REPEAT
    n ← n DIV 10
    counter ← counter + 1
UNTIL n = 0
RETURN counter
END
```

### 7. Find Greatest Common Divisor (GCD) of Two Numbers
- **Note**: Algorithm not provided in the text, but a common approach (Euclidean algorithm) can be described:
```pseudocode
START
DECLARE a, b, temp
INPUT a, b
WHILE b ≠ 0
    temp ← b
    b ← a MOD b
    a ← temp
ENDWHILE
PRINT a
STOP
```

## Key Points
- Algorithms are systematic, efficient solutions to computational problems.
- Pseudocode and flowcharts are standard tools for representing algorithms.
- Good algorithms are clear, effective, and independent of programming languages.
- Practical examples demonstrate how algorithms solve real-world and programming problems.