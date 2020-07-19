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



####  Number of Retiring Employees by Title:


          


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


  For my Analysis,The Employees table has all of the information I need and uses the emp_no,first_name,last_name. The Salaries table has the additional information I need salary and title table has from date. The only problem is that the Employees table holds data for all employees, even the ones who are not retiring. If i use this table, I will have a far bigger list to present than expected that'why.I joined  3 tables to use  inner join for employess with title and salary. I considered for retiring  employee who were born  between Jan. 1, 1952 and Dec. 31, 1955. and also on hire date(BETWEEN '1985-01-01' AND '1988-12-31).I got table with many duplicates .This is because  some employees have switched titles over the years.then I decided  Partition data to show only most recent title per employee.
    
    
    
    
#### Partition the data to show only most recent title per employee:




            SELECT emp_no,
            first_name,
            last_name,
            title,
            salary,
            from_date
            INTO emp_title_list
            FROM
            (SELECT emp_no,
            first_name,
            last_name,
            title,
            salary,
            from_date, ROW_NUMBER() OVER
            (PARTITION BY (emp_no)
            ORDER BY from_date DESC) rn
            FROM emp_title 
            ) tmp WHERE rn = 1
            ORDER BY emp_no;
            SELECT *FROM emp_title_list;
            
            
            
  For Partition data, I need to required partition formule. I applyed on previous created table. then i got clean data.


#### count for each employee with title:



                SELECT COUNT(emp_no) 
                INTO title_count
                FROM emp_title_list
                SELECT *FROM title_count;
                
                
 By using count method. I got 33118  employee with title.then I need each departments employees list.
                
                
 #### count for retirement employee with title
 
 
 
                SELECT title,
                COUNT (emp_no)
                INTO retirement_emp_title
                FROM emp_title_list
                GROUP BY title;
                SELECT *FROM retirement_emp_title;
                
                
                
  Finally, I got retirement employees with recent titleby using count() and group by.Based on my Analysis ,Company have 7 different departments employees ready to retriment.
  list for  each departments are "Engineer	- 2711", "Senior Engineer -	13651", "Manager- 2 ","Assistant Engineer"	- 251", "Staff-	2022 ", "Senior Staff-	12872","Technique Leader	-1609 ",Company have a lot of senior employees  in  senior enginneer & senior staff.



###  Technical Analysis Deliverable 2:



####  Mentorship Eligibility:


            SELECT e.emp_no,
                e.first_name,
                e.last_name,
                t.title,
                t.from_date,
                t.to_date
            INTO mentorship
            FROM employees as e
            INNER JOIN titles as t
            ON (e.emp_no = t.emp_no)
            WHERE (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
            AND (t.to_date = '9999-01-01');
            SELECT *FROM mentorship;
            
            
            
 For mentorship eligibility,The Employees table has all of the information I need and uses the emp_no,first_name,last_name. The title table has the additional information I need title,from_date,to_date.I cann't use only Employees table bacause  The only problem is that the Employees table holds data for all employees, even the ones who are not qualify for mentorship. If i use this table, I will have a far bigger list to present than expected that'why.I joined  2 tables to use  inner join for employess with title.I considered for mentorship  employee who were born  between Jan. 1, 1965 and Dec. 31, 1965. There were 1549 rows, including the header row. Data were containing  of all employees who were born  1965.


####   Total counts for mentorship:



                SELECT COUNT(title) 
                INTO mentorship_count
                FROM mentorship;
                SELECT *FROM mentorship_count
                
                
                
 By using count(), I got  1549 number of employees for mentorship.



   

