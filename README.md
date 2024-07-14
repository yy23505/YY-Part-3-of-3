Project description: This README file accompanies the SQL scripts for the assessment on the EMP and DEPT tables from the fictional organisation "COMPANY1". The scripts are written in MySQL and can be executed in the MySQL Workbench.

## Installation
Visit the MySQL Community Installer Download page https://dev.mysql.com/downloads/installer/.
Click the 'Download' button for the 'Windows (x86, 32-bit), MSI Installer'. If there are two options, choose the file that is larger in size.
Selected Version: 8.0.38
Selected Operating System: Microsoft Windows
License information: Windows (x86, 32-bit), MSI Installer	8.0.38	303.6M	(mysql-installer-community-8.0.38.0.msi)	MD5: 3d7df7be5bc0c18a6b770dd642efcb3e 
When asked to sign up or sign in, clicked the 'No thanks, just start my download' link.
During installation, selected ‘Developer Default’.
Default suggestions kept whilst working through the installer.
Choose a password for database which was needed to be connected to the server.
Once the MySQL installation was completed, MySQL Workbench was launched for the Query Navigator.

## Creating Database
Create database COMPANY1;
USE COMPANY1;
## Creating Tables 
create table EMP(EMPNO INT,
    ENAME CHAR (20),
    JOB CHAR (50),
    MGR INT,
    HIREDATE DATE,
    SAL DOUBLE,
    COMM DOUBLE,
    DEPTNO INT); 
CREATE TABLE `company1`.`dept` (
  `DEPTNO` INT NOT NULL,
  `DNAME` VARCHAR(45) NOT NULL,
  `LOC` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`DEPTNO`));
SELECT * FROM company1.emp;   
SELECT * FROM company1.dept;

## Importing CSV files to MySQL
Step 1: Prepare Excel file
Excel file is in a format that can be easily imported into MySQL. This means: Each column in the Excel file should correspond to a column in the MySQL table. Also, The data in each column should be in a format that can be easily converted to the corresponding MySQL data type.
Excel file should be saved as a CSV file.
Step 2: Create a table in MySQL
Create the tables in MySQL that matches the structure of the Excel file (these have been created as above)
Step 3: Import the CSV file into MySQL
In the Navigator section in MySQL, right click on the table and select Table Data Import Wizard. 
Choose file path
Select file and Next
Follow prompts accordingly
Step 4: Verify the import
Once the import is complete, verify that the data has been imported correctly by running a query against the tables i.e.
SELECT * FROM company1.emp;   
SELECT * FROM company1.dept;

Result: Database and Tables have been created successfully.

-- Question 1 and Outcome: List all Employees whose salary is greater than 1,000 but not 2,000. Show the Employee Name, Department and Salary.

select emp.ENAME as Name, dept.DNAME as Department, emp.SAL as Salary
from emp, dept
where emp.DEPTNO = dept.DEPTNO
and emp.SAL >1000 and emp.SAL <2000;

This script joins the EMP and DEPT tables on the deptno column and selects the employee name, department, and salary for employees whose salary is greater than 1,000 but less than 2,000.

-- Question 2 and Outcome:.	Count the number of people in department 30 who receive a salary and a commission. 

select count(emp.EMPNO) as Number_of_people_in_Dep_30_HAS_SAL_and_COM
from emp
where emp.DEPTNO = 30
and emp.SAL is NOT NULL
and emp.COMM is NOT NULL;

This script selects the count of employees in department 30 who have a salary greater than 0 and a commission greater than 0.
    
-- Question 3 and Outcome:	Find the name and salary of the employees that have a salary greater or equal to 1,000 and live in Dallas. 

select emp.ENAME as Name, emp.SAL as Salary
from emp, dept
where emp.DEPTNO = dept.DEPTNO
and emp.SAL >=1000 
and dept.LOC ='Dallas';

This script selects the employee name and salary for employees who have a salary greater than or equal to 1,000 and live in Dallas.

-- Question 4 and Outcome:	Find all departments that do not have any current employees. 

select dept.DNAME as department
from emp, dept
where emp.DEPTNO is NULL;

This script selects the department name for departments that do not have any current employees by using a subquery to exclude departments that have employees.

-- Question 5 and Outcome:	List the department number, the average salary, and the number/count of employees of each department. 

select dept.DNAME, emp.DEPTNO, count(emp.DEPTNO) as No_of_Employee, avg(emp.SAL) as average_salary, ROUND(avg(emp.SAL), 2) as ROUND_avg_Sal
  from emp, dept
  where emp.DEPTNO = dept.DEPTNO
  group by emp.DEPTNO;

This script joins the EMP and DEPT tables, groups the results by department number, and calculates the average salary and count of employees for each department.
