# Database Notes for Test 1

This README provides a concise overview of essential database concepts, focusing on CRUD operations and the distinction between DDL and DML, which are crucial for your Database Test 1.

**Core Focus: CRUD Operations**

CRUD stands for **Create, Read, Update, and Delete**. These are the fundamental operations you'll perform on a database:

-   **Create:** Building the database structure and tables.
-   **Read:** Querying and retrieving information from the database.
-   **Update:** Modifying existing information within the database.
-   **Delete:** Removing data from tables or deleting entire tables and databases.

**Understanding DDL and DML: Safety and Management**

For database safety and effective management, it's vital to differentiate between **Data Definition Language (DDL)** and **Data Manipulation Language (DML)**. These languages serve distinct purposes:

**1. Data Definition Language (DDL) - Defining the Database Structure**

DDL commands are used to **define and manage the structure** of your database. They are concerned with creating, altering, and deleting database objects like databases and tables. Think of DDL as the "architect" of your database.

   **Key Operations (DDL):**

   -   **Creation:** Building new database objects.
   -   **Alteration:** Modifying the structure of existing objects.
   -   **Deletion:** Removing database objects.

   **Examples (DDL):**

   **i. Creating a Database and Table:**
      ```sql
      CREATE DATABASE Example_Database;

      CREATE TABLE Example_Table (
          Index_ID INT PRIMARY KEY,  -- Define Index_ID as Primary Key
          Name VARCHAR(100) NOT NULL,
          Surname VARCHAR(100) NOT NULL,
          EMAIL VARCHAR(50) UNIQUE
      );
      ```
      -   **Explanation:** This code first creates a database named `Example_Database`. Then, it creates a table named `Example_Table` within this database.  The table has columns for `Index_ID` (as the primary key), `Name`, `Surname`, and `EMAIL`, with specified data types and constraints (like `NOT NULL` and `UNIQUE`).

   **ii. Adding a Column to a Table:**
      ```sql
      ALTER TABLE Example_Table
      ADD COLUMN Salary DECIMAL(6, 2);
      ```
      -   **Explanation:** This `ALTER TABLE` command modifies the `Example_Table` by adding a new column named `Salary`. The `Salary` column is defined with the `DECIMAL(6, 2)` data type, suitable for storing numbers with up to 6 digits in total, with 2 digits after the decimal point.

   **iii. Modifying a Column's Definition:**
      ```sql
      ALTER TABLE Example_Table
      MODIFY COLUMN Surname VARCHAR(50) NOT NULL;
      ```
      -   **Explanation:** This `ALTER TABLE` command modifies the `Surname` column in `Example_Table`. It changes the maximum length allowed for `Surname` from `VARCHAR(100)` to `VARCHAR(50)`.  It retains the `NOT NULL` constraint.

   **iv. Dropping (Deleting) Tables and Databases (Use with Caution!)**
      ```sql
      DROP TABLE Example_Table;
      DROP DATABASE Example_Database; -- Use with extreme caution, especially in exams/tests!
      ```
      -   **Explanation:**
          -   `DROP TABLE Example_Table;` removes the entire `Example_Table` from the database.
          -   `DROP DATABASE Example_Database;` removes the entire `Example_Database` and all objects within it.
          -   **Important Note:**  `DROP` commands are **destructive** and permanently delete data and database objects. **Avoid using `DROP DATABASE` or `DROP TABLE` in exam or test scenarios unless explicitly instructed to do so, as it can lead to data loss.**

**2. Data Manipulation Language (DML) - Managing Data Content**

DML commands are used to **manage the data** stored within the database tables. They are focused on working with the actual records (rows) in your tables. Think of DML as the "data manager" of your database.

   **Key Operations (DML):**

   -   **Insertion:** Adding new data into tables.
   -   **Retrieval:** Querying and reading data from tables.
   -   **Updating:** Modifying existing data in tables.
   -   **Deletion:** Removing data from tables (but not the tables themselves).

   **Examples (DML):**

   **i. Insertion (Populating Data):**
      ```sql
      INSERT INTO Example_Table (Index_ID, Name, Surname, EMAIL)
      VALUES
          (1, "Samukelo", 'Gift', 'SamukeloGift@domain.com'),
          (2, "Gifty", "Sam", "GiftySam@cput.ac.za");
      ```
      -   **Explanation:** This `INSERT INTO` command adds two new rows of data into the `Example_Table`.  Each `VALUES(...)` set represents a new record, providing values for the `Index_ID`, `Name`, `Surname`, and `EMAIL` columns in the specified order.

   **ii. Retrieval (Querying Data):**
      ```sql
      SELECT * FROM Example_Table;                -- Select all columns and rows
      SELECT Name FROM Example_Table;              -- Select only the 'Name' column from all rows
      SELECT Name, Surname, EMAIL FROM Example_Table; -- Select specific columns
      ```
      -   **Explanation:**
          -   `SELECT * FROM Example_Table;` retrieves all columns (`*`) from all rows in the `Example_Table`.
          -   `SELECT Name FROM Example_Table;` retrieves only the `Name` column from all rows.
          -   `SELECT Name, Surname, EMAIL FROM Example_Table;` retrieves the specified columns (`Name`, `Surname`, `EMAIL`) from all rows.

   **iii. Updating Data:**
      ```sql
      UPDATE Example_Table
      SET Name = 'Samson'
      WHERE Name = 'Samukelo';
      ```
      -   **Explanation:** This `UPDATE` command modifies existing data. It sets the `Name` column to 'Samson' for all rows in `Example_Table` where the current `Name` is 'Samukelo'. The `WHERE` clause is crucial to specify which rows should be updated.

   **iv. Deletion (Removing Data from Tables):**
      ```sql
      DELETE FROM Example_Table
      WHERE Name = 'Samson';
      ```
      -   **Explanation:** This `DELETE FROM` command removes rows from the `Example_Table`.  It deletes all rows where the `Name` column is equal to 'Samson'.  Again, the `WHERE` clause is essential to target specific rows for deletion.

By understanding the distinction between DDL and DML and mastering CRUD operations, you will be well-prepared for your Database Test 1. Good luck!
