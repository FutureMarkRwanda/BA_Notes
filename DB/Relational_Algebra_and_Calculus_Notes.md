# Relational Algebra and Relational Calculus Notes

## In Summary
This guide focuses on relational algebra and relational calculus, key theoretical foundations for querying and managing data in relational databases, using an Online Fashion Store (OFS) as a practical example. It covers the Entity-Relationship (ER) Model, Relational Model, and database schema concepts, with OFS-specific examples and SQL equivalents to ensure clarity for beginners.

## Relational Algebra
### Definition and Purpose
- **Relational Algebra**: A procedural query language that defines how to retrieve and manipulate data in a relational database. It provides a mathematical foundation for SQL and operates on relations (tables) to produce new relations.
- **Purpose**: Retrieve data (e.g., OFS customer orders) or perform operations (insert, update, delete) by specifying both **what** data to retrieve and **how** to retrieve it.
- **Characteristics**:
  - Uses mathematical operators (e.g., σ, ∏, ∪) without English keywords.
  - Forms the basis for high-level languages like SQL.
  - Operators take relations as input and produce relations as output, enabling complex queries.

### Types of Operations
Relational algebra operations are divided into:
1. **Basic/Fundamental Operations**:
   - **Unary Operations** (operate on one table):
     - **Select (σ)**: Filters rows based on a condition.
     - **Project (∏)**: Selects specific columns.
     - **Rename (ρ)**: Renames relations or attributes.
   - **Binary Operations** (operate on two tables):
     - **Union (∪)**: Combines rows from two tables, removing duplicates.
     - **Intersection (∩)**: Returns rows common to two tables.
     - **Set Difference (−)**: Returns rows in one table but not another.
     - **Cartesian Product (×)**: Combines all rows from two tables.
2. **Derived Operations**:
   - **Joins**: Theta Join, Natural Join, Outer Joins (Left, Right, Full).
   - **Division (÷)**: Finds tuples related to all tuples in another relation.

### OFS Examples
Consider the following OFS tables:
- **Customers**: `(CustomerID, Name, City)`
- **Orders**: `(OrderID, CustomerID, Total)`
- **Products**: `(ProductID, Name, Price)`

#### Select (σ)
- **Purpose**: Select rows meeting a condition (similar to SQL WHERE).
- **Syntax**: `σ Condition (Table)`
- **OFS Example**: Find customers in Kigali.
  ```
  σ City="Kigali" (Customers)
  ```
- **SQL Equivalent**:
  ```sql
  SELECT * FROM Customers WHERE City = 'Kigali';
  ```
- **Output** (example):

  | CustomerID | Name  | City   |
  |------------|-------|--------|
  | C10100     | Steve | Kigali |
  | C10111     | Olive | Kigali |

#### Project (∏)
- **Purpose**: Select specific columns (similar to SQL SELECT).
- **Syntax**: `∏ Column1, Column2 (Table)`
- **OFS Example**: Display customer names and cities.
  ```
  ∏ Name, City (Customers)
  ```
- **SQL Equivalent**:
  ```sql
  SELECT Name, City FROM Customers;
  ```
- **Output** (example):

  | Name  | City      |
  |-------|-----------|
  | Steve | Kigali    |
  | Olive | Kigali    |
  | Kabanda | Musanze |

#### Rename (ρ)
- **Purpose**: Rename a relation or its attributes.
- **Syntax**: `ρ NewName (Table)` or `ρ NewName(NewAttr1, NewAttr2) (Table)`
- **OFS Example**: Rename Customers to OFS_Customers and attributes to (ID, CustomerName).
  ```
  ρ OFS_Customers(ID, CustomerName, City) ∏ CustomerID, Name, City (Customers)
  ```
- **SQL Equivalent**:
  ```sql
  SELECT CustomerID AS ID, Name AS CustomerName, City FROM Customers;
  ```

#### Union (∪)
- **Purpose**: Combine rows from two tables, removing duplicates.
- **Conditions**: Tables must have the same number of attributes with compatible domains.
- **OFS Example**: List all product names from Products and archived products (Products_Archive).
  ```
  ∏ Name (Products) ∪ ∏ Name (Products_Archive)
  ```
- **SQL Equivalent**:
  ```sql
  SELECT Name FROM Products UNION SELECT Name FROM Products_Archive;
  ```

#### Intersection (∩)
- **Purpose**: Return rows common to two tables.
- **OFS Example**: Find customers who placed orders and are in a loyalty program (Loyalty).
  ```
  ∏ CustomerID (Orders) ∩ ∏ CustomerID (Loyalty)
  ```
- **SQL Equivalent**:
  ```sql
  SELECT CustomerID FROM Orders INTERSECT SELECT CustomerID FROM Loyalty;
  ```

#### Set Difference (−)
- **Purpose**: Return rows in one table but not in another.
- **OFS Example**: Find products not ordered.
  ```
  ∏ ProductID (Products) − ∏ ProductID (Orders)
  ```
- **SQL Equivalent** (MySQL workaround, as it lacks EXCEPT):
  ```sql
  SELECT ProductID FROM Products WHERE ProductID NOT IN (SELECT ProductID FROM Orders);
  ```

#### Cartesian Product (×)
- **Purpose**: Combine all rows from two tables.
- **Syntax**: `Table1 × Table2`
- **OFS Example**: Combine Customers and Products.
  ```
  Customers × Products
  ```
- **Cardinality**: Number of rows = Rows(Customers) × Rows(Products).
- **Degree**: Number of columns = Columns(Customers) + Columns(Products).
- **SQL Equivalent**:
  ```sql
  SELECT * FROM Customers CROSS JOIN Products;
  ```

#### Joins
- **Theta Join**: Joins tables based on a condition (non-equality).
  - **OFS Example**: Find orders where Total > Product Price.
    ```
    Orders ⋈ Orders.Total > Products.Price Products
    ```
    - **SQL**:
      ```sql
      SELECT * FROM Orders, Products WHERE Orders.Total > Products.Price;
      ```
- **Natural Join (⋈)**: Joins tables on equal attributes.
  - **OFS Example**: Join Orders and Customers on CustomerID.
    ```
    Orders ⋈ Customers
    ```
    - **SQL**:
      ```sql
      SELECT * FROM Orders NATURAL JOIN Customers;
      ```
- **Outer Joins**:
  - **Left Outer Join (⟕)**: Includes all rows from the left table.
    ```
    Customers ⟕ Orders
    ```
    - **SQL**:
      ```sql
      SELECT * FROM Customers LEFT OUTER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
      ```
  - **Right Outer Join (⟖)**: Includes all rows from the right table.
  - **Full Outer Join (⟗)**: Includes all rows from both tables.

#### Division (÷)
- **Purpose**: Find tuples in one relation associated with all tuples in another.
- **OFS Example**: Find customers who ordered all products in a specific category (Category_Products).
  ```
  Orders ÷ ∏ ProductID (Category_Products)
  ```
- **SQL Equivalent** (approximation):
  ```sql
  SELECT CustomerID FROM Orders o
  WHERE NOT EXISTS (
      SELECT ProductID FROM Category_Products cp
      WHERE NOT EXISTS (
          SELECT * FROM Orders o2
          WHERE o2.CustomerID = o.CustomerID AND o2.ProductID = cp.ProductID
      )
  );
  ```

## Relational Calculus
### Definition and Purpose
- **Relational Calculus**: A declarative, non-procedural query language that specifies **what** data to retrieve without detailing **how**. It uses logical formulas to describe desired results.
- **Types**:
  - **Tuple Relational Calculus (TRC)**: Focuses on tuples (rows).
  - **Domain Relational Calculus (DRC)**: Focuses on attribute values.
- **Purpose**: Provides a mathematical basis for querying relational databases, complementing relational algebra.

### Tuple Relational Calculus (TRC)
- **Definition**: Specifies queries using tuple variables and logical predicates.
- **Syntax**: `{ t | P(t) }`
  - `t`: Tuple variable (represents a row).
  - `P(t)`: Predicate (conditions for tuples).
  - Uses logical operators: AND (∧), OR (∨), NOT (¬).
  - Quantifiers:
    - **Existential (∃)**: There exists a tuple satisfying the condition.
    - **Universal (∀)**: All tuples satisfy the condition.
- **OFS Example**: Find customer names with orders over $100.
  ```
  { t.Name | Customers(t) ∧ ∃ o (Orders(o) ∧ o.CustomerID = t.CustomerID ∧ o.Total > 100) }
  ```
- **SQL Equivalent**:
  ```sql
  SELECT Name FROM Customers c
  WHERE EXISTS (SELECT * FROM Orders o WHERE o.CustomerID = c.CustomerID AND o.Total > 100);
  ```

### Domain Relational Calculus (DRC)
- **Definition**: Specifies queries using domain variables (attribute values) and predicates.
- **Syntax**: `{ <x1, x2, ..., xn> | P(x1, x2, ..., xn) }`
  - `x1, x2, ...`: Domain variables (attribute values).
  - `P`: Predicate with comparison operators and quantifiers.
- **OFS Example**: Find product names with ProductID > 10.
  ```
  { <Name, ProductID> | <Name, ProductID> ∈ Products ∧ ProductID > 10 }
  ```
- **SQL Equivalent**:
  ```sql
  SELECT Name, ProductID FROM Products WHERE ProductID > 10;
  ```
- **OFS Example (Complex)**: Find customer names and order amounts for orders from the "Main" warehouse.
  ```
  { <c, a> | ∃ l (<c, l> ∈ OrderDetails ∧ ∃ w (<l, w, a> ∈ Orders ∧ w = "Main")) }
  ```
- **SQL Equivalent**:
  ```sql
  SELECT c.Name, o.Total
  FROM Customers c, OrderDetails od, Orders o
  WHERE c.CustomerID = od.CustomerID AND od.OrderID = o.OrderID AND o.Warehouse = 'Main';
  ```

## ER Model
### Entities
- **Definition**: Objects with physical (e.g., Customer) or conceptual (e.g., Order) existence.
- **Entity Set**: Collection of entities of the same type (e.g., all OFS customers).
- **Strong Entity**: Has a key attribute (e.g., Customer with CustomerID). Represented by a rectangle.
- **Weak Entity**: Depends on a strong entity, no unique key (e.g., OrderDetails depending on Orders). Represented by a double rectangle.
- **OFS Example**:
  - Strong: Customers (CustomerID, Name).
  - Weak: OrderDetails (OrderID, ProductID, Quantity), depends on Orders.

### Attributes
- **Definition**: Properties of entities (e.g., Customer: Name, Email).
- **Types**:
  - **Key Attribute**: Uniquely identifies an entity (e.g., CustomerID). Shown with underlined oval.
  - **Composite Attribute**: Composed of multiple attributes (e.g., Address: Street, City). Oval with sub-ovals.
  - **Multivalued Attribute**: Multiple values (e.g., PhoneNumbers). Double oval.
  - **Derived Attribute**: Calculated from others (e.g., Age from DOB). Dashed oval.
- **OFS Example**:
  - Customer: CustomerID (Key), Name, Address (Composite: Street, City), PhoneNumbers (Multivalued), Age (Derived).

### Cardinality
- **Definition**: Number of times an entity participates in a relationship.
- **Types**:
  - **One-to-One**: One Customer has one Account (e.g., Customer ↔ Account).
  - **One-to-Many**: One Customer places many Orders (e.g., Customer → Orders).
  - **Many-to-One**: Many Orders belong to one Customer.
  - **Many-to-Many**: Customers purchase multiple Products, Products bought by multiple Customers.
- **OFS Example**: Customer to Orders is One-to-Many.

### OFS ERD
- **Entities**: Customers, Orders, Products.
- **Relationships**: Customer places Orders (One-to-Many), Orders contain Products (Many-to-Many via OrderDetails).
- **Diagram** (text representation):
  ```bash
  [Customers] --(Places)--> [Orders] --(Contains)--> [Products]
  | CustomerID (PK)        | OrderID (PK)            | ProductID (PK)
  | Name                  | CustomerID (FK)         | Name
  | Address (Composite)   | Total                   | Price
  ```

## Relational Model
- **Definition**: Represents data as tables (relations) with rows (tuples) and columns (attributes), introduced by Edgar F. Codd (1970).
- **Components**:
  - **Tables**: Relations (e.g., OFS Products table).
  - **Attributes**: Columns (e.g., ProductID, Name).
  - **Tuples**: Rows (e.g., a specific product).
  - **Primary Key**: Unique identifier (e.g., ProductID).
  - **Foreign Key**: Links tables (e.g., Orders.CustomerID references Customers.CustomerID).
  - **Normalization**: Reduces redundancy by decomposing tables.
- **OFS Example**:
  ```sql
  CREATE TABLE Customers (
      CustomerID INT PRIMARY KEY,
      Name VARCHAR(50),
      City VARCHAR(50)
  );
  CREATE TABLE Orders (
      OrderID INT PRIMARY KEY,
      CustomerID INT,
      Total DECIMAL(10,2),
      FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
  );
  ```

### Types of Keys
- **Candidate Key**: Minimal set of attributes to uniquely identify tuples (e.g., CustomerID, Email in Customers).
- **Primary Key**: Chosen candidate key (e.g., CustomerID).
- **Super Key**: Any set of attributes that uniquely identifies tuples (e.g., {CustomerID, Name}).
- **Alternate Key**: Candidate keys not chosen as primary (e.g., Email).
- **Foreign Key**: Links to another table’s primary key (e.g., Orders.CustomerID).
- **Composite Key**: Multiple attributes to uniquely identify tuples (e.g., OrderDetails(OrderID, ProductID)).

## Database Schema
- **Definition**: Logical blueprint defining database structure, constraints, and access rules.
- **Types**:
  - **Logical Schema**: Defines tables, attributes, relationships (e.g., OFS tables).
  - **Physical Schema**: Describes storage details (e.g., indexing, file organization).
- **Components**:
  - **Structure**: Tables, attributes, data types (e.g., Customers: CustomerID INT, Name VARCHAR).
  - **Constraints**: Primary Key, Foreign Key, Unique, Check.
  - **Security**: Access control (e.g., GRANT SELECT to OFS users).
  - **Views**: Virtual tables (e.g., view for high-value orders).
  - **Data Integrity**: Ensures consistency (e.g., foreign key constraints).
- **OFS Example**:
  ```sql
  CREATE TABLE Products (
      ProductID INT PRIMARY KEY,
      Name VARCHAR(50) NOT NULL,
      Price DECIMAL(10,2) CHECK (Price > 0),
      UNIQUE(Name)
  );
  ```

## Exercises
1. **Relational Algebra**:
   - Write a query to select OFS customers with orders > $50.
     ```
     σ Total > 50 (Orders) ⋈ Customers
     ```
   - Project product names and prices for products over $100.
     ```
     ∏ Name, Price (σ Price > 100 (Products))
     ```
   - Find customers who ordered all products in a category (use division).
2. **Relational Calculus**:
   - TRC: Find customer names with orders from "Main" warehouse.
     ```
     { t.Name | Customers(t) ∧ ∃ o (Orders(o) ∧ o.CustomerID = t.CustomerID ∧ o.Warehouse = "Main") }
     ```
   - DRC: Find order IDs with total > $200.
     ```
     { <o> | ∃ c, t (<o, c, t> ∈ Orders ∧ t > 200) }
     ```
3. **ER Model**:
   - Draw an ERD for OFS with Customers, Orders, Products, and OrderDetails (Many-to-Many).
   - Define attributes and cardinalities.

## References
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Tutorialspoint: Domain Relational Calculus](https://www.tutorialspoint.com/domain-relational-calculus-in-dbms)
- [GeeksforGeeks: Tuple Relational Calculus](https://www.geeksforgeeks.org/tuple-relational-calculus-trc-in-dbms/)
- [Javatpoint: Relational Calculus](https://www.javatpoint.com/dbms-relational-calculus)