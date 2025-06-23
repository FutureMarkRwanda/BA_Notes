# PHP Forms and MySQLi Operations Notes

## PHP MySQLi Functions
- MySQLi (MySQL Improved) functions allow interaction with MySQL database servers.
- Below is a table of key MySQLi functions and their descriptions:

| **Function**                  | **Description**                                                                 |
|-------------------------------|---------------------------------------------------------------------------------|
| `affected_rows()`            | Returns the number of affected rows in the previous MySQL operation.            |
| `autocommit()`               | Turns on or off auto-committing database modifications.                         |
| `begin_transaction()`         | Starts a transaction.                                                          |
| `change_user()`              | Changes the user of the specified database connection.                          |
| `character_set_name()`       | Returns the default character set for the database connection.                  |
| `close()`                    | Closes a previously opened database connection.                                 |
| `commit()`                   | Commits the current transaction.                                               |
| `connect()`                  | Opens a new connection to the MySQL server.                                     |
| `connect_errno()`            | Returns the error code from the last connection error.                          |
| `connect_error()`            | Returns the error description from the last connection error.                   |
| `data_seek()`                | Adjusts the result pointer to an arbitrary row in the result-set.              |
| `debug()`                    | Performs debugging operations.                                                 |
| `dump_debug_info()`          | Dumps debugging info into the log.                                             |
| `errno()`                    | Returns the last error code for the most recent function call.                 |
| `error()`                    | Returns the last error description for the most recent function call.          |
| `error_list()`               | Returns a list of errors for the most recent function call.                    |
| `fetch_all()`                | Fetches all result rows as an associative array, numeric array, or both.       |
| `fetch_array()`              | Fetches a result row as an associative, numeric array, or both.                |
| `fetch_assoc()`              | Fetches a result row as an associative array.                                  |
| `fetch_field()`              | Returns the next field in the result-set as an object.                         |
| `fetch_field_direct()`       | Returns metadata for a single field in the result-set as an object.            |
| `fetch_fields()`             | Returns an array of objects representing fields in a result-set.              |
| `fetch_lengths()`            | Returns the lengths of the columns of the current row in the result-set.       |
| `fetch_object()`             | Returns the current row of a result-set as an object.                          |
| `fetch_row()`                | Fetches one row from a result-set as an enumerated array.                      |
| `field_count()`              | Returns the number of columns for the most recent query.                       |
| `field_seek()`               | Sets the field cursor to the given field offset.                               |
| `get_charset()`              | Returns a character set object.                                                |
| `get_client_info()`          | Returns the MySQL client library version.                                      |
| `get_client_stats()`         | Returns statistics about client per-process.                                   |
| `get_client_version()`       | Returns the MySQL client library version as an integer.                        |
| `get_connection_stats()`     | Returns statistics about the client connection.                                |
| `get_host_info()`            | Returns the MySQL server hostname and connection type.                         |
| `get_proto_info()`           | Returns the MySQL protocol version.                                            |
| `get_server_info()`          | Returns the MySQL server version.                                              |
| `get_server_version()`       | Returns the MySQL server version as an integer.                                |
| `info()`                     | Returns information about the last executed query.                             |
| `init()`                     | Initializes MySQLi and returns a resource for use with `real_connect()`.       |
| `insert_id()`                | Returns the auto-generated ID from the last query.                             |
| `kill()`                     | Asks the server to kill a MySQL thread.                                        |
| `more_results()`             | Checks if there are more results from a multi-query.                           |
| `multi_query()`              | Performs one or more queries on the database.                                  |
| `next_result()`              | Prepares the next result-set from `multi_query()`.                             |
| `options()`                  | Sets extra connect options affecting connection behavior.                     |
| `ping()`                     | Pings a server connection or tries to reconnect if the connection is down.     |
| `poll()`                     | Polls connections.                                                            |
| `prepare()`                  | Prepares an SQL statement for execution.                                       |
| `query()`                    | Performs a query against a database.                                           |
| `real_connect()`             | Opens a new connection to the MySQL server.                                    |
| `real_escape_string()`       | Escapes special characters in a string for use in an SQL statement.            |
| `real_query()`               | Executes a single SQL query.                                                   |
| `reap_async_query()`         | Returns result from an async SQL query.                                        |
| `refresh()`                  | Refreshes/flushes tables or caches, or resets replication server information.  |
| `rollback()`                 | Rolls back the current transaction for the database.                           |
| `select_db()`                | Selects the default database for database queries.                             |
| `set_charset()`              | Sets the default client character set.                                         |
| `set_local_infile_default()` | Unsets user-defined handler for LOAD DATA LOCAL INFILE command.                |
| `set_local_infile_handler()` | Sets callback function for LOAD DATA LOCAL INFILE command.                     |
| `sqlstate()`                 | Returns the SQLSTATE error code for the error.                                 |
| `ssl_set()`                  | Establishes secure connections using SSL.                                      |
| `stat()`                     | Returns the current system status.                                             |
| `stmt_init()`                | Initializes a statement for use with `stmt_prepare()`.                         |
| `store_result()`             | Transfers a result-set from the last query.                                    |
| `thread_id()`                | Returns the thread ID for the current connection.                              |
| `thread_safe()`              | Returns whether the client library is compiled as thread-safe.                 |
| `use_result()`               | Initiates retrieval of a result-set from the last query executed.              |
| `warning_count()`            | Returns the number of warnings from the last query in the connection.          |

- **mysqli_num_rows()**:
  - Returns the number of rows in a result set.
  - Used to check if data exists in the database.
  - Requires a prior database connection.
  - **Example**:
    ```php
    $result = $conn->query("SELECT * FROM users");
    echo mysqli_num_rows($result); // Outputs number of rows
    ```

## CRUD Operations
- **CRUD**: Stands for Create, Read, Update, and Delete—fundamental database operations.
- Implemented in PHP using SQL statements (`INSERT`, `SELECT`, `UPDATE`, `DELETE`).

### 1. Database Setup
- **Create Database**:
  ```sql
  CREATE DATABASE student_db;
  USE student_db;
  ```
- **Create Table** (`users`):
  ```sql
  CREATE TABLE users (
      id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
      fname VARCHAR(100) NOT NULL,
      lname VARCHAR(100) NOT NULL,
      email VARCHAR(255) NOT NULL,
      password VARCHAR(255) NOT NULL,
      gender VARCHAR(255) NOT NULL
  );
  ```
- Verify table creation:
  ```sql
  SHOW TABLES;
  ```

### 2. Database Connection
- **Code Example** (`connection.php`):
  ```php
  <?php
  $servername = 'localhost';
  $username = 'root';
  $password = '';
  $dbname = 'student_db';

  $conn = new mysqli($servername, $username, $password, $dbname);

  if ($conn->connect_error) {
      exit('Connection failed: ' . $conn->connect_error);
  }
  ?>
  ```

### 3. Create Operation (Form and Processing)
- **Form Interface** (`signup.html`):
  ```html
  <!DOCTYPE html>
  <html>
  <body>
      <h2>Signup Form</h2>
      <form action="create.php" method="POST">
          <fieldset>
              <legend>Personal information:</legend>
              First name:<br>
              <input type="text" name="firstname"><br>
              Last name:<br>
              <input type="text" name="lastname"><br>
              Email:<br>
              <input type="email" name="email"><br>
              Password:<br>
              <input type="password" name="password"><br>
              Gender:<br>
              <input type="radio" name="gender" value="Male">Male
              <input type="radio" name="gender" value="Female">Female<br><br>
              <input type="submit" name="submit" value="Submit">
          </fieldset>
      </form>
  </body>
  </html>
  ```
- **Create Record** (`create.php`):
  ```php
  <?php
  include 'connection.php';
  if (isset($_POST['submit'])) {
      $first_name = $_POST['firstname'];
      $last_name = $_POST['lastname'];
      $email = $_POST['email'];
      $password = $_POST['password'];
      $gender = $_POST['gender'];

      $sql = "INSERT INTO users (fname, lname, email, password, gender) VALUES ('$first_name', '$last_name', '$email', '$password', '$gender')";
      $result = $conn->query($sql);

      if ($result == true) {
          echo 'New record created successfully.';
      } else {
          echo 'Error: ' . $sql . '<br>' . $conn->error;
      }
      $conn->close();
  }
  ?>
  <html>
      <a class="btn btn-info" href="signup.html"><br><br>Back</a>
      <a class="btn btn-info" href="read.php"><br><br>View record from database</a>
  </html>
  ```
- **Security Note**: Use prepared statements to prevent SQL injection (example below).

### 4. Read Operation
- **Read Records** (`read.php`):
  ```php
  <?php
  include 'connection.php';
  $sql = 'SELECT * FROM users';
  $result = $conn->query($sql);
  ?>
  <html>
  <head>
      <title>View Page</title>
      <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.0/css/bootstrap.min.css">
  </head>
  <body>
      <div class="container">
          <h2>Users</h2>
          <table class="table">
              <thead>
                  <tr>
                      <th>ID</th>
                      <th>First Name</th>
                      <th>Last Name</th>
                      <th>Email</th>
                      <th>Gender</th>
                      <th>Action</th>
                  </tr>
              </thead>
              <tbody>
                  <?php
                  if ($result->num_rows > 0) {
                      while ($row = $result->fetch_assoc()) {
                  ?>
                  <tr>
                      <td><?php echo $row['id']; ?></td>
                      <td><?php echo $row['fname']; ?></td>
                      <td><?php echo $row['lname']; ?></td>
                      <td><?php echo $row['email']; ?></td>
                      <td><?php echo $row['gender']; ?></td>
                      <td>
                          <a class="btn btn-info" href="update.php?id=<?php echo $row['id']; ?>">Edit</a>
                          <a class="btn btn-danger" href="delete.php?id=<?php echo $row['id']; ?>">Delete</a>
                      </td>
                  </tr>
                  <?php
                      }
                  }
                  ?>
              </tbody>
          </table>
      </div>
  </body>
  </html>
  ```

### 5. Update Operation
- **Update Form** (`update.php`):
  ```php
  <?php
  include 'connection.php';
  $id = $_GET['id'];
  $sql = "SELECT * FROM users WHERE id = ?";
  $stmt = $conn->prepare($sql);
  $stmt->bind_param("i", $id);
  $stmt->execute();
  $result = $stmt->get_result();
  $row = $result->fetch_assoc();
  ?>
  <!DOCTYPE html>
  <html>
  <body>
      <h2>Update User</h2>
      <form action="update.php" method="POST">
          <input type="hidden" name="id" value="<?php echo $row['id']; ?>">
          <fieldset>
              <legend>Personal information:</legend>
              First name:<br>
              <input type="text" name="firstname" value="<?php echo $row['fname']; ?>"><br>
              Last name:<br>
              <input type="text" name="lastname" value="<?php echo $row['lname']; ?>"><br>
              Email:<br>
              <input type="email" name="email" value="<?php echo $row['email']; ?>"><br>
              Password:<br>
              <input type="password" name="password" value="<?php echo $row['password']; ?>"><br>
              Gender:<br>
              <input type="radio" name="gender" value="Male" <?php if ($row['gender'] == 'Male') echo 'checked'; ?>>Male
              <input type="radio" name="gender" value="Female" <?php if ($row['gender'] == 'Female') echo 'checked'; ?>>Female<br><br>
              <input type="submit" name="submit" value="Update">
          </fieldset>
      </form>
  </body>
  </html>
  <?php
  if (isset($_POST['submit'])) {
      $id = $_POST['id'];
      $first_name = $_POST['firstname'];
      $last_name = $_POST['lastname'];
      $email = $_POST['email'];
      $password = $_POST['password'];
      $gender = $_POST['gender'];

      $sql = "UPDATE users SET fname = ?, lname = ?, email = ?, password = ?, gender = ? WHERE id = ?";
      $stmt = $conn->prepare($sql);
      $stmt->bind_param("sssssi", $first_name, $last_name, $email, $password, $gender, $id);
      if ($stmt->execute()) {
          echo "Record updated successfully.";
          header("Location: read.php");
      } else {
          echo "Error updating record: " . $conn->error;
      }
      $stmt->close();
      $conn->close();
  }
  ?>
  ```

### 6. Delete Operation
- **Delete Record** (`delete.php`):
  ```php
  <?php
  include 'connection.php';
  $id = $_GET['id'];
  $sql = "DELETE FROM users WHERE id = ?";
  $stmt = $conn->prepare($sql);
  $stmt->bind_param("i", $id);
  if ($stmt->execute()) {
      echo "Record deleted successfully.";
      header("Location: read.php");
  } else {
      echo "Error deleting record: " . $conn->error;
  }
  $stmt->close();
  $conn->close();
  ?>
  ```

## Practical Notes
- **Security**:
  - Use prepared statements (`prepare()`, `bind_param()`) to prevent SQL injection.
  - Hash passwords using `password_hash()` before storing them.
  - Validate and sanitize user inputs to ensure data integrity.
  - Use HTTPS for secure data transmission.
- **Best Practices**:
  - Store database credentials in a separate configuration file (`connection.php`).
  - Close database connections and statements after use (`$conn->close()`, `$stmt->close()`).
  - Use Bootstrap or other CSS frameworks for better form and table styling.
  - Implement error handling for all database operations.
- **Form Handling**:
  - Use `method="POST"` for sensitive data to avoid URL exposure.
  - Validate form submissions using `isset($_POST['submit'])` or similar checks.
  - Use `$_GET` for non-sensitive operations like retrieving records for editing or deletion.
- **Testing**:
  - Test CRUD operations with sample data to verify functionality.
  - Check edge cases (e.g., empty inputs, invalid emails, duplicate records).
  - Ensure redirects (`header()`) work correctly after operations.