# Unit 4: Introduction to Database

## 4.1 Definitions of Key Terms
Understanding key database terms is essential for learning database concepts.

- **Database**: An organized collection of data, typically stored and accessed electronically from a computer system.
- **Database Management System (DBMS)**: Software that manages databases, allowing users to create, read, update, and delete data (e.g., MySQL, Oracle, SQLite).
- **Table**: A structure in a database that stores data in rows and columns, similar to a spreadsheet.
- **Record (Row)**: A single entry in a table, representing one instance of data.
- **Field (Column)**: A single attribute of a record, defining a specific type of data (e.g., name, age).
- **Primary Key**: A unique identifier for each record in a table (e.g., student ID).
- **Foreign Key**: A field in one table that links to the primary key of another table to establish relationships.
- **Query**: A request for data or operations on a database, often written in SQL (Structured Query Language).
- **SQL**: A language used to interact with relational databases for querying and managing data.
- **Example**: In a student database, a table named `Students` might have fields `StudentID` (primary key), `Name`, and `Age`.

## 4.2 Different Areas Where Databases Can Be Applied
Databases are used across various domains to manage and retrieve data efficiently.

- **Business**:
  - Customer relationship management (CRM) systems to track client information.
  - Inventory management to monitor stock levels.
  - Example: A retail store uses a database to manage product details and sales.
- **Education**:
  - Student information systems for grades, attendance, and enrollment.
  - Library management systems for tracking books.
  - Example: A university database stores student records and course schedules.
- **Healthcare**:
  - Electronic health records (EHR) to store patient data.
  - Appointment scheduling systems.
  - Example: A hospital database tracks patient diagnoses and treatments.
- **Finance**:
  - Banking systems for account management and transactions.
  - Fraud detection systems analyzing transaction patterns.
  - Example: A bank uses a database to store customer account details.
- **E-Commerce**:
  - Product catalogs and order processing.
  - User profiles for personalized recommendations.
  - Example: Amazon uses a database to manage products and customer orders.
- **Government**:
  - Citizen records for identification and voting systems.
  - Tax management systems.
  - Example: A government database stores citizen IDs and tax records.

## 4.3 Database Approaches
Different database approaches define how data is structured and managed.

- **Flat File Database**:
  - Simple structure, often stored as text files or spreadsheets.
  - Suitable for small-scale data (e.g., CSV files).
  - Limitations: No relationships, poor scalability.
  - Example: A single Excel file storing employee names and salaries.
- **Relational Database**:
  - Organizes data into tables linked by keys (primary and foreign keys).
  - Uses SQL for querying.
  - Advantages: Supports complex queries, enforces data integrity.
  - Example: MySQL database with tables for `Orders` and `Customers` linked by `CustomerID`.
- **Hierarchical Database**:
  - Organizes data in a tree-like structure with parent-child relationships.
  - Example: A file system with folders and subfolders.
  - Limitations: Rigid structure, complex to modify.
- **Network Database**:
  - Extends hierarchical model, allowing multiple parent-child relationships.
  - Example: A database where employees report to multiple managers.
  - Limitations: Complex to implement and maintain.
- **NoSQL Database**:
  - Handles unstructured or semi-structured data (e.g., JSON, key-value).
  - Types: Document, key-value, column-store, graph.
  - Advantages: Scalable for big data, flexible schema.
  - Example: MongoDB storing user profiles as JSON documents.
- **Example (Relational Database - SQL)**:
  ```sql
  CREATE TABLE Students (
      StudentID INT PRIMARY KEY,
      Name VARCHAR(50),
      Age INT
  );
  INSERT INTO Students (StudentID, Name, Age) VALUES (1, 'Alice', 20);
  ```

## 4.4 Database Access Levels and Users
Database access levels and users determine who can interact with the database and to what extent.

- **Access Levels**:
  - **Read-Only**: View data without modifying it (e.g., SELECT queries).
  - **Read-Write**: View and modify data (e.g., INSERT, UPDATE, DELETE).
  - **Administrative**: Full control, including creating tables, managing users, and setting permissions.
- **User Types**:
  - **End Users**: Access data through applications (e.g., employees using a CRM system).
  - **Application Developers**: Write software to interact with the database.
  - **Database Administrators (DBAs)**: Manage database structure, performance, and security.
- **Access Control**:
  - **Authentication**: Verifying user identity (e.g., username and password).
  - **Authorization**: Defining what actions a user can perform (e.g., granting SELECT or INSERT permissions).
  - **Example (SQL)**:
    ```sql
    GRANT SELECT ON Students TO 'user1';
    GRANT ALL PRIVILEGES ON Students TO 'admin';
    ```
- **Security Considerations**:
  - Use strong passwords and encryption.
  - Limit access to sensitive data (e.g., personal information).
  - Regularly audit user permissions.
- **Example**: A school database allows students (read-only) to view grades, teachers (read-write) to update grades, and DBAs (administrative) to manage the database structure.