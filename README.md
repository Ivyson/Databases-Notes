# Databases-Notes
This README File is used for creating useful notes that may be utilised for Database Test 1. 
- Main Focus should be placed on the CRUD function of databases:
1. Create - Being Able To create Databases
2. Read - Querying Information from a database
3. Updating - Update Information on a database
4. Delete - Being able to remove data from the database, remove the database itself. Remove data from the tables within the database's tables
## Difference Between DDL & DML
### Database Definition Language
   - Defining the database, creation, Alteration & Updating a database
   1. Example 1   
      ```SQL
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
   3. Example 3
      ```SQL
      ALTER TABLE Example_Table
      MODIFY Surname VARCHAR(50) NOT NULL;
      ```
      - The above mentioned synatx is for changing the placeholder for surname, from being able to store 100 Characters to now storing just 50.
   4. Example 4
      ```SQL
      DROP TABLE Example_Table;
      DROP DATABASE Example_Database -- It is always advised to not use these lines unless really necessary.. Especially in Exam/ Test Cases...
      ```
      - The above mentioned syntax is for Deleting the table and database itself.

### Database Management Language 
- This is the syntax used to manage the database,This Lannguage is Data focused, the data stored in the table. this include the following examples:
  1. Example 1 (Insertion) 
     ```SQL
     INSERT INTO Example_Table(Index_ID, Name, Surname, Email)
     VALUES(1, "Samukelo", 'Gift', 'SamukeloGift@domain.com'),
     (2, "Gifty", "Sam", "GiftySam@cput.ac.za");
     ```
     - The above Mentioned command is responsible for populating data within an existing table.

  2. Example 2 (Retrieval)
     ```SQL
     SELECT * FROM Example_Table;
     SELECT Name FROM Example_Table;
     SELECT Name, Surname, Email FROM Example_Table;
     ```
  3. Example 3 (Updating)
     ```SQL
     UPDATE Example_Table
     SET Name = 'Samson'
     WHERE Name = 'Samukelo';
     ```
  4. Example 4 (DELETION)
     ```SQL
     DELETE FROM Example_Table WHERE Name = 'Samson';
     ```
       
## Chapter 1 - 6 Activity 
- While we have been able to create databases from the above used examples, Now, the theory from here will be extrapolating from the above learnt lessons.
  1. Creating A database flow goes as following:
     ```SQL
     --Create a database with name 223146145_Msimanga_Home_Affairs
     --First Check the names of databases Available to avoid duplication
     SHOW DATABASES;
     CREATE DATABASE 223146145_Msimanga_Home_Affairs;
     --if name already exists, delete the old database
     -- DROP DATABASE 223146145_Msimanga_Home_Affairs;
     USE 223146145_Msimanga_Home_Affairs; -- This ensures that we are using the recently created database with name 'Task1'
     -- Citizens Table
      CREATE TABLE Citizens (
       CitizenID INT AUTO_INCREMENT PRIMARY KEY,
       IDNumber VARCHAR(20) UNIQUE NOT NULL,
       FirstName VARCHAR(50) NOT NULL,
       LastName VARCHAR(50) NOT NULL,
       DateOfBirth DATE,
       Nationality VARCHAR(50)
      );
   
      -- Passports Table
      CREATE TABLE Passports (
          PassportID INT AUTO_INCREMENT PRIMARY KEY,
          CitizenID INT NOT NULL,
          PassportNumber VARCHAR(20) UNIQUE NOT NULL,
          DateOfIssue DATE,
          DateOfExpiry DATE,
          PlaceOfIssue VARCHAR(100),
          FOREIGN KEY (CitizenID) REFERENCES Citizens(CitizenID)
      );
      
      -- Visas Table
      CREATE TABLE Visas (
          VisaID INT AUTO_INCREMENT PRIMARY KEY,
          PassportID INT NOT NULL,
          VisaType VARCHAR(50),
          IssueDate DATE,
          ExpiryDate DATE,
          Purpose VARCHAR(200),
          FOREIGN KEY (PassportID) REFERENCES Passports(PassportID)
      );
      
      -- Birth Certificate Table
      CREATE TABLE BirthCertificates (
           CertificateID INT PRIMARY KEY AUTO_INCREMENT,
           CitizenID INT,
           CertificateNumber VARCHAR(20) UNIQUE NOT NULL,
           DateOfIssue DATE NOT NULL,
           PlaceOfBirth VARCHAR(255) NOT NULL,
           IssuedBy VARCHAR(255) NOT NULL,
           FOREIGN KEY (CitizenID) REFERENCES Citizens(CitizenID) );
      
      -- MarriageCertificates Table
      CREATE TABLE MarriageCertificates (
        CertificateID INT PRIMARY KEY AUTO_INCREMENT,
        CitizenID1 INT,
        CitizenID2 INT,
        CertificateNumber VARCHAR(20) UNIQUE NOT NULL,
        DateOfMarriage DATE NOT NULL,
        PlaceOfMarriage VARCHAR(255) NOT NULL,
        FOREIGN KEY (CitizenID1) REFERENCES Citizens(CitizenID),
        FOREIGN KEY (CitizenID2) REFERENCES Citizens(CitizenID) );
      
      ```
2. Display the tables,
   ```SQL
   SHOW TABLES;
   ```
3. Describe the Tables
   ```SQL
   DESC Table1
   ```
4. Show the primary and foreign keys
   ```SQL
   -- This will create a table with headings Column_name, Table_Name etc... under those columns will be the name of the table, column name of the foreign keys and the primary keys
   SELECT TABLE_NAME, COLUMN_NAME, CONSTRAINT_NAME, REFERENCED_TABLE_NAME, REFERENCED_COLUMN_NAME FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE
   WHERE TABLE_SCHEMA = 'Msimanga_223146145_home_affairs'
   AND (CONSTRAINT_NAME = 'PRIMARY' OR REFERENCED_TABLE_NAME IS NOT NULL);
   ```

5. Populating the data to the tables
   ```SQL
   -- Populating Citizens Table
   INSERT INTO Citizens (IDNumber, FirstName, LastName, DateOfBirth, Nationality) VALUES
   ('9001015009082', 'Alice', 'Smith', '1990-01-01', 'South African'),
   ('8505205010087', 'Bob', 'Johnson', '1985-05-20', 'American'),
   ('9810255011089', 'Carol', 'Williams', '1998-10-25', 'British'),
   ('7601025012085', 'David', 'Brown', '1976-01-02', 'Canadian'),
   ('0203155013081', 'Eve', 'Jones', '2002-03-15', 'Australian');
   
   -- Populating Passports Table
   INSERT INTO Passports (CitizenID, PassportNumber, DateOfIssue, DateOfExpiry, PlaceOfIssue) VALUES
   (1, 'PA123456', '2020-02-10', '2030-02-09', 'Pretoria'),
   (2, 'PB789012', '2018-07-15', '2028-07-14', 'Cape Town'),
   (3, 'PC345678', '2022-11-01', '2032-10-31', 'Durban'),
   (4, 'PD901234', '2015-05-01', '2025-04-30', 'Johannesburg'),
   (5, 'PE567890', '2023-08-20', '2033-08-19', 'Bloemfontein');
   
   -- Populating Visas Table
   INSERT INTO Visas (PassportID, VisaType, IssueDate, ExpiryDate, Purpose) VALUES
   (1, 'Tourist', '2024-01-15', '2024-04-15', 'Vacation'),
   (2, 'Student', '2023-09-01', '2025-08-31', 'Study'),
   (3, 'Business', '2024-02-20', '2024-05-20', 'Conference'),
   (4, 'Work', '2022-06-10', '2024-06-09', 'Employment'),
   (5, 'Transit', '2024-03-01', '2024-03-15', 'Layover');
   
   -- Populating MarriageCertificates Table
   INSERT INTO MarriageCertificates (CitizenID1, CitizenID2, CertificateNumber, DateOfMarriage, PlaceOfMarriage)
   VALUES (1, 2, 'MC12345678901234567890', '2010-06-20', 'Cape Town City Hall'),
          (3, 4, 'MC98765432109876543210', '2005-12-12', 'Pretoria Gardens'),
          (5, 1, 'MC11223344556677889900', '2022-08-08', 'Bloemfontein Church'),
          (2, 3, 'MC55667788990011223344', '2018-03-15', 'Johannesburg Hotel'),
          (4, 5, 'MC99887766554433221100', '2000-01-01', 'Durban Beach');

   
   -- Populating BirthCertificates Table
   INSERT INTO BirthCertificates
      (CitizenID, CertificateNumber, DateOfIssue, PlaceOfBirth, IssuedBy) VALUES (1, 'BC-19900105-001', '1990-01-05', 'Cape Town Hospital', 'Cape Town Home Affairs'),
      (2, 'BC-19850520-002', '1985-05-20', 'Johannesburg Clinic', 'Johannesburg Home Affairs'),
      (3, 'BC-19981025-003', '1998-10-25', 'Pretoria Maternity Ward', 'Pretoria Home Affairs'),
      (4, 'BC-19760102-004', '1976-01-02', 'Durban Medical Centre', 'Durban Home Affairs'),
      (5, 'BC-20020315-005', '2002-03-15', 'Bloemfontein Birth Unit', 'Bloemfontein Home Affairs');
   ```
6. Showing Tuples returned in any of my relations would be executed as follows:
   ```SQL
   SELECT * FROM Visas;
   -- This will return the results (Also called tuple).. Need to confirm though...
   ```
7. Remember that the primary key is supposed to be unique, so for the question whereby they ask to populate a duplicate, enter an already existing Primary key, the db will reject this
 ```SQL
INSERT INTO BirthCertificates VALUES(1, 'BC-100001-11', '2019-02-02', 'Pretoria Maternal Ward', 'Pretorial Home Affairs');
```
8. Explain what is meant by Referential and Entity Integrity
  - **Referential Integrity** : A rule that ensures Integrity within related tables or tables that are in relation, This is about keeping integrity within the data shared by tables. Example Includes Foreign referenced keys. This rule is for ensuring that no data is orphaned, promoting consinstenct within the **tables**
  - **Entity Integrity** : A rule that mantains integrity within a table's data. This rule is for ensuring that each data within the table is unique and not repeated through the rows. Example includes Primary Keys within the **table**.
9. Explanation of MYSQL Clauses:
   1. `WHERE`: Used to filter information in a a query made before it. Targetting specified Row/Columns..
      ```SQL
      SELECT Name FROM Table_1 WHERE Age > 18;
      ```
   2. `ORDER-BY`: This clause is used to present data in a specific way, An example include ordering the data in an Ascending order when a user queries it.
      ```SQL
      SELECT * FROM Table_1
      ORDER BY Last_Name ASC; -- This will show table ORGANISED using the last name in an ascending order.
      ```
   3. `GROUP-BY`: Divides the data into groups, more like having buckets to fit data of specific nature in. Example includes, Fitting all males in the table in just one group, and so is true with females.
      ```SQL
      SELECT Gender, COUNT(*) AS Gender_Count
      FROM Table_1
      GROUP BY GENDER;
      ```
   4. `HAVING`: Following From the `GROUP BY` Clause, `HAVING` filters an output using a specific condition. It is acting like a `WHERE` Clause but `HAVING` operates on the instead of ROWS. With this being said, `HAVING` Clause can only be used in GROUPS, OR AFTER A `GROUP BY` Clause.
      ```SQL
      SELECT GENDER, COUNT(*) AS Num_Gender
      FROM Table_1
      GROUP BY GENDER
      HAVING COUNT(*) > 2;
      ```
   5. `Aggregate Functions`: Aggregate Function are the mysql defined functions for Calculating a specific aggragation like Finding a sum of specific column, and average, counting a number of elements in that column etc...
      ```SQL
      SELECT MIN(SALARY) FROM Table_1;
      SELECT Name, COUNT(*) AS Numbering
      FROM Table_1;
      SELECT Name, COUNT(*) AS Numbering
      FROM Table_1
      GROUP BY Gender;
      --Aggregate functions are AVG(), SUM(), MIN(), MAX(), COUNT() etc...
      ```
   6. `UPDATE`: This clause is used to update an existing field in the table,
      ```SQL
      UPDATE TABLE_1
      SET Column_name = "New Value"
      WHERE Column_name = "Old Value";
      ```
   7. `DELETE`: Removes the existing field from the table,
      ```SQL
      DELETE FROM Column_Name
      WHERE Age < 18;
      ```
   8. `Union` Used to concatinate results from two `SELECT` Queries. Union cuts off duplicates, to store duplicates, `UNION ALL` should be used:
      ```SQL
      SELECT Name FROM Table_1
      UNION
      SELECT Name FROM Table_2;
      ```
      - `UNION ALL` is much more faster than `UNION` ever since `UNION` has to remove duplicates first.
   9. `INTERSECT`: Retrieves data that exists between two SELECT queries:
       ```SQL
       SELECT NAME FROM Table_1
       WHERE age > 20
       INTERSECT
       SELECT NAME FROM Table_2
       WHERE Age > 20;
       ```
      10. `SELECT & SELECT DISTINCT`: SELECT Retrieves the specified data, all of it with duplicates whereas `SELECT DISTINCT Coulmn_name` only retrieves distinct Columns in a specified Column Name
          ```SQL
          SELECT * FROM Table_1; -- Retrieves every data in the table
          SELECT DISTINCT Column_Name FROM Table_1; --This will only retrieve distinct columns, removing duplicates
          ```
