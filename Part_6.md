# SQL Databases

## Introduction

Data is one of the most important parts of any application.

Applications like:

* Instagram
* Amazon
* Netflix
* WhatsApp
* Banking Systems

need a place to store and manage data.

One of the most common ways to store structured data is using **SQL Databases**.

SQL databases are based on the **Relational Database Model**, where data is organized into tables and relationships.

---

# What are SQL Databases?

## Definition

SQL stands for:

**Structured Query Language**

SQL Databases are databases that store data in the form of tables consisting of rows and columns.

They use SQL to:

* Create data
* Read data
* Update data
* Delete data

These operations are commonly called:

```text
CRUD Operations
```

* Create
* Read
* Update
* Delete

---

## Popular SQL Databases

* MySQL
* PostgreSQL
* Oracle Database
* Microsoft SQL Server
* SQLite

---

# Relational Databases

## Definition

A Relational Database stores data in multiple tables and connects those tables using relationships.

In simple words:

> Data is stored in separate tables, and relationships are used to connect related data.

---

## Example

An E-Commerce Application may have:

```text
Users Table
Orders Table
Products Table
Payments Table
```

Instead of storing everything in one large table, data is divided into smaller related tables.

This reduces duplication and improves organization.

---

# Tables, Rows, and Columns

Understanding these three concepts is fundamental.

---

# Table

## Definition

A table is a collection of related data.

Think of it as a spreadsheet.

### Example

### Users Table

| UserID | Name  | Email                                     |
| ------ | ----- | ----------------------------------------- |
| 1      | Rahul | [rahul@gmail.com](mailto:rahul@gmail.com) |
| 2      | Aman  | [aman@gmail.com](mailto:aman@gmail.com)   |

Here, the entire structure is called a table.

---

# Row

## Definition

A row represents a single record.

### Example

```text
1 | Rahul | rahul@gmail.com
```

This complete entry represents one row.

---

## Example

| UserID | Name  | Email                                     |
| ------ | ----- | ----------------------------------------- |
| 1      | Rahul | [rahul@gmail.com](mailto:rahul@gmail.com) |
| 2      | Aman  | [aman@gmail.com](mailto:aman@gmail.com)   |

There are 2 rows in this table.

---

# Column

## Definition

A column represents a specific attribute of data.

### Example

| UserID | Name | Email |
| ------ | ---- | ----- |

Columns are:

* UserID
* Name
* Email

Each column stores a specific type of information.

---

# Visualization

```text
          Columns
    ---------------------
    UserID | Name | Email
Rows ↓
    ---------------------
      1   | Rahul | rahul@gmail.com
      2   | Aman  | aman@gmail.com
```

---

# Constraints

## Definition

Constraints are rules applied to database columns to maintain data accuracy and integrity.

In simple words:

> Constraints prevent invalid data from being stored.

---

## Why Constraints Are Important

Without constraints:

```text
UserID = NULL
Email = Empty
Duplicate IDs
```

could be inserted.

This can cause serious problems.

---

# Common Constraints

## NOT NULL

Ensures a column cannot contain NULL values.

### Example

```sql
Name VARCHAR(100) NOT NULL
```

Every user must have a name.

---

## UNIQUE

Ensures all values are unique.

### Example

```sql
Email VARCHAR(100) UNIQUE
```

No two users can have the same email.

---

## DEFAULT

Provides a default value.

### Example

```sql
Status VARCHAR(20) DEFAULT 'Active'
```

---

## CHECK

Validates data before insertion.

### Example

```sql
Age INT CHECK (Age >= 18)
```

Only users above 18 years can be stored.

---

# Primary Key

## Definition

A Primary Key uniquely identifies every row in a table.

### Characteristics

* Unique
* Cannot be NULL
* Only one Primary Key per table

---

## Example

### Users Table

| UserID (PK) | Name  |
| ----------- | ----- |
| 1           | Rahul |
| 2           | Aman  |
| 3           | Priya |

Here:

```text
UserID
```

is the Primary Key.

Every user has a unique ID.

---

## Why Primary Key Is Important

Without a Primary Key:

```text
Rahul
Rahul
Rahul
```

it becomes difficult to identify a specific user.

Primary Keys solve this problem.

---

# Foreign Key

## Definition

A Foreign Key is a column that references the Primary Key of another table.

It creates relationships between tables.

---

## Example

### Users Table

| UserID (PK) | Name  |
| ----------- | ----- |
| 1           | Rahul |
| 2           | Aman  |

### Orders Table

| OrderID | UserID (FK) |
| ------- | ----------- |
| 101     | 1           |
| 102     | 1           |
| 103     | 2           |

Here:

```text
Orders.UserID
```

references:

```text
Users.UserID
```

This creates a relationship between users and orders.

---

# Primary Key vs Foreign Key

| Feature         | Primary Key               | Foreign Key     |
| --------------- | ------------------------- | --------------- |
| Purpose         | Uniquely identifies a row | Connects tables |
| Unique          | Yes                       | Not Required    |
| NULL Allowed    | No                        | Usually Yes     |
| Count Per Table | One                       | Multiple        |

---

# Joins and Relationships

## What is a Join?

A Join combines data from multiple tables using relationships.

In simple words:

> Joins allow us to fetch related data from different tables.

---

## Example

### Users Table

| UserID | Name  |
| ------ | ----- |
| 1      | Rahul |
| 2      | Aman  |

### Orders Table

| OrderID | UserID |
| ------- | ------ |
| 101     | 1      |
| 102     | 2      |

---

Using JOIN:

```sql
SELECT *
FROM Users
JOIN Orders
ON Users.UserID = Orders.UserID;
```

Result:

| Name  | OrderID |
| ----- | ------- |
| Rahul | 101     |
| Aman  | 102     |

---

# Types of Relationships

In relational databases, tables are connected using relationships.

There are three major relationship types:

1. One-to-One
2. One-to-Many
3. Many-to-Many

---

# One-to-One Relationship

## Definition

One record in Table A is related to exactly one record in Table B.

---

## Example

### Users Table

| UserID |
| ------ |
| 1      |
| 2      |

### UserProfiles Table

| ProfileID | UserID |
| --------- | ------ |
| 101       | 1      |
| 102       | 2      |

Relationship:

```text
One User
     ↓
One Profile
```

---

## Real-World Example

* User → Passport
* User → Profile
* Employee → Employee ID Card

---

## Visualization

```text
User 1  ↔  Profile 1
User 2  ↔  Profile 2
```

---

# One-to-Many Relationship

## Definition

One record in Table A can be related to many records in Table B.

This is the most common database relationship.

---

## Example

### Users Table

| UserID | Name  |
| ------ | ----- |
| 1      | Rahul |

### Orders Table

| OrderID | UserID |
| ------- | ------ |
| 101     | 1      |
| 102     | 1      |
| 103     | 1      |

One user can place multiple orders.

---

## Visualization

```text
User
  ↓
 ├── Order 1
 ├── Order 2
 └── Order 3
```

---

## Real-World Examples

* User → Orders
* Customer → Transactions
* Teacher → Students
* Category → Products

---

# Many-to-Many Relationship

## Definition

Many records in Table A can be related to many records in Table B.

---

## Example

Students and Courses

A student can enroll in multiple courses.

A course can have multiple students.

---

### Students Table

| StudentID | Name  |
| --------- | ----- |
| 1         | Rahul |
| 2         | Aman  |

---

### Courses Table

| CourseID | Course |
| -------- | ------ |
| 101      | Java   |
| 102      | SQL    |

---

### Enrollment Table

| StudentID | CourseID |
| --------- | -------- |
| 1         | 101      |
| 1         | 102      |
| 2         | 101      |

---

## Visualization

```text
Student 1
    ├── Java
    └── SQL

Student 2
    └── Java
```

---

## Why a Third Table Is Needed?

Direct Many-to-Many relationships are not supported efficiently.

A bridge table (junction table) is created.

Example:

```text
Students
     ↓
Enrollments
     ↓
Courses
```

This bridge table stores relationships.

---

# Relationship Summary

| Relationship | Example            |
| ------------ | ------------------ |
| One-to-One   | User ↔ Profile     |
| One-to-Many  | User → Orders      |
| Many-to-Many | Students ↔ Courses |

---

# Real-World Database Example

Consider an E-Commerce System.

### One-to-One

```text
User ↔ User Profile
```

### One-to-Many

```text
User → Orders
```

### Many-to-Many

```text
Orders ↔ Products
```

One order contains multiple products.

One product can appear in multiple orders.

---

# Why SQL Databases Are Popular

SQL databases provide:

* Structured data storage
* Data consistency
* Strong relationships
* Powerful querying
* Data integrity
* ACID compliance

They are ideal for applications where relationships between data are important.

Examples:

* Banking Systems
* E-Commerce Platforms
* ERP Systems
* Hospital Management Systems

---

# Key Takeaways

## Relational Databases

* Store data in tables.
* Use relationships to connect data.

## Tables, Rows, Columns

* Table → Collection of data
* Row → Single record
* Column → Data attribute

## Constraints

Maintain data integrity.

Examples:

* NOT NULL
* UNIQUE
* CHECK
* DEFAULT

## Primary Key

* Uniquely identifies rows.
* Cannot be NULL.
* Must be unique.

## Foreign Key

* References another table's Primary Key.
* Creates relationships.

## Joins

* Combine data from multiple tables.
* Use relationships between tables.

## Relationship Types

### One-to-One

```text
User ↔ Profile
```

### One-to-Many

```text
User → Orders
```

### Many-to-Many

```text
Students ↔ Courses
```

using a bridge table.

## Final Note

SQL databases organize data into related tables using Primary Keys, Foreign Keys, and Relationships. These concepts form the foundation of database design and are heavily used in Full Stack Development, Backend Development, and System Design interviews.
