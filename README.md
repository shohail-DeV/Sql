# Sql
....
-- Instructor Table
create database collegeDB;

USE collegeDB;
CREATE TABLE Instructor (
    ID INT(5),
    Name VARCHAR(30),
    Dept_name VARCHAR(20),
    Salary INT
);

-- Inserting data into Instructor table
INSERT INTO Instructor (ID, Name, Dept_name, Salary) VALUES
    (10101, 'Srinivasan', 'Comp. Sci.', 65000),
    (12121, 'Wu', 'Finance', 90000),
    (15151, 'Mozart', 'Music', 40000),
    (22222, 'Einstein', 'Physics', 95000),
    (32343, 'El Said', 'History', 60000),
    (33456, 'Gold', 'Physics', 87000),
    (45565, 'Katz', 'Comp. Sci.', 75000),
    (58583, 'Califieri', 'History', 62000),
    (76543, 'Singh', 'Finance', 80000),
    (76766, 'Crick', 'Biology', 72000),
    (83821, 'Brandt', 'Comp. Sci.', 92000),
    (98345, 'Kim', 'Elec. Eng.', 80000);

-- 1. Create the Course table with corrected data type for Credits

CREATE TABLE Course (
  Course_id VARCHAR(10),
  Title VARCHAR(30),
  Dept_name VARCHAR(20),
  Credits INT  
);

-- Insert course data

INSERT INTO Course (Course_id, Title, Dept_name, Credits)
VALUES
  ('BIO-101', 'Intro. to Biology', 'Biology', 4.00),
  ('BIO-301', 'Genetics', 'Biology', 4.00),
  ('BIO-399', 'Computational Biology', 'Biology', 3.00),
  ('CS-101', 'Intro. to Computer Science', 'Comp. Sci.', 4.00),
  ('CS-190', 'Game Design', 'Comp. Sci.', 4.00),
  ('CS-315', 'Robotics', 'Comp. Sci.', 3.00),
  ('CS-319', 'Image Processing', 'Comp. Sci.', 3.00),
  ('CS-347', 'Database System Concepts', 'Comp. Sci.', 3.00),
  ('EE-181', 'Intro. to Digital Systems', 'Elec. Eng.', 3.00),
  ('FIN-201', 'Investment Banking', 'Finance', 3.00),
  ('HIS-351', 'World History', 'History', 3.00),
  ('MU-199', 'Music Video Production', 'Music', 3.00),
  ('PHY-101', 'Physical Principles', 'Physics', 4.00);



-- Prereq Table
CREATE TABLE Prereq (
    Course_id VARCHAR(10),
    Prereq_id VARCHAR(10)
);

-- Inserting data into Prereq table
INSERT INTO Prereq (Course_id, Prereq_id) VALUES
    ('BIO-301', 'BIO-101'),
    ('BIO-399', 'BIO-101'),
    ('CS-190', 'CS-101'),
    ('CS-315', 'CS-101'),
    ('CS-319', 'CS-101'),
    ('CS-347', 'CS-101'),
    ('EE-181', 'PHY-101');

-- Department Table
CREATE TABLE Department (
    Dept_name VARCHAR(20),
    Building VARCHAR(20),
    Budget INT
);

-- Inserting data into Department table
INSERT INTO Department (Dept_name, Building, Budget) VALUES
    ('Biology', 'Watson', 90000),
    ('Comp. Sci.', 'Taylor', 100000),
    ('Elec. Eng.', 'Taylor', 85000),
    ('Finance', 'Painter', 120000),
    ('History', 'Painter', 50000),
    ('Music', 'Packard', 80000),
    ('Physics', 'Watson', 70000);

-- Teaches Table
CREATE TABLE Teaches (
    ID INT,
    Course_id VARCHAR(10),
    Sec_id INT,
    Semester VARCHAR(10),
    Year INT
);

-- Inserting data into Teaches table
INSERT INTO Teaches (ID, Course_id, Sec_id, Semester, Year) VALUES
    (10101, 'CS-101', 1, 'Fall', 2009),
    (10101, 'CS-315', 1, 'Spring', 2010),
    (10101, 'CS-347', 1, 'Fall', 2009),
    (12121, 'FIN-201', 1, 'Spring', 2010),
    (15151, 'MU-199', 1, 'Spring', 2010),
    (22222, 'PHY-101', 1, 'Fall', 2009),
    (32343, 'HIS-351', 1, 'Spring', 2010),
    (45565, 'CS-101', 1, 'Spring', 2010),
    (45565, 'CS-319', 1, 'Spring', 2010),
    (76766, 'BIO-101', 1, 'Summer', 2009),
    (76766, 'BIO-301', 1, 'Summer', 2010),
    (83821, 'CS-190', 1, 'Spring', 2009),
    (83821, 'CS-190', 2, 'Spring', 2009),
    (83821, 'CS-319', 2, 'Spring', 2010),
    (98345, 'EE-181', 1, 'Spring', 2009);
    
    
    
    
    
    
-- Display the structure of all the tables

SELECT * FROM Instructor;
SELECT * FROM Course;
SELECT * FROM Prereq;
SELECT * FROM Department;
SELECT * FROM Teaches;

-- Display the name and department of each instructor
SELECT Name, Dept_name FROM Instructor;

-- Display the name and salary of Comp. Sci. Instructors
SELECT Name, Salary FROM Instructor WHERE Dept_name = 'Comp. Sci.';

-- Display the records of instructor who belongs to Physics department and getting salary less than 90000
SELECT * FROM Instructor WHERE Dept_name = 'Physics' AND Salary < 90000;

-- Display the name of the instructors who do not belong to Comp. Sci. Department
SELECT Name FROM Instructor WHERE Dept_name != 'Comp. Sci.';

-- Display the names of the different department distinctly available in Instructor table
SELECT DISTINCT Dept_name FROM Instructor;

-- Display all Course_id's that are taught in Spring semester of 2009
SELECT DISTINCT Course_id FROM Teaches WHERE Semester = 'Spring' AND Year = 2009;

-- Display course titles that are taught in Comp. Sci. Department and do not have credit equals to 3
SELECT Title FROM Course WHERE Dept_name = 'Comp. Sci.' AND Credits != 3;

-- Display all columns of course table sorted in descending order of department names
SELECT * FROM Course ORDER BY Dept_name DESC;

-- Add a date_of_join column to instructor table
ALTER TABLE Instructor ADD COLUMN date_of_join DATE;
SET SQL_SAFE_UPDATES = 0;

-- Insert date values to existing rows
UPDATE Instructor SET date_of_join = '2022-01-01' WHERE ID = 10101;
UPDATE Instructor SET date_of_join = '2021-02-15' WHERE ID = 12121;
UPDATE Instructor SET date_of_join = '2020-03-10' WHERE ID = 15151;
UPDATE Instructor SET date_of_join = '2019-04-05' WHERE ID = 22222;
UPDATE Instructor SET date_of_join = '2018-05-20' WHERE ID = 32343;
UPDATE Instructor SET date_of_join = '2017-06-25' WHERE ID = 33456;
UPDATE Instructor SET date_of_join = '2016-07-30' WHERE ID = 45565;
UPDATE Instructor SET date_of_join = '2015-08-15' WHERE ID = 58583;
UPDATE Instructor SET date_of_join = '2014-09-10' WHERE ID = 76543;
UPDATE Instructor SET date_of_join = '2013-10-05' WHERE ID = 76766;
UPDATE Instructor SET date_of_join = '2012-11-20' WHERE ID = 83821;
UPDATE Instructor SET date_of_join = '2011-12-15' WHERE ID = 98345;

-- Change the name of dept_name to department in all the tables
ALTER TABLE Instructor RENAME COLUMN Dept_name TO department;
ALTER TABLE Course RENAME COLUMN Dept_name TO department;
-- ALTER TABLE Department RENAME COLUMN Dept_name TO department;

-- Change the name of "Prereq" table with new name "Prerequired"
-- ALTER TABLE Prereq RENAME TO Prerequired;

-- Change Course_id column name to Sub_code
ALTER TABLE Course RENAME COLUMN Course_id TO Sub_code;
ALTER TABLE Prerequired RENAME COLUMN Course_id TO Sub_code;

-- Change the data type of name to varchar (50)
ALTER TABLE Instructor RENAME TO Instructor_old;
CREATE TABLE Instructor (
    ID int(5),
    Name VARCHAR(50),
    department VARCHAR(20),
    Salary int(6),
    date_of_join DATE
);
INSERT INTO Instructor (ID, Name, department, Salary, date_of_join)
SELECT ID, Name, department, Salary, date_of_join FROM Instructor_old;
DROP TABLE Instructor_old;









-- SELECT Course_id, Title, Credits
-- FROM Course
-- WHERE Dept_name IN ('Physics', 'Music', 'Finance', 'Biology');

SELECT * 
FROM Instructor 
WHERE Name LIKE 'K%' AND Salary > 65000;

SELECT Name, department, 
       Salary * 1.25 AS Gross_Salary, 
       Salary * 1.25 * 0.7 AS Net_Salary
FROM Instructor;

SELECT * 
FROM Instructor 
WHERE Salary BETWEEN 60000 AND 80000;

SELECT * 
FROM Instructor 
WHERE SUBSTR(Name, 2, 1) = 'r';

SELECT Name 
FROM Instructor 
WHERE department = 'Comp. Sci.'
ORDER BY Salary DESC;

UPDATE Instructor 
SET Salary = Salary * 1.15;

UPDATE Instructor 
SET Salary = Salary * 1.03 
WHERE department = 'Comp. Sci.' AND Salary < 70000;

SELECT Name, Salary * 12 AS Annual_Salary 
FROM Instructor;

UPDATE Course 
SET Title = 'Game Theory' 
WHERE Title = 'Game Design';

DELETE FROM Instructor 
WHERE department = 'History';

DELETE FROM Course 
WHERE Sub_code LIKE 'BIO%';

SELECT AVG(Salary) AS Avg_Salary 
FROM Instructor 
WHERE department = 'Physics';

SELECT department, AVG(Salary) AS Avg_Salary 
FROM Instructor 
GROUP BY department;

SELECT ID, Name, department 
FROM Instructor 
WHERE Salary = (SELECT MAX(Salary) FROM Instructor);

SELECT COUNT(*) AS Num_Instructors 
FROM Instructor 
WHERE department = 'Comp. Sci.';

-- SELECT SUM(Credits) AS Total_Credits 
-- FROM Course 
-- WHERE department = 'Comp. Sci.';

SELECT department, COUNT(*) AS Num_Instructors, SUM(Salary) AS Total_Salary 
FROM Instructor 
WHERE department IN ('Physics', 'Comp. Sci.')
GROUP BY department;

-- SELECT department, SUM(Credits) AS Total_Credits 
-- FROM Course 
-- WHERE department IN ('Comp. Sci.', 'Biology')
-- GROUP BY department;

SELECT Building, SUM(Budget) AS Total_Budget 
FROM Department 
GROUP BY Building;

SELECT department, COUNT(*) AS Num_Instructors 
FROM Instructor 
GROUP BY department;

SELECT department, COUNT(*) AS Num_Instructors 
FROM Instructor 
GROUP BY department 
ORDER BY Num_Instructors DESC;

SELECT Semester, COUNT(*) AS Num_Courses 
FROM Teaches 
GROUP BY Semester;

SELECT department 
FROM Instructor 
GROUP BY department 
HAVING COUNT(*) < 2;

SELECT department, COUNT(*) AS Num_Instructors 
FROM Instructor 
WHERE department != 'Finance'
GROUP BY department 
HAVING COUNT(*) >= 2 
ORDER BY Num_Instructors DESC;

SELECT department 
FROM Instructor 
GROUP BY department 
HAVING SUM(Salary) > 50000;

SELECT SUM(Budget) AS Total_Budget 
FROM Department 
WHERE Building = 'Watson';

SELECT MAX(Salary) AS Highest_Salary 
FROM Instructor 
WHERE department = 'Comp. Sci.';

-- SELECT INITCAP('yourname') AS Capitalized_Name;

SELECT SUBSTR('yourname', 2, 5) AS Substring_Name;

SELECT LENGTH('Your University Name') AS Name_Length;

-- SELECT INITCAP(Name) AS Capitalized_Name 
-- FROM Instructor;

SELECT department, SUBSTR(department, 1, 3) AS Dept_Code 
FROM Instructor;

-- SELECT Name, TO_CHAR(date_of_join, 'Month') AS Joining_Month 
-- FROM Instructor;

-- SELECT Name, TO_CHAR(date_of_join, 'DD/MM/YY') AS Joining_Date 
-- FROM Instructor;

-- SELECT Name, MONTHS_BETWEEN(SYSDATE, date_of_join) AS Experience_Months 
-- FROM Instructor;

-- SELECT Name, 
       -- FLOOR(MONTHS_BETWEEN(SYSDATE, date_of_join) / 12) AS Years, 
       -- MOD(MONTHS_BETWEEN(SYSDATE, date_of_join), 12) AS Months 
-- FROM Instructor;
 
 SELECT Name, TO_CHAR(date_of_join, 'Day') AS Joining_Day 
FROM Instructor;

-- SELECT SYSDATE + 15 AS Future_Date 
-- FROM DUAL;

-- SELECT TRUNC(94204.27348, 2) AS Truncated_Value 
-- FROM DUAL;

SELECT 5 + POWER(8, 9) AS Expression_Value 
FROM DUAL;

SELECT SQRT(6464312) AS Square_Root 
FROM DUAL;

SELECT LOWER('HELLO ITER') AS "lower case" 
FROM DUAL;

CREATE TABLE CUSTOMER (
    CUST_NO CHAR(5) PRIMARY KEY CHECK (CUST_NO LIKE 'C%'),
    NAME VARCHAR(50) NOT NULL,
    PHONE_NO CHAR(10),
    CITY VARCHAR(50) NOT NULL
);

CREATE TABLE BRANCH (
    BRANCH_CODE CHAR(5) PRIMARY KEY,
    BRANCH_NAME VARCHAR(50) NOT NULL,
    BRANCH_CITY VARCHAR(50) CHECK (BRANCH_CITY IN ('DELHI', 'MUMBAI', 'KOLKATA', 'CHENNAI'))
);

CREATE TABLE ACCOUNT (
    ACCOUNT_NO CHAR(5) PRIMARY KEY CHECK (ACCOUNT_NO LIKE 'A%'),
    TYPE CHAR(2) CHECK (TYPE IN ('SB', 'FD', 'CA')),
    BALANCE DECIMAL(15, 2) CHECK (BALANCE < 10000000),
    BRANCH_CODE CHAR(5),
    FOREIGN KEY (BRANCH_CODE) REFERENCES BRANCH(BRANCH_CODE)
);

CREATE TABLE DEPOSITOR (
    CUST_NO CHAR(5),
    ACCOUNT_NO CHAR(5),
    PRIMARY KEY (CUST_NO, ACCOUNT_NO),
    FOREIGN KEY (CUST_NO) REFERENCES CUSTOMER(CUST_NO),
    FOREIGN KEY (ACCOUNT_NO) REFERENCES ACCOUNT(ACCOUNT_NO)
);

CREATE TABLE LOAN (
    LOAN_NO CHAR(5) PRIMARY KEY CHECK (LOAN_NO LIKE 'L%'),
    CUST_NO CHAR(5),
    AMOUNT DECIMAL(15, 2) CHECK (AMOUNT > 1000),
    BRANCH_CODE CHAR(5),
    FOREIGN KEY (CUST_NO) REFERENCES CUSTOMER(CUST_NO),
    FOREIGN KEY (BRANCH_CODE) REFERENCES BRANCH(BRANCH_CODE)
);

CREATE TABLE INSTALLMENT (
    INST_NO INT CHECK (INST_NO <= 10),
    LOAN_NO CHAR(5),
    INST_AMOUNT DECIMAL(15, 2) NOT NULL,
    PRIMARY KEY (INST_NO, LOAN_NO),
    FOREIGN KEY (LOAN_NO) REFERENCES LOAN(LOAN_NO)
);


INSERT INTO BRANCH (BRANCH_CODE, BRANCH_NAME, BRANCH_CITY) VALUES 
('B001', 'JANAKPURI BRANCH', 'DELHI'),
('B002', 'CHANDNICHOWK BRANCH', 'DELHI'),
('B003', 'JUHU BRANCH', 'MUMBAI'),
('B004', 'ANDHERI BRANCH', 'MUMBAI'),
('B005', 'SALTLAKE BRANCH', 'KOLKATA'),
('B006', 'SRIRAMPURAM BRANCH', 'CHENNAI');


INSERT INTO ACCOUNT (ACCOUNT_NO, TYPE, BALANCE, BRANCH_CODE) VALUES 
('A0001', 'SB', 200000, 'B003'),
('A0002', 'SB', 15000, 'B002'),
('A0003', 'CA', 850000, 'B004'),
('A0004', 'CA', 35000, 'B004'),
('A0005', 'FD', 28500, 'B005'),
('A0006', 'FD', 550000, 'B005'),
('A0007', 'SB', 48000, 'B001'),
('A0008', 'SB', 7200, 'B002'),
('A0009', 'SB', 18750, 'B003'),
('A0010', 'FD', 99000, 'B004');


INSERT INTO CUSTOMER (CUST_NO, NAME, PHONE_NO, CITY) VALUES 
('C0001', 'RAJ ANAND SINGH', '9861258466', 'DELHI'),
('C0002', 'ANKITA SINGH', '9879958651', 'BANGALORE'),
('C0003', 'SOUMYA JHA', '9885623344', 'MUMBAI'),
('C0004', 'ABHIJIT MISHRA', '9455845425', 'MUMBAI'),
('C0005', 'YASH SARAF', '9665854585', 'KOLKATA'),
('C0006', 'SWAROOP RAY', '9437855466', 'CHENNAI'),
('C0007', 'SURYA NARAYAN PRADHAN', '9937955212', 'GURGAON'),
('C0008', 'PRANAV PRAVEEN', '9336652441', 'PUNE'),
('C0009', 'STUTI MISRA', '7870266534', 'DELHI'),
('C0010', 'ASLESHA TIWARI', NULL, 'MUMBAI');

INSERT INTO LOAN (LOAN_NO, CUST_NO, AMOUNT, BRANCH_CODE) VALUES 
('L0001', 'C0005', 3000000, 'B006'),
('L0002', 'C0001', 50000, 'B005'),
('L0003', 'C0002', 8000000, 'B004'),
('L0004', 'C0010', 100000, 'B004'),
('L0005', 'C0009', 9500000, 'B005'),
('L0006', 'C0008', 25000, 'B006');

INSERT INTO DEPOSITOR (CUST_NO, ACCOUNT_NO) VALUES 
('C0003', 'A0001'),
('C0004', 'A0001'),
('C0004', 'A0002'),
('C0006', 'A0003'),
('C0006', 'A0004'),
('C0001', 'A0005'),
('C0002', 'A0005'),
('C0010', 'A0006'),
('C0009', 'A0007'),
('C0008', 'A0008'),
('C0007', 'A0009'),
('C0006', 'A0010');

INSERT INTO INSTALLMENT (INST_NO, LOAN_NO, INST_AMOUNT) VALUES 
(1, 'L0005', 500000),
(1, 'L0002', 10000),
(1, 'L0003', 50000),
(1, 'L0004', 20000),
(2, 'L0005', 500000),
(1, 'L0006', 3000),
(2, 'L0002', 10000),
(3, 'L0002', 10000),
(2, 'L0003', 50000),
(2, 'L0004', 20000);


SELECT NAME, PHONE_NO, CUST_NO 
FROM CUSTOMER 
WHERE CUST_NO = (SELECT CUST_NO FROM DEPOSITOR WHERE ACCOUNT_NO = 'A0004');


SELECT NAME 
FROM CUSTOMER 
WHERE CUST_NO NOT IN (SELECT CUST_NO FROM LOAN);


SELECT BRANCH_CITY 
FROM BRANCH 
WHERE BRANCH_CODE = (SELECT BRANCH_CODE 
                     FROM LOAN 
                     WHERE CUST_NO = (SELECT CUST_NO 
                                      FROM CUSTOMER 
                                      WHERE NAME = 'ASLESHA TIWARI'));


SELECT INST_NO, LOAN_NO, INST_AMOUNT 
FROM INSTALLMENT 
WHERE LOAN_NO IN (SELECT LOAN_NO 
                  FROM LOAN 
                  WHERE CUST_NO = (SELECT CUST_NO 
                                   FROM CUSTOMER 
                                   WHERE NAME = 'ANKITA SINGH'));

SELECT BRANCH_NAME, BRANCH_CITY 
FROM BRANCH 
WHERE BRANCH_CODE IN (SELECT BRANCH_CODE 
                      FROM ACCOUNT 
                      WHERE ACCOUNT_NO IN (SELECT ACCOUNT_NO 
                                           FROM DEPOSITOR 
                                           WHERE CUST_NO = (SELECT CUST_NO 
                                                            FROM CUSTOMER 
                                                            WHERE NAME = 'ABHIJIT MISHRA')));


SELECT ACCOUNT_NO 
FROM ACCOUNT 
WHERE BALANCE > SOME (SELECT BALANCE FROM ACCOUNT WHERE TYPE = 'FD');

SELECT ACCOUNT_NO 
FROM ACCOUNT 
WHERE BALANCE > ALL (SELECT BALANCE FROM ACCOUNT WHERE TYPE = 'FD');

SELECT * 
FROM BRANCH 
WHERE EXISTS (SELECT 1 FROM LOAN WHERE BRANCH.BRANCH_CODE = LOAN.BRANCH_CODE);

SELECT * 
FROM LOAN 
WHERE NOT EXISTS (SELECT 1 FROM INSTALLMENT WHERE LOAN.LOAN_NO = INSTALLMENT.LOAN_NO);

UPDATE ACCOUNT 
SET BALANCE = CASE 
                 WHEN BALANCE > 80000 THEN BALANCE * 1.06 
                 ELSE BALANCE * 1.05 
              END;
              
SELECT LOAN.LOAN_NO 
FROM LOAN 
JOIN BRANCH ON LOAN.BRANCH_CODE = BRANCH.BRANCH_CODE 
WHERE BRANCH.BRANCH_CITY = 'MUMBAI';

SELECT DISTINCT ACCOUNT.TYPE 
FROM ACCOUNT 
JOIN BRANCH ON ACCOUNT.BRANCH_CODE = BRANCH.BRANCH_CODE 
WHERE BRANCH.BRANCH_CITY = 'DELHI';

SELECT CUSTOMER.NAME, CUSTOMER.PHONE_NO 
FROM CUSTOMER 
JOIN DEPOSITOR ON CUSTOMER.CUST_NO = DEPOSITOR.CUST_NO 
JOIN ACCOUNT ON DEPOSITOR.ACCOUNT_NO = ACCOUNT.ACCOUNT_NO 
WHERE ACCOUNT.BALANCE > 100000;

SELECT INSTALLMENT.INST_NO, INSTALLMENT.INST_AMOUNT 
FROM INSTALLMENT 
JOIN LOAN ON INSTALLMENT.LOAN_NO = LOAN.LOAN_NO 
JOIN CUSTOMER ON LOAN.CUST_NO = CUSTOMER.CUST_NO 
WHERE CUSTOMER.NAME = 'RAJ ANAND SINGH';

SELECT DISTINCT CUSTOMER.NAME 
FROM CUSTOMER 
WHERE CUSTOMER.CUST_NO NOT IN (
    SELECT DEPOSITOR.CUST_NO 
    FROM DEPOSITOR 
    JOIN ACCOUNT ON DEPOSITOR.ACCOUNT_NO = ACCOUNT.ACCOUNT_NO 
    WHERE ACCOUNT.TYPE = 'SB'
);

SELECT DISTINCT CUSTOMER.NAME 
FROM CUSTOMER 
JOIN LOAN ON CUSTOMER.CUST_NO = LOAN.CUST_NO 
JOIN INSTALLMENT ON LOAN.LOAN_NO = INSTALLMENT.LOAN_NO 
WHERE INSTALLMENT.INST_AMOUNT = 50000;

SELECT DISTINCT CUSTOMER.PHONE_NO 
FROM CUSTOMER 
JOIN DEPOSITOR ON CUSTOMER.CUST_NO = DEPOSITOR.CUST_NO 
JOIN ACCOUNT ON DEPOSITOR.ACCOUNT_NO = ACCOUNT.ACCOUNT_NO 
JOIN BRANCH ON ACCOUNT.BRANCH_CODE = BRANCH.BRANCH_CODE 
WHERE BRANCH.BRANCH_NAME = 'SALTLAKE';


SELECT DISTINCT BRANCH.BRANCH_NAME, BRANCH.BRANCH_CITY 
FROM BRANCH 
JOIN ACCOUNT ON BRANCH.BRANCH_CODE = ACCOUNT.BRANCH_CODE 
JOIN DEPOSITOR ON ACCOUNT.ACCOUNT_NO = DEPOSITOR.ACCOUNT_NO 
JOIN CUSTOMER ON DEPOSITOR.CUST_NO = CUSTOMER.CUST_NO 
WHERE CUSTOMER.NAME = 'ABHIJIT MISHRA';

SELECT ACCOUNT.TYPE, ACCOUNT.BALANCE 
FROM ACCOUNT 
JOIN DEPOSITOR ON ACCOUNT.ACCOUNT_NO = DEPOSITOR.ACCOUNT_NO 
JOIN CUSTOMER ON DEPOSITOR.CUST_NO = CUSTOMER.CUST_NO 
WHERE CUSTOMER.NAME = 'SWAROOP RAY';

WITH BranchBalances AS (
    SELECT BRANCH_CODE, SUM(BALANCE) AS TotalBalance 
    FROM ACCOUNT 
    GROUP BY BRANCH_CODE
),
AvgTotalBalance AS (
    SELECT AVG(TotalBalance) AS AvgBalance 
    FROM BranchBalances
)
SELECT BRANCH_CODE 
FROM BranchBalances 
WHERE TotalBalance > (SELECT AvgBalance FROM AvgTotalBalance);
