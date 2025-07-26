---
tags:
  - "#backend"
references: https://youtu.be/HXV3zeQKqGY?si=CbO_L1udwspvQ_TR
date_created: 2024-06-07
date_modified: 2025-03-17
---
---
# Basic Queries
### Create Table

```sql
CREATE TABLE student (
   student_id INT, -- can also define primary here
   name VARCHAR(20),
   major VARCHAR(30),
   PRIMARY KEY(student_id)
);
-- To display table
DESCRIBE student;

-- To remove table
DROP TABLE student;

-- Add new column to table
ALTER TABLE student
ADD gpa DECIMAL(3, 2);

-- To drop a specific column
ALTER TABLE student
DROP COLUMN gpa;
```

### To insert into a table

```sql
-- inserting a row
INSERT INTO student VALUES (1, 'Jack', 'Biology');
INSERT INTO student VALUES (2, 'Kate', 'Sociology');

-- insert a null attribute
INSERT INTO student (student_id, name) VALUES (3, 'Claire');

-- To show everything inside table
SELECT * FROM student;
```

#### Constraints

```sql
CREATE TABLE student (
	student_id INT AUTO_INCREMENT PRIMARY KEY, -- auto++ from 1
	name VARCHAR(20) NOT NULL, -- any row can't be empty
	-- major VARCHAR(30) UNIQUE -- every row must be unique
	major VARCHAR(30) DEFAULT 'Undecided' -- default if null
);

SELECT * FROM student;

INSERT INTO student(name, major) VALUES ('Jack', 'Biology');
INSERT INTO student VALUES (null, 'Kate', 'Sociology');
INSERT INTO student (name) VALUES ('Claire');
INSERT INTO student VALUES (5, 'Mike', 'Computer Science');

DROP TABLE student;
```

#### SQL Comparison Operators

| Operator | Description              |
| -------- | ------------------------ |
| =        | Equal to                 |
| >        | Greater than             |
| <        | Less than                |
| >=       | Greater than or equal to |
| <=       | Less than or equal to    |
| <>       | Not equal to             |

### Update

```sql
-- Update all biology majors to bio
UPDATE student
SET major = 'Bio'
WHERE major = 'Biology';

-- Update student_id 4's major to Mathematics
UPDATE student
SET major = 'Mathematics'
WHERE student_id = 4;

-- Update students with bio and chem to biochem
UPDATE student
SET major = 'Biochemistry'
WHERE major = 'Bio' OR major = 'Chemistry';

-- update multiple attributes
UPDATE student
SET name = 'Tom', major = 'undecided'
WHERE student_id = 1;

-- where is optional
UPDATE student
SET major = 'idk';

-- delete all data
DELETE FROM student

-- delete specific tuple
DELETE FROM student
WHERE student_id = 5;
```

### Select

```sql
CREATE TABLE student (
    student_id INT PRIMARY KEY,
    name VARCHAR(20),
    major VARCHAR(30)
);

INSERT INTO student VALUES (1, 'Jack', 'Biology');
INSERT INTO student VALUES (2, 'Kate', 'Sociology');
INSERT INTO student VALUES (3, 'Claire', 'Chemistry');
INSERT INTO student VALUES (4, 'Jack', 'Biology');
INSERT INTO student VALUES (5, 'Mike', 'Computer Science');

-- Select every column from student table
SELECT * FROM student;

-- Select name column
SELECT name FROM student;

-- Select multiple column, sorted by name
SELECT student.name, student.major
FROM student
ORDER BY name; --ASC default

-- Select multiple column, sorted desc. by id
SELECT student.name, student.major
FROM student
ORDER BY student_id DESC;

-- Sort first by major, then then desc. by id
SELECT *
FROM student
ORDER BY major, student_id DESC;

-- We can limit our query to topmost
SELECT name
FROM student
ORDER BY major
LIMIT 3;

-- can also add conditions
SELECT *
FROM student
WHERE major = 'Biology';

-- specified name
SELECT *
FROM student
WHERE name IN ('Claire', 'Jack');

SELECT *
FROM student
WHERE major IN ('Biology', 'Chemistry') AND student_id > 2;

-- there also exists BETWEEN and is NULL

-- WILDCARD
-- `%` represents any combination of characters.
-- `_` represents only one character.
SELECT * FROM worker WHERE first_name = '_i%' -- 'himanshu', 'rishav'

-- DISTINCT
SELECT DISTINCT departments FROM worker


```

---
# Complex Company Queries

![[Pasted image 20250317163327.png | 600]]

## Create

### To create foreign key while creating

```sql
CREATE TABLE branch (
  mgr_id INT, 
  FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
);
```

### To add foreign key to an existing table

```sql
ALTER TABLE employee
ADD FOREIGN KEY(branch_id)
REFERENCES branch(branch_id)
ON DELETE SET NULL;
```

### To create composite Primary Key

```sql
CREATE TABLE works_with(
		PRIMARY KEY(emp_id, client_id)
);
```

## Inserting

You need to be careful when inserting in tables with interconnected foreign keys.

- You can’t reference a foreign key that doesn’t exist. Need to set that to null

```sql
INSERT INTO employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL);
```

Now that we have created a employee with id = 100, we can insert a branch that references it

```sql
INSERT INTO branch VALUES(1, 'Corporate', 100, '2006-02-09');
```

Now that branch exists, we can update employee 100 to have that as foreign key.

```sql
UPDATE employee
SET branch_id = 1
WHERE emp_id = 100;
```

And also insert all employee that reference ‘`Corporate`' branch into employee table

```sql
INSERT INTO employee VALUES(101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, 1);
```

---
## Wildcard

