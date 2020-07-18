# Pewlett_Hackard_Analysis


## Challenge Overview

 Challenge consists of three parts: two additional analyses and a technical report . for complete these tasks, submit the following deliverables:



Technical Analysis Deliverable 1: Number of Retiring Employees by Title.  create three new tables, one showing number of [titles] retiring, one showing number of employees with each title, and one showing a list of current employees born between Jan. 1, 1952 and Dec. 31, 1955. New tables are exported as CSVs. 



Technical Analysis Deliverable 2: Mentorship Eligibility. A table containing employees who are eligible for the mentorship program .submit  table and the CSV containing the data (and the CSV containing the data).



## Resources:

*  department.csv
*  dept_emp.csv
*  dept_manager.csv
*  employees.csv
*  salaries.csv
*  titles.csv
*  pgadmin
*  postgres



## Challenge Summary:



### Technical Analysis Deliverable 1:



*  Number of Retiring Employees by Title.
          


          --Number of Retiring Employees by Title
            SELECT e.emp_no,
                e.first_name,
                e.last_name,
                t.title,
                s.salary,
                t.from_date
            INTO emp_title
            FROM employees as e
            INNER JOIN titles as t
            ON (e.emp_no = t.emp_no)
            INNER JOIN salaries as s
            ON (e.emp_no = s.emp_no)
            WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')
            AND (e.hire_date BETWEEN '1985-01-01' AND '1988-12-31')
            AND (t.to_date = '9999-01-01');
            SELECT*FROM emp_title;



   

