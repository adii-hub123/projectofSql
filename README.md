# projectofSql
Created an SQL-based Employee Data Management System with tables for employee details, KYC status, and attendance. Implemented joins, filtering, and aggregation queries to generate reports such as pending KYC, department-wise count, salary summary, and attendance analysis.



EMPLOYEE DATA MANAGEMENT SYSTEM (FULL SQL PROJECT)
Create Database
CREATE DATABASE employee_management;
USE employee_management;

Create Tables
Employee Table
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    joining_date DATE,
    salary INT,
    employment_status VARCHAR(20)
);

KYC Details Table
CREATE TABLE kyc_details (
    kyc_id INT PRIMARY KEY,
    employee_id INT,
    aadhaar_status VARCHAR(20),
    pan_status VARCHAR(20),
    bank_status VARCHAR(20),
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id)
);

Attendance Table
CREATE TABLE attendance (
    attendance_id INT PRIMARY KEY,
    employee_id INT,
    date DATE,
    status VARCHAR(20),
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id)
);

Insert Sample Data

Employee Records
INSERT INTO employees VALUES
(1, 'Aditya Mishra', 'Operations', '2024-01-15', 22000, 'Active'),
(2, 'Rohit Sharma', 'IT', '2023-06-10', 30000, 'Active'),
(3, 'Anjali Singh', 'HR', '2022-11-22', 25000, 'Active'),
(4, 'Vivek Yadav', 'Finance', '2021-04-18', 27000, 'Active'),
(5, 'Priya Verma', 'IT', '2023-09-01', 29000, 'Resigned');

KYC Records
INSERT INTO kyc_details VALUES
(1, 1, 'Verified', 'Pending', 'Verified'),
(2, 2, 'Verified', 'Verified', 'Verified'),
(3, 3, 'Pending', 'Pending', 'Verified'),
(4, 4, 'Verified', 'Verified', 'Pending'),
(5, 5, 'Verified', 'Pending', 'Pending');

Attendance Records
INSERT INTO attendance VALUES
(1, 1, '2024-06-01', 'Present'),
(2, 1, '2024-06-02', 'Absent'),
(3, 2, '2024-06-01', 'Present'),
(4, 3, '2024-06-01', 'Present'),
(5, 4, '2024-06-01', 'Absent');

SQL Queries
View All Tables
SELECT * FROM employees;
SELECT * FROM kyc_details;
SELECT * FROM attendance;

Pending KYC Employees
SELECT e.name, e.department,
       k.aadhaar_status, k.pan_status, k.bank_status
FROM employees e
JOIN kyc_details k ON e.employee_id = k.employee_id
WHERE k.aadhaar_status='Pending'
   OR k.pan_status='Pending'
   OR k.bank_status='Pending';

Department-wise Employee Count
SELECT department, COUNT(*)
FROM employees
GROUP BY department;

Salary Summary by Department
SELECT department, SUM(salary)
FROM employees
GROUP BY department;

Active vs Resigned Employees
SELECT employment_status, COUNT(*)
FROM employees
GROUP BY employment_status;

Attendance Summary
SELECT employee_id,
       SUM(CASE WHEN status='Present' THEN 1 ELSE 0 END) AS present_days,
       SUM(CASE WHEN status='Absent' THEN 1 ELSE 0 END) AS absent_days
FROM attendance
GROUP BY employee_id;

END OF PROJECT

