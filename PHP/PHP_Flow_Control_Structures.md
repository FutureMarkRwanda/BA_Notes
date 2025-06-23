# PHP Flow Control Structures

## Summary

This topic covers PHP’s flow control structures, which manage the execution flow of scripts using conditional and looping constructs. It includes selection structures (if, else, elseif, switch), looping structures (for, while, do-while, foreach), and jumping structures (break, continue, goto), enabling dynamic decision-making and repetition in code.

- **Introduction to Flow Controls**: Overview of statements and their role in PHP scripts.
- **Sequential Logic**: Default linear execution of PHP statements.
- **Selection Control Structures**: Conditional execution using if, else, elseif, and switch.
- **Looping Control Structures**: Repetitive execution using for, while, do-while, and foreach.
- **Jumping Control Structures**: Controlling loop or switch flow with break, continue, and goto.

---

## Introduction to Flow Controls

PHP scripts consist of statements like assignments, function calls, loops, or conditionals, typically ending with a semicolon. Statements can be grouped using curly braces `{}` to form a statement-group, treated as a single statement. Flow control structures determine how these statements are executed, either conditionally, repetitively, or by jumping to specific points.

**Key Concepts**:
- Statements execute sequentially unless altered by control structures.
- Curly braces `{}` group multiple statements for conditional or looping execution.
- Alternative syntax (using `:` and `endif`, `endfor`, etc.) is available for cleaner HTML integration.
- Brackets used: `()` (parentheses), `{}` (curly braces), `[]` (square brackets).

**Example**: A script with grouped statements checks user roles and outputs messages conditionally, using curly braces for clarity.

A developer uses flow control to display different webpage content based on user authentication status.

---

## Sequential Logic

Sequential logic executes statements in the order they are written, following a linear flow unless modified by control structures. This is the default behavior in PHP, suitable for straightforward tasks.

Unless directed otherwise (e.g., by loops or conditionals), PHP processes statements sequentially, executing each line as it appears in the script. This is ideal for simple, linear tasks like initializing variables or outputting static content.

**Example**: A script outputs a welcome message followed by a user’s name in sequence.

**Output**:
```
Welcome to the site!
User: Alice
```


```php
<?php
echo "Welcome to the site!";
$name = "Alice";
echo "User: $name";
?>
```


---

## Selection Control Structures

Selection control structures enable conditional execution based on Boolean expressions, using relational operators (`==`, `>`, `<`, `>=`, `<=`) and logical operators (`AND`, `OR`, `NOT`). They include `if`, `else`, `elseif`, and `switch`.

These structures perform logical tests to decide which code block executes. They are essential for dynamic applications, such as user authentication or role-based access.

### If

The `if` statement evaluates a Boolean expression. If true, it executes the associated statement or block; if false, it skips it. Multiple statements are grouped in curly braces `{}` or alternative syntax (`:` and `endif`).

**Example**: Display "a is bigger than b" if `$a` is greater than `$b`.


```php
<?php
$a = 10;
$b = 5;
if ($a > $b) {
    echo "a is bigger than b";
}
?>
```

**Output**: `a is bigger than b`

### Else

The `else` statement extends `if`, executing a different block if the `if` condition is false. It’s used for binary decisions, ensuring one of two paths is taken.

**Example**: Display "a is greater than b" if `$a > $b`, otherwise display "a is NOT greater than b".


```php
<?php
$a = 5;
$b = 10;
if ($a > $b) {
    echo "a is greater than b";
} else {
    echo "a is NOT greater than b";
}
?>
```

**Output**: `a is NOT greater than b`

### Elseif

The `elseif` (or `else if`) statement checks additional conditions if the preceding `if` or `elseif` conditions are false. It executes only if its condition is true. Use curly braces or alternative syntax, noting that `else if` (two words) requires curly braces to avoid parse errors in alternative syntax.

**Example**: Display messages based on whether `$a` is greater than, equal to, or less than `$b`.


```php
<?php
$a = 5;
$b = 5;
if ($a > $b) {
    echo "a is bigger than b";
} elseif ($a == $b) {
    echo "a is equal to b";
} else {
    echo "a is smaller than b";
}
?>
```

**Output**: `a is equal to b`

### Switch

The `switch` statement compares a single expression against multiple values, executing the matching `case` block. A `break` statement prevents fall-through to subsequent cases. The `default` case handles unmatched values and must be last. Alternative syntax uses `:` and `endswitch`.

**Example**: Display messages based on the value of `$i` using `switch`.


```php
<?php
$i = 1;
switch ($i) {
    case 0:
        echo "i equals 0";
        break;
    case 1:
        echo "i equals 1";
        break;
    case 2:
        echo "i equals 2";
        break;
    default:
        echo "i is not equal to 0, 1 or 2";
}
?>
```

**Output**: `i equals 1`

A web app uses `if-elseif-else` to display user role-specific dashboards and `switch` to handle different payment methods.

---

## Looping Control Structures

Looping structures repeat code execution based on conditions or iterations, including `for`, `while`, `do-while`, and `foreach`, ideal for processing arrays or repetitive tasks.

Loops automate repetitive tasks, such as iterating over data or generating patterns, controlled by conditions or counters.

### For

The `for` loop executes a block for a specified number of iterations, defined by three expressions: initialization, condition, and increment. It supports curly braces or alternative syntax (`:` and `endfor`). Empty expressions allow flexibility, often using `break` for control.

**Example**: Print numbers 1 to 10 using a `for` loop.


```php
<?php
for ($i = 1; $i <= 10; $i++) {
    echo $i;
}
?>
```

**Output**: `12345678910`

### While

The `while` loop executes as long as its condition is true, checking the condition at the start of each iteration. If false initially, the loop skips entirely. It supports curly braces or alternative syntax (`:` and `endwhile`).

**Example**: Print numbers 1 to 10 using a `while` loop.


```php
<?php
$i = 1;
while ($i <= 10) {
    echo $i++;
}
?>
```

**Output**: `12345678910`

### Do-While

The `do-while` loop executes at least once, checking its condition at the end of each iteration. It’s useful when the loop body must run before condition evaluation.

**Example**: Print a number once, stopping if it’s not greater than 0.


```php
<?php
$i = 0;
do {
    echo $i;
} while ($i > 0);
?>
```

**Output**: `0`

### Foreach

The `foreach` loop iterates over arrays or objects, assigning each element’s value (or key and value) to variables. It’s ideal for array processing, with two syntaxes: value-only or key-value. Unset references after use to avoid unintended behavior.

**Example**: Iterate over an array to double its values.


```php
<?php
$arr = array(1, 2, 3, 4);
foreach ($arr as &$value) {
    $value = $value * 2;
}
unset($value);
print_r($arr);
?>
```

**Output**: `Array ( [0] => 2 [1] => 4 [2] => 6 [3] => 8 )`

A developer uses `for` to generate a numbered list, `foreach` to display database records, and `do-while` for a retry mechanism in a form submission.

---

## Jumping Control Structures

Jumping structures interrupt or skip execution within loops or switches, including `break`, `continue`, and `goto`, controlling flow dynamically.

These structures allow exiting loops/switches, skipping iterations, or jumping to labeled points, enhancing control over complex logic.

### Break

The `break` statement terminates the current `for`, `foreach`, `while`, `do-while`, or `switch` structure. An optional numeric argument specifies how many nested structures to exit (default is 1).

**Example**: Stop a loop when a condition is met, e.g., finding "stop" in an array.


```php
<?php
$arr = array('one', 'two', 'three', 'four', 'stop', 'five');
foreach ($arr as $val) {
    if ($val == 'stop') {
        break;
    }
    echo "$val<br>";
}
?>
```

**Output**:
```
one
two
three
four
```

### Continue

The `continue` statement skips the current loop iteration, moving to the next iteration’s condition check. In a `switch` within a loop, `continue 2` targets the outer loop. An optional argument specifies levels to skip (default is 1).

**Example**: Skip even keys in an array.


```php
<?php
$arr = array('one', 'two', 'three', 'four');
foreach ($arr as $key => $value) {
    if ($key % 2 == 0) {
        continue;
    }
    echo "$value<br>";
}
?>
```

**Output**:
```
two
four
```

### Goto

The `goto` statement jumps to a labeled point in the same file and context, useful for exiting nested loops but restricted from jumping into loops or functions.

**Example**: Jump to a label to skip code.


```php
<?php
goto a;
echo 'Foo';
a:
echo 'Bar';
?>
```

**Output**: `Bar`

A script uses `break` to exit a loop when an error occurs, `continue` to skip invalid data, and `goto` to redirect flow in a complex validation process.

---

## Exercises

Exercises reinforce flow control concepts through practical tasks, such as printing array data or generating patterns using loops.

### Exercise 1: Province Details

Use a `for` loop to iterate over an array of province details, printing each element separated by commas.


```php
<?php
$provinceDetails = array(
    array("KIGALI", 3, "50SQM"),
    array("EASTERN", 7, "40SQM"),
    array("WESTERN", 7, "30SQM"),
    array("NORTHERN", 5, "40SQM")
);
for ($i = 0; $i < count($provinceDetails); $i++) {
    echo implode(", ", $provinceDetails[$i]) . "<br>";
}
?>
```

**Output**:
```
KIGALI, 3, 50SQM
EASTERN, 7, 40SQM
WESTERN, 7, 30SQM
NORTHERN, 5, 40SQM
```

### Exercise 2: Pyramid Patterns

Use nested `for` loops to print numerical pyramid patterns, as specified in the exercises labeled A, B, C.

**CODES (Pattern A)**:
```php
<?php
for ($i = 1; $i <= 9; $i++) {
    for ($j = 1; $j <= $i; $j++) {
        echo $j;
    }
    echo "<br>";
}
?>
```

**Output**:
```
1
12
123
1234
12345
123456
1234567
12345678
123456789
```

**CODES (Pattern B)**:
```php
<?php
for ($i = 1; $i <= 9; $i++) {
    for ($j = 1; $j <= $i; $j++) {
        echo $j;
    }
    for ($j = $i - 1; $j >= 1; $j--) {
        echo $j;
    }
    echo "<br>";
}
?>
```

**Output**:
```
1
121
12321
1234321
123454321
12345654321
1234567654321
123456787654321
12345678987654321
```

**CODES (Pattern C)**:
```php
<?php
for ($i = 1; $i <= 9; $i++) {
    for ($j = 1; $j <= $i; $j++) {
        echo $j;
    }
    for ($j = $i - 1; $j >= 1; $j--) {
        echo $j;
    }
    echo "<br>";
}
?>
```

**Output** (same as Pattern B):
```
1
121
12321
1234321
123454321
12345654321
1234567654321
123456787654321
12345678987654321
```

**Note**: Patterns B and C produce identical outputs based on the provided specification. Pattern E (star pattern) is not implemented here but can be added if needed.

A student practices loops by generating pyramid patterns for a web-based math tool, using `for` loops to create dynamic outputs.