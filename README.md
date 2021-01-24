# Pewlett Hackard Analysis

## Overview of the Analysis
The purpose of this analysis is to determine the number of retiring employees per title and identify employees who are eligible to participate in a mentorship program to help prepare Bobby’s manager for the “silver tsunami” as many current employees reach retirement age.

## Resources
Data Source: [Retirement Titles CSV File](Queries/Data/retirement_titles.csv), [Unique Titles CSV File](Queries/Data/unique_titles.csv), [Retiring Titles CSV File](Queries/Data/retiring_titles.csv), [Mentorship Eligibility CSV File](Queries/Data/mentorship_eligibility.csv)

Software: pgAdmin 4, SQL, VS Code

## Results :loop:
- There are 90,398 employees who are at the retirement age.
- Approximately 33% of the retiring employees have titles of Senior Engineer.
- Approximately 31% of the retiring employees have titles of Senior Staff.
- There are 1,549 retiring employees who are eligible for the Mentorship Program.

## Summary
As the "silver tsunami" begins to make an impact, 90,398 roles will need to be filled. With only 1,549 retiring employees who are eligible for the Mentorship Program, there are not enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees. That's a ratio of approximately 58 new employees to one retiring employee. With the retiring employee working reduced hours, mentoring 58 new employees will not be feasible and it's setting the retiring employee up for failure.

Instead, we can run the querie below to include in the Mentorship Program retiring employees with birth dates from 1963 to 1965 (our original querie was from 1965 only). This broadens the pool of mentors for new employees to 38,401 or approximately 2 or 3 new employees per mentor. Additionally, current employees with senior titles who are not considered a 'retiring employee' may be included in the Mentorship Program to further broaden the mentor pool for a closer one-to-one relationship to a new employee. 

    SELECT DISTINCT ON (e.emp_no) e.emp_no,
        e.first_name,
        e.last_name,
        e.birth_date,
        de.from_date,
        de.to_date,
        t.title
    FROM employees as e
    LEFT JOIN dept_emp as de
    ON (e.emp_no = de.emp_no)
    LEFT JOIN titles as t
    ON (e.emp_no = t.emp_no)
    WHERE (e.birth_date BETWEEN '1963-01-01' AND '1965-12-31')
    AND (de.to_date = '9999-01-01')
    ORDER BY emp_no;
