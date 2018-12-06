SQL Conventions
1. All SQL Keywords/reserved words should be in Uppercase.
2. Column Names are separated by underscore(_).
3. Every statement must be terminated by semicolon(;)
4. — is used to comment a line in SQL.

-- DDL Data Definition Language
CREATE TABLE tasks
(
  task_name VARCHAR(255),
  complete CHAR(1)
);

-- DML Data Manipulation Language
INSERT INTO tasks VALUES ('SQL Course', 'Y');

SELECT * FROM tasks;

CREATE TABLE persons
(
  first_name VARCHAR(255),
  last_name VARCHAR(255)
);

INSERT INTO persons VALUES('LEELA', 'JAGU');

SELECT * FROM persons;
SELECT concat(first_name, ' ', last_name) AS full_name FROM persons;


Database
————————
Database is a set of related data and how it is organised.

Database Management Systems(DBMS) are specialised computer programs for databases.
DBMS has 4 characteristics
1. Data Definition - define the data being tracked.
2. Data Manipulation - add, update or remove data.
3. Data Retrieval - extract and report on data in database.
4. Administration - defining users on the system,security,monitoring,system administration.


Types of Databases:

1. Flat File Database 
   Data is kept in a file on the operating system. It is out-dated one.
2. Relational Database
   Data is kept on database tables, which have Relations to each other. Most commonly used.
3. Hierarchical Database
   Data is kept in tree like structure.
4. NOSQL Database.
   This segment is a group of specialize databases which have variety of data models - but doesn’t use SQL.
Data Models include : Key-Value Store,Document Based,Column Based.
5. Distributed/Cloud Database
   Designed to run on many servers for massive scalable and Highly Available Systems, often NOSQL.


Relational Database:
Relational Databases store data in tables which have relations to other tables.
Relational Databases use SQL for data definition and manipulation statements.
Relational Databases are most widely used database.

Table:
Table is like a spreadsheet.
Data is kept in columns and rows.
Each Column is assigned with 
1. A unique name.
2. Data type.
3. optionally constraints (e.g.: is required,length of string etc)
Each Row is a distinct Database Record.

Primary Key:
A Primary key is an optional special database column or columns used to identify a database record.
It is Highly recommended to specify a primary key for every table.

Surrogate Key:
Surrogate Key is a type of primary key which will generate a unique value.
This key have no business value and should never change.
It is typically a system generated self incrementing number.
This key is considered as a best practice in Relational Database Design.

Table Relations:
Relations are defined through foreign key constraints in conjunction with Primary keys.
Types of Relations:
1. One to One - Record in TableA matches exactly one record in TableB.
2. One to Many - Record in TableA matches many in TableB, but TableB matches only one record in TableA.
3. Many to Many - Record in TableA matches many in TableB and TableB matches many records in TableA.

Refer Entity Relationship Diagram for representing Databases on a High level.


CREATE TABLE customer
(
  id INTEGER,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  address VARCHAR(100),
  city VARCHAR(100),
  state VARCHAR(2),
  zip_code VARCHAR(10)
);

CREATE TABLE drink_order
(
  id INTEGER,
  customer_id INTEGER,
  description VARCHAR(100)
);

INSERT INTO customer VALUES (1234,'LEELA','JAGU','ADDRESS','CITY','AP','520001');
INSERT INTO drink_order VALUES(1249,1234,'JUICE');



DDL - Data Definition Language(i.e., CREATE TABLE) is used to define the relational model
Under the covers RDBMS will store data about your tables in catalog tables.
This is used to enforce data being stored conforms to the rules you have defined for the data like
You can’t store a text in a numeric filed.
You must provide a value(Not Null)

DML - Data Manipulation Language
Allows you to add(INSERT), change(UPDATE) or remove(DELETE) data.
RDBMS enforces data manipulation adheres to the rules of Data Definition.
RDBMS allows setup rules for multi-user systems.
These rules manage what happens in competing conditions(what happens when two users want to update the same data, at the same time)
Enforces Data Integrity - what happens when things go wrong?


Data Retrieval is the act of pulling data out of database.
RDBMS determines the optimal way to retrieve data out of the database.
Multi-table joins can become very complex.
  consider tables with billions and billions of rows.
  Reports can go from seconds to hours when the retrieval strategy is wrong.
RDBMS also considers what happens when updates occur while your report is running.

Administration
Users - RDBMS define user accounts.
User accounts have security roles which control what individual users can see,update,delete etc
RDBMS have tools to see performance metrics which can be used to identify costly operations.
System Administration includes
Defining users
where the database stores its data on computer system
Backups and Auditing.

MYSQL Features:
It is Relational Database Management System.
MySQL supports ANSI/SQL Standard
MYSQL is developed in C and C++ making it portable across many different platforms
MYSQL is very fast,stable and scalable.
There are MYSQL clients for all popular Languages.
C,C++,Java,PHP,Python,Ruby,etc
It has
Stored Procedures
Triggers
Cursors
Updated Views
Query Cache
Subselects
It is ACID Compliance
Atomicity - all or nothing
Consistency - transactions are valid to rules of the DB
Isolation - Results of transactions are as if they are done end to end
Durability - once a transaction is committed it remains so


USE employees;

SELECT 
    emp_no, COUNT(*) AS emp_count
FROM
    employees
WHERE
    emp_no > 1         -- conditions to select data
GROUP BY emp_no        -- How to group data
HAVING emp_count > 0   -- conditions for aggregate functions
ORDER BY emp_no        -- How to order data
LIMIT 5, 10;		   -- limit result set returned LIMIT start_record_number,end_record_number;


Column Alias:
SELECT 
    emp_no, first_name AS firstName, last_name AS lastName
FROM
    employees;

SELECT 
    emp_no, first_name AS 'First Name', last_name AS 'Last Name'
FROM
    employees;

Concat Function:
SELECT 
    emp_no,
    first_name AS 'First Name',
    last_name AS 'Last Name',
    CONCAT(first_name, ' ', last_name) AS 'Full Name'
FROM
    employees;

Arithmetic Operations:
SELECT 
    salary,
    salary * 0.01 AS weekly,
    salary * 0.01 * 4 AS monthly,
    salary * 0.01 * 52 AS yearly,
    salary + 200 * 0.01 AS multiply_first,
    (salary + 200) * 0.01 AS add_first,
    salary * 0.01 / 7 AS daily,
    salary DIV 3 AS div_op,
    salary % 3 AS mod_op
FROM
    salaries;

Datatypes:
A data type defines data type of a column i.e., text,number,date etc
MySQL supports standard ANSI SQL Datatypes.
Datatypes are broken down into following categories.
1. Numeric Data type.
2. Date and Time Datatype.
3. String Datatype.
4. Spatial Datatype.
5. JSON Datatype.

Formating Date:
SELECT 
    from_date AS original,
    DATE_FORMAT(from_date, '%M %d %Y') AS Version1,
    DATE_FORMAT(from_date, '%m %D %Y') AS Version2,
    DATE_FORMAT(from_date, '%m-%d-%Y') AS Version3
FROM
    salaries;

Left and Right:
USE employees;

SELECT LEFT(first_name,1), first_name FROM employees;

SELECT RIGHT(first_name,1), first_name FROM employees;

SELECT LEFT(first_name,2), first_name FROM employees;

SELECT RIGHT(first_name,2), first_name FROM employees;

SELECT first_name AS 'First Name', last_name AS 'Last Name',
CONCAT(LEFT(first_name,1), LEFT(last_name,1)) AS Initials FROM employees;

Equals and Not Equals:

SELECT * FROM employees WHERE first_name='Elvis';

SELECT * FROM employees WHERE first_name <> 'Elvis';

SELECT * FROM employees WHERE first_name != 'Elvis';

AND OR :
SELECT * FROM employees WHERE first_name='Elvis';

SELECT * FROM employees WHERE first_name='Elvis' AND gender = 'M';

SELECT * FROM employees WHERE first_name='Elvis' AND last_name='Cherinka';

SELECT * FROM employees WHERE first_name='Elvis' OR last_name='Cherinka';

SELECT * FROM employees WHERE first_name='Elvis' AND last_name='Cherinka'
OR first_name='Elvis' AND last_name='Verhoeff';

IN NOTIN:
SELECT * FROM employees WHERE first_name IN ('Elvis', 'Tzvetan', 'Parto', 'Georgi');

SELECT * FROM employees WHERE first_name IN ('Elvis', 'Tzvetan', 'Parto', 'Georgi')
AND last_name NOT IN ('Hiyoshi','Highland'); 

IS NULL IS NOT NULL:
SELECT * FROM sys.sys_config;

SELECT * FROM sys.sys_config WHERE value IS NULL;

SELECT * FROM sys.sys_config WHERE value IS NOT NULL;

If we are in one schema then we can access table in other schema by using schema.element_name 
Greater than Less than:
SELECT * FROM salaries WHERE salary > 60000 ORDER BY salary ASC;

SELECT * FROM salaries WHERE salary < 60000 ORDER BY salary DESC;

SELECT * FROM salaries WHERE salary < 60000 AND from_date > '2002-01-01' ORDER BY salary DESC;

SELECT COUNT(*) FROM salaries WHERE salary < 60000 ORDER BY salary DESC;

SELECT COUNT(*) FROM salaries WHERE salary < 60000 AND from_date > '2002-01-01' ORDER BY salary DESC;

Greater than or Less than will be applicable to numeric and date values but not strings.

Like NotLike:
SELECT * FROM employees WHERE first_name LIKE 'E%';

SELECT * FROM employees WHERE first_name LIKE 'E%' AND last_name NOT LIKE '_e%';

SELECT COUNT(*) FROM employees WHERE first_name LIKE 'E%';

SELECT COUNT(*) FROM employees WHERE first_name LIKE 'E%' AND last_name NOT LIKE '_e%';

Here _ indicates one character.

BETWEEN AND NOT BETWEEN
SELECT * FROM salaries;

SELECT * FROM salaries WHERE salary >= 50000 AND salary <= 60000 ORDER BY salary ASC;

SELECT * FROM salaries WHERE salary BETWEEN 50000 AND 60000 ORDER BY salary ASC;

SELECT COUNT(*) FROM salaries WHERE salary >= 50000 AND salary <= 60000;

SELECT * FROM salaries WHERE from_date BETWEEN '1991-05-17' AND '2000-01-01' ORDER BY from_date DESC;

SELECT * FROM salaries WHERE from_date NOT BETWEEN '1991-05-17' AND '2000-01-01' ORDER BY from_date ASC;

BETWEEN can be applied on numeric and date value

ORDER BY
SELECT * FROM salaries;

SELECT * FROM salaries ORDER BY salary;

SELECT * FROM salaries ORDER BY from_date,salary;

SELECT * FROM salaries ORDER BY from_date asc,salary desc;

Ascending is default ordering and we can specify ordering for multiple columns.

LIMIT:
SELECT * FROM employees LIMIT 20;

SELECT * FROM employees LIMIT 19, 20;

Here the first parameter is offset means it will fetch from 19 record and display 20 records from 19 record, this will be used in pagination.


DISTINCT:
SELECT DISTINCT first_name FROM employees;

SELECT COUNT(DISTINCT first_name) FROM employees;

SELECT DISTINCT birth_date FROM employees;

SELECT COUNT(DISTINCT birth_date) FROM employees;

Sub Query:
SELECT DISTINCT first_name FROM employees WHERE first_name LIKE 'E%';

SELECT * FROM employees WHERE first_name IN (SELECT DISTINCT first_name FROM employees WHERE first_name LIKE 'E%');

Group By:
SELECT first_name, COUNT(*) FROM employees GROUP BY first_name;

SELECT birth_date, COUNT(*) FROM employees GROUP BY birth_date;

SELECT salary, count(*) AS sal_count FROM salaries GROUP BY salary ORDER BY sal_count DESC;

Having:
SELECT salary, count(*) AS sal_count FROM salaries GROUP BY salary HAVING sal_count>100 ORDER BY sal_count DESC;

SELECT 
    salary, COUNT(*) AS sal_count
FROM
    salaries
WHERE from_date> '2000-01-01'    
GROUP BY salary
HAVING sal_count > 100
ORDER BY sal_count DESC;

Here Having is applied to aggregate columns instead where as Group by is applied to table columns.

SUM:
SELECT date_format(from_date , '%Y') AS year, sum(salary) FROM salaries GROUP BY year;

Max and Min:
SELECT date_format(from_date , '%Y') AS salary_year, MIN(salary) AS min_sal FROM salaries GROUP BY salary_year;

SELECT date_format(from_date , '%Y') AS salary_year, MAX(salary) AS max_sal FROM salaries GROUP BY salary_year;


SELECT 
    salary_year, min_sal, max_sal, max_sal - min_sal AS delta
FROM
    (SELECT 
        DATE_FORMAT(from_date, '%Y') AS salary_year,
            MIN(salary) AS min_sal,
            MAX(salary) AS max_sal
    FROM
        salaries
    GROUP BY salary_year) AS sub_select;

AVG:
SELECT date_format(from_date , '%Y') AS salary_year, AVG(salary) AS avg_sal FROM salaries GROUP BY salary_year;

Assignment:
Employees excluding managers
SELECT 
    DATE_FORMAT(from_date, '%Y') AS salary_year,
    SUM(salary) AS total_sal,
    MAX(salary) AS max_sal,
    MIN(salary) AS min_sal,
    AVG(salary) AS avg_sal
FROM
    salaries
WHERE
    emp_no NOT IN (SELECT DISTINCT
            emp_no
        FROM
            dept_manager)
GROUP BY salary_year;

Inner Join:
SELECT 
    *
FROM
    employees
        JOIN
    dept_manager ON employees.emp_no = dept_manager.emp_no;

Table Aliases:
SELECT 
    *
FROM
    employees AS emp
        JOIN
    dept_manager AS dm ON emp.emp_no = dm.emp_no
        JOIN
    departments AS dept ON dm.dept_no = dept.dept_no;

Limiting Column Names:
SELECT 
    emp.emp_no, first_name, last_name, dept_name
FROM
    employees AS emp
        JOIN
    dept_manager AS dm ON emp.emp_no = dm.emp_no
        JOIN
    departments AS dept ON dm.dept_no = dept.dept_no
ORDER BY dept_name , first_name;

Where Clause:
SELECT 
    emp.emp_no, first_name, last_name, dept_name
FROM
    employees AS emp
        JOIN
    dept_manager AS dm ON emp.emp_no = dm.emp_no
        JOIN
    departments AS dept ON dm.dept_no = dept.dept_no
    WHERE
    dm.to_date = '9999-01-01'
ORDER BY dept_name;

SELECT 
    emp.emp_no, first_name, last_name, dept_name
FROM
    employees AS emp
        JOIN
    dept_manager AS dm ON emp.emp_no = dm.emp_no
        JOIN
    departments AS dept ON dm.dept_no = dept.dept_no
    WHERE
    dm.to_date = '9999-01-01'
    AND gender = 'M'
ORDER BY dept_name;

Assignment:
SELECT 
    emp.emp_no, first_name, last_name, dept_name, title
FROM
    employees AS emp
        JOIN
    dept_emp AS de ON emp.emp_no = de.emp_no
        JOIN
    departments AS dept ON de.dept_no = dept.dept_no
        JOIN
    titles AS t ON t.emp_no = emp.emp_no
WHERE
    de.to_date = '9999-01-01'
        AND t.to_date = '9999-01-01'
ORDER BY dept_name , last_name;

Here INNER JOIN is same as JOIN
if you don't specify INNER it is treated as INNER JOIN

UNION
SELECT 
    emp.emp_no, first_name, last_name, dept_name, 'Manager' AS emp_type
FROM
    employees AS emp
        JOIN
    dept_manager AS dm ON emp.emp_no = dm.emp_no
        JOIN
    departments AS dept ON dm.dept_no = dept.dept_no
    WHERE
    dm.to_date = '9999-01-01'
UNION
SELECT 
    emp.emp_no, first_name, last_name, dept_name, 'Employee' AS emp_type
FROM
    employees AS emp
        JOIN
    dept_emp AS de ON emp.emp_no = de.emp_no
        JOIN
    departments AS dept ON de.dept_no = dept.dept_no
WHERE
    de.to_date = '9999-01-01'
ORDER BY emp_type, dept_name , last_name;

LEFT OUTER JOIN
SELECT 
    *
FROM
    employees AS emp
        LEFT JOIN
    dept_manager AS dm ON emp.emp_no = dm.emp_no
    ORDER BY emp.emp_no;
    
SELECT 
    *
FROM
    employees AS emp
        LEFT JOIN
    dept_manager AS dm ON emp.emp_no = dm.emp_no
    WHERE dm.emp_no IS NOT NULL
    ORDER BY emp.emp_no;

Employees without Active Title:
SELECT 
    *
FROM
    employees AS emp
        LEFT JOIN
    titles AS t ON emp.emp_no = t.emp_no and t.to_date = '9999-01-01'
    WHERE t.emp_no IS NULL
    ORDER BY emp.emp_no;

INSERT
INSERT INTO departments VALUES('d999', 'Awesome Gurus');

INSERT INTO departments(dept_no, dept_name) VALUES('d998', 'Awesome Gurus2');

INSERT INTO departments(dept_no, dept_name) VALUES('d997', '');

INSERT INTO employees SELECT MAX(emp_no)+1, '1991-05-17','Leela','Jagu','M','2000-01-01' FROM employees;

Inserting Employee Record and establish relationship between different tables.
INSERT INTO employees SELECT MAX(emp_no)+1, '1991-05-17','Leela','Jagu','M','2000-01-01' FROM employees;

INSERT INTO titles VALUES (500000, 'Analyst', '2000-01-01','9999-01-01');

INSERT INTO salaries VALUES(500000, '4000', '2000-01-01','9999-01-01');

INSERT INTO dept_emp VALUES(500000, 'd005','2000-01-01','9999-01-01');

Update:
UPDATE departments 
SET dept_name = 'New Dept'
WHERE dept_no = 'd999';

Update single record
SELECT * FROM employees
WHERE emp_no=500000;

UPDATE employees
SET first_name='Sam', last_name='Axe'
WHERE emp_no=500000;

For Update and Delete statements we need to mention primary key in the where clause so that it will be much faster.

CRUD Operations
INSERT INTO employees SELECT MAX(emp_no)+1, '1991-05-17', 'Leela', 'Jagu', 'M', '2018-11-01' FROM employees;

SELECT * FROM employees WHERE emp_no = 500000;

UPDATE employees 
SET birth_date='1991-06-17'
WHERE emp_no = 500000;

DELETE FROM employees 
WHERE emp_no = 500000;

Starting a transaction
begin;

commiting a transaction
commit;

rollback a transaction
rollback;

Mysql automatically commit every DML statemetn in the background 
i.e., set autocommit=1;

To disable Auto Commit Feature
set autocommit=0;

If a session is terminated(or when mysql workbench is exited) then all uncommitted transactions will be rollbacked!!!

In Oracle we have explicitly mention this commit statement as autocommit is off in oracle.

Creating Employee Record and establishing relationship with other tables using transaction.
USE employees;

begin;

INSERT INTO employees SELECT MAX(emp_no)+1, '1991-05-17','Leela','Jagu','M','2000-01-01' FROM employees;

INSERT INTO titles SELECT  MAX(emp_no), 'Analyst', '2000-01-01','9999-01-01' FROM employees;

INSERT INTO salaries SELECT  MAX(emp_no), '4000', '2000-01-01','9999-01-01' FROM employees;

INSERT INTO dept_emp SELECT  MAX(emp_no), 'd005','2000-01-01','9999-01-01' FROM employees;

commit;

SELECT  MAX(emp_no) FROM employees;

Database Locks:
SELECT * FROM employees WHERE emp_no = 500000;

begin;

UPDATE employees 
SET birth_date = '1992-05-17' 
WHERE emp_no = 500000;

commit;


Another Update is done via terminal.
UPDATE employees SET birth_date = '1993-05-17' WHERE emp_no = 500000;

User Defined Variables
SET @foo = 'bar';

SELECT @foo;



SELECT @employee_no:=MAX(emp_no)+1 FROM employees;

begin;

INSERT INTO employees VALUES(@employee_no, '1991-05-17','Sam','Axe','M','2000-01-01');

INSERT INTO titles VALUES(@employee_no, 'Analyst', '2000-01-01','9999-01-01');

INSERT INTO salaries VALUES(@employee_no, '5000', '2000-01-01','9999-01-01');

INSERT INTO dept_emp VALUES(@employee_no, 'd005','2000-01-01','9999-01-01');

commit;

SELECT * FROM employees 
WHERE emp_no=@employee_no;

Lost Update:
SELECT * FROM salaries WHERE emp_no = 500000;

begin;

UPDATE salaries 
SET salary= salary + 20
WHERE emp_no = 500000;

commit;


Using Terminal
SELECT @modified_salary:=salary FROM salaries WHERE emp_no = 500000;

begin;

UPDATE salaries 
SET salary= @modified_salary + 10
WHERE emp_no = 500000;

commit;

Here in the terminal session we are caching to the modified_salary variable so even if the first transaction is finished, the transaction in the terminal will not see the updated value that is executing in the terminal, because its value is stored in the variable, so we lost the update that is made through sql client editor.
To avoid this we will use Select for Update while storing session variable, so that it will check whether any lock is present on that select statement if not then only it will store the value into variable, from now select for update has obtained lock.

SELECT @modified_salary:=salary FROM salaries WHERE emp_no = 500000 FOR UPDATE;

begin;

UPDATE salaries 
SET salary= @modified_salary + 10
WHERE emp_no = 500000;

commit;

SELECT * FROM salaries WHERE emp_no = 500000;

Assignments:
SELECT 
    cust.first_name AS 'First Name',
    cust.last_name AS 'Last Name',
    DATE_FORMAT(ord.order_date, '%M, %d, %Y') AS 'Order Date',
    ord.ship_address AS 'Ship Address',
    ord.ship_city AS 'City',
    ord.ship_state_province AS 'State',
    ord.ship_zip_postal_code AS 'Zip',
    ord.ship_country_region AS 'Country',
    products.product_code AS 'Product Code',
    products.product_name AS 'Product Name',
    FORMAT(products.list_price, 2) AS 'List Price',
    FORMAT(ord_det.quantity, 0) AS 'Quantity',
    FORMAT((ord_det.quantity * products.standard_cost),
        2) AS 'Total Cost'
FROM
    orders AS ord
        JOIN
    order_details AS ord_det ON ord.id = ord_det.order_id
        JOIN
    customers AS cust ON cust.id = ord.customer_id
        JOIN
    products ON products.id = ord_det.product_id
;

Sales Report by Year, State limiting to order invocied

SELECT 
    DATE_FORMAT(ord.order_date, '%Y - %m') AS 'Sales Month',
    ord.ship_state_province AS state,
    CONCAT('$',
            FORMAT(SUM(products.list_price * ord_det.quantity),
                2)) AS Revenue
FROM
    orders AS ord
        JOIN
    order_details AS ord_det ON ord.id = ord_det.order_id
        JOIN
    products ON ord_det.product_id = products.id
WHERE
    ord_det.status_id = 2
GROUP BY DATE_FORMAT(ord.order_date, '%Y - %m') , state
ORDER BY DATE_FORMAT(ord.order_date, '%Y - %m') , state ASC
;

Report by year - month, product limited to order invoiced
SELECT 
    DATE_FORMAT(ord.order_date, '%Y - %m') AS 'Sales Month',
    products.product_name AS product,
    CONCAT('$',
            FORMAT(SUM(products.list_price * ord_det.quantity),
                2)) AS Sales,
    CONCAT('$',
            FORMAT(SUM(products.standard_cost * ord_det.quantity),
                2)) AS Cost,
    CONCAT('$',
            FORMAT(SUM((products.list_price - products.standard_cost) * ord_det.quantity),
                2)) AS Profit
FROM
    orders AS ord
        JOIN
    order_details AS ord_det ON ord.id = ord_det.order_id
        JOIN
    products ON ord_det.product_id = products.id
WHERE
    ord_det.status_id = 2
GROUP BY DATE_FORMAT(ord.order_date, '%Y - %m') , product
ORDER BY DATE_FORMAT(ord.order_date, '%Y - %m') ASC , SUM((products.list_price - products.standard_cost) * ord_det.quantity) DESC
;

View:
use northwind;

create or replace view first_view
as select * from products;

select * from first_view;

drop view first_view;


CREATE OR REPLACE VIEW order_view AS
    SELECT 
        emp.first_name AS 'Emp First Name',
        emp.last_name AS 'Emp Last Name',
        cust.first_name AS 'Cust First Name',
        cust.last_name AS 'Cust Last Name',
        ord.ship_name AS 'Shipper Name',
        products.product_code AS 'Product Code',
        products.product_name AS 'Product Name',
        ord_status.status_name AS 'Order Status Name',
        ord_det_status.status_name AS 'Order Detail Status Name',
        ord_tax_status.tax_status_name AS 'Order Tax Status Name'
    FROM
        orders AS ord
            JOIN
        order_details AS ord_det ON ord.id = ord_det.order_id
            JOIN
        products ON products.id = ord_det.product_id
            JOIN
        orders_status AS ord_status ON ord_status.id = ord.status_id
            JOIN
        order_details_status AS ord_det_status ON ord_det_status.id = ord_det.status_id
            JOIN
        orders_tax_status AS ord_tax_status ON ord_tax_status.id = IFNULL(ord.tax_status_id, 1)
            JOIN
        employees AS emp ON emp.id = ord.employee_id
            JOIN
        customers AS cust ON cust.id = ord.customer_id;

select * from order_view;

drop view order_view;

Create and Truncate Table:
use employees;

select count(*) from salaries;

create table salaries2 as select * from salaries;

select count(*) from salaries2;

truncate table salaries2;

Dropping Table:
drop table salaries2;

Create Table with Primary Key and Auto Increment:
use employees;

CREATE TABLE customer
(
  id INTEGER auto_increment,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  address VARCHAR(255),
  city VARCHAR(100),
  state VARCHAR(2),
  zip_code VARCHAR(10),
  PRIMARY KEY (id)
);


CREATE TABLE drink_order
(
 id INTEGER auto_increment,
 customer_id INTEGER,
 description VARCHAR(255),
 PRIMARY KEY (id)
);

INSERT INTO customer VALUES(null, 'Leela', 'Jagu', 'Address', 'City', 'AP', '000');
INSERT INTO drink_order VALUES(12344, 1234, 'Drink');

Foreign Key:
Foreign Key should be unique to the Database Schema
convention:
fk_table1_table2[num]
fk_drink_order_customer1
fk_drink_order_customer2

use employees;

DROP TABLE IF EXISTS customer;
DROP TABLE IF EXISTS drink_order;

CREATE TABLE customer
(
  id INTEGER auto_increment,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  address VARCHAR(255),
  city VARCHAR(100),
  state VARCHAR(2),
  zip_code VARCHAR(10),
  PRIMARY KEY (id)
);


CREATE TABLE drink_order
(
 id INTEGER auto_increment,
 customer_id INTEGER,
 description VARCHAR(255),
 PRIMARY KEY (id),
 CONSTRAINT fk_drink_order_customer
 FOREIGN KEY (customer_id)
 REFERENCES customer (id)
);

INSERT INTO customer VALUES(null, 'Leela', 'Jagu', 'Address', 'City', 'AP', '000');
INSERT INTO drink_order VALUES(12344, 1, 'Drink');

select * from customer;
select * from drink_order;

Unique Index:
CREATE TABLE customer
(
  id INTEGER auto_increment,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  address VARCHAR(255),
  city VARCHAR(100),
  state VARCHAR(2),
  zip_code VARCHAR(10),
  PRIMARY KEY (id),
  UNIQUE KEY unique_idx (first_name,last_name,address)
);

INSERT INTO customer VALUES(null, 'Leela2', 'Jagu2', 'Address', 'City', 'AP', '000');

Index:
Index Names should be unique for a table.
Indexs will allow for faster search operations if we have lot of rows with same index value as it will go directly to that partition and perform operations.
CREATE TABLE customer
(
  id INTEGER auto_increment,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  address VARCHAR(255),
  city VARCHAR(100),
  state VARCHAR(2),
  zip_code VARCHAR(10),
  PRIMARY KEY (id),
  UNIQUE KEY unique_idx (first_name,last_name,address),
  INDEX last_name_idx (last_name)
);

Assignment:
use employees;

DROP TABLE IF EXISTS book;
DROP TABLE IF EXISTS author;

CREATE TABLE author
(
  id INTEGER auto_increment,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  email VARCHAR(255),
  phone VARCHAR(15),
  website VARCHAR(255),
  date_created TIMESTAMP,
  date_updated TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (id),
  UNIQUE KEY email_unique_idx (email)
);


CREATE TABLE book
(
 id INTEGER auto_increment,
 author_id INTEGER,
 title VARCHAR(100),
 subtitle VARCHAR(100),
 description TEXT,
 isbn CHAR(13),
 price DECIMAL(9,2),
 date_created TIMESTAMP,
 date_updated TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
 PRIMARY KEY (id),
 UNIQUE KEY isbn_unique_idx (isbn),
 CONSTRAINT fk_book_author1
 FOREIGN KEY (author_id)
 REFERENCES author (id)
);

Adding and Dropping Column:
ALTER TABLE author add column middle_name varchar(100);

ALTER TABLE author drop column middle_name;

Altering Column Order:
ALTER TABLE author MODIFY middle_name varchar(100) AFTER first_name;

ALTER TABLE author add column middle_name varchar(100) AFTER last_name;

ALTER TABLE author CHANGE middle_name middle_name_new varchar(100) AFTER first_name;

Adding and Droping Index:
ALTER TABLE author add index last_name_idx (last_name);

ALTER TABLE author drop index last_name_idx;

Dropping and Adding Foreign Key:
ALTER TABLE book drop foreign key fk_book_author_1;

ALTER TABLE book add 
foreign key fk_book_author_1(author_id)
references author (id);

Virtual Column:
ALTER TABLE book add column upc_barcode char(12) as (lpad(upc,12,'0'));

