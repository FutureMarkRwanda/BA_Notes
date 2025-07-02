# PostgreSQL Schemas and Advanced Features Notes

## Summary
These notes cover PostgreSQL’s schemas, table partitioning, views, materialized views, and indexes. Designed for beginners, they provide a clear understanding of these features, including their definitions, benefits, limitations, and practical SQL examples, with exercises for revision.

## Schemas
### Definition
A schema in PostgreSQL is a logical container within a database that groups related objects (e.g., tables, views, functions, indexes) into a namespace. It organizes database elements, prevents naming conflicts, and enhances access control. A default `public` schema exists, but creating custom schemas is optional.

### Features
- **Organization**: Groups tables, views, functions, and other objects for better manageability.
- **Namespacing**: Allows objects with the same name in different schemas (e.g., `schema1.table1` and `schema2.table1`).
- **Access Control**: Enables fine-grained permissions on schemas and their objects.

### Benefits
- **Improved Organization**: Simplifies navigation in large databases.
- **Modularity**: Isolates different parts of an application for maintainability.
- **Security**: Restricts access to sensitive data via schema-level permissions.
- **Consolidation**: Allows multiple applications to share a database with separate schemas.

### Creating a Schema
- **Syntax**:
  ```sql
  CREATE SCHEMA schema_name;
  -- Or with optional check
  CREATE SCHEMA IF NOT EXISTS schema_name;
  ```
- **Example (psql)**:
  ```sql
  CREATE SCHEMA data_store;
  \dn -- List schemas
  ```
- **pgAdmin 4**:
  1. Right-click Databases > select a database (e.g., `test_db`).
  2. Choose Create > Schema, enter name (e.g., `data_store`), and save.

### Creating a Table in a Schema
- **Syntax**:
  ```sql
  CREATE TABLE schema_name.table_name (
      column_name datatype,
      ...
  );
  ```
- **Example**:
  ```sql
  CREATE TABLE data_store.users (
      user_id INT PRIMARY KEY,
      name VARCHAR(50)
  );
  \dt data_store.* -- List tables in schema
  ```

### Schema Privileges
- Users only access objects in schemas they own unless granted privileges.
- **Grant Usage**:
  ```sql
  GRANT USAGE ON SCHEMA data_store TO user_name;
  ```
- **Grant Create**:
  ```sql
  GRANT CREATE ON SCHEMA data_store TO user_name;
  ```
- **Example**:
  ```sql
  CREATE ROLE user_name LOGIN PASSWORD 'pass123';
  GRANT USAGE, CREATE ON SCHEMA data_store TO user_name;
  ```

### Altering a Schema
- **Rename Schema**:
  ```sql
  ALTER SCHEMA data_store RENAME TO new_store;
  ```
- **Change Owner**:
  ```sql
  ALTER SCHEMA new_store OWNER TO new_owner;
  ```
- **Move Table Between Schemas**:
  ```sql
  ALTER TABLE data_store.users SET SCHEMA new_store;
  ```

### Dropping a Schema
- **Syntax**:
  ```sql
  DROP SCHEMA schema_name [CASCADE | RESTRICT];
  -- CASCADE: Drops schema and all objects
  -- RESTRICT: Prevents drop if objects exist (default)
  ```
- **Example**:
  ```sql
  DROP SCHEMA new_store CASCADE;
  ```
- **Drop Table in Schema**:
  ```sql
  DROP TABLE new_store.users;
  ```

## Table Partitioning
### Definition
Table partitioning divides a large table into smaller, manageable partitions, each acting as a separate table with its own storage and constraints. It enhances query performance and simplifies data management.

### Benefits
- **Performance**: Faster queries by scanning only relevant partitions.
- **Efficient Data Operations**: Faster bulk inserts/deletes on partitions.
- **Manageability**: Independent partition maintenance (e.g., backups, vacuuming).
- **Scalability**: Easily add partitions as data grows.
- **Load Balancing**: Distributes data across storage or servers.

### Types of Partitioning
- **Range Partitioning**: Divides data based on a column’s value range (e.g., dates).
- **List Partitioning**: Divides data based on specific column values (e.g., categories).
- **Hash Partitioning**: Distributes data evenly using a hash function.

### Creating a Partitioned Table
- **Range Partitioning**:
  ```sql
  CREATE TABLE sales (
      sale_id INT,
      sale_date DATE,
      amount NUMERIC(10,2)
  ) PARTITION BY RANGE (sale_date);
  CREATE TABLE sales_2023 PARTITION OF sales
      FOR VALUES FROM ('2023-01-01') TO ('2024-01-01');
  CREATE TABLE sales_2024 PARTITION OF sales
      FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');
  ```
- **List Partitioning**:
  ```sql
  CREATE TABLE employees (
      emp_id INT,
      region VARCHAR(50),
      salary NUMERIC(10,2)
  ) PARTITION BY LIST (region);
  CREATE TABLE employees_east PARTITION OF employees
      FOR VALUES IN ('East');
  CREATE TABLE employees_west PARTITION OF employees
      FOR VALUES IN ('West');
  ```
- **Hash Partitioning**:
  ```sql
  CREATE TABLE orders (
      order_id INT,
      customer_id INT,
      amount NUMERIC(10,2)
  ) PARTITION BY HASH (customer_id);
  CREATE TABLE orders_p0 PARTITION OF orders
      FOR VALUES WITH (MODULUS 3, REMAINDER 0);
  CREATE TABLE orders_p1 PARTITION OF orders
      FOR VALUES WITH (MODULUS 3, REMAINDER 1);
  CREATE TABLE orders_p2 PARTITION OF orders
      FOR VALUES WITH (MODULUS 3, REMAINDER 2);
  ```

### Managing Partitions
- **Insert Data**:
  ```sql
  INSERT INTO sales (sale_id, sale_date, amount)
  VALUES (1, '2023-06-15', 100.00);
  ```
- **Query Data**:
  ```sql
  SELECT * FROM sales WHERE sale_date >= '2023-01-01' AND sale_date < '2024-01-01';
  ```
- **Rename Partition**:
  ```sql
  ALTER TABLE sales_2023 RENAME TO sales_y2023;
  ```
- **Drop Partitioned Table**:
  ```sql
  DROP TABLE sales;
  ```
- **Detach Partition**:
  ```sql
  ALTER TABLE sales DETACH PARTITION sales_y2023;
  -- Or concurrently to avoid locking
  ALTER TABLE sales DETACH PARTITION sales_y2023 CONCURRENTLY;
  ```
- **Reattach Partition**:
  ```sql
  ALTER TABLE sales ATTACH PARTITION sales_y2023
      FOR VALUES FROM ('2023-01-01') TO ('2024-01-01');
  ```

### Limitations
- Supports only range, list, and hash partitioning.
- No automatic partition pruning for OR conditions.
- Inheritance-based partitioning can be complex.
- Limited ALTER TABLE operations on partitioned tables.
- Performance overhead for inserts/updates due to partition management.
- Complex maintenance for large numbers of partitions.

## Views
### Definition
A view is a virtual table derived from one or more base tables, providing an alternative perspective of the data. Views simplify queries and control access.

### Advantages
- **Simplified Queries**: Encapsulates complex joins/aggregations for easier querying.
- **Security**: Restricts access to specific columns/rows, hiding sensitive data.
- **Logical Data Independence**: Allows base table changes without affecting applications.

### Limitations
- **Performance**: Real-time query execution may be slower for complex views.
- **Dependencies**: Base table changes can break dependent views.

### Creating a View
- **Example**:
  ```sql
  CREATE TABLE employees (
      emp_id INT PRIMARY KEY,
      name VARCHAR(50),
      dept_id INT
  );
  CREATE TABLE departments (
      dept_id INT PRIMARY KEY,
      dept_name VARCHAR(50)
  );
  CREATE VIEW employee_details AS
      SELECT e.emp_id, e.name, d.dept_name
      FROM employees e
      JOIN departments d ON e.dept_id = d.dept_id;
  ```
- **Query View**:
  ```sql
  SELECT * FROM employee_details;
  ```

### Updatable Views
Views are updatable if they meet these criteria:
- Single table in the `FROM` clause.
- No aggregate functions, `GROUP BY`, `HAVING`, `LIMIT`, `DISTINCT`, `UNION`, etc.
- **Example**:
  ```sql
  CREATE VIEW emp_names AS
      SELECT emp_id, name FROM employees;
  UPDATE emp_names SET name = 'Bob' WHERE emp_id = 1;
  INSERT INTO emp_names (emp_id, name) VALUES (2, 'Alice');
  ```

## Materialized Views
### Definition
A materialized view is a physical snapshot of a view’s query results, stored as a table. Unlike regular views, it doesn’t recompute data on access unless refreshed.

### Benefits
- **Improved Performance**: Precomputed results speed up complex queries.
- **Reduced Resource Usage**: Avoids repeated computations.
- **Offline Analysis**: Suitable for reports or historical data.
- **Improved Concurrency**: Static data reduces contention.
- **Query Optimization**: Stores intermediate results for analytics.
- **Reduced Complexity**: Simplifies application logic.

### Disadvantages
- **Storage Overhead**: Stores data copies, increasing space requirements.
- **Maintenance Overhead**: Requires periodic refreshes.
- **Staleness**: Data may be outdated if not refreshed frequently.
- **Performance Impact**: Refreshing affects DML operations.
- **Limited Use Cases**: Best for frequent, complex queries.
- **Concurrency Issues**: Refreshing may cause inconsistencies.

### Creating a Materialized View
- **Syntax**:
  ```sql
  CREATE MATERIALIZED VIEW view_name AS query WITH [NO] DATA;
  ```
- **Example**:
  ```sql
  CREATE TABLE orders (
      order_id INT PRIMARY KEY,
      customer_id INT,
      order_amount NUMERIC(10,2)
  );
  CREATE MATERIALIZED VIEW customer_orders AS
      SELECT customer_id, SUM(order_amount) AS total, AVG(order_amount) AS avg_amount
      FROM orders
      GROUP BY customer_id
      WITH DATA;
  ```

### Refreshing Materialized Views
- **Full Refresh**:
  ```sql
  REFRESH MATERIALIZED VIEW customer_orders;
  ```
- **Concurrent Refresh** (requires unique index):
  ```sql
  CREATE UNIQUE INDEX idx_customer_orders ON customer_orders (customer_id);
  REFRESH MATERIALIZED VIEW CONCURRENTLY customer_orders;
  ```

### Dropping Materialized Views
- **Syntax**:
  ```sql
  DROP MATERIALIZED VIEW view_name;
  ```
- **Example**:
  ```sql
  DROP MATERIALIZED VIEW customer_orders;
  ```

## Indexes
### Definition
Indexes are database structures that speed up data retrieval by maintaining sorted pointers to table data. They act like an index in a book, enabling faster lookups.

### Advantages
- **Rapid Data Access**: Reduces query time, especially for large tables.
- **Boosted Query Efficiency**: Improves `WHERE` and `JOIN` performance.
- **Reduced Disk I/O**: Minimizes data scanned during queries.
- **Data Integrity**: Unique indexes prevent duplicate values.

### Disadvantages
- **Increased Storage**: Indexes require additional space.
- **Slower Write Operations**: Updates to `INSERT`, `UPDATE`, `DELETE` due to index maintenance.
- **HOT Updates**: MVCC creates new row versions, increasing I/O.

### Types of Indexes
1. **B-tree (Balanced Tree)**: Default, supports `<`, `<=`, `=`, `>=`, `>`, `BETWEEN`, `IN`, `IS NULL`.
   - **Syntax**:
     ```sql
     CREATE INDEX idx_name ON table_name (column_name);
     -- Or
     CREATE INDEX idx_name ON table_name USING btree (column_name);
     ```
2. **Hash**: Fast for equality (`=`) comparisons, not suitable for ranges.
   - **Syntax**:
     ```sql
     CREATE INDEX idx_hash ON table_name USING hash (column_name);
     ```
3. **GIN (Generalized Inverted Index)**: For arrays, JSONB, full-text search.
   - **Syntax**:
     ```sql
     CREATE INDEX idx_gin ON table_name USING gin (column_name);
     ```
4. **GiST (Generalized Search Tree)**: For geometric data, full-text search, ranges.
   - **Syntax**:
     ```sql
     CREATE INDEX idx_gist ON table_name USING gist (column_name);
     ```
5. **SP-GiST (Space-Partitioned GiST)**: For non-balanced data (e.g., prefix searches).
   - **Syntax**:
     ```sql
     CREATE INDEX idx_spgist ON table_name USING spgist (column_name);
     ```
6. **BRIN (Block Range Index)**: For large tables, indexes data block ranges.
   - **Syntax**:
     ```sql
     CREATE INDEX idx_brin ON table_name USING brin (column_name);
     ```

### Creating Indexes
- **Single-Column Index**:
  ```sql
  CREATE TABLE books (
      book_id INT PRIMARY KEY,
      title VARCHAR(100)
  );
  CREATE INDEX idx_title ON books (title);
  ```
- **Multicolumn Index**:
  ```sql
  CREATE INDEX idx_book_details ON books (title, book_id);
  ```
- **Modify Index**:
  ```sql
  ALTER INDEX idx_title RENAME TO idx_book_title;
  ```

## Exercises
1. **Schema Management**:
   - Create a schema `analytics` and a table `reports` within it.
   - Grant `USAGE` and `CREATE` to a role `analyst`.
     ```sql
     CREATE SCHEMA analytics;
     CREATE TABLE analytics.reports (
         report_id INT PRIMARY KEY,
         title VARCHAR(100)
     );
     CREATE ROLE analyst LOGIN PASSWORD 'analyst123';
     GRANT USAGE, CREATE ON SCHEMA analytics TO analyst;
     ```
2. **Table Partitioning**:
   - Create a range-partitioned table `logs` by `log_date` for 2023 and 2024.
   - Insert and query data.
     ```sql
     CREATE TABLE logs (
         log_id INT,
         log_date DATE
     ) PARTITION BY RANGE (log_date);
     CREATE TABLE logs_2023 PARTITION OF logs
         FOR VALUES FROM ('2023-01-01') TO ('2024-01-01');
     INSERT INTO logs VALUES (1, '2023-06-01');
     SELECT * FROM logs WHERE log_date < '2024-01-01';
     ```
3. **Views**:
   - Create a view `active_users` showing users with `is_active = true`.
   - Update a user’s name via the view.
     ```sql
     CREATE VIEW active_users AS
         SELECT user_id, name FROM users WHERE is_active = true;
     UPDATE active_users SET name = 'Charlie' WHERE user_id = 1;
     ```
4. **Materialized Views**:
   - Create a materialized view for average transaction amounts by user.
   - Refresh and query it.
     ```sql
     CREATE MATERIALIZED VIEW user_totals AS
         SELECT user_id, AVG(amount) AS avg_amount
         FROM transactions
         GROUP BY user_id
         WITH DATA;
     REFRESH MATERIALIZED VIEW user_totals;
     SELECT * FROM user_totals;
     ```
5. **Indexes**:
   - Create a B-tree index on `employees.name` and a GIN index on `documents.data` (JSONB).
     ```sql
     CREATE INDEX idx_emp_name ON employees (name);
     CREATE INDEX idx_doc_data ON documents USING gin (data);
     ```

## References
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- Provided PostgreSQL content on schemas, partitioning, views, and indexes.