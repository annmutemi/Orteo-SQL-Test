# Orteo-SQL-Test
Repository for my Orteo SQL Interview Quiz
Orteo SQL Test 
Questions with Responses: Tables with data for the respective questions are available:  

1.	Information about pets is kept in two separate tables:
TABLE dogs
id INTEGER NOT NULL PRIMARY KEY,
name VARCHAR(50) NOT NULL

TABLE cats
id INTEGER NOT NULL PRIMARY KEY,
name VARCHAR(50) NOT NULL

Write a query that selects all distinct pet names.

Answer: 

SELECT DISTINCT name FROM dogs UNION SELECT DISTINCT name FROM cats;
 And also works too
SELECT name FROM dogs UNION SELECT name FROM cats 

Notes:  

Each SELECT statement within UNION must have the same number of columns
The columns must also have similar data types
The columns in each SELECT statement must also be in the same order

The UNION operator selects only distinct values by default without allowing duplicate values.  

Output: 
+ Options
name

denis	
mweke	
mutinda	
mwendwas	
muluwas	


2.	Given the following data definition, write a query that returns the number of students whose first name is Grace. String comparisons should be case sensitive.
TABLE students
id INTEGER PRIMARY KEY,
firstName VARCHAR(30) NOT NULL,
lastName VARCHAR(30) NOT NULL

Answer
SELECT COUNT (*) FROM students WHERE firstName LIKE '%Grace%' COLLATE SQL_Latin1_General_CP1_CS_AS; 
Options
COUNT(*)	
2	

If the database was created as Case Insesintive  however by default databases are case insensitive

3.	An employee is a manager if any other employee has their managerId set to the first employees id. An employee who is a manager may or may not also have a manager
TABLE employees
id INTEGER NOT NULL PRIMARY KEY
managerId INTEGER REFERENCES employees(id)
name VARCHAR(30) NOT NULL

Write a query that selects the names of employees who are not managers. 

Answer
First I have created the table employees with the following SQL syntax:  CREATE TABLE employees(id INTEGER NOT NULL PRIMARY KEY, managerId INTEGER REFERENCES employees(id), name VARCHAR(30) NOT NULL);
Then I have populated it with data as in the following SQL syntax:  
INSERT INTO employees (id, managerId, name) VALUES (5, 2, 'Wisdom Kamau');
Then this Query selects employees who are not managers: 
SELECT name FROM employees WHERE id NOT IN (SELECT managerId FROM employees WHERE managerId IS NOT NULL);
In my case as in the SQL employees table:  
name

 
  Edit
  Copy
  Delete
Mutua
 
  Edit
  Copy
  Delete
Johnson
 
  Edit
  Copy
  Delete
Ann Mutinda Wanjiru
 
  Edit
  Copy
  Delete
Wisdom Kamau

4.	You work for a startup that makes an online presentation software. You have an event log that records every time a user inserted an image into a presentation. (One user can insert multiple images.) The event_log SQL table looks like this:

user_id	event_date_time
7494212	1535308430
7494212	1535308433
1475185	1535308444
6946725	1535308475
6946725	1535308476
6946725	1535308477

 
…and it has over one billion rows.
Note: If the event_date_time column’s format doesn’t look familiar, google “epoch timestamp”!

Write an SQL query to find out how many users inserted more than 1000 but less than 2000 images in their presentations!

Answer
First we have to count the number of images per user: Then the users who fulfill a certain condition:  We have to run a simple COUNT() function with a GROUP BY clause on the event_log table.
SELECT COUNT (*) FROM (SELECT user_id, COUNT(event_date_time) AS image_per_user FROM event_log GROUP BY user_id) AS image_per_user WHERE image_per_user < 2000 AND image_per_user > 1000;
