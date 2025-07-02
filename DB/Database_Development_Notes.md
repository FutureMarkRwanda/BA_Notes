# Basics of Database Development

## Summary

This guide introduces database development, focusing on the design and management of structured data through the lens of an Online Fashion Store (OFS). It covers core database concepts, relational models, SQL operations, and administrative tasks with practical OFS examples for beginners.

---

## 1. Introduction to Databases

### Key Terms and Definitions

| Term        | Definition                                      | OFS Example                               |
| ----------- | ----------------------------------------------- | ----------------------------------------- |
| Data        | Raw, unprocessed facts                          | `"Blue Dress", $50`                       |
| Information | Processed data with meaning                     | `100 dresses sold in 2025`                |
| Database    | Organized collection of related data            | Tables of products, customers, and orders |
| DBMS        | Software to create, manage, and query databases | MySQL used to manage OFS data             |

### Importance of Databases

* Efficient storage and retrieval of large data sets (e.g., orders, customers)
* Elimination of redundancy (no duplicate product entries)
* Role-based access and data security
* Easy data sharing among multiple users

---

## 2. Database System Components

| Component  | Description                             | OFS Example                       |
| ---------- | --------------------------------------- | --------------------------------- |
| Hardware   | Physical infrastructure (servers, etc.) | Server hosting the OFS database   |
| Software   | DBMS and supporting programs            | MySQL or MongoDB                  |
| Data       | Structured digital facts                | Product, customer, and order data |
| Users      | People interacting with the DB          | Admins, customers, analysts       |
| Procedures | Policies for handling and updating data | Order processing rules            |

---

## 3. Levels of Data Measurement

| Level    | Description                              | OFS Example                |
| -------- | ---------------------------------------- | -------------------------- |
| Nominal  | Categories without order                 | Product type: Dress, Shirt |
| Ordinal  | Ordered categories                       | Ratings: 1 to 5 stars      |
| Interval | Equal intervals but no true zero         | Satisfaction score (0–100) |
| Ratio    | True zero exists, meaningful comparisons | Price: \$50, Quantity: 10  |

---

## 4. Types of Database Users

| User Type                    | Description                                | OFS Example                      |
| ---------------------------- | ------------------------------------------ | -------------------------------- |
| Database Administrator (DBA) | Manages DB structure and permissions       | Creates user roles and backups   |
| Naive/Parametric Users       | Use the system without technical knowledge | Customers placing orders         |
| Sophisticated Users          | Query the database directly                | Data analysts generating reports |
| Database Designers           | Design structure and relationships         | Define table structure           |
| Application Programmers      | Build applications that access DB          | Write code for order checkout    |
| Casual Users                 | Occasional access to reports               | Managers reviewing inventory     |

---

## 5. Database Creation Process

### 1. Fact-Finding

* Collect user requirements
* Methods: Interviews, questionnaires
* OFS Example: Interview store managers about customer preferences

### 2. Abstraction

* Extract only relevant data
* OFS Example: Store age and preferences for marketing, not hobbies

### 3. Organization

* Structure data into tables

Example:

| CustomerID | Name | Age | Preference |
| ---------- | ---- | --- | ---------- |
| 1          | Mary | 25  | Dresses    |
| 2          | John | 30  | Shirts     |

---

## 6. Paper-Based vs. Computerized Databases

| Feature       | Paper-Based | DBMS (Computerized)      |
| ------------- | ----------- | ------------------------ |
| Efficiency    | Low         | High                     |
| Redundancy    | High        | Minimal                  |
| Accessibility | Manual      | Multi-user access        |
| Reliability   | Error-prone | Consistent and automated |

### Example Comparison

**Traditional File System (C++)**

```cpp
ofstream file("products.txt");
file << "1,Blue Dress,50\n";
```

**DBMS (MySQL)**

```sql
CREATE TABLE Products (
  ProductID INT PRIMARY KEY,
  Name VARCHAR(50),
  Price DECIMAL(10,2)
);
```

---

## 7. Types of DBMS

| Type               | Description                        | OFS Use Case                       |
| ------------------ | ---------------------------------- | ---------------------------------- |
| Relational (RDBMS) | Table-based, uses SQL              | MySQL for structured customer data |
| Document-based     | JSON-like, schema-less             | MongoDB for product descriptions   |
| Graph-based        | Nodes and edges                    | Neo4j for product recommendations  |
| Hierarchical       | Tree structure                     | Legacy inventory systems           |
| Network            | Complex many-to-many relationships | Supplier and distributor networks  |
| Object-Oriented    | Based on object models             | Integration with OO applications   |

---

## 8. DBMS vs Flat File Systems

| Feature           | DBMS (MySQL)   | Flat File (CSV/Text) |
| ----------------- | -------------- | -------------------- |
| Multi-user Access | Yes            | No                   |
| Data Redundancy   | Minimal        | High                 |
| Security          | Role-based     | Limited              |
| Query Support     | Advanced (SQL) | Limited or manual    |

---

## 9. Database Architecture

### Three-Schema Architecture

1. **External Level** – Different user views (e.g., customer sees only orders)
2. **Conceptual Level** – Logical structure (e.g., table design)
3. **Internal Level** – Physical data storage on disk

### Data Independence

* **Logical Independence**: Modify schema without affecting user views
* **Physical Independence**: Change physical storage without schema changes

---

## 10. Relational Data Model

| Term           | Meaning                                  | OFS Example              |
| -------------- | ---------------------------------------- | ------------------------ |
| Relation/Table | Set of rows and columns                  | `Products`, `Customers`  |
| Tuple/Row      | A single record                          | One customer             |
| Attribute      | Column describing a property             | `Price`, `Email`         |
| Primary Key    | Uniquely identifies a row                | `ProductID`              |
| Foreign Key    | Reference to another table’s primary key | `CustomerID` in `Orders` |

---

## 11. Entity Relationship Diagram (ERD)

### Elements

* **Entities**: Things being modeled (Customers, Products)
* **Attributes**: Characteristics of entities (Name, Price)
* **Relationships**: How entities relate (Customer places Order)

### Symbols

| Symbol    | Meaning      |
| --------- | ------------ |
| Rectangle | Entity       |
| Ellipse   | Attribute    |
| Diamond   | Relationship |

[Read More](https://www.lucidchart.com/pages/er-diagrams)

---

## 12. Relational Algebra Operations

| Operation  | Symbol | SQL Equivalent Example                      |
| ---------- | ------ | ------------------------------------------- |
| Selection  | σ      | `SELECT * FROM Products WHERE Price > 100;` |
| Projection | π      | `SELECT Name FROM Products;`                |
| Join       | ⋈      | `JOIN Orders ON Orders.CustomerID = ...`    |
| Union      | ∪      | `SELECT ... UNION SELECT ...;`              |

---

## 13. Database Constraints

| Constraint  | Purpose                             | OFS Example              |
| ----------- | ----------------------------------- | ------------------------ |
| Primary Key | Ensure unique rows                  | `ProductID`              |
| Foreign Key | Enforce relationship between tables | `CustomerID` in `Orders` |
| Unique      | Prevent duplicate values            | `Email`                  |
| Check       | Validate values based on conditions | `Price > 0`              |
| Not Null    | Disallow empty fields               | `Product Name`           |

---

## 14. Data Dictionary Example

| Table    | Column    | Data Type     | Nullable | Description   |
| -------- | --------- | ------------- | -------- | ------------- |
| Products | ProductID | INT           | No       | Primary key   |
| Products | Name      | VARCHAR(50)   | No       | Product name  |
| Products | Price     | DECIMAL(10,2) | No       | Product price |

---

## 15. SQL Command Categories

### DDL (Data Definition Language)

```sql
CREATE DATABASE OFS;
CREATE TABLE Products (...);
ALTER TABLE Products ADD COLUMN Description VARCHAR(200);
DROP TABLE Products;
TRUNCATE TABLE Orders;
```

### DML (Data Manipulation Language)

```sql
INSERT INTO Products VALUES (...);
SELECT * FROM Products WHERE Price > 50;
UPDATE Products SET Price = 60 WHERE ProductID = 1;
DELETE FROM Products WHERE ProductID = 1;
```

### DCL (Data Control Language)

```sql
GRANT SELECT ON Products TO 'user'@'localhost';
REVOKE SELECT ON Products FROM 'user'@'localhost';
```

### TCL (Transaction Control Language)

```sql
START TRANSACTION;
INSERT INTO Orders VALUES (...);
COMMIT;
ROLLBACK;
```

---

## 16. MySQL User Management

```sql
CREATE USER 'ofs_user'@'localhost' IDENTIFIED BY 'SecurePass#2025';
GRANT ALL PRIVILEGES ON OFS.* TO 'ofs_user'@'localhost';
FLUSH PRIVILEGES;
```

Password policies can be enforced:

```sql
SET GLOBAL validate_password.policy = STRONG;
```

---

## 17. Concurrency Control Techniques

| Technique          | Description                                 | OFS Example                           |
| ------------------ | ------------------------------------------- | ------------------------------------- |
| Two-Phase Locking  | Locks during transaction to avoid conflicts | Lock during product update            |
| Timestamp Ordering | Order transactions by time                  | Prevent race conditions               |
| MVCC               | Snapshot-based multi-user access            | Customers see consistent stock levels |

---

## 18. Advanced SQL Features

### Joins

```sql
SELECT o.OrderID, c.Name
FROM Orders o
INNER JOIN Customers c ON o.CustomerID = c.CustomerID;
```

### Nested Queries

```sql
SELECT Name FROM Customers
WHERE CustomerID IN (
  SELECT CustomerID FROM Orders WHERE Total > 100
);
```

### Aggregate Functions

```sql
SELECT COUNT(*) AS OrderCount, SUM(Total) AS TotalSales FROM Orders;
```

### Views

```sql
CREATE VIEW HighValueProducts AS
SELECT Name, Price FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);
```

---

## 19. Database Administration

* **Backup**:

  ```bash
  mysqldump -u root -p OFS > ofs_backup.sql
  ```

* **Import**:

  ```bash
  mysql -u root -p OFS < ofs_backup.sql
  ```

* **Clone Table**:

  ```sql
  CREATE TABLE Products_Archive LIKE Products;
  INSERT INTO Products_Archive SELECT * FROM Products;
  ```

---

## 20. Exercises

1. Design and create an OFS database with `Products`, `Customers`, and `Orders` tables.
2. Insert at least 5 records in each table.
3. Write SQL queries to:

   * Select products priced above \$50
   * Join customers with their orders
   * Calculate total sales using `SUM`

---

## Assignment

**Task**: Create a complete OFS database using MySQL
**Deliverables**:

* SQL script for table creation and data insertion
* At least 5 functional queries
* Backup `.sql` file

**Submission**: Email your zipped SQL files to the instructor by **May 2, 2023**

---

## References

* [MySQL Documentation](https://dev.mysql.com/doc/)
* [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
* [GeeksforGeeks: Relational Algebra in DBMS](https://www.geeksforgeeks.org/introduction-of-relational-algebra-in-dbms/)

