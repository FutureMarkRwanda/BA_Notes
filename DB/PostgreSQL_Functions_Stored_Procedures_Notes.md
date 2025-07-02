# PostgreSQL Functions and Stored Procedures Notes

## Summary
PostgreSQL user-defined functions (UDFs) and stored procedures extend database functionality by encapsulating reusable logic and complex operations. These notes provide a beginner-friendly guide to UDFs and stored procedures, covering their definitions, benefits, disadvantages, syntax, parameter modes, calling methods, and management, with practical PL/pgSQL examples and exercises for revision.

## User-Defined Functions (UDFs)
### Definition
UDFs are custom functions created by users to perform specific tasks or calculations in PostgreSQL, reusable within queries like built-in functions. They encapsulate SQL or PL/pgSQL logic to extend database capabilities.

### Benefits
- **Code Reusability**: Encapsulates logic for reuse across queries/applications.
- **Performance Optimization**: Pre-compiled execution plans reduce overhead.
- **Security**: Encapsulates sensitive logic, reducing SQL injection risks.
- **Modularity**: Breaks complex tasks into manageable units.
- **Abstraction**: Hides implementation details, simplifying queries.
- **Ease of Maintenance**: Centralized updates ensure consistency.
- **Cross-Platform Compatibility**: Portable to systems supporting PL/pgSQL, PL/Python, etc.
- **Parameterized Input**: Accepts parameters for flexible logic.
- **Extended Functionality**: Supports custom calculations, transformations, and validations.

### Disadvantages
- **Performance Overhead**: Poorly designed functions may slow execution.
- **Debugging Complexity**: Harder to debug than SQL queries.
- **Dependency Management**: Dependencies on tables/views require careful handling.
- **Limited Portability**: PL/pgSQL-specific code may not transfer to other DBMS.
- **Potential Complexity**: Complex logic can reduce readability.
- **Versioning Challenges**: Managing updates across environments is complex.
- **Security Risks**: Vulnerable if not properly validated/secured.
- **Learning Curve**: Requires proficiency in procedural languages.

### Syntax
```sql
CREATE OR REPLACE FUNCTION function_name (argument_name data_type)
RETURNS data_type AS $$
DECLARE
    -- Variable declarations
BEGIN
    -- Function body
END;
$$ LANGUAGE plpgsql;
```
- **CREATE OR REPLACE**: Creates or updates the function.
- **function_name**: Unique function name.
- **argument_name data_type**: Input parameters (optional).
- **RETURNS data_type**: Specifies return type.
- **LANGUAGE plpgsql**: Uses PL/pgSQL (other options: SQL, PL/Python, etc.).

### Parameter Modes
- **IN**: Read-only input (default).
- **OUT**: Write-only, returns values.
- **INOUT**: Read and write, modifies input for return.

### Calling Methods
- **Positional Notation**: Arguments in defined order.
  ```sql
  SELECT my_function(1, 2);
  ```
- **Named Notation**: Specify parameter names.
  ```sql
  SELECT my_function(arg1 => 1, arg2 => 2);
  ```
- **Mixed Notation**: Combine positional and named.
  ```sql
  SELECT my_function(1, arg2 => 2);
  ```

### Examples
1. **Sum of Two Integers**:
   ```sql
   CREATE OR REPLACE FUNCTION add_numbers(a INT, b INT) RETURNS INT AS $$
   BEGIN
       RETURN a + b;
   END;
   $$ LANGUAGE plpgsql;
   -- Call
   SELECT add_numbers(5, 3); -- Returns 8
   ```

2. **Area of a Circle**:
   ```sql
   CREATE OR REPLACE FUNCTION circle_area(radius FLOAT) RETURNS FLOAT AS $$
   BEGIN
       RETURN 3.14159 * radius * radius;
   END;
   $$ LANGUAGE plpgsql;
   -- Call
   SELECT circle_area(5); -- Returns ~78.53975
   ```

3. **Factorial of a Number**:
   ```sql
   CREATE OR REPLACE FUNCTION factorial(n INT) RETURNS BIGINT AS $$
   DECLARE
       result BIGINT := 1;
       i INT;
   BEGIN
       FOR i IN 1..n LOOP
           result := result * i;
       END LOOP;
       RETURN result;
   END;
   $$ LANGUAGE plpgsql;
   -- Call
   SELECT factorial(5); -- Returns 120
   ```

4. **Count Employees**:
   ```sql
   CREATE OR REPLACE FUNCTION count_employees() RETURNS INT AS $$
   DECLARE
       emp_count INT;
   BEGIN
       SELECT COUNT(*) INTO emp_count FROM employees;
       RETURN emp_count;
   END;
   $$ LANGUAGE plpgsql;
   -- Call
   SELECT count_employees();
   ```

5. **Employee Name**:
   ```sql
   CREATE OR REPLACE FUNCTION get_employee_name(emp_id INT) RETURNS TEXT AS $$
   DECLARE
       full_name TEXT;
   BEGIN
       SELECT first_name || ' ' || last_name INTO full_name
       FROM employees WHERE employee_id = emp_id;
       RETURN full_name;
   END;
   $$ LANGUAGE plpgsql;
   -- Call
   SELECT get_employee_name(1);
   ```

6. **Add Employee (IN Parameters)**:
   ```sql
   CREATE OR REPLACE FUNCTION add_employee(
       p_first_name VARCHAR,
       p_last_name VARCHAR,
       p_email VARCHAR,
       p_hire_date DATE,
       p_salary NUMERIC
   ) RETURNS VOID AS $$
   BEGIN
       INSERT INTO employees (first_name, last_name, email, hire_date, salary)
       VALUES (p_first_name, p_last_name, p_email, p_hire_date, p_salary);
   END;
   $$ LANGUAGE plpgsql;
   -- Call
   SELECT add_employee('Dan', 'Uwamungu', 'u@gmail.com', '2024-04-09', 200000);
   ```

7. **OUT Parameter Example**:
   ```sql
   CREATE OR REPLACE FUNCTION get_employee_info(emp_id INT, OUT emp_name TEXT, OUT emp_salary NUMERIC) AS $$
   BEGIN
       SELECT first_name || ' ' || last_name, salary
       INTO emp_name, emp_salary
       FROM employees WHERE employee_id = emp_id;
   END;
   $$ LANGUAGE plpgsql;
   -- Call
   SELECT * FROM get_employee_info(1);
   ```

8. **INOUT Parameter Example**:
   ```sql
   CREATE OR REPLACE FUNCTION increment_salary(emp_id INT, INOUT emp_salary NUMERIC) AS $$
   BEGIN
       SELECT salary + 1000 INTO emp_salary
       FROM employees WHERE employee_id = emp_id;
   END;
   $$ LANGUAGE plpgsql;
   -- Call
   SELECT increment_salary(1, 50000); -- Returns 51000
   ```

## Stored Procedures
### Definition
Stored procedures are reusable, named blocks of PL/pgSQL or SQL code stored in the database, designed to execute tasks (e.g., data manipulation, transaction control). Unlike UDFs, they support explicit transaction management and do not require a return value.

### Benefits
- **Code Reusability**: Encapsulates logic for reuse.
- **Performance Optimization**: Pre-compiled for efficiency.
- **Security/Access Control**: Granular permissions for execution.
- **Modularity**: Organizes complex operations.
- **Encapsulation**: Hides complex logic.
- **Input/Output Parameters**: Flexible with IN/INOUT modes.
- **Transaction Control**: Supports `BEGIN`, `COMMIT`, `ROLLBACK`.

### Disadvantages
- **Debugging**: Harder than application code due to limited tools.
- **Maintenance**: Complex procedures are hard to update.
- **Resource Utilization**: May consume significant CPU/memory.
- **Concurrency Issues**: Risk of deadlocks with poor design.
- **Developer Skill Set**: Requires PL/pgSQL expertise.
- **Deployment Complexity**: Coordinating changes with schema/application.
- **Security Concerns**: Vulnerable to SQL injection if not secured.
- **Migration Difficulties**: Changes require careful handling.

### Syntax
```sql
CREATE [OR REPLACE] PROCEDURE procedure_name(parameter_list)
LANGUAGE plpgsql
AS $$
DECLARE
    -- Variable declarations
BEGIN
    -- Procedure body
END;
$$;
```
- **CREATE OR REPLACE**: Creates or updates the procedure.
- **procedure_name**: Unique name.
- **parameter_list**: IN or INOUT parameters (OUT not supported).
- **LANGUAGE plpgsql**: Uses PL/pgSQL.
- **No RETURN**: Procedures do not return values like functions.

### Differences from UDFs
| Feature                | Stored Procedure                       | User-Defined Function (UDF)           |
|------------------------|----------------------------------------|---------------------------------------|
| **Purpose**            | Executes tasks, complex logic          | Returns a value for queries           |
| **Return Values**      | No return value (or OUT/INOUT)        | Must return a specific data type      |
| **Calling Mechanism**  | `CALL procedure_name()`               | `SELECT function_name()`              |
| **Functionality**      | DML, control flow, transactions        | Calculations, transformations          |
| **Transactions**       | Explicit `COMMIT`/`ROLLBACK`           | Inherits caller’s transaction         |
| **Error Handling**     | Robust with `EXCEPTION`                | Limited error handling                |
| **Security**           | Granular permissions                   | Inherits creator’s permissions        |
| **Performance**        | Pre-compiled, efficient for tasks      | Compiled at runtime, may be slower    |

### Examples
1. **Add Account Record**:
   ```sql
   CREATE OR REPLACE PROCEDURE add_account(
       p_name VARCHAR,
       p_balance NUMERIC
   )
   LANGUAGE plpgsql
   AS $$
   BEGIN
       INSERT INTO accounts (name, balance)
       VALUES (p_name, p_balance);
       COMMIT;
   END;
   $$;
   -- Call
   CALL add_account('Kabanda', 40000);
   ```

2. **Update Account Balance**:
   ```sql
   CREATE OR REPLACE PROCEDURE update_account_balance(
       p_account_id INT,
       p_new_balance NUMERIC
   )
   LANGUAGE plpgsql
   AS $$
   BEGIN
       UPDATE accounts
       SET balance = p_new_balance
       WHERE account_id = p_account_id;
       COMMIT;
   END;
   $$;
   -- Call
   CALL update_account_balance(1, 55000);
   ```

3. **Delete Account Record**:
   ```sql
   CREATE OR REPLACE PROCEDURE delete_account(p_account_id INT)
   LANGUAGE plpgsql
   AS $$
   BEGIN
       DELETE FROM accounts WHERE account_id = p_account_id;
       COMMIT;
   END;
   $$;
   -- Call
   CALL delete_account(1);
   ```

## Managing Functions
### Listing Functions
- **Command**:
  ```sql
  \df
  ```
- Lists all user-defined functions in the current database.

### Modifying Functions
- **Syntax**:
  ```sql
  ALTER FUNCTION function_name(parameter_list) RENAME TO new_function_name;
  -- Or other options: LEAKPROOF, IMMUTABLE, STABLE, SECURITY, etc.
  ```
- **Example**:
  ```sql
  ALTER FUNCTION factorial(INT) RENAME TO calc_factorial;
  ```

### Dropping Functions
- **Syntax**:
  ```sql
  DROP FUNCTION [IF EXISTS] function_name (parameter_data_types);
  ```
- **Example**:
  ```sql
  DROP FUNCTION IF EXISTS calc_factorial(INT);
  ```

### Function Privileges
- **Grant Privileges**:
  ```sql
  GRANT EXECUTE ON FUNCTION my_function TO user_name;
  GRANT USAGE ON FUNCTION my_function TO user_name;
  GRANT ALL PRIVILEGES ON FUNCTION my_function TO user_name WITH GRANT OPTION;
  ```
- **Revoke Privileges**:
  ```sql
  REVOKE EXECUTE ON FUNCTION my_function FROM user_name;
  ```
- **Example**:
  ```sql
  GRANT EXECUTE ON FUNCTION add_numbers TO app_user;
  ```

## Exercises
1. **Function Creation**:
   - Create a function to multiply two numbers without parameters (hardcode values).
     ```sql
     CREATE OR REPLACE FUNCTION multiply_numbers() RETURNS INT AS $$
     DECLARE
         a INT := 4;
         b INT := 5;
     BEGIN
         RETURN a * b;
     END;
     $$ LANGUAGE plpgsql;
     -- Call
     SELECT multiply_numbers(); -- Returns 20
     ```

2. **INOUT Parameter Function**:
   - Create a function to double a given salary and return it.
     ```sql
     CREATE OR REPLACE FUNCTION double_salary(INOUT p_salary NUMERIC) AS $$
     BEGIN
         p_salary := p_salary * 2;
     END;
     $$ LANGUAGE plpgsql;
     -- Call
     SELECT double_salary(50000); -- Returns 100000
     ```

3. **Stored Procedure**:
   - Create a procedure to insert a new employee with first_name, last_name, and salary.
     ```sql
     CREATE OR REPLACE PROCEDURE add_new_employee(
         p_first_name VARCHAR,
         p_last_name VARCHAR,
         p_salary NUMERIC
     )
     LANGUAGE plpgsql
     AS $$
     BEGIN
         INSERT INTO employees (first_name, last_name, salary)
         VALUES (p_first_name, p_last_name, p_salary);
         COMMIT;
     END;
     $$;
     -- Call
     CALL add_new_employee('Jane', 'Doe', 75000);
     ```

4. **Function with Named Notation**:
   - Create a function to calculate total cost (quantity * price) using named notation.
     ```sql
     CREATE OR REPLACE FUNCTION calculate_cost(quantity INT, price NUMERIC) RETURNS NUMERIC AS $$
     BEGIN
         RETURN quantity * price;
     END;
     $$ LANGUAGE plpgsql;
     -- Call
     SELECT calculate_cost(quantity => 10, price => 25.50); -- Returns 255.00
     ```

5. **Manage Function**:
   - Create a function, grant EXECUTE to a role, and rename it.
     ```sql
     CREATE OR REPLACE FUNCTION simple_count() RETURNS INT AS $$
     BEGIN
         RETURN (SELECT COUNT(*) FROM accounts);
     END;
     $$ LANGUAGE plpgsql;
     GRANT EXECUTE ON FUNCTION simple_count TO analyst;
     ALTER FUNCTION simple_count() RENAME TO account_count;
     ```

## References
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- Provided PostgreSQL content on functions and stored procedures.