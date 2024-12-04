# HR-Database-Insights

![Intro image](https://github.com/user-attachments/assets/c49a0267-61ca-4b27-9780-8d4f45d4be50)


---

## Introduction

This project involves analyzing the AdventureWorks database using SQL queries. The database contains information about employees, departments, job titles, and other relevant data. The goal is to extract insights and meaningful information from the database.


**_Disclaimer_** : _All Datasets and reports do not represent any company, institution, or country, but just a dummy dataset to demonstrate capabilities of SQL_

## Problem Statement
The problem is to design and execute SQL queries that can efficiently retrieve and analyze data from the AdventureWorks database.


## Skills/concepts demonstrated:
1. SQL querying and data analysis
2. Joining tables (INNER JOIN, LEFT JOIN)
3. Aggregate functions (GROUP BY, COUNT, AVG, SUM)
4. Subqueries and filtering data
5. Data categorization and labeling


## The goals of this project were

1. Retrieve employee information, including names, job titles, and departments.
2. Analyze employee data based on hire date, department, and job title.
3. Calculate average salaries by job title and department.
4. Identify employees with missing email addresses.
5. Group employees by department, job title, and hire year.

## Queries and Results

## Query 1: List Employees with Job Title and Department


SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle, e.BirthDate, e.MaritalStatus, e.HireDate
FROM person.Person p
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID;

![List Employees with Job Title and Department](https://github.com/user-attachments/assets/fc4bee23-4217-48e3-bc51-26ac14447a40)



## Query 2: Employees by Department


SELECT p.FirstName, p.LastName, d.Name AS "Department Name"
FROM Person.Person p
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID
INNER JOIN HumanResources.EmployeeDepartmentHistory edh ON edh.BusinessEntityID = p.BusinessEntityID
INNER JOIN HumanResources.Department d ON d.DepartmentID = edh.DepartmentID
ORDER BY p.BusinessEntityID;

![Employees by Department](https://github.com/user-attachments/assets/ffc327fa-fdf0-46dd-b56e-a5d9c7de3506)


## Query 3: Employees with Hire Date and Department


SELECT p.FirstName, p.LastName, e.hiredate, D.name AS 'Department Name',
    CASE WHEN e.Hiredate > '2009-12-31' THEN 'New Staff' ELSE 'Old Staff' END AS 'Employee Hire Category',
    CASE WHEN d.Name = 'Production' THEN 'Production employee' ELSE 'non-production employee' END AS 'Employee Department Category'
FROM Person.Person p
LEFT JOIN HumanResources.EmployeeDepartmentHistory edh ON edh.BusinessEntityID = p.BusinessEntityID
LEFT JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID
LEFT JOIN HumanResources.Department d ON d.DepartmentID = edh.DepartmentID
ORDER BY p.businessentityID;

![Employees with Hire Date and Department](https://github.com/user-attachments/assets/8de5b590-3078-4449-85e4-f7357d485e3b)


## Query 4: Employees with Email Status


SELECT p.FirstName, p.LastName, e.hiredate, e.JobTitle, ea.EmailAddress,
    CASE WHEN ea.EmailAddress IS NULL OR ea.EmailAddress = '' THEN 'No Email' ELSE ea.EmailAddress END AS 'EmailStatus'
FROM person.Person p
LEFT JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID
LEFT JOIN person.EmailAddress ea ON ea.BusinessEntityID = p.BusinessEntityID;

![Employees with Email Status](https://github.com/user-attachments/assets/03f4837e-c94b-457e-994e-ced47e7f36df)


## Query 5: Group Employees by Department and Job Title


SELECT d.Name AS department, COUNT(e.businessentityID) AS EmployeeCount
FROM HumanResources.Employee e
INNER JOIN HumanResources.EmployeeDepartmentHistory edh ON e.BusinessEntityID = edh.BusinessEntityID
INNER JOIN HumanResources.Department d ON d.DepartmentID = edh.DepartmentID
GROUP BY d.Name
ORDER BY d.Name;

![Group Employees by Department and Job Title](https://github.com/user-attachments/assets/0fadd7ea-ea0c-44d8-a5da-4cbb6c23c67c)


## Query 6: Average Salary by Job Title


SELECT e.jobtitle, AVG(eph.rate) AS AverageSalary
FROM person.person p
INNER JOIN humanresources.employee e ON p.businessentityID = e.businessentityID
INNER JOIN humanresources.EmployeePayHistory eph ON eph.businessentityID = p.businessentityID
GROUP BY e.Jobtitle
ORDER BY e.Jobtitle;

![Average Salary by Job Title](https://github.com/user-attachments/assets/2333c4a5-e8e9-4b1f-a9f4-d68b8b74bcae)



## Query 7: Employees Hired After 2009


SELECT hiredate, DATEPART(year, hiredate) AS Hireyear, COUNT(*) AS CountofEmployee
FROM HumanResources.employee
GROUP BY hiredate
HAVING COUNT(*) > 5
ORDER BY Hiredate;


![Employees Hired After 2009](https://github.com/user-attachments/assets/0e476cc3-58eb-4571-997f-3348ae0638dc)



## Recommendations

1. Use INNER JOINs for efficient data retrieval.
2. Utilize subqueries for complex filtering.
3. Apply aggregate functions for data analysis.
4. Label and categorize data for better insights.

## Conclusion 😄
This project demonstrates the use of SQL queries to analyze and extract valuable insights from the AdventureWorks database. By applying various SQL concepts, l can efficiently retrieve and analyze data, providing meaningful information for business decisions.
