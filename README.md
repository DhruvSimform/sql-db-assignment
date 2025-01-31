# SQL Database Assignment

This project involves creating and managing an `EMPLOYEE` database with two tables: `EmployeeInfo` and `EmployeePosition`. It includes database creation, table creation, data insertion, and executing various SQL queries.

## 📄 Documentation
For a detailed explanation, refer to the attached [SQL_DB_Task.odt](SQL_DB_Task.odt) file.

## 📌 Live Preview
🔗 [Project URL](https://dhruvsimform.github.io/sql-db-assignment/)

## 🏗 Database Structure
### Tables:
1. **EmployeeInfo**
   - EmpID (Primary Key, Auto-increment)
   - EmpFname (First Name)
   - EmpLname (Last Name)
   - Department
   - Project
   - Address
   - DOB (Date of Birth)
   - Gender

2. **EmployeePosition**
   - EmpID (Foreign Key referencing `EmployeeInfo.EmpID`)
   - EmpPosition
   - DateOfJoining
   - Salary

## 🔧 Setup Instructions
1. **Create Database**
   ```sql
   CREATE DATABASE EMPLOYEE;
   ```
2. **Create Tables**
   ```sql
   CREATE TABLE EmployeeInfo (
       EmpID SERIAL PRIMARY KEY,
       EmpFname VARCHAR(50) NOT NULL,
       EmpLname VARCHAR(50) NOT NULL,
       Department VARCHAR(20) NOT NULL,
       Project VARCHAR(10) NOT NULL,
       Address VARCHAR(100) NOT NULL,
       DOB DATE NOT NULL,
       Gender CHAR(1) NOT NULL
   );

   CREATE TABLE EmployeePosition (
       EmpID INT REFERENCES EmployeeInfo(EmpID) UNIQUE,
       EmpPosition VARCHAR(20),
       DateOfJoining DATE NOT NULL,
       Salary INT
   );
   ```
3. **Insert Data**
   ```sql
   INSERT INTO EmployeeInfo (EmpFname, EmpLname, Department, Project, Address, DOB, Gender) VALUES
   ('Sanjay', 'Mehra', 'HR', 'P1', 'Hyderabad(HYD)', '1976-12-01', 'M'),
   ('Ananya', 'Mishra', 'Admin', 'P2', 'Delhi(DEL)', '1968-05-02', 'F'),
   ('Rohan', 'Diwan', 'Account', 'P3', 'Mumbai(BOM)', '1980-01-01', 'M'),
   ('Sonia', 'Kulkarni', 'HR', 'P1', 'Hyderabad(HYD)', '1992-05-02', 'F'),
   ('Ankit', 'Kapoor', 'Admin', 'P2', 'Delhi(DEL)', '1994-07-03', 'M');

   INSERT INTO EmployeePosition (EmpID, EmpPosition, DateOfJoining, Salary) VALUES
   (1, 'Manager', '2022-05-01', 500000),
   (2, 'Executive', '2022-05-02', 75000),
   (3, 'Manager', '2022-05-01', 90000),
   (4, 'Lead', '2022-05-02', 85000),
   (5, 'Executive', '2022-05-01', 300000);
   ```

## 🔍 SQL Queries
1. **Count employees in Admin department**
   ```sql
   SELECT COUNT(*) AS "No of employees in Admin" FROM EmployeeInfo WHERE Department='Admin';
   ```
2. **Retrieve first four characters of last names**
   ```sql
   SELECT SUBSTRING(EmpLname,1,4) AS "EmpLname" FROM EmployeeInfo;
   ```
3. **Find employees with a salary between 50,000 and 100,000**
   ```sql
   SELECT * FROM EmployeeInfo ei 
   JOIN EmployeePosition ep ON ei.EmpID = ep.EmpID 
   WHERE ep.Salary BETWEEN 50000 AND 100000;
   ```
4. **Find employees whose first name starts with "S"**
   ```sql
   SELECT EmpFname FROM EmployeeInfo WHERE EmpFname LIKE 'S%';
   ```
5. **Fetch top N records ordered by salary**
   ```sql
   SELECT * FROM EmployeePosition ORDER BY Salary DESC LIMIT 5;
   ```
6. **Exclude employees with first names "Sanjay" and "Sonia"**
   ```sql
   SELECT * FROM EmployeeInfo WHERE EmpFname NOT IN ('Sanjay', 'Sonia');
   ```
7. **Department-wise count of employees sorted by count**
   ```sql
   SELECT Department, COUNT(*) AS "NoOfEmployees" 
   FROM EmployeeInfo 
   GROUP BY Department 
   ORDER BY COUNT(*);
   ```
8. **Create an index on last name for optimized searches**
   ```sql
   CREATE INDEX idx_emp_last_name ON EmployeeInfo(EmpLname);
   ```



