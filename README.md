# Pewlett-Hackard-Analysis
Module 7

## Overview of the analysis:

### Purpose
Pewlett Hackard, a large company with currently over 300,000 employees has a large population of baby boomers who are soon to enter retirement (referred to by the company. The company is looking into which employees are eligible to retire and need specifications about which positions (and how many) will subsequently need filling. Bobby - an HR analyst for the company - has requested this information from datasets contained within CSV files and as of more recently - SQL.

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

The `retirement_titles` table includes contains duplicate employee numbers and shows every job title a single employee has had, a similar table without these duplicate rows was needed - hence the creation of the `unique_titles` table. The table appears as follows:

![unique_titles_table](https://user-images.githubusercontent.com/107309793/182827301-128375b8-9339-4f64-82c7-5b246676fe87.png)

This table includes the `emp_no`, `first_name`, `last_name`, and `title` columns. Here is the query:

![unique_titles_query](https://user-images.githubusercontent.com/107309793/182828387-ce38c780-876a-48e5-aa8f-d6d1c8b31619.png)

This query utilizes the `DISTINCT ON` statement which returns only 1 of the duplicate rows (in this case it will return each unique `emp_no`). The row that results in the table is determined by the `ORDER BY` clause at the end (the `to_date` column was sorted in descending order to display each employees most recent title). The `unique_titles` table was created by filtering the retirement_titles table for only the employees who are still employed with (via the `WHERE` clause).

### Retirement Titles Table (with count)

To better summarize how many employees of each title are retiring, the `retiring_titles` table was created. It appears as follows:

![retiring_titles_table](https://user-images.githubusercontent.com/107309793/182830044-c482a880-7dae-4e1e-bae7-24bb66e9b759.png)

The table displays a `count` of the number of employees who are ready to retire and the associated  `title` for this count. Here is the query:

![retiring_titles_query](https://user-images.githubusercontent.com/107309793/182830295-d5482670-2a2f-4b79-bd4f-8934745160fb.png)

The query utilizes a `COUNT` statement to perform a count on the number of rows that exist in the table within the `title` column within the `unique_titles` table. Technically any column can be utilized in this statement since we need every row counted. The individual count for each title was created in `retiring_titles` using the `GROUP BY` clause and grouping all of the unique titles together. Lastly the table was sorted by descending count to reorganize the table to the titles with the largest number of retiring employees to the smallest.

### Mentorship Eligibility Table

To finally obtain a list of employees who are eligible to participate in a mentorship program to ready them for retiring within the next 10 years, the `mentorship_eligibility` table was created. It appears as follows:

![mentorship_eligibility_table](https://user-images.githubusercontent.com/107309793/182832260-52592b86-cfc7-486c-befd-5223ab82d31e.png)

This table includes `emp_no`, `first_name`, `last_name`, `birth_date`, `from_date`, and `to_date` columns. Here is the corresponding query:

![mentorship_eligibility_query](https://user-images.githubusercontent.com/107309793/182832494-6e891b6d-8b1d-4f23-a43c-dc9246aecb74.png)

To obtain unique employee numbers in each row the `DISTINCT ON` statement is utilized again. The `employees` table is merged with the `dept_emp` and then the `titles` table to obtain all the columns of interest. The `mentorship_eligibility` table is then filtered by the `to_date` column (finding only employees who are still employed) and for employees born between 1965-01-01 and 1965-12-31. These employees will likely enter retirement in 10 years.

## Summary:

### Number of roles needed to fill following the "silver tsunami"
The total number of roles that need to be filled is 72,458. This can be determined by creating a query that counts the total number of rows in the `unique_titles` table. This is a substantial chunk of the total population of the company (300,0224 - the total number of rows in the `employees` table).

### Total number of next generation retirement-ready employees to mentor
The total number of employees that are eligible for the mentorship program is 1,549. This can be obtained by creating a query which counts the total number of rows in the `mentorship_eligibility` table. This is far smaller of a chunk of employees compared to those who will be retiring currently (born in 1955 vs born in 1965). It might not be worth the companies time, money, and resources to start this mentorship program since it's such a small chunk of the overall employee population, but it depends on just how extensive this mentorship program is. The program may not be fleshed out at this point.
