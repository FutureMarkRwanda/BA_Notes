# PHP Database Connection Notes

## Database Setup
- **Creating a Database**:
  - Access the database management tool (e.g., phpMyAdmin).
  - Navigate to the "Databases" tab.
  - Enter a database name (e.g., `student_db`).
  - Set collation to `utf8mb4_general_ci`.
  - Click "Create".
- **Using Command Line**:
  ```sql
  CREATE DATABASE student_db;
  USE student_db;
  ```

- **Creating a Table**:
  - In phpMyAdmin, select the database (e.g., `student_db`).
  - Click "Create table".
  - Enter table name (e.g., `users`) and number of columns (e.g., 4).
  - Define columns with appropriate data types, lengths, and attributes:
    - Example:
      - `id`: `VARCHAR(10)`, no default, primary key.
      - `username`: `TEXT`, no default.
      - `password`: `VARCHAR(10)`, no default.
      - Another field as needed (e.g., `email` or `role`).
  - Click "Save".
- **Using SQL Command**:
  ```sql
  CREATE TABLE users (
      id VARCHAR(10) PRIMARY KEY,
      username TEXT,
      password VARCHAR(10),
      role VARCHAR(10)
  );
  ```

- **Inserting Data**:
  - In phpMyAdmin, select the `users` table, go to the "Insert" tab, and enter data (e.g., `id: 1`, `username: admin`, `password: admin@123`, `role: admin`).
  - Click "Go" to save.
- **Using SQL Command**:
  ```sql
  INSERT INTO users (id, username, password, role) VALUES ('1', 'admin', 'admin@123', 'admin');
  ```

## Connecting PHP to MySQL
- PHP provides multiple methods to connect to a MySQL database. Below are the three methods outlined in the document.

### First Method: MySQLi (Object-Oriented)
- Uses the MySQL Improved extension (`mysqli`).

```php
<?php
$servername = "localhost";
$username = "root";
$password = "";
$database = "student_db";

// Create connection
$conn = new mysqli($servername, $username, $password, $database);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
?>
```
- **Key Points**:
  - Requires server name, username, password, and database name.
  - Checks for connection errors using `connect_error`.
  - Terminates execution with `die()` if the connection fails.

### Second Method: MySQLi (Procedural)
- Also uses the MySQLi extension but in a procedural style.

```php
<?php
$servername = "localhost";
$username = "root";
$password = "";

// Create connection
$conn = mysqli_connect($servername, $username, $password);

// Check connection
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}
echo "Connected successfully";
?>
```
- **Key Points**:
  - Similar to the object-oriented method but uses procedural functions like `mysqli_connect()`.
  - Does not specify the database during connection; the database can be selected later using `mysqli_select_db()`.
  - Error checking with `mysqli_connect_error()`.

### Third Method: PHP Data Objects (PDO)
- Uses PDO for a more flexible and secure connection, supporting multiple database types.

```php
<?php
$servername = "localhost";
$username = "root";
$password = "";
$database = "student_db";

try {
    $conn = new PDO("mysql:host=$servername;dbname=$database", $username, $password);
    // Set the PDO error mode to exception
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected successfully";
} catch(PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
```
- **Key Points**:
  - Uses a DSN (Data Source Name) string to specify the database type and details.
  - Sets error mode to throw exceptions for better error handling.
  - Wrapped in a try-catch block to handle connection failures gracefully.

## Validating Credentials with a Database
- **Login Form Creation** (`login_db.php`):
  - Create an HTML form to collect `username` and `password`.
  ```php
  <html>
  <body>
      <h2>Login Form</h2>
      <form method="POST" action="">
          <label>Username:</label>
          <input type="text" name="username"><br><br>
          <label>Password:</label>
          <input type="password" name="password"><br><br>
          <input type="submit" name="submit" value="Login">
      </form>
  </body>
  </html>
  ```
- **PHP Validation Logic**:
  - Connect to the database using one of the above methods.
  - Query the `users` table to validate credentials.
  - Example using MySQLi (Object-Oriented):
  ```php
  <?php
  if (isset($_POST['submit'])) {
      $username = $_POST['username'];
      $password = $_POST['password'];

      $servername = "localhost";
      $username_db = "root";
      $password_db = "";
      $database = "student_db";

      $conn = new mysqli($servername, $username_db, $password_db, $database);

      if ($conn->connect_error) {
          die("Connection failed: " . $conn->connect_error);
      }

      // Prepare and execute query
      $sql = "SELECT * FROM users WHERE username = ? AND password = ?";
      $stmt = $conn->prepare($sql);
      $stmt->bind_param("ss", $username, $password);
      $stmt->execute();
      $result = $stmt->get_result();

      if ($result->num_rows > 0) {
          // Valid credentials
          header("Location: homepage.php");
          exit();
      } else {
          // Invalid credentials
          echo "Invalid username or password.";
      }

      $stmt->close();
      $conn->close();
  }
  ?>
  ```
- **Key Points**:
  - Uses prepared statements to prevent SQL injection.
  - Checks if the form is submitted using `isset($_POST['submit'])`.
  - Redirects to `homepage.php` on successful login.
  - Displays an error message for invalid credentials.
  - Closes the statement and connection to free resources.

## Practical Notes
- **Security**:
  - Always use prepared statements or parameterized queries to prevent SQL injection.
  - Hash passwords before storing them in the database (e.g., using `password_hash()`).
  - Use HTTPS to secure data transmission.
- **Error Handling**:
  - Check connection errors in all methods.
  - Use PDO’s exception mode for robust error handling.
- **Best Practices**:
  - Store database credentials in a separate configuration file.
  - Close database connections after use to optimize resources.
  - Test database operations with sample data to ensure reliability.
- **Environment Setup**:
  - Ensure MySQL/MariaDB is installed and running.
  - Verify phpMyAdmin or command-line access for database management.
  - Use `localhost` for local development, updating to appropriate server details for production.