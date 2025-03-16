# Databases-Notes
This README File is used for creating useful notes that may be utilised for Database Test 1. 
- Main Focus should be placed on the CRUD of database:
1. Create - Being Able To create Databases
2. Read - Querying Information from a database
3. Updating - Update Information on a database
4. Delete - Being able to remove data from the database, remove the database itself. Remove data from the tables within the database's tables
## Difference Between DDL & DML
1. Database Definition Language -- Defining the database, creation, Alteration & Updating a database
   1. Example 1   
      ```SQL
      l
      CREATE DATABASE Example_Database;
      CREATE TABLE Example_Table(
      Index_ID INT PRIMARY,
      Name VARCHAR(100) NOT NULL,
      Surname VARCHAR(100) NOT NULL,
      EMAIL VARCHAR(50) UNIQUE
      );
      ```
    - The above mentioned Code is responsible for Creating a database that has a table named `Example_Table`
  2. Example 2
         ```SQL
         ALTER TABLE Example_Table
         ADD COLUMN Salary DECIMAL(6, 2);
         ```
         - The above mentioned table is for changing the structure of the existing table by Adding another Column of TYPE Decimal, Holding around 6 digits rounded 2 digits off.
         iii. Example 3
          ```SQL
          ALTER TABLE Example_Table
          MODIFY Surname VARCHAR(50) NOT NULL;
          ```
          - The above mentioned synatx is for changing the placeholder for surname, from being able to store 100 Characters to now storing just 50.
          iv. Example 4
          ```SQL
          DROP TABLE Example_Table;
          DROP DATABASE Example_Database -- It is always advised to not use these lines unless really necessary.. Especially in Exam/ Test Cases...
          ```
          - The above mentioned syntax is for Deleting the table and database itself.

    1. Database Management Language -- This is the syntax used to manage the database,This Lannguage is Data focused, the data stored in the table. this include the following examples:
         i. Example 1 (Insertion) 
          ```SQL
          INSERT INTO Example_Table(Index_ID, Name, Surname, Email)
          VALUES(1, "Samukelo", 'Gift', 'SamukeloGift@domain.com'),
          (2, "Gifty", "Sam", "GiftySam@cput.ac.za");
          ```
          - The above Mentioned command is responsible for populating data within an existing table.

       ii. Example 2 (Retrieval)
        ```SQL
        SELECT * FROM Example_Table;
        SELECT Name FROM Example_Table;
        SELECT Name, Surname, Email FROM Example_Table;
        ```
       iii. Example 3 (Updating)
       ```SQL
       UPDATE Example_Table
       SET Name = 'Samson'
       WHERE Name = 'Samukelo';
       ```
       iv. Example 4 (DELETION)
       ```SQL
       DELETE FROM Example_Table WHERE Name = 'Samson';
       ```
       
