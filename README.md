# Pewlett-Hackard-Analysis
    Introduction to DBA and SQL

## Overview of the Analysis
    Based on recent analysis to discover retiring employees in the coming years, our team was tasked to determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program.

### Purpose
    The client has a significant number of employees retiring in the coming years, a phenomena that the client has dubbed "The Silver Tsunami". Our goal is to identify all employees approaching retirement, identify operational titles and potential vacancies, and identify retirees eligible to participate in a mentorship program. This will aid the client in prioritizing the positions that would benefit most from experiential learning with a mentor. 

## Results
    * Retiring Employees by Title Results
        * 25,916 Senior Engineer Retiring
        * 24,926 Senior Staff Retiring
    * Employees Eligible for Mentorship Program Results
        * 1,549 Employees eligible to serve as mentors
            * 413 Senior Engineers
            * 303 Senior Staff
![Retirement_Count.png](https://github.com/stovepipe/Pewlett-Hackard-Analysis/blob/main/Resources/Retirement_Count.png)

## Summary
    * How many roles will need to be filled as the "silver tsunami" begins to make an impact?
        * 72,458 roles will need to be filled as the "silver tsunami" impacts the company.
    * Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
        * No, we do not believe that there are enough eligible mentors. With only 413 Senior Engineers eligible tio be mentors and 25,916 retiring Senior Engineers, there will still be a significant gap to fill.

### Recommendations
    * Update the mentorship eligibility query to include a wider range of eligible employees. This can be completed by adjusting the "WHERE" filter to reflect 1965-1970.
    
    SELECT DISTINCT ON (e.emp_no)
	    e.emp_no,
	    e.first_name,
	    e.last_name,
	    e.birth_date,
	    de.from_date,
	    de.to_date,
	    t.title
    INTO mentorship_eligibility
    FROM employees as e
    INNER JOIN dept_emp as de
    ON (e.emp_no = de.emp_no)
    INNER JOIN titles as t
    ON (e.emp_no = t.emp_no)
    WHERE de.to_date = ('9999-01-01')
    AND (e.birth_date BETWEEN '1965-01-01' AND '1970-12-31')
    ORDER BY e.emp_no, de.to_date DESC;

    * Review the manager_info table, recognizing that 4 departments are missing identifiable management. With additional management oversight, the "silver tsunami' can be managed on a more individual level.