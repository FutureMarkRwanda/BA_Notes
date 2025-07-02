# PL/pgSQL CASE and Looping Statements Notes

## Summary
These notes cover PL/pgSQL’s CASE statement for conditional logic and looping statements (LOOP, WHILE, FOR) for iterative execution, along with the CONTINUE statement for skipping loop iterations. Designed for beginners, they include detailed syntax, explanations, PostgreSQL-specific examples, and exercises for revision, focusing on database development concepts.

## CASE Statement
The CASE statement in PL/pgSQL enables conditional logic, similar to switch statements in other programming languages. It evaluates conditions and returns corresponding results. It has two forms: **Simple CASE** and **Searched CASE**.

### Simple CASE
Evaluates a single expression against multiple values.
- **Syntax**:
  ```sql
  CASE expression
      WHEN value1 THEN result1
      WHEN value2 THEN result2
      ...
      ELSE default_result
  END;
  ```
- **Explanation**:
  - `expression`: The value to evaluate.
  - `WHEN value THEN result`: Returns `result` if `expression` matches `value`.
  - `ELSE default_result`: Optional; returns if no conditions match.
  - `END`: Closes the CASE statement.

- **Example**: Display grade status based on a score.
  ```sql
  DO $$
  DECLARE
      score INT := 85;
      grade_status TEXT;
  BEGIN
      grade_status := CASE score
          WHEN 100 THEN 'Perfect'
          WHEN 90 THEN 'Excellent'
          WHEN 80 THEN 'Good'
          ELSE 'Average'
      END;
      RAISE NOTICE 'Score: %, Status: %', score, grade_status;
  END;
  $$;
  -- Output: Score: 85, Status: Average
  ```

- **Example**: Update employee salaries (20% increase for salaries between 50,000 and 55,000).
  ```sql
  DO $$
  BEGIN
      UPDATE employees
      SET salary = CASE
          WHEN salary BETWEEN 50000 AND 55000 THEN salary * 1.20
          ELSE salary
      END;
      RAISE NOTICE 'Salaries updated';
  END;
  $$;
  ```

### Searched CASE
Evaluates independent boolean conditions, not tied to a single expression.
- **Syntax**:
  ```sql
  CASE
      WHEN condition1 THEN expression1
      WHEN condition2 THEN expression2
      ...
      ELSE default_expression
  END;
  ```
- **Explanation**:
  - `WHEN condition THEN expression`: Returns `expression` if `condition` is true.
  - `ELSE default_expression`: Optional; returns if no conditions are true.
  - `END`: Closes the CASE statement.

- **Example**: Categorize students based on scores.
  ```sql
  SELECT student_id, name, score,
         CASE
             WHEN score > 90 THEN 'Excellent'
             WHEN score BETWEEN 80 AND 90 THEN 'Good'
             ELSE 'Average'
         END AS category
  FROM students;
  ```

- **Example**: Increase student scores (1.1 for >90, 1.05 for 80–89).
  ```sql
  UPDATE students
  SET score = CASE
      WHEN score > 90 THEN score * 1.1
      WHEN score BETWEEN 80 AND 89 THEN score * 1.05
      ELSE score
  END;
  ```

### CASE with Aggregate Functions
Combines CASE with aggregates (e.g., COUNT, SUM) for conditional aggregation.
- **Example**: Count employees by salary range.
  ```sql
  SELECT
      COUNT(CASE WHEN salary < 50000 THEN 1 END) AS low_salary,
      COUNT(CASE WHEN salary BETWEEN 50000 AND 75000 THEN 1 END) AS mid_salary,
      COUNT(CASE WHEN salary > 75000 THEN 1 END) AS high_salary
  FROM employees;
  ```

## Looping Statements
PL/pgSQL supports looping constructs for repetitive execution: LOOP, WHILE, and FOR loops.

### Unconditional LOOP
Executes statements until terminated by an `EXIT` or `RETURN` statement.
- **Syntax**:
  ```sql
  <<label>>
  LOOP
      statements;
      IF condition THEN
          EXIT;
      END IF;
  END LOOP;
  ```
- **Notes**:
  - Requires a termination condition to avoid infinite loops.
  - Include increment/decrement to update loop variables.
- **Example**: Print numbers 1 to 5.
  ```sql
  DO $$
  DECLARE
      counter INT := 1;
  BEGIN
      LOOP
          RAISE NOTICE 'Number: %', counter;
          counter := counter + 1;
          EXIT WHEN counter > 5;
      END LOOP;
  END;
  $$;
  -- Output: Number: 1, Number: 2, ..., Number: 5
  ```
- **Example**: Print numbers 10 to 1.
  ```sql
  DO $$
  DECLARE
      counter INT := 10;
  BEGIN
      LOOP
          RAISE NOTICE 'Number: %', counter;
          counter := counter - 1;
          EXIT WHEN counter < 1;
      END LOOP;
  END;
  $$;
  -- Output: Number: 10, Number: 9, ..., Number: 1
  ```

### WHILE Loop
Repeats as long as a condition is true.
- **Syntax**:
  ```sql
  WHILE condition LOOP
      statements;
      increment/decrement;
  END LOOP;
  ```
- **Example**: Display numbers 1 to 10.
  ```sql
  DO $$
  DECLARE
      counter INT := 1;
  BEGIN
      WHILE counter <= 10 LOOP
          RAISE NOTICE 'Number: %', counter;
          counter := counter + 1;
      END LOOP;
  END;
  $$;
  -- Output: Number: 1, Number: 2, ..., Number: 10
  ```

### FOR Loop
Iterates over a range of values or query results.
- **Syntax (Range)**:
  ```sql
  <<label>>
  FOR loop_cnt IN [REVERSE] from..to [BY step] LOOP
      statements;
  END LOOP;
  ```
- **Syntax (Query)**:
  ```sql
  FOR variable IN SELECT query LOOP
      statements;
  END LOOP;
  ```
- **Example**: Display numbers 1 to 10.
  ```sql
  DO $$
  BEGIN
      FOR i IN 1..10 LOOP
          RAISE NOTICE 'Number: %', i;
      END LOOP;
  END;
  $$;
  -- Output: Number: 1, Number: 2, ..., Number: 10
  ```
- **Example**: Display numbers 10 to 1.
  ```sql
  DO $$
  BEGIN
      FOR i IN REVERSE 10..1 LOOP
          RAISE NOTICE 'Number: %', i;
      END LOOP;
  END;
  $$;
  -- Output: Number: 10, Number: 9, ..., Number: 1
  ```
- **Example**: Display all records from students table.
  ```sql
  DO $$
  DECLARE
      rec RECORD;
  BEGIN
      FOR rec IN SELECT * FROM students LOOP
          RAISE NOTICE 'Student: %, Score: %', rec.name, rec.score;
      END LOOP;
  END;
  $$;
  ```
- **Example**: Increase salary by 5% for employees with salary < 50,000.
  ```sql
  DO $$
  DECLARE
      emp RECORD;
  BEGIN
      FOR emp IN SELECT employee_id, salary FROM employees WHERE salary < 50000 LOOP
          UPDATE employees
          SET salary = salary * 1.05
          WHERE employee_id = emp.employee_id;
          RAISE NOTICE 'Updated salary for employee % to %', emp.employee_id, emp.salary * 1.05;
      END LOOP;
  END;
  $$;
  ```

## CONTINUE Statement
Skips the current loop iteration and moves to the next, used with LOOP, WHILE, or FOR loops.
- **Syntax**:
  ```sql
  CONTINUE [label] [WHEN boolean-expression];
  ```
- **Explanation**:
  - `label`: Optional; specifies the loop to continue (for nested loops).
  - `WHEN boolean-expression`: Optional; skips iteration if true.
  - Without `label` or `WHEN`, skips the current iteration of the innermost loop.

- **Example**: Display even numbers from 1 to 10.
  ```sql
  DO $$
  DECLARE
      i INT := 1;
  BEGIN
      LOOP
          EXIT WHEN i > 10;
          IF i % 2 != 0 THEN
              i := i + 1;
              CONTINUE;
          END IF;
          RAISE NOTICE 'Even Number: %', i;
          i := i + 1;
      END LOOP;
  END;
  $$;
  -- Output: Even Number: 2, Even Number: 4, ..., Even Number: 10
  ```

- **Example**: Display numbers 1 to 10, skipping 7.
  ```sql
  DO $$
  BEGIN
      FOR i IN 1..10 LOOP
          CONTINUE WHEN i = 7;
          RAISE NOTICE 'Number: %', i;
      END LOOP;
  END;
  $$;
  -- Output: Number: 1, Number: 2, ..., Number: 6, Number: 8, ..., Number: 10
  ```

## Exercises
1. **Simple CASE**:
   - Write a PL/pgSQL block to categorize a department as ‘Small’ (<10 employees), ‘Medium’ (10–50), or ‘Large’ (>50).
     ```sql
     DO $$
     DECLARE
         emp_count INT;
         dept_size TEXT;
     BEGIN
         SELECT COUNT(*) INTO emp_count FROM employees WHERE dept_id = 1;
         dept_size := CASE
             WHEN emp_count < 10 THEN 'Small'
             WHEN emp_count BETWEEN 10 AND 50 THEN 'Medium'
             ELSE 'Large'
         END;
         RAISE NOTICE 'Department size: %', dept_size;
     END;
     $$;
     ```

2. **Searched CASE**:
   - Write a query to adjust employee bonuses: +10% for salary < 40,000, +5% for salary 40,000–60,000.
     ```sql
     UPDATE employees
     SET bonus = CASE
         WHEN salary < 40000 THEN salary * 0.10
         WHEN salary BETWEEN 40000 AND 60000 THEN salary * 0.05
         ELSE 0
     END;
     ```

3. **CASE with Aggregate**:
   - Count students by grade category (Excellent: >90, Good: 80–90, Average: <80).
     ```sql
     SELECT
         COUNT(CASE WHEN score > 90 THEN 1 END) AS excellent,
         COUNT(CASE WHEN score BETWEEN 80 AND 90 THEN 1 END) AS good,
         COUNT(CASE WHEN score < 80 THEN 1 END) AS average
     FROM students;
     ```

4. **WHILE Loop**:
   - Write a PL/pgSQL block to print odd numbers from 1 to 9.
     ```sql
     DO $$
     DECLARE
         num INT := 1;
     BEGIN
         WHILE num <= 9 LOOP
             RAISE NOTICE 'Odd Number: %', num;
             num := num + 2;
         END LOOP;
     END;
     $$;
     ```

5. **FOR Loop with Query**:
   - Write a PL/pgSQL block to log names of employees with salary > 60,000.
     ```sql
     DO $$
     DECLARE
         emp RECORD;
     BEGIN
         FOR emp IN SELECT first_name, salary FROM employees WHERE salary > 60000 LOOP
             RAISE NOTICE 'Employee: %, Salary: %', emp.first_name, emp.salary;
         END LOOP;
     END;
     $$;
     ```

6. **CONTINUE Statement**:
   - Write a PL/pgSQL block to print numbers 1 to 10, skipping multiples of 3.
     ```sql
     DO $$
     BEGIN
         FOR i IN 1..10 LOOP
             CONTINUE WHEN i % 3 = 0;
             RAISE NOTICE 'Number: %', i;
         END LOOP;
     END;
     $$;
     ```

## References
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- Provided PL/pgSQL content on CASE and looping statements.