# PL/pgSQL Procedural Language Notes

## Summary
PL/pgSQL (Procedural Language/PostgreSQL) is a powerful procedural language that extends PostgreSQL’s SQL capabilities with control structures, functions, and stored procedures. These notes provide a beginner-friendly guide to PL/pgSQL’s characteristics, block structure, operators, variables, control structures, and practical examples, with exercises for revision.

## PL/pgSQL Overview
### Definition
PL/pgSQL is a procedural language for PostgreSQL, enabling complex logic, control flow (e.g., if-else, loops), and error handling. Similar to Oracle’s PL/SQL, it supports user-defined functions and stored procedures for advanced database operations.

### Characteristics
- **Extending SQL**: Adds procedural capabilities like conditionals, loops, and exception handling.
- **User-Defined Functions/Procedures**: Encapsulates reusable logic within the database.
- **SQL Integration**: Seamlessly interacts with SQL for direct table operations.
- **Data Type Inheritance**: Uses PostgreSQL’s user-defined types, functions, and operators.
- **Security**: Supports trusted/untrusted functions to control access levels.

### Advantages
- **Reduced Network Traffic**: Groups SQL statements into functions/procedures, minimizing client-server round trips.
- **Improved Efficiency**: Performs complex calculations server-side, reducing client workload.
- **Code Reusability**: Encapsulates logic for reuse across applications.
- **Enhanced Functionality**: Supports complex logic not possible with plain SQL.
- **Database Integrity**: Enforces data constraints within the database.
- **Security**: Trusted/untrusted functions reduce SQL injection risks.
- **Procedural Capabilities**: Supports loops, conditionals, and exception handling.

### Disadvantages
- **Portability**: Specific to PostgreSQL, limiting use in other databases.
- **Complexity**: More complex than SQL for developers unfamiliar with procedural programming.
- **Debugging**: Challenging due to complex logic and limited tooling.
- **Performance**: Poorly written code can degrade performance for large datasets.
- **Limited Tooling**: Fewer IDEs/support compared to SQL.
- **Maintenance**: Complex codebases can reduce readability and maintainability.

### Applications
- **Business Logic**: Implements calculations, validations, and rules.
- **Data Transformation**: Cleansing, enrichment, and derived data creation.
- **Data Migration**: Transfers data between systems/formats.
- **ETL Processes**: Supports extract, transform, load workflows.
- **Data Validation**: Enforces integrity constraints.
- **Stored Procedures**: Encapsulates database operations for performance.
- **Reporting**: Generates reports with complex transformations.
- **Data Warehousing**: Handles data loading and aggregation.
- **Geospatial Processing**: Combines with PostGIS for spatial analysis.
- **Triggers**: Automates tasks and enforces rules on data changes.
- **Security**: Implements access control, auditing, and logging.

## PL/pgSQL Block Structure
### Types of Blocks
- **Anonymous Blocks**: Executed once using `DO`, not stored.
- **Named Blocks**: Functions or stored procedures, stored and reusable.

### Anonymous Block Structure
- **Syntax**:
  ```sql
  DO $$
  [ <<label>> ]
  DECLARE
      /* Variable declarations */
  BEGIN
      /* Executable statements */
  EXCEPTION
      /* Exception handling */
  END [ label ];
  $$;
  ```
- **Explanation**:
  - `DO`: Initiates anonymous block.
  - `$$`: Delimiters for PL/pgSQL code (customizable).
  - `DECLARE`: Optional variable declarations.
  - `BEGIN...END`: Required executable section.
  - `EXCEPTION`: Optional error handling.

### Named Block Structure
- **Syntax**:
  ```sql
  CREATE FUNCTION function_name() RETURNS return_type AS $$
  [ <<label>> ]
  DECLARE
      /* Variable declarations */
  BEGIN
      /* Executable statements */
  EXCEPTION
      /* Exception handling */
  END [ label ];
  $$ LANGUAGE plpgsql;
  ```
- **Example**:
  ```sql
  CREATE FUNCTION add_numbers(a INT, b INT) RETURNS INT AS $$
  BEGIN
      RETURN a + b;
  END;
  $$ LANGUAGE plpgsql;
  SELECT add_numbers(5, 3); -- Returns 8
  ```

## Operators
PL/pgSQL supports operators similar to SQL:
- **Arithmetic**: `+`, `-`, `*`, `/`, `%` (modulo).
- **Comparison**: `=`, `<>`, `!=`, `<`, `<=`, `>`, `>=`.
- **Logical**: `AND`, `OR`, `NOT`.
- **Concatenation**: `||` (e.g., `'Hello' || ' World'`).
- **Assignment**: `:=` or `=` (e.g., `x := 10`).

## Comments
- **Single-Line**: `-- Comment text`
- **Multi-Line**: `/* Comment text */`
- **Example**:
  ```sql
  DO $$
  BEGIN
      -- Print a message
      RAISE NOTICE 'Starting execution';
      /* Multi-line comment
         for detailed explanation */
  END;
  $$;
  ```

## Variables
Variables store values that can change within a block, always associated with a data type.
- **Syntax**:
  ```sql
  variable_name data_type := expression;
  ```
- **%TYPE**: Inherits a column’s or variable’s data type.
  ```sql
  variable_name table_name.column_name%TYPE;
  ```
- **%ROWTYPE**: Stores a table row’s structure.
  ```sql
  row_variable table_name%ROWTYPE;
  ```
- **Record Type**: Stores a single row without predefined structure.
  ```sql
  variable_name RECORD;
  ```

### Examples
- **Basic Variable**:
  ```sql
  DO $$
  DECLARE
      counter INT := 0;
  BEGIN
      counter := counter + 1;
      RAISE NOTICE 'Counter: %', counter;
  END;
  $$;
  ```
- **%TYPE**:
  ```sql
  DO $$
  DECLARE
      emp_name employees.name%TYPE;
  BEGIN
      SELECT name INTO emp_name FROM employees WHERE emp_id = 1;
      RAISE NOTICE 'Employee Name: %', emp_name;
  END;
  $$;
  ```
- **%ROWTYPE**:
  ```sql
  DO $$
  DECLARE
      emp_row employees%ROWTYPE;
  BEGIN
      SELECT * INTO emp_row FROM employees WHERE emp_id = 1;
      RAISE NOTICE 'Employee: %, Dept: %', emp_row.name, emp_row.dept_id;
  END;
  $$;
  ```
- **Record Type**:
  ```sql
  DO $$
  DECLARE
      emp_record RECORD;
  BEGIN
      SELECT emp_id, name INTO emp_record FROM employees WHERE emp_id = 1;
      RAISE NOTICE 'ID: %, Name: %', emp_record.emp_id, emp_record.name;
  END;
  $$;
  ```

## Control Structures
PL/pgSQL supports conditional and looping structures for managing code execution.

### Conditional Statements
- **IF-THEN**:
  ```sql
  IF condition THEN
      statements;
  END IF;
  ```
- **IF-THEN-ELSE**:
  ```sql
  IF condition THEN
      statements;
  ELSE
      additional_statements;
  END IF;
  ```
- **IF-THEN-ELSIF**:
  ```sql
  IF condition1 THEN
      statements;
  ELSIF condition2 THEN
      statements;
  ELSE
      additional_statements;
  END IF;
  ```
- **CASE**:
  ```sql
  CASE expression
      WHEN value1 THEN statements;
      WHEN value2 THEN statements;
      ELSE statements;
  END CASE;
  ```

### Looping Statements
- **LOOP**: Unconditional loop, exits with `EXIT`.
  ```sql
  LOOP
      statements;
      EXIT WHEN condition;
  END LOOP;
  ```
- **WHILE**: Loops while a condition is true.
  ```sql
  WHILE condition LOOP
      statements;
  END LOOP;
  ```
- **FOR**: Iterates over a range or query result.
  ```sql
  FOR variable IN range LOOP
      statements;
  END LOOP;
  -- Or for query
  FOR variable IN SELECT query LOOP
      statements;
  END LOOP;
  ```
- **FOREACH**: Iterates over array elements.
  ```sql
  FOREACH element IN ARRAY array_name LOOP
      statements;
  END LOOP;
  ```

### Examples
- **IF-THEN Example** (Add commission for salesman_id = 5000):
  ```sql
  DO $$
  DECLARE
      v_salesman_id INT := 5000;
  BEGIN
      IF v_salesman_id = 5000 THEN
          UPDATE salesman SET commission = commission + 100;
          RAISE NOTICE 'Added 100 to commission for salesman_id 5000';
      END IF;
  END;
  $$;
  ```
- **IF-THEN-ELSE Example** (Add commission based on salesman_id):
  ```sql
  DO $$
  DECLARE
      v_salesman_id INT := 6000;
  BEGIN
      IF v_salesman_id > 5000 THEN
          UPDATE salesman SET commission = commission + 100;
          RAISE NOTICE 'Added 100 to commission for salesman_id %', v_salesman_id;
      ELSE
          UPDATE salesman SET commission = commission + 200;
          RAISE NOTICE 'Added 200 to commission for salesman_id %', v_salesman_id;
      END IF;
  END;
  $$;
  ```
- **Count Commissions Example**:
  ```sql
  DO $$
  DECLARE
      total_commissions INT;
  BEGIN
      SELECT COUNT(commission) INTO total_commissions FROM salesman;
      RAISE NOTICE 'Total number of commissions: %', total_commissions;
  END;
  $$;
  ```

## Exercises
1. **Anonymous Block**:
   - Write a PL/pgSQL anonymous block to calculate the square of a number (e.g., 5).
     ```sql
     DO $$
     DECLARE
         num INT := 5;
         result INT;
     BEGIN
         result := num * num;
         RAISE NOTICE 'Square of % is %', num, result;
     END;
     $$;
     ```
2. **Function Creation**:
   - Create a function to return the total number of rows in a `users` table.
     ```sql
     CREATE FUNCTION count_users() RETURNS INT AS $$
     DECLARE
         total INT;
     BEGIN
         SELECT COUNT(*) INTO total FROM users;
         RETURN total;
     END;
     $$ LANGUAGE plpgsql;
     SELECT count_users();
     ```
3. **%TYPE Variable**:
   - Write a block to display an employee’s name and city using %TYPE.
     ```sql
     DO $$
     DECLARE
         v_name employees.name%TYPE;
         v_city employees.city%TYPE;
     BEGIN
         SELECT name, city INTO v_name, v_city FROM employees WHERE emp_id = 1;
         RAISE NOTICE 'Employee: %, City: %', v_name, v_city;
     END;
     $$;
     ```
4. **%ROWTYPE**:
   - Use %ROWTYPE to fetch and display a row from a `salesman` table.
     ```sql
     DO $$
     DECLARE
         salesman_row salesman%ROWTYPE;
     BEGIN
         SELECT * INTO salesman_row FROM salesman WHERE salesman_id = 5000;
         RAISE NOTICE 'Salesman: %, Commission: %', salesman_row.name, salesman_row.commission;
     END;
     $$;
     ```
5. **Control Structure**:
   - Write a function to categorize salesman commission: ‘High’ (>0.2), ‘Medium’ (0.1–0.2), ‘Low’ (<0.1).
     ```sql
     CREATE FUNCTION categorize_commission(salesman_id INT) RETURNS TEXT AS $$
     DECLARE
         v_commission salesman.commission%TYPE;
         category TEXT;
     BEGIN
         SELECT commission INTO v_commission FROM salesman WHERE salesman_id = salesman_id;
         CASE
             WHEN v_commission > 0.2 THEN category := 'High';
             WHEN v_commission BETWEEN 0.1 AND 0.2 THEN category := 'Medium';
             ELSE category := 'Low';
         END CASE;
         RETURN category;
     END;
     $$ LANGUAGE plpgsql;
     ```

## References
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- Provided PL/pgSQL content.