# Module 2

# Types of SQL Statements

## 1. Overview

SQL statements are the primary method for interacting with Relational Databases. They allow you to work with:

- **Entities:** Tables
- **Attributes:** Columns
- **Tuples:** Rows with data values

SQL statements are broadly categorized into two types: **Data Definition Language (DDL)** and **Data Manipulation Language (DML)**.

---

## 2. Data Definition Language (DDL)

DDL statements are used to **define, change, or drop** database objects (like tables) themselves. They deal with the _structure_ of the database, not the specific data inside the rows.

### Common DDL Commands:

- **CREATE:** Used for creating new tables and defining their columns.
- **ALTER:** Used for modifying existing tables (e.g., adding/dropping columns, changing data types).
- **TRUNCATE:** Used for deleting **all data** inside a table, but keeps the table structure intact.
- **DROP:** Used for deleting the table entirely (structure + data).

---

## 3. Data Manipulation Language (DML)

DML statements are used to **read and modify** the actual data within the tables. These are often referred to as **CRUD** operations (Create, Read, Update, Delete).

### Common DML Commands:

- **INSERT:** Adds a single row or multiple rows of data into a table. _(Create)_
- **SELECT:** Reads or retrieves specific rows from a table. _(Read)_
- **UPDATE:** Edits existing rows in a table. _(Update)_
- **DELETE:** Removes specific rows of data from a table. _(Delete)_

---

# The CREATE TABLE Statement

## 1. Overview

The `CREATE TABLE` statement is the most common **Data Definition Language (DDL)** command. It is used to define a new entity (table) and its attributes (columns) within a relational database.

## 2. Basic Syntax

To create a table, you must specify the table name and define the columns within parentheses.

**Structure:**

```sql
CREATE TABLE table_name (
    column1 datatype [optional_constraints],
    column2 datatype [optional_constraints],
    ...
);

```

- **Process:**

1. Start with `CREATE TABLE`.
2. Specify the `table_name`.
3. Open parentheses `( ... )`.
4. List column names followed by their **Data Type** and optional **Constraints**.
5. Separate each column definition with a comma.

---

## 3. Example 1: Creating a Simple Table

**Scenario:** Creating a table to store Canadian Provinces.

**SQL Code:**

```sql
CREATE TABLE provinces (
    id CHAR(2) PRIMARY KEY NOT NULL,
    name VARCHAR(24)
);

```

**Breakdown of Data Types:**

- **CHAR(2):** A character string of **fixed length** (always 2 characters). Used for abbreviations like 'AB', 'BC'.
- **VARCHAR(24):** A character string of **variable length** (up to 24 characters). Used for full names like 'Alberta' or 'British Columbia'.

---

## 4. Example 2: Complex Table with Constraints

**Scenario:** Creating an `Author` table for a library database.

**SQL Code:**

```sql
CREATE TABLE author (
    Author_ID CHAR(2) PRIMARY KEY NOT NULL,
    Lastname VARCHAR(15) NOT NULL,
    Firstname VARCHAR(15) NOT NULL,
    Email VARCHAR(40),
    City VARCHAR(15),
    Country CHAR(2)
);

```

**Key Constraints Explained:**

- **PRIMARY KEY:**
- Designates a column (or set of columns) as the unique identifier for the table.
- Ensures there are **no duplicate values** (e.g., two authors cannot have the same ID).
- Uniquely identifies each tuple (row).

- **NOT NULL:**
- Ensures that a column **cannot be left empty**.
- In the example above, `Lastname` and `Firstname` must have values because every author must have a name.

---

# Modifying and Deleting Tables (DDL)

## 1. The ALTER TABLE Statement

The `ALTER TABLE` statement is used to modify the structure of an existing table without deleting it. It allows you to:

- Add or remove columns.
- Modify the data type of columns.
- Add or remove keys and constraints.

**Key Syntax Note:** Unlike the `CREATE TABLE` statement, `ALTER TABLE` **does not** use parentheses to enclose parameters.

### A. Adding a Column

Used when you need to store new information in an existing table.

- **Syntax:** `ALTER TABLE table_name ADD COLUMN column_name data_type;`
- **Example:** Adding a telephone number column to the author table.

```sql
ALTER TABLE author ADD COLUMN telephone_number BIGINT;

```

_(Note: `BIGINT` can hold numbers up to 19 digits long)._

### B. Modifying a Column (Data Type)

Used to change the data type of an existing column (e.g., changing a numeric field to a character field to allow dashes and brackets).

- **Syntax:** `ALTER TABLE table_name ALTER COLUMN column_name SET DATA TYPE new_data_type;`
- **Example:** Changing the telephone number to `CHAR` to allow formatting.

```sql
ALTER TABLE author ALTER COLUMN telephone_number SET DATA TYPE CHAR(20);

```

> **Warning:** Altering a column that already contains data can cause errors if the existing data is incompatible with the new type (e.g., trying to convert text "ABC" into a Numeric type).

### C. Dropping a Column

Used when a column is no longer needed in the table specification.

- **Syntax:** `ALTER TABLE table_name DROP COLUMN column_name;`
- **Example:** Removing the telephone number column.

```sql
ALTER TABLE author DROP COLUMN telephone_number;

```

---

## 2. The DROP TABLE Statement

The `DROP TABLE` statement is used to completely remove a table from the database.

- **Effect:** It deletes the **Table Structure** AND all **Data** contained within it.
- **Syntax:** `DROP TABLE table_name;`
- **Example:**

```sql
DROP TABLE author;

```

---

## 3. The TRUNCATE TABLE Statement

The `TRUNCATE TABLE` statement is used to delete **all rows** of data in a table while keeping the table structure intact.

- **Efficiency:** It is generally faster and more efficient than using a `DELETE` statement without a `WHERE` clause.
- **Keyword:** The `IMMEDIATE` keyword is often used to indicate immediate processing and emphasizes that the action **cannot be reversed**.
- **Syntax:** `TRUNCATE TABLE table_name IMMEDIATE;`
- **Example:**

```sql
TRUNCATE TABLE author IMMEDIATE;

```

---

# Data Movement Utilities

## 1. Overview

Data Engineers and Database Administrators (DBAs) frequently move data in and out of databases.
**Common Reasons for Data Movement:**

- **Populating:** Filling the database and objects (tables) with initial data.
- **Duplication:** Creating copies of the database for development or testing environments.
- **Disaster Recovery:** Creating snapshots of the database state.
- **Integration:** Generating new tables using data from external sources or files.
- **Appending:** Adding data into existing tables.

---

## 2. Methods for Data Movement

There are three primary categories of tools used for moving data:

1. **Backup and Restore**
2. **Import and Export**
3. **Load**

---

## 3. Backup and Restore

This method is used to create an exact replica of the database.

- **Backup Operation:**
- Creates a file (or set of files) that encapsulates **all** database objects and their data.
- **Preserves:** Schemas, tables, views, functions, stored procedures, constraints, triggers, security settings, and relationships.

- **Restore Operation:**
- Creates an exact copy of the original database from the backup files.

- **Use Cases:**
- **Disaster Recovery:** Essential for preserving production data.
- **Cloning:** Creating identical environments for Dev/Test teams.

---

## 4. Import and Export

These operations focus on moving data between the database and external files.

- **Import Operation:**
- Reads data from a file.
- Performs a series of **INSERT statements** against the target table.

- **Export Operation:**
- Retrieves data from a designated table.
- Stores it in a chosen file format.

### Supported File Formats

| Format                                   | Description                                                                                                                                   |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **DEL (Delimited ASCII)**                | Uses special characters to separate column values (e.g., **CSV**). Common for data exchange between different systems.                        |
| **ASC (Non-delimited ASCII)**            | Used for flat text files where columns are aligned by fixed width (no delimiters).                                                            |
| **PC/IXF (Integration Exchange Format)** | A structured format that includes a description of the table + the data. Preferred for moving data _within_ the same database manager family. |
| **JSON**                                 | Increasingly popular due to REST web services; supported by modern tools for structured/semi-structured data.                                 |

---

## 5. The Load Utility (vs. Import)

While **Import** uses SQL `INSERT` commands, **Load** is a high-performance alternative for massive datasets.

- **Mechanism:** Writes formatted pages **directly** into the database (bypassing the SQL engine).
- **Pros:**
- Significantly faster than Import.
- Ideal for **large volumes** of data.

- **Cons:**
- **Bypasses Checks:** Does _not_ perform referential integrity or table constraint checking.
- **Logging:** May bypass database logging (which increases speed but affects recoverability during the load).

---

## 6. DB2 Examples

Different interfaces exist for these operations:

- **Command Line (CLI):** Allows typing file names, formats, and table names directly.
- _Note:_ The Export utility can use a **SQL Query** to export only a specific subset of data.

- **DB2 Cloud Web Console:** A visual interface.
- _Steps:_ Select Table View Data Export Button Export to CSV.

---

# Database Objects and Hierarchy

## 1. Overview of Hierarchy

Relational Database Management Systems (RDBMS) organize various objects (tables, constraints, indexes) in a hierarchical structure. This organization enables administrators to effectively manage security, maintenance, and accessibility.

**General Hierarchy Structure:**

- **Instance:** The highest level; a logical boundary.
- **Database:** Contained within an instance.
- **Schema:** A logical grouping within a database.
- **Objects:** The actual data structures (tables, views, etc.) within a schema.

---

## 2. Database Instance

An instance represents a logical boundary for a database or set of databases. It organizes objects and sets configuration parameters.

- **Function:**
- Acts as a distinct environment.
- Has its own set of system catalog tables (tracking objects).
- Has its own configuration files.

- **Isolation:** Objects within one instance are isolated from those in another.
- **Deployment:** Multiple instances can exist on a single physical server, creating distinct server environments.
- **Cloud Context:** In cloud databases, "instance" often refers to a specific running copy of a service.

---

## 3. Relational Database

A relational database is a collection of objects designed for the storage, management, and retrieval of data.

- **Composition:** Includes tables, views, indexes, functions, triggers, and packages.
- **Object Types:**
- **System Objects:** Built-in / defined by the system.
- **User-Defined Objects:** Created by users to store business data.

- **Relationships:** Engineers establish relationships between tables to reduce redundancy and improve data integrity.
- **Distributed Database:** A type where tables and other objects are shared across different interconnected computer systems.

---

## 4. Schemas

A **Schema** is a specialized database object used to logically group other database objects.

### Key Functions

1. **Logical Grouping:** Can contain tables, views, nicknames, triggers, functions, and packages.
2. **Naming Context (Namespace):**

- Prevents ambiguous references.
- Allows objects with the same name to exist in different schemas (e.g., `Internal.Sales` vs. `External.Sales`).

3. **Assignment:**

- **Explicit:** You can assign an object to a specific schema by including the schema name during creation.
- **Implicit:** If no name is specified, the object is assigned to the **default schema** (usually the current user's schema).

### Types of Schemas

- **User Schema:** Stores user-defined objects like tables and views.
- **System Schema:** Stores configuration info and metadata (e.g., lists of users, access permissions, index details).

---

## 5. Partitioning

Partitioning involves distributing and managing data across multiple segments within the system.

- **Table Partitioning:** Splitting large tables into multiple logical partitions, where each contains a subset of data.
- **Use Case:** Critical for large volumes of data, such as Data Warehousing and Business Intelligence, to enhance query performance.

---

## 6. Specific Database Objects

Database design involves defining these objects and their relationships.

| Object          | Description                                                                                       |
| --------------- | ------------------------------------------------------------------------------------------------- |
| **Tables**      | Logical structures consisting of rows and columns that store the actual data.                     |
| **Constraints** | Rules enforced on data to ensure validity (e.g., ensuring an Employee ID is unique).              |
| **Indexes**     | A set of pointers used to improve query performance and ensure data uniqueness.                   |
| **Views**       | A virtual representation of data from one or more tables. It does **not** store data permanently. |
| **Aliases**     | An alternative, often shorter, name for an object (like a table) to simplify referencing.         |

**Management:** These objects are created and managed using **DDL (Data Definition Language)** statements like `CREATE` or `ALTER`, via GUIs, scripts, or APIs.

# --
