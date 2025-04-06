# DAILY SQL CHEAT SHEET - MySQL

A beginner-to-advanced cheat sheet for MySQL queries. Continuously expandable!

---

## 📚 Table of Contents
- [📦 Database & Table Management (DDL)](#-database--table-management-ddl)
- [✍️ Insert / Update / Delete Data (DML)](#-insert--update--delete-data-dml)
- [📊 Select (Read Data)](#-select-read-data)
- [🎯 Filtering & Conditions](#-filtering--conditions)
- [🔗 Joins (Multi-table Queries)](#-joins-multi-table-queries)
- [🧮 Aggregates & Group By](#-aggregates--group-by)
- [👥 User & Privilege Management](#-user--privilege-management)
- [💾 Backup & Import (CLI)](#-backup--import-cli)
- [🔐 Foreign Keys](#-foreign-keys)
- [🧰 Bonus Commands](#-bonus-commands)
- [📌 Common Useful Queries](#-common-useful-queries)
- [✏️ Additions/Changes Log](#-additionschanges-log)

---

## 📦 DATABASE & TABLE MANAGEMENT (DDL)
```sql
CREATE DATABASE mydb;
USE mydb;

CREATE TABLE students (
  id INT AUTO_INCREMENT PRIMARY KEY,
  full_name VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  dob DATE,
  marks INT
);

ALTER TABLE students ADD phone VARCHAR(15);
RENAME TABLE students TO student_info;

DROP TABLE student_info;
DROP DATABASE mydb;
```

---

## ✍️ INSERT / UPDATE / DELETE DATA (DML)
```sql
INSERT INTO students (full_name, email, dob, marks)
VALUES ('John Doe', 'john@example.com', '2002-04-05', 87);

UPDATE students SET marks = 95 WHERE email = 'alice@gmail.com';

DELETE FROM students WHERE id = 2;
```

---

## 📊 SELECT (READ DATA)
```sql
SELECT * FROM students;
SELECT full_name, email FROM students;
SELECT * FROM students WHERE marks > 80;
SELECT * FROM students ORDER BY marks DESC;
SELECT * FROM students LIMIT 5;
```

---

## 🎯 FILTERING & CONDITIONS
```sql
SELECT * FROM students WHERE marks > 80 AND dob > '2002-01-01';
SELECT * FROM students WHERE marks BETWEEN 70 AND 90;
SELECT * FROM students WHERE full_name IN ('Alice', 'Bob');
SELECT * FROM students WHERE email LIKE '%@gmail.com';
```

---

## 🔗 JOINS (MULTI-TABLE QUERIES)
```sql
SELECT s.full_name, c.course_name
FROM students s
JOIN courses c ON s.id = c.student_id;

SELECT s.full_name, c.course_name
FROM students s
LEFT JOIN courses c ON s.id = c.student_id;
```

---

## 🧮 AGGREGATES & GROUP BY
```sql
SELECT COUNT(*) FROM students;
SELECT AVG(marks) FROM students;
SELECT course_id, AVG(marks) AS avg_marks FROM students GROUP BY course_id;
SELECT course_id, COUNT(*) AS total FROM students GROUP BY course_id HAVING total > 5;
```

---

## 👥 USER & PRIVILEGE MANAGEMENT
```sql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON mydb.* TO 'newuser'@'localhost';
REVOKE SELECT ON mydb.* FROM 'newuser'@'localhost';
DROP USER 'newuser'@'localhost';
```

---

## 💾 BACKUP & IMPORT (CLI)
```bash
mysqldump -u root -p mydb > mydb_backup.sql
mysql -u root -p mydb < mydb_backup.sql
```

---

## 🔐 FOREIGN KEYS
```sql
CREATE TABLE enrollments (
  id INT AUTO_INCREMENT PRIMARY KEY,
  student_id INT,
  course_id INT,
  FOREIGN KEY (student_id) REFERENCES students(id),
  FOREIGN KEY (course_id) REFERENCES courses(id)
);
```

---

## 🧰 BONUS COMMANDS
```sql
DESC tablename;
SHOW TABLES;
SHOW DATABASES;
SHOW COLUMNS FROM tablename;
SHOW CREATE TABLE tablename;
```

---

## 📌 COMMON USEFUL QUERIES
```sql
-- Get the current date and time
SELECT NOW();

-- Get unique values from a column
SELECT DISTINCT course_name FROM courses;

-- Find NULL or NOT NULL entries
SELECT * FROM students WHERE phone IS NULL;
SELECT * FROM students WHERE phone IS NOT NULL;

-- Search using multiple patterns
SELECT * FROM students WHERE email LIKE '%gmail%' OR email LIKE '%yahoo%';

-- Rename a column
ALTER TABLE students CHANGE phone contact_number VARCHAR(15);

-- Get top N records by group
SELECT student_id, MAX(marks) FROM students GROUP BY student_id;

-- Check for duplicates
SELECT email, COUNT(*) FROM students GROUP BY email HAVING COUNT(*) > 1;

-- Pagination
SELECT * FROM students LIMIT 10 OFFSET 20;

-- Union two SELECTs
SELECT email FROM students
UNION
SELECT email FROM alumni;
```

---

### ✏️ Additions/Changes Log
- Initial version created on April 6, 2025
- Added categorized Table of Contents
- Added "Common Useful Queries" section
