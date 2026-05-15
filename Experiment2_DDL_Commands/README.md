# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'

```sql
CREATE TABLE Attendance(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK(Status IN ('Present', 'Absent','Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
    );
```

**Output:**

<img width="1227" height="327" alt="image" src="https://github.com/user-attachments/assets/f343e522-2223-47d6-b88f-207683f165eb" />



**Question 2**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.
````sql
CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
````
```sql
INSERT INTO Customers(CustomerID, Name, Address) VALUES (304,'Peter Parker','Spider St');
```

**Output:**

<img width="1193" height="311" alt="image" src="https://github.com/user-attachments/assets/3ccad484-571f-4d1f-8eea-66b6f7bf267d" />



**Question 3**
---
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
CREATE TABLE contacts(
    contact_id INTEGER PRIMARY KEY,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    email TEXT,
    phone TEXT NOT NULL CHECK(LENGTH(phone)>=10)
);
```

**Output:**

<img width="1189" height="311" alt="image" src="https://github.com/user-attachments/assets/11f7092d-8a40-4185-8b5d-7b925cc24b33" />


**Question 4**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments(
    AssignmentID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY(ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1181" height="245" alt="image" src="https://github.com/user-attachments/assets/f832a0ff-a7c5-4878-ab5b-b57eb1122aa7" />


**Question 5**
---
Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer
````sql
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
````
```sql
ALTER TABLE customer
RENAME COLUMN city TO location;
```

**Output:**

<img width="1180" height="313" alt="image" src="https://github.com/user-attachments/assets/01f94054-39b4-459a-9d00-eaae7591fbde" />


**Question 6**
---
Create a table named Members with the following columns:

MemberID as INTEGER
MemberName as TEXT
JoinDate as DATE

```sql
CREATE TABLE Members(
    MemberID INTEGER,
    MemberName TEXT,
    JoinDate DATE
);
```

**Output:**

<img width="1171" height="360" alt="image" src="https://github.com/user-attachments/assets/d6bd5d01-33b9-4ef2-a95d-c40e7a38056b" />


**Question 7**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
INSERT INTO Customers
SELECT * FROM Old_customers;
```

**Output:**

<img width="1173" height="242" alt="image" src="https://github.com/user-attachments/assets/30960709-6aed-4929-acc2-034ed5b746ae" />


**Question 8**
---
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.

```sql
CREATE TABLE Bonuses(
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK(BonusAmount>0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1176" height="233" alt="image" src="https://github.com/user-attachments/assets/72b847f8-4e0e-4b53-8394-4fa135bc135d" />


**Question 9**
---
Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.
````sql
EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst
````
Note: The Department and Salary columns will use their default values.  

```sql
INSERT INTO Employee(EmployeeID,Name,Position) VALUES (4,'Emily White','Analyst');
```

**Output:**

<img width="1091" height="294" alt="image" src="https://github.com/user-attachments/assets/27a98871-8b39-4be6-b7ae-8fa5aaed946d" />

**Question 10**
---
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

```sql
ALTER TABLE Student_details
ADD MobileNumber NUMBER;

ALTER TABLE Student_details
ADD Address VARCHAR(100);
```

**Output:**

<img width="1175" height="287" alt="image" src="https://github.com/user-attachments/assets/c30fd268-95a5-417f-b64c-ee78ecbaa7d3" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
