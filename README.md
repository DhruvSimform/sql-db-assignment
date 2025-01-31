README.md
markdown
Copy
Edit
# SQL Database Assignment

This project involves creating and managing an `EMPLOYEE` database with two tables: `EmployeeInfo` and `EmployeePosition`. It includes database creation, table creation, data insertion, and executing various SQL queries.

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
Create Tables
sql
Copy
Edit
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
Insert Data
sql
Copy
Edit
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
🔍 SQL Queries
Count employees in Admin department
sql
Copy
Edit
SELECT COUNT(*) AS "No of employees in Admin" FROM EmployeeInfo WHERE Department='Admin';
Retrieve first four characters of last names
sql
Copy
Edit
SELECT SUBSTRING(EmpLname,1,4) AS "EmpLname" FROM EmployeeInfo;
Find employees with a salary between 50,000 and 100,000
sql
Copy
Edit
SELECT * FROM EmployeeInfo ei 
JOIN EmployeePosition ep ON ei.EmpID = ep.EmpID 
WHERE ep.Salary BETWEEN 50000 AND 100000;
Find employees whose first name starts with "S"
sql
Copy
Edit
SELECT EmpFname FROM EmployeeInfo WHERE EmpFname LIKE 'S%';
Fetch top N records ordered by salary
sql
Copy
Edit
SELECT * FROM EmployeePosition ORDER BY Salary DESC LIMIT 5;
Exclude employees with first names "Sanjay" and "Sonia"
sql
Copy
Edit
SELECT * FROM EmployeeInfo WHERE EmpFname NOT IN ('Sanjay', 'Sonia');
Department-wise count of employees sorted by count
sql
Copy
Edit
SELECT Department, COUNT(*) AS "NoOfEmployees" 
FROM EmployeeInfo 
GROUP BY Department 
ORDER BY COUNT(*);
Create an index on last name for optimized searches
sql
Copy
Edit
CREATE INDEX idx_emp_last_name ON EmployeeInfo(EmpLname);
📄 Documentation
For a detailed explanation, refer to the attached SQL_DB_Task.odt file.

📜 License
This project is for educational purposes.
