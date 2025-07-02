# PostgreSQL Notes

## Summary
PostgreSQL is a robust, open-source relational database management system (RDBMS) that supports both SQL and non-relational (JSON) queries. Developed by a global volunteer community, it offers advanced features like multi-version concurrency control, geospatial support, and extensibility. These notes provide a beginner-friendly guide to PostgreSQL’s features, data types, installation, roles, table inheritance, and basic operations, with SQL examples and exercises for revision.

## PostgreSQL Overview
### Definition and History
- **PostgreSQL**: Pronounced "post-gress-Q-L," it’s an open-source RDBMS, freely available, developed by volunteers, and not controlled by any single entity.
- **History**:
  - Originated as the Ingres project by Michael Stonebraker at UC Berkeley in 1982.
  - Evolved into POSTGRES, introducing user-defined data types and relationships.
  - Renamed PostgreSQL, initially for UNIX-like platforms, later supporting Windows, macOS, and Solaris.
  - Stonebraker received the 2014 Turing Award for his contributions.

### Features
- Supports dynamic web applications via client-server architecture.
- Write-ahead logging for fault tolerance.
- Multi-version concurrency control (MVCC) for concurrent access.
- ANSI SQL compliance and object-oriented capabilities.
- PostGIS extension for geospatial data.
- JSON/JSONB support for NoSQL integration.
- Compatible with Python, Java, C/C++, C#, Node.js, Go, Ruby, Perl, Tcl.
- Log-based and trigger-based replication with SSL.
- Standby server and high availability.
- Mature server-side programming (e.g., stored procedures).

### Advantages
- Fault-tolerant with write-ahead logging.
- Open-source, allowing free use and modification.
- Supports geospatial data via PostGIS.
- Easy to learn with minimal training.
- Low maintenance for embedded and enterprise use.

### Disadvantages
- Limited brand recognition due to lack of single ownership.
- Slower than MySQL in some performance metrics.
- Some open-source apps support MySQL but not PostgreSQL.
- Speed optimizations require more effort due to compatibility focus.

### Applications
- **Financial Industry**: ACID-compliant for transaction processing and analytics, integrable with Matlab and R.
- **Geospatial Data**: PostGIS for geographic information systems.
- **Manufacturing**: Backend for supply chain optimization.
- **Web Technology**: Scalable storage for frameworks like Django, Node.js, Hibernate, PHP.
- **Scientific Data**: Manages large datasets with powerful SQL and analytical capabilities.

## PostgreSQL Data Types
PostgreSQL supports a variety of data types for flexible data storage.

### Boolean
Stores `true`, `false`, or `null`. Values like `1`, `yes`, `y`, `t` convert to `true`; `0`, `no`, `f` convert to `false`.
- **Example**:
  ```sql
  CREATE TABLE users (
      user_id INT PRIMARY KEY,
      is_active BOOLEAN
  );
  INSERT INTO users VALUES (1, 't');
  SELECT * FROM users WHERE is_active = true;
  ```

### Character
- `CHAR(n)`: Fixed-length, padded with spaces; errors if string exceeds `n`.
- `VARCHAR(n)`: Variable-length, up to `n` characters, no padding.
- `TEXT`: Unlimited length.
- **Example**:
  ```sql
  CREATE TABLE documents (
      doc_id INT PRIMARY KEY,
      title VARCHAR(100),
      content TEXT
  );
  INSERT INTO documents VALUES (1, 'Report', 'Detailed analysis...');
  ```

### Numeric
- **Integers**:
  - `SMALLINT`: 2 bytes, -32,768 to 32,767.
  - `INT`: 4 bytes, -2,147,483,648 to 2,147,483,647.
  - `SERIAL`: Auto-incrementing integer.
- **Floating-Point**:
  - `FLOAT(n)`: Up to 8 bytes, `n` precision.
  - `REAL`: 4-byte floating-point.
  - `NUMERIC(d,p)`: Precise, `d` digits, `p` decimals.
- **Example**:
  ```sql
  CREATE TABLE transactions (
      tx_id SERIAL PRIMARY KEY,
      amount NUMERIC(10,2)
  );
  INSERT INTO transactions (amount) VALUES (123.45);
  ```

### Temporal
- `DATE`: Stores dates.
- `TIME`: Stores time of day.
- `TIMESTAMP`: Stores date and time.
- `TIMESTAMPTZ`: Timezone-aware timestamp.
- `INTERVAL`: Stores time periods.
- **Example**:
  ```sql
  CREATE TABLE logs (
      log_id INT PRIMARY KEY,
      event_time TIMESTAMPTZ
  );
  INSERT INTO logs VALUES (1, NOW());
  ```

### Arrays
Stores arrays of any data type (e.g., `TEXT[]`, `INT[]`).
- **Example**:
  ```sql
  CREATE TABLE projects (
      project_id INT PRIMARY KEY,
      categories TEXT[]
  );
  INSERT INTO projects VALUES (1, ARRAY['web', 'data']);
  SELECT * FROM projects WHERE 'web' = ANY(categories);
  ```

### JSON/JSONB
- `JSON`: Stores plain JSON, parsed on query.
- `JSONB`: Binary JSON, supports indexing for faster queries.
- **Example**:
  ```sql
  CREATE TABLE records (
      record_id INT PRIMARY KEY,
      data JSONB
  );
  INSERT INTO records VALUES (1, '{"name": "Alice", "role": "Admin"}');
  SELECT data->'name' FROM records;
  ```

### UUID
Stores universally unique identifiers per RFC 4122, ideal for unique IDs.
- **Example**:
  ```sql
  CREATE TABLE sessions (
      session_id UUID PRIMARY KEY,
      user_id INT
  );
  INSERT INTO sessions (session_id, user_id) VALUES (gen_random_uuid(), 1);
  ```

### Special
- `inet`: IPv4/IPv6 addresses.
- `macaddr`: MAC addresses.
- `point`, `box`, `lseg`, `polygon`: Geometric types.
- **Example**:
  ```sql
  CREATE TABLE locations (
      loc_id INT PRIMARY KEY,
      coordinates point
  );
  INSERT INTO locations VALUES (1, '(10.5, 20.3)');
  ```

## Installation and Verification
### Installation
- **Download**: From [PostgreSQL Download](https://www.postgresql.org/download/).
- **Steps**:
  1. Download the EDB installer for your operating system.
  2. Choose installation folder and components (e.g., pgAdmin, psql).
  3. Set data directory and superuser (postgres) password.
  4. Configure port (default: 5432) and locale.
  5. Complete installation.
- **Example**:
  - Install PostgreSQL 16, set password to 'secure123', use default port.

### Verification
- **psql Shell**:
  ```sql
  psql -U postgres
  SELECT version();
  \conninfo
  ```
  - Output: Displays PostgreSQL version and connection details.
- **pgAdmin**:
  1. Open pgAdmin, enter superuser password.
  2. Expand Servers, check Properties for version.
- **Example**:
  ```sql
  CREATE DATABASE test_db;
  \l
  ```

## PostgreSQL GUI
### pgAdmin
A graphical interface for managing PostgreSQL databases.
- **Dashboard**: Displays servers, schemas, tables, and roles.
- **Query Tool**: Run SQL queries interactively.
  - **Example**:
    ```sql
    CREATE TABLE students (
        student_id INT PRIMARY KEY,
        name VARCHAR(50),
        age INT
    );
    INSERT INTO students VALUES (1, 'Wick', 22);
    SELECT * FROM students;
    ```
- **Create Database**:
  - In pgAdmin, right-click Databases, select Create > Database, name it `rca`.
  - **SQL**:
    ```sql
    CREATE DATABASE rca;
    ```

## Roles and Privileges
### Roles
Represent users or groups for access control.
- **User Roles**: Individual accounts (e.g., `bob`).
- **Group Roles**: Shared privileges (e.g., `managers`).
- **Example**:
  ```sql
  CREATE ROLE bob LOGIN PASSWORD 'bob123';
  CREATE ROLE managers NOLOGIN;
  ```

### Privileges
Define actions like `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `CONNECT`.
- **Commands**:
  - `CREATE ROLE`: Creates a role.
  - `GRANT`: Assigns privileges.
  - `REVOKE`: Removes privileges.
  - `ALTER ROLE`: Modifies role attributes.
- **Example**:
  ```sql
  CREATE TABLE data (
      data_id INT PRIMARY KEY,
      value VARCHAR(50)
  );
  GRANT SELECT, INSERT ON data TO bob;
  GRANT ALL ON data TO managers;
  REVOKE INSERT ON data FROM bob;
  ```

### Role Attributes
- `LOGIN/NOLOGIN`: Controls login ability.
- `SUPERUSER/NOSUPERUSER`: Grants/restricts full access.
- `CREATEDB/NOCREATEDB`: Allows/prevents database creation.
- `CREATEROLE/NOCREATEROLE`: Allows/prevents role creation.
- `INHERIT/NOINHERIT`: Enables/disables privilege inheritance.
- `PASSWORD`: Sets authentication password.
- `VALID UNTIL`: Sets role expiration.
- **Example**:
  ```sql
  CREATE ROLE admin LOGIN SUPERUSER PASSWORD 'admin123';
  CREATE ROLE temp_user LOGIN VALID UNTIL '2026-12-31';
  ALTER ROLE bob WITH CREATEDB;
  ALTER ROLE bob PASSWORD 'newpass123';
  ALTER ROLE bob NOSUPERUSER;
  ```

## Table Inheritance
### Definition
Child tables inherit columns, constraints (e.g., CHECK, NOT NULL), indexes, and triggers from parent tables, enabling hierarchical data structures.

### Types
- **Single Inheritance**: Child inherits from one parent.
- **Multiple Inheritance**: Child inherits from multiple parents, merging their structures.
- **Note**: Differs from object-oriented programming; focuses on table structure.

### Single Inheritance
- **Syntax**:
  ```sql
  CREATE TABLE parent_table (...);
  CREATE TABLE child_table (...) INHERITS (parent_table);
  ```
- **Example**:
  ```sql
  CREATE TABLE vehicles (
      vehicle_id INT PRIMARY KEY,
      model VARCHAR(50),
      price NUMERIC(10,2)
  );
  CREATE TABLE cars (
      color VARCHAR(20)
  ) INHERITS (vehicles);
  INSERT INTO cars (vehicle_id, model, price, color) VALUES (1, 'Sedan', 25000.00, 'Blue');
  SELECT * FROM vehicles; -- Includes cars data
  SELECT * FROM cars;
  ```

### Multiple Inheritance
- **Syntax**:
  ```sql
  CREATE TABLE child_table (...) INHERITS (parent_table_1, parent_table_2);
  ```
- **Example**:
  ```sql
  CREATE TABLE products (
      product_id INT PRIMARY KEY,
      name VARCHAR(50)
  );
  CREATE TABLE inventory (
      stock INT
  ) INHERITS (products);
  CREATE TABLE warehouse (
      location VARCHAR(50)
  ) INHERITS (products, inventory);
  INSERT INTO warehouse (product_id, name, stock, location)
  VALUES (1, 'Widget', 100, 'Main');
  SELECT * FROM products; -- Includes warehouse data
  ```

### Remove Inheritance
- **Syntax**:
  ```sql
  ALTER TABLE child_table NO INHERIT parent_table;
  ```
- **Example**:
  ```sql
  ALTER TABLE cars NO INHERIT vehicles;
  ```

### Benefits
- **Code Reuse**: Define common columns/constraints in parent table.
- **Data Sharing**: Query parent table to access child table data.
- **Polymorphism**: Treat child tables as parent type in queries.

## Basic PostgreSQL Operations
### Create Table
- **Example**:
  ```sql
  CREATE TABLE employees (
      emp_id SERIAL PRIMARY KEY,
      name VARCHAR(50),
      department VARCHAR(50),
      metadata JSONB
  );
  ```

### Insert Data
- **Example**:
  ```sql
  INSERT INTO employees (name, department, metadata)
  VALUES ('Alice', 'HR', '{"role": "Manager"}'),
         ('Bob', 'IT', '{"role": "Developer"}');
  ```

### Query Data
- **Example**:
  ```sql
  SELECT name, metadata->'role' AS role
  FROM employees
  WHERE department = 'IT';
  ```

### Describe Table
- **psql Command**:
  ```sql
  \d employees
  \d+ employees -- Detailed description
  ```

## Common psql Commands
- `\q`: Exit psql.
- `\c dbname`: Connect to a database.
- `\dt`: List tables.
- `\du`: List roles.
- `\l`: List databases.
- `\conninfo`: Show connection details.
- `\d table_name`: Describe a table.
- `\d+ table_name`: Detailed table description.
- `\dn`: List schemas.
- `\dv`: List views.
- `\o file`: Save query output to a file.
- `\i file`: Run commands from a file.
- `\H`: Output in HTML format.
- `\g`: Repeat last command.
- `\a`: Toggle aligned/unaligned output.
- **Connect to Database**:
  ```sql
  psql -U postgres -d rca
  ```
- **Example**:
  ```sql
  \c rca
  \dt
  \d employees
  ```

## Exercises
1. **Database Creation**:
   - Create a database `test_db` and a table `users` with `user_id UUID`, `name VARCHAR(50)`, and `data JSONB`.
     ```sql
     CREATE DATABASE test_db;
     \c test_db
     CREATE TABLE users (
         user_id UUID PRIMARY KEY,
         name VARCHAR(50),
         data JSONB
     );
     ```
2. **Roles and Privileges**:
   - Create a role `app_user` with `LOGIN` and `SELECT`, `INSERT` on `users`.
   - Create a role `admin` with `SUPERUSER` and `CREATEDB`.
     ```sql
     CREATE ROLE app_user LOGIN PASSWORD 'user123';
     GRANT SELECT, INSERT ON users TO app_user;
     CREATE ROLE admin LOGIN SUPERUSER PASSWORD 'admin123' CREATEDB;
     ```
3. **Table Inheritance**:
   - Create a parent table `items` (`item_id INT`, `name VARCHAR(50)`) and a child table `books` with an `author` column.
   - Insert data and query both tables.
     ```sql
     CREATE TABLE items (
         item_id INT PRIMARY KEY,
         name VARCHAR(50)
     );
     CREATE TABLE books (
         author VARCHAR(50)
     ) INHERITS (items);
     INSERT INTO books (item_id, name, author) VALUES (1, 'Database 101', 'Smith');
     SELECT * FROM items;
     ```
4. **Data Types**:
   - Create a table `events` with a `location point` and insert a coordinate.
   - Query events where `location` is within a specific area.
     ```sql
     CREATE TABLE events (
         event_id INT PRIMARY KEY,
         location point
     );
     INSERT INTO events VALUES (1, '(10, 20)');
     SELECT * FROM events WHERE location <@ box '((0,0),(20,20))';
     ```
5. **Queries**:
   - Write a query to extract `role` from a JSONB column in a `records` table.
     ```sql
     SELECT data->'role' FROM records WHERE data->>'name' = 'Alice';
     ```

## References
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- Provided PostgreSQL content (summarized and integrated).