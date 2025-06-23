# PHP Basic Syntax and Execution

## Summary

This topic covers PHP’s basic syntax and execution methods, including writing and running PHP scripts, using echo/print statements, comments, and variables. It explains how to execute PHP via a web server or CLI, focusing on XAMPP.

- **Syntax and Output**: Using echo, print, and comments in PHP scripts.
- **Variables**: Declaring and using variables in a loosely typed system.
- **Execution**: Running PHP scripts in XAMPP or via CLI.

---

## Syntax and Output

PHP scripts use specific syntax to output content and document code, embedded in HTML or run standalone. Output is generated using `echo` or `print`, and comments enhance code readability by explaining logic or hiding code from execution.

**Key Elements**:
- **PHP Tags**: Code resides within `<?php ?>`, marking the start and end of PHP code.
- **Echo**: Outputs data (e.g., strings, variables) to the browser, supports multiple arguments separated by commas, has no return value, and is faster due to optimized performance.
- **Print**: Outputs data, supports only a single argument, returns an integer value of 1, and is slower than `echo`.
- **Comments**:
  - Single-line: Use `//` (C++ style) or `#` (Unix style) to comment one line.
  - Multi-line: Use `/* */` to enclose multiple lines, ignored during execution.

### Echo

**Explanation**: The `echo` statement is used to display output, such as text, variables, or HTML, directly to the browser. It is versatile, allowing multiple strings or values to be output in a single statement by separating them with commas. It is commonly used in web applications for rendering dynamic content due to its speed and simplicity.

**Example**: Let’s output the following using `echo`:
```
Echo: Hello, World!
Print: Hello, World!
```

**CODES**:
```php
<?php
echo "Echo: Hello, ", "World! <br>";
print "Print: Hello, World!";
?>
```

### Comments

**Explanation**: Comments document code to improve readability and maintainability, allowing developers to explain logic or temporarily disable code without affecting execution. Single-line comments (`//` or `#`) are ideal for short notes, while multi-line comments (`/* */`) are used for longer explanations or blocking multiple lines.

**Example**: Let’s comment lines in our code to demonstrate both single-line and multi-line comments.

**CODES**:
```php
<?php
// This is a single-line comment
# Another single-line comment
/*
This is a
multi-line comment
*/
echo "PHP Comments Example";
?>
```

**Notes**:
- `echo` is preferred in high-traffic applications for its performance advantage over `print`.
- Comments are essential for collaborative projects, ensuring code is understandable to other developers.

**Scenario**: A developer uses `echo` to display a welcome message on a webpage and adds comments to explain the code for future team members.

---

## Variables

Variables in PHP store data, such as strings, numbers, or arrays, and are loosely typed, meaning data types are automatically assigned based on values. They are case-sensitive and use a `$` prefix to identify them.

**Key Rules**:
- Start with `$` followed by a letter or underscore (e.g., `$name`, `$_count`).
- Contain alphanumeric characters or underscores (A-z, 0-9, \_).
- No spaces or special symbols (except \_).
- Case-sensitive (e.g., `$user` ≠ `$USER`).
- Assigned using `=` (e.g., `$var = value;`).

**Data Types** (Auto-assigned):
- String: Text (e.g., `"hello"`).
- Integer: Whole numbers (e.g., `100`).
- Float: Decimals (e.g., `3.14`).
- Array, Boolean, NULL, etc.

**Explanation**: Variables are used to store and manipulate data dynamically, such as user input or database results. PHP’s loose typing allows variables to change types during execution (e.g., from string to integer), simplifying development but requiring careful handling to avoid errors.

**Example**: Let’s declare variables to store a name, age, and price, then output them using `echo`.

**CODES**:
```php
<?php
$name = "Alice";
$age = 25;
$price = 99.99;
echo "Name: $name <br>";
echo "Age: $age <br>";
echo "Price: $$price";
?>
```

**Additional Example**: Let’s demonstrate dynamic typing and case sensitivity with variables.

**CODES**:
```php
<?php
$var = "Text"; // String
echo "Var: $var <br>";
$var = 42; // Integer
echo "Var: $var <br>";
$color = "Blue";
$COLOR = "Red";
echo "Lowercase color: $color <br>";
echo "Uppercase COLOR: $COLOR";
?>
```

**Scenario**: A web application uses variables to store user profile data, dynamically displaying names and balances on a dashboard.

---

## Execution

PHP scripts can be executed via a web server (e.g., Apache in XAMPP) to generate dynamic web content or via the Command Line Interface (CLI) for testing or automation. XAMPP provides an environment to run PHP locally.

**Execution Methods**:
- **Web Server (XAMPP)**:
  1. Save PHP files in `C:\xampp\htdocs` (e.g., `test.php`).
  2. Start Apache and MySQL in XAMPP Control Panel.
  3. Access via `http://localhost/test.php` in a browser.
- **CLI**:
  1. Open a terminal.
  2. Navigate to the PHP file’s directory (e.g., `cd C:\xampp\htdocs`).
  3. Run: `php filename.php`.

**Explanation**: Web server execution is the primary method for PHP web applications, rendering output in browsers, while CLI execution is useful for scripts, debugging, or automation tasks. Proper setup ensures scripts run without errors.

**Example**: Let’s run a PHP script to display variable output via both XAMPP and CLI.

**CODES** (variables.php):
```php
<?php
$name = "Alice";
$age = 25;
echo "Name: $name <br>";
echo "Age: $age";
?>
```

**Web Execution**:
- Save as `variables.php` in `C:\xampp\htdocs`.
- Access `http://localhost/variables.php`.
- **Output**:
```
Name: Alice
Age: 25
```

**CLI Execution**:
```bash
cd C:\xampp\htdocs
php variables.php
```
- **Output**:
```
Name: Alice
Age: 25
```

**Troubleshooting Tips**:
- **Blank Page**: Check for syntax errors (e.g., missing `;`) or ensure Apache is running.
- **404 Error**: Verify file is in `htdocs` and URL is correct (e.g., `http://localhost/variables.php`).
- **CLI Failure**: Ensure PHP path (e.g., `C:\xampp\php`) is in system environment variables.
- **Variable Output Issues**: Use double quotes `"$var"` for interpolation, not single quotes `'$var'`.

**Scenario**: A student runs a PHP script in XAMPP to display user data in a browser, tests it via CLI, and resolves a blank page by fixing a missing semicolon.