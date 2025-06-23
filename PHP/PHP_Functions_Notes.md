# PHP Functions Notes

## Definition
- A function is a self-contained block of code that performs a specific task.
- Functions are reusable and can be called multiple times within a program.
- PHP supports both built-in functions (e.g., `gettype()`, `print_r()`, `var_dump()`) and user-defined functions.

## User-Defined Functions
- Allow developers to create custom reusable code packages.
- Maintained separately from the main program.

### Advantages
1. **Reduces Code Repetition**: Extracts commonly used code into a single component, callable anywhere in the script.
2. **Easier Maintenance**: Changes in a function are automatically applied wherever the function is called.
3. **Error Elimination**: Dividing code into functions makes it easier to locate and fix errors.
4. **Reusability**: Functions can be reused in other applications by including the PHP file containing them.

## Function Creation and Calling
- **Syntax**:
  ```php
  function functionName() {
      // Code to be executed
  }
  ```
- **Declaration**:
  - Starts with the keyword `function`.
  - Followed by the function name, parentheses `()`, and curly brackets `{}` containing the code.
- **Calling**: Execute a function by writing its name followed by parentheses, e.g., `functionName()`.

### Rules for Function Names
1. Must end with parentheses `()`.
2. Begins with the keyword `function`.
3. Cannot start with a number; can start with a letter or underscore.
4. Not case-sensitive.

## Functions with Parameters
- Parameters act like variables inside the function.
- Multiple parameters can be passed.
- **Example**:
  ```php
  function addNumber($num1, $num2) {
      $sum = $num1 + $num2;
      echo "Sum of the two numbers is: $sum";
  }
  addNumber(5, 10); // Outputs: Sum of the two numbers is: 15
  ```

## Functions Returning Values
- Use the `return` statement to send a value back to the calling code.
- Stops function execution upon return.
- Can return multiple values using an array, e.g., `return array(1, 2, 3, 4)`.
- **Example**:
```php
function addNumbers($a, $b) {
    return $a + $b;
}
echo addNumbers(5, 5); // Outputs: 10
```

## Passing Arguments by Reference
- Use `&` to pass arguments by reference, allowing the function to modify the original variable.
- **Example**:
```php
function modifyValue(&$value) {
    $value += 10;
}
$number = 5;
modifyValue($number);
echo $number; // Outputs: 15
```

## Passing Arrays to Functions
- Arrays can be passed as arguments to process multiple values.
- **Example**:
```php
function sumArray($numbers) {
    return array_sum($numbers);
}
$arr = [1, 2, 3, 4];
echo sumArray($arr); // Outputs: 10
```

## Recursive Functions
- A function that calls itself until a condition is met.
- Useful for complex mathematical calculations or nested data structures.
- **Example**:
```php
function factorial($n) {
    if ($n <= 1) return 1;
    return $n * factorial($n - 1);
}
echo factorial(5); // Outputs: 120
```

## PHP as a Loosely Typed Language
- PHP automatically assigns data types to variables based on their value.
- **Example**:
```php
function addNumbers(int $a, int $b) {
    return $a + $b;
}
echo addNumbers(5, "5 days"); // Outputs: 10 (string "5 days" is cast to int 5)
```

## Superglobal Variables
- Always accessible, regardless of scope.
- Common superglobals:
  - `$GLOBALS`: Access global variables within functions.
  - `$_SERVER`: Holds information about headers, paths, and script locations.
  - `$_REQUEST`: Collects form data (both GET and POST).
  - `$_POST`: Collects form data submitted via POST method.
  - `$_GET`: Collects form data submitted via GET method.
  - `$_FILES`: Handles file uploads.
  - `$_ENV`: Returns environment variables.
  - `$_COOKIE`: Manages cookies.
  - `$_SESSION`: Manages session variables.

### Using `$_POST`
- Collects form data submitted via the POST method.
- **Example**:
  ```php
  <form method="post" action="<?php echo $_SERVER['PHP_SELF']; ?>">
      Name: <input type="text" name="name">
      <input type="submit" value="Submit">
  </form>
  <?php
  if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $name = $_POST['name'];
      echo "Hello, $name!";
  }
  ?>
  ```

### Using `$_GET`
- Collects form data submitted via the GET method.
- Data is visible in the URL query string, making it less secure for sensitive information.
- Used to request data from a specified resource.
- **Example**:
  ```php
  <form method="get" action="<?php echo $_SERVER['PHP_SELF']; ?>">
      Name: <input type="text" name="name">
      <input type="submit" value="Submit">
  </form>
  <?php
  if ($_SERVER["REQUEST_METHOD"] == "GET" && isset($_GET['name'])) {
      $name = $_GET['name'];
      echo "Hello, $name!";
  }
  ?>
  ```

### Comparison of `$_GET` and `$_POST`
| Feature                | `$_GET`                                                                 | `$_POST`                                                                |
|------------------------|-------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Data Visibility**    | Data is visible in the URL query string (e.g., `?name=value`).           | Data is sent in the HTTP request body, not visible in the URL.           |
| **Security**           | Less secure; suitable for non-sensitive data due to URL visibility.      | More secure; suitable for sensitive data like passwords.                 |
| **Data Size Limit**    | Limited by URL length (varies by browser, typically ~2000 characters).   | No strict limit; can handle larger data (depends on server settings).    |
| **Use Case**           | Retrieving data, search queries, or bookmarkable URLs.                   | Submitting forms with sensitive data or large amounts of data.           |
| **Caching**            | Can be cached or bookmarked due to URL-based data.                      | Not cached or bookmarked, as data is not in the URL.                    |
| **Method**             | Uses HTTP GET method.                                                   | Uses HTTP POST method.                                                  |

## Practical Notes
- Functions enhance code modularity and scalability.
- Use descriptive function names to improve readability.
- Leverage superglobals like `$_GET` and `$_POST` for handling form data, choosing based on security and data size needs.
- Test functions thoroughly to ensure they handle edge cases and errors gracefully.