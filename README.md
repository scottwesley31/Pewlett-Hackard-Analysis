# Pewlett-Hackard-Analysis
Module 7

## Overview of the analysis:

### Purpose
Pewlett Hackard, a large company with currently over 100,000 employees has a large population of baby boomers who are soon to enter retirement (referred to by the company. The company is looking into which employees are eligible to retire and need specifications about which positions (and how many) will subsequently need filling. Bobby - an HR analyst for the company - has requested this information from datasets contained within CSV files and as of more recently - SQL.

Following these intial database queries, Bobby's manager also needs the number of retiring employees per title and to identify the employees who are eligible for a mentorship program. 

## Results:

The determination of the nubmer of retiring employees per title and the identification of eliqible and retiring employees for the mentorship program was accomplished through the use of multiple queries in SQL. These queries created tables which contain the requested information.

### Retirement Titles Table
In order to isolate all of the employees (who are still employed) in the company who are ready to retire (born between January 1, 1952 and December 31, 1955) and whta their titles are - the `retirement_titles` table was created. The table appears as follows:

![retirement_titles_table](https://user-images.githubusercontent.com/107309793/182825255-a314accb-47b3-4c36-9aa9-80a4ff559064.png)

This table includes the `emp_no`, `first_name`, `last_name`, `title`, `from_date`, and `to_date`. Here is the query executed in SQL to create the table:

![retirement_titles_query](https://user-images.githubusercontent.com/107309793/182825590-d57ebabc-63e0-4b0f-ae77-f481fcee6e9f.png)

The `retirement_titles` table results from joining columns located within the `employees` and `titles` tables that exist in the PH-EmployeeDB database already. To obtain only the employees who are old enough to retire, a `WHERE` clause was utilized which filters for only the employees born between 1952-01-01 and 1955-12-31.

### Unique Titles Table

The `retirement_titles` table includes contains duplicate employee numbers and shows every job title a single employee has had, a similar table without these duplicate rows was needed - hence the creation of the `unique_titles` table.

### Retirement Titles Table (with count)

### Mentorship Eligibility Table


## Summary:
