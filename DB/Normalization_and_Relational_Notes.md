# Normalization and Relational Database Notes

## In Summary
This guide covers normalization, denormalization, relational algebra, relational calculus, the Entity-Relationship (ER) Model, and the Relational Model, tailored to an Online Fashion Store (OFS). It provides a beginner-friendly foundation for designing and querying relational databases, with practical examples and SQL code.

## Normalization
### Definition and Purpose
- **Normalization**: The process of organizing data in a database to minimize redundancy and eliminate undesirable characteristics like insertion, update, and deletion anomalies.
- **Purpose**:
  - Reduce data redundancy (e.g., avoid duplicate OFS customer data).
  - Ensure data integrity by removing anomalies.
  - Divide larger tables into smaller, related tables linked by relationships.
- **OFS Example**: Normalize customer and order data to avoid repeating customer details in every order record.

### Types of Anomalies
- **Insertion Anomaly**: Cannot insert a new record due to missing data.
  - **OFS Example**: Unable to add a new customer without an order if customer data is stored in an Orders table.
- **Deletion Anomaly**: Deleting a record removes unintended data.
  - **OFS Example**: Deleting an order removes customer details if stored together.
- **Update Anomaly**: Updating a single value requires multiple row updates.
  - **OFS Example**: Updating a customer’s address requires changing multiple order records if address is stored with orders.

### Advantages of Normalization
- Minimizes data redundancy (e.g., one customer record in OFS).
- Enhances database organization and consistency.
- Supports flexible database design for OFS scalability.
- Enforces relational integrity via keys and constraints.

### Disadvantages of Normalization
- Requires understanding user needs before design.
- Higher normal forms (4NF, 5NF) may degrade query performance.
- Time-consuming for complex relations.
- Poor decomposition can lead to bad design.

### Functional Dependency
- **Definition**: A relationship where one set of attributes (determinant) uniquely determines another (dependent). Denoted as `X → Y`.
- **OFS Example**: In a Products table, `ProductID → Name` (ProductID determines Name).
- **Types**:
  - **Trivial Functional Dependency**: `B` is a subset of `A` (e.g., `{ProductID, Name} → ProductID`).
  - **Non-trivial Functional Dependency**: `B` is not a subset of `A` (e.g., `ProductID → Name`).

### Normal Forms
Normalization progresses through stages called normal forms, each with specific constraints.

#### First Normal Form (1NF)
- **Rule**: All attributes must be atomic (single-valued, no multi-valued or composite attributes).
- **OFS Example**: A Customers table with a multi-valued PhoneNumber attribute violates 1NF.
  ```bash
  Before 1NF:
  | CustomerID | Name  | PhoneNumbers       |
  |------------|-------|--------------------|
  | 1          | Mary  | 123456, 789012     |
  ```
  - Solution: Create a new row for each phone number.
  ```bash
  After 1NF:
  | CustomerID | Name  | PhoneNumber |
  |------------|-------|-------------|
  | 1          | Mary  | 123456      |
  | 1          | Mary  | 789012      |
  ```
- **SQL**:
  ```sql
  CREATE TABLE Customers (
      CustomerID INT,
      Name VARCHAR(50),
      PhoneNumber VARCHAR(20),
      PRIMARY KEY (CustomerID, PhoneNumber)
  );
  ```

#### Second Normal Form (2NF)
- **Rules**:
  1. Table must be in 1NF.
  2. No partial dependency (non-prime attributes must depend on the entire candidate key).
- **OFS Example**: A table with CustomerID, OrderID (composite key), and CustomerName (partially dependent on CustomerID) violates 2NF.
  ```bash
  Before 2NF:
  | CustomerID | OrderID | CustomerName | OrderTotal |
  |------------|---------|--------------|------------|
  | 1          | 101     | Mary         | 50.00      |
  | 1          | 102     | Mary         | 75.00      |
  ```
  - Solution: Split into Customers and Orders tables.
  ```bash
  Customers:
  | CustomerID | Name  |
  |------------|-------|
  | 1          | Mary  |

  Orders:
  | OrderID | CustomerID | OrderTotal |
  |---------|------------|------------|
  | 101     | 1          | 50.00      |
  | 102     | 1          | 75.00      |
  ```
- **SQL**:
  ```sql
  CREATE TABLE Customers (
      CustomerID INT PRIMARY KEY,
      Name VARCHAR(50)
  );
  CREATE TABLE Orders (
      OrderID INT PRIMARY KEY,
      CustomerID INT,
      OrderTotal DECIMAL(10,2),
      FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
  );
  ```

#### Third Normal Form (3NF)
- **Rules**:
  1. Table must be in 2NF.
  2. No transitive dependency (non-prime attributes must not depend on other non-prime attributes).
- **OFS Example**: A Products table with ProductID, CategoryID, and CategoryName (transitively dependent on ProductID via CategoryID) violates 3NF.
  ```bash
  Before 3NF:
  | ProductID | Name       | CategoryID | CategoryName |
  |-----------|------------|------------|--------------|
  | 1         | Blue Dress | 101        | Dresses      |
  | 2         | Red Shirt  | 102        | Shirts       |
  ```
  - Solution: Split into Products and Categories tables.
  ```bash
  Products:
  | ProductID | Name       | CategoryID |
  |-----------|------------|------------|
  | 1         | Blue Dress | 101        |
  | 2         | Red Shirt  | 102        |

  Categories:
  | CategoryID | CategoryName |
  |------------|--------------|
  | 101        | Dresses      |
  | 102        | Shirts       |
  ```
- **SQL**:
  ```sql
  CREATE TABLE Categories (
      CategoryID INT PRIMARY KEY,
      CategoryName VARCHAR(50)
  );
  CREATE TABLE Products (
      ProductID INT PRIMARY KEY,
      Name VARCHAR(50),
      CategoryID INT,
      FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID)
  );
  ```

#### Boyce-Codd Normal Form (BCNF)
- **Rules**:
  1. Table must be in 3NF.
  2. For every functional dependency `X → Y`, `X` must be a super key.
- **OFS Example**: An Employees table with EmpID, Department, and DeptManager (where Department → DeptManager) violates BCNF if Department is not a super key.
  ```bash
  Before BCNF:
  | EmpID | Department | DeptManager |
  |-------|------------|-------------|
  | 1     | Sales      | Alice       |
  | 2     | Sales      | Alice       |
  ```
  - Solution: Split into Employees and Departments tables.
  ```bash
  Departments:
  | Department | DeptManager |
  |------------|-------------|
  | Sales      | Alice       |

  Employees:
  | EmpID | Department |
  |-------|------------|
  | 1     | Sales      |
  | 2     | Sales      |
  ```
- **SQL**:
  ```sql
  CREATE TABLE Departments (
      Department VARCHAR(50) PRIMARY KEY,
      DeptManager VARCHAR(50)
  );
  CREATE TABLE Employees (
      EmpID INT PRIMARY KEY,
      Department VARCHAR(50),
      FOREIGN KEY (Department) REFERENCES Departments(Department)
  );
  ```

#### Fourth Normal Form (4NF)
- **Rules**:
  1. Table must be in BCNF.
  2. No multi-valued dependencies (e.g., multiple independent values for an attribute).
- **OFS Example**: A Customers table with CustomerID, FavoriteCategory, and FavoriteColor (independent multi-valued attributes) violates 4NF.
  ```bash
  Before 4NF:
  | CustomerID | FavoriteCategory | FavoriteColor |
  |------------|-----------------|---------------|
  | 1          | Dresses         | Blue          |
  | 1          | Shirts          | Red           |
  ```
  - Solution: Split into separate tables.
  ```bash
  CustomerCategories:
  | CustomerID | FavoriteCategory |
  |------------|-----------------|
  | 1          | Dresses         |
  | 1          | Shirts          |

  CustomerColors:
  | CustomerID | FavoriteColor |
  |------------|---------------|
  | 1          | Blue          |
  | 1          | Red           |
  ```
- **SQL**:
  ```sql
  CREATE TABLE CustomerCategories (
      CustomerID INT,
      FavoriteCategory VARCHAR(50),
      PRIMARY KEY (CustomerID, FavoriteCategory)
  );
  CREATE TABLE CustomerColors (
      CustomerID INT,
      FavoriteColor VARCHAR(50),
      PRIMARY KEY (CustomerID, FavoriteColor)
  );
  ```

#### Fifth Normal Form (5NF)
- **Rules**:
  1. Table must be in 4NF.
  2. No join dependency; joining tables must be lossless.
- **OFS Example**: A table tracking Customers, Products, and Warehouses with join dependency violates 5NF.
  ```bash
  Before 5NF:
  | CustomerID | ProductID | Warehouse |
  |------------|-----------|-----------|
  | 1          | 101       | Main      |
  | 1          | 102       | East      |
  ```
  - Solution: Split into three tables to eliminate join dependency.
  ```bash
  CustomerProducts:
  | CustomerID | ProductID |
  |------------|-----------|
  | 1          | 101       |
  | 1          | 102       |

  ProductWarehouses:
  | ProductID | Warehouse |
  |-----------|-----------|
  | 101       | Main      |
  | 102       | East      |

  CustomerWarehouses:
  | CustomerID | Warehouse |
  |------------|-----------|
  | 1          | Main      |
  | 1          | East      |
  ```
- **SQL**:
  ```sql
  CREATE TABLE CustomerProducts (
      CustomerID INT,
      ProductID INT,
      PRIMARY KEY (CustomerID, ProductID)
  );
  CREATE TABLE ProductWarehouses (
      ProductID INT,
      Warehouse VARCHAR(50),
      PRIMARY KEY (ProductID, Warehouse)
  );
  CREATE TABLE CustomerWarehouses (
      CustomerID INT,
      Warehouse VARCHAR(50),
      PRIMARY KEY (CustomerID, Warehouse)
  );
  ```

## Denormalization
### Definition and Purpose
- **Denormalization**: Intentionally adding redundant data to tables to optimize query performance by reducing joins.
- **Purpose**: Improve read performance for OFS reporting (e.g., faster sales reports).
- **OFS Example**: Combine Customers and Orders into one table for faster order history queries.
  ```bash
  Denormalized:
  | CustomerID | Name  | OrderID | OrderTotal |
  |------------|-------|---------|------------|
  | 1          | Mary  | 101     | 50.00      |
  | 1          | Mary  | 102     | 75.00      |
  ```

### Pros of Denormalization
- Faster data retrieval with fewer joins.
- Simpler queries (e.g., single table for OFS order reports).
- Improved read performance for analytics.

### Cons of Denormalization
- Increased data redundancy (e.g., repeated customer names).
- Higher storage requirements.
- Complex updates (e.g., update all rows for a customer’s name change).
- Potential data inconsistency if not managed properly.

### OFS Use Case
- **Normalized**: Separate Customers and Orders tables require joins for reports.
- **Denormalized**: Single table with customer and order data for faster reporting, but updates to customer details are complex.

## Relational Algebra
### Definition and Purpose
- **Relational Algebra**: A procedural query language for manipulating relational databases using mathematical operators.
- **Purpose**: Define how to retrieve OFS data (e.g., customer orders) and form the basis for SQL.
- **Characteristics**: Uses operators (e.g., σ, ∏) to transform input relations into output relations.

### Operations
- **Unary**:
  - **Select (σ)**: Filters rows (e.g., `σ Total > 50 (Orders)`).
  - **Project (∏)**: Selects columns (e.g., `∏ Name, Price (Products)`).
  - **Rename (ρ)**: Renames tables/attributes.
- **Binary**:
  - **Union (∪)**: Combines rows, removes duplicates.
  - **Intersection (∩)**: Common rows.
  - **Set Difference (−)**: Rows in one table but not another.
  - **Cartesian Product (×)**: Combines all rows.
  - **Joins**: Theta, Natural, Outer Joins.
  - **Division (÷)**: Tuples related to all tuples in another relation.

### OFS Examples
- **Select**: Find orders over $100.
  ```
  σ Total > 100 (Orders)
  ```
  - **SQL**:
    ```sql
    SELECT * FROM Orders WHERE Total > 100;
    ```
- **Project**: List product names and prices.
  ```
  ∏ Name, Price (Products)
  ```
  - **SQL**:
    ```sql
    SELECT Name, Price FROM Products;
    ```
- **Natural Join**: Combine Orders and Customers.
  ```
  Orders ⋈ Customers
  ```
  - **SQL**:
    ```sql
    SELECT * FROM Orders NATURAL JOIN Customers;
    ```

## Relational Calculus
### Definition
- **Relational Calculus**: A declarative query language specifying what data to retrieve without how.
- **Types**:
  - **Tuple Relational Calculus (TRC)**: Uses tuple variables.
  - **Domain Relational Calculus (DRC)**: Uses attribute values.

### Tuple Relational Calculus (TRC)
- **Syntax**: `{ t | P(t) }` (t = tuple, P(t) = predicate).
- **OFS Example**: Find customer names with orders > $100.
  ```
  { t.Name | Customers(t) ∧ ∃ o (Orders(o) ∧ o.CustomerID = t.CustomerID ∧ o.Total > 100) }
  ```
- **SQL**:
  ```sql
  SELECT Name FROM Customers c WHERE EXISTS (SELECT * FROM Orders o WHERE o.CustomerID = c.CustomerID AND o.Total > 100);
  ```

### Domain Relational Calculus (DRC)
- **Syntax**: `{ <x1, x2, ...> | P(x1, x2, ...) }`.
- **OFS Example**: Find product names with ProductID > 10.
  ```
  { <Name, ProductID> | <Name, ProductID> ∈ Products ∧ ProductID > 10 }
  ```
- **SQL**:
  ```sql
  SELECT Name, ProductID FROM Products WHERE ProductID > 10;
  ```

## ER Model
### Entities
- **Strong Entity**: Has a primary key (e.g., Customers: CustomerID).
- **Weak Entity**: Depends on a strong entity (e.g., OrderDetails depends on Orders).
- **OFS Example**: Customers (strong), OrderDetails (weak).

### Attributes
- **Key**: CustomerID.
- **Composite**: Address (Street, City).
- **Multivalued**: PhoneNumbers.
- **Derived**: Age (from DOB).

### Cardinality
- **One-to-Many**: One Customer, many Orders.
- **Many-to-Many**: Customers and Products via OrderDetails.

### OFS ERD
```bash
[Customers] --(Places)--> [Orders] --(Contains)--> [Products]
| CustomerID (PK)        | OrderID (PK)            | ProductID (PK)
| Name                  | CustomerID (FK)         | Name
| Address               | Total                   | Price
```

## Relational Model
- **Components**: Tables, Tuples, Attributes, Primary Keys, Foreign Keys.
- **OFS Example**:
  ```sql
  CREATE TABLE Customers (
      CustomerID INT PRIMARY KEY,
      Name VARCHAR(50)
  );
  CREATE TABLE Orders (
      OrderID INT PRIMARY KEY,
      CustomerID INT,
      FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
  );
  ```

### Keys
- **Candidate Key**: CustomerID, Email.
- **Primary Key**: CustomerID.
- **Super Key**: {CustomerID, Name}.
- **Alternate Key**: Email.
- **Foreign Key**: Orders.CustomerID.
- **Composite Key**: OrderDetails(OrderID, ProductID).

## Exercises
1. **Normalization**:
   - Normalize the following OFS table to 3NF:
     ```bash
     | CustomerID | Name  | OrderID | ProductID | ProductName | Category |
     |------------|-------|---------|-----------|-------------|----------|
     | 1          | Mary  | 101     | 201       | Blue Dress  | Dresses  |
     ```
   - Identify functional dependencies and split into tables.
2. **Relational Algebra**:
   - Find customers with orders > $50.
     ```
     σ Total > 50 (Orders) ⋈ Customers
     ```
   - List unique product names from Products and Products_Archive.
     ```
     ∏ Name (Products) ∪ ∏ Name (Products_Archive)
     ```
3. **Relational Calculus**:
   - TRC: Find customers with orders from "Main" warehouse.
     ```
     { t.Name | Customers(t) ∧ ∃ o (Orders(o) ∧ o.CustomerID = t.CustomerID ∧ o.Warehouse = "Main") }
     ```
   - DRC: Find order IDs with total > $200.
     ```
     { <o> | ∃ c, t (<o, c, t> ∈ Orders ∧ t > 200) }
     ```

## References
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Tutorialspoint: Domain Relational Calculus](https://www.tutorialspoint.com/domain-relational-calculus-in-dbms)
- [GeeksforGeeks: Tuple Relational Calculus](https://www.geeksforgeeks.org/tuple-relational-calculus-trc-in-dbms/)
- [Javatpoint: Relational Calculus](https://www.javatpoint.com/dbms-relational-calculus)