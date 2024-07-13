Create database COMPANY1;
USE COMPANY1;
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

-- Q1 1.	List all Employees whose salary is greater than 1,000 but not 2,000. Show the Employee Name, Department and Salary (4 marks)
select emp.ENAME as Name, dept.DNAME as Department, emp.SAL as Salary
from emp, dept
where emp.DEPTNO = dept.DEPTNO
and emp.SAL >1000 and emp.SAL <2000;

-- Q2  2.	Count the number of people in department 30 who receive a salary and a commission. (4 marks)

select count(emp.EMPNO) as Number_of_people_in_Dep_30_HAS_SAL_and_COM
from emp
where emp.DEPTNO = 30
and emp.SAL is NOT NULL
and emp.COMM is NOT NULL;
    
-- Q3 3.	Find the name and salary of the employees that have a salary greater or equal to 1,000 and live in Dallas. (4 marks)
select emp.ENAME as Name, emp.SAL as Salary
from emp, dept
where emp.DEPTNO = dept.DEPTNO
and emp.SAL >=1000 
and dept.LOC ='Dallas';

-- Q4 4.	Find all departments that do not have any current employees. (4 marks)
select dept.DNAME as department
from emp, dept
where emp.DEPTNO is NULL;

-- Q5 5.	List the department number, the average salary, and the number/count of employees of each department. (4 marks)
select dept.DNAME, emp.DEPTNO, count(emp.DEPTNO) as No_of_Employee, avg(emp.SAL) as average_salary, ROUND(avg(emp.SAL), 2) as ROUND_avg_Sal
  from emp, dept
  where emp.DEPTNO = dept.DEPTNO
  group by emp.DEPTNO;
