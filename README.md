# Databases-Notes
This README File is used for creating useful notes that may be utilised for Database Test 1. 
- Main Focus should be placed on the CRUD of database:
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
     CREATE DATABASE 223146145_Msimanga_Home_Affairs;
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
