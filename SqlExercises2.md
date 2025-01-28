# Introduction

In this exercise, you will learn the fundamentals of setting up and using a **PostgreSQL** database, one of the most popular open-source relational database management systems. You will also be introduced to **pgAdmin**, a web-based administration tool for managing PostgreSQL databases through a graphical user interface (GUI). By the end of the exercise, you will have hands-on experience with:

1. **Installing PostgreSQL** and **pgAdmin** on your system (or using a hosted environment).
2. **Creating** and **connecting** to a PostgreSQL database.
3. **Designing** and **creating** tables using SQL commands.
4. **Inserting** sample data into the tables.
5. **Retrieving** data with basic `SELECT` queries to understand how SQL works.

Understanding these core concepts will provide a strong foundation for more advanced database topics, such as joining multiple tables, indexing, and optimizing queries.

---

## Part 1: Installation and Setup

1. **Install PostgreSQL**

   - Download the latest version of PostgreSQL from the [official website](https://www.postgresql.org/download/), or use your system’s package manager (e.g., Homebrew on macOS, APT on Ubuntu/Debian).
   - When prompted during installation on Windows, ensure the “pgAdmin” component is selected.

2. **Launch pgAdmin**

   - If you installed PostgreSQL with the Windows installer, pgAdmin is included by default.
   - On macOS or Linux, search your applications for “pgAdmin” or run `pgAdmin4` if installed via a package manager.
   - Alternatively, if you prefer the command line, open your terminal and use the `psql` tool to access the PostgreSQL server.

3. **Create a New Database**
   - In pgAdmin, expand the server tree and right-click on **Databases** to create a new database (e.g., `mydb`).
   - If using `psql`, you can run:
     ```sql
     CREATE DATABASE mydb;
     \c mydb  -- to connect to the newly created database
     ```

---

## Part 2: Create the Required Tables

1. **Students Table**

   ```sql
   CREATE TABLE students (
    student_id     SERIAL PRIMARY KEY,
    first_name     VARCHAR(50) NOT NULL,
    last_name      VARCHAR(50) NOT NULL,
    gender         CHAR(1)     NOT NULL,
    date_of_birth  DATE        NOT NULL,
    major          VARCHAR(100)
   );
   ```

2. **Teachers Table**

   ```sql
   CREATE TABLE teachers (
    teacher_id  SERIAL PRIMARY KEY,
    first_name  VARCHAR(50) NOT NULL,
    last_name   VARCHAR(50) NOT NULL,
    department  VARCHAR(100)
   );
   ```

3. **Courses Table**

   ```sql
   CREATE TABLE courses (
    course_id    SERIAL PRIMARY KEY,
    course_name  VARCHAR(100) NOT NULL,
    teacher_id   INT NOT NULL,
    semester     VARCHAR(50),
    CONSTRAINT fk_courses_teacher
        FOREIGN KEY (teacher_id)
        REFERENCES teachers (teacher_id)
   );
   ```

4. **Enrollments Table**

   ```sql
   CREATE TABLE enrollments (
    enrollment_id   SERIAL PRIMARY KEY,
    student_id      INT NOT NULL,
    course_id       INT NOT NULL,
    enrollment_date DATE NOT NULL,
    grade           CHAR(1),
    CONSTRAINT fk_enrollments_student
        FOREIGN KEY (student_id)
        REFERENCES students (student_id),
    CONSTRAINT fk_enrollments_course
        FOREIGN KEY (course_id)
        REFERENCES courses (course_id)
   );
   ```

---

## Part 3: Insert Sample Data

1. **Insert Data into Students**

   ```sql
   INSERT INTO students (first_name, last_name, gender, date_of_birth, major)
   VALUES
   ('Alice', 'Johnson', 'F', '2000-03-12', 'Computer Science'),
   ('Bob', 'Smith', 'M', '1999-07-24', 'Mathematics'),
   ('Carol', 'Davis', 'F', '1998-11-02', 'English'),
   ('David', 'Brown', 'M', '2001-01-17', 'Computer Science'),
   ('Emily', 'Miller', 'F', '2000-05-05', 'Business'),
   ('Frank', 'Wilson', 'M', '1999-02-10', 'Physics'),
   ('Grace', 'Harris', 'F', '2001-06-20', 'Mathematics'),
   ('Henry', 'Clark', 'M', '2002-09-13', 'History'),
   ('Ivy', 'Lee', 'F', '1999-12-25', 'Business'),
   ('John', 'Walker', 'M', '2000-10-10', 'Computer Science');
   ```

1. **Insert Data into Teachers**

   ```sql
   INSERT INTO teachers (first_name, last_name, department)
   VALUES
   ('Laura', 'Adams', 'Computer Science'),
   ('Mark', 'Baker', 'Mathematics'),
   ('Nina', 'Collins', 'English'),
   ('Oliver', 'Davis', 'Business'),
   ('Paula', 'Evans', 'Physics');
   ```

1. **Insert Data into Courses**

   ```sql
   INSERT INTO courses (course_name, teacher_id, semester)
   VALUES
   ('Intro to Programming', 1, 'Fall 2023'),
   ('Advanced Calculus', 2, 'Fall 2023'),
   ('English Literature', 3, 'Fall 2023'),
   ('Business Ethics', 4, 'Fall 2023'),
   ('Physics I', 5, 'Fall 2023'),
   ('Data Structures', 1, 'Spring 2024');
   ```

1. **Insert Data into Enrollments**

   ```sql
   INSERT INTO enrollments (student_id, course_id, enrollment_date, grade)
   VALUES
   (1, 1, '2023-08-25', 'A'),  -- Alice in Intro to Programming
   (1, 6, '2024-01-15', NULL), -- Alice in Data Structures (no grade yet)
   (2, 2, '2023-08-27', 'B'),  -- Bob in Advanced Calculus
   (3, 3, '2023-08-30', 'A'),  -- Carol in English Literature
   (4, 1, '2023-08-25', 'B'),  -- David in Intro to Programming
   (5, 4, '2023-08-28', 'A'),  -- Emily in Business Ethics
   (6, 5, '2023-09-02', 'C'),  -- Frank in Physics I
   (2, 6, '2024-01-16', NULL), -- Bob in Data Structures (no grade yet)
   (7, 2, '2023-08-27', 'B'),  -- Grace in Advanced Calculus
   (8, 3, '2023-08-30', 'B'),  -- Henry in English Literature
   (9, 4, '2023-08-28', 'A'),  -- Ivy in Business Ethics
   (10, 1, '2023-08-25', 'A'), -- John in Intro to Programming
   (10, 6, '2024-01-15', NULL);-- John in Data Structures (no grade yet)
   ```

## **Done. Now you have a small database to practice multi-table queries.**

---

## SQL Query Exercises

1.  **Simple JOIN: Retrieve a list of all students and the courses they are enrolled in.**

    **Expected Result**
    | first_name | last_name | course_name |
    |------------|----------|-------------------------|
    | Alice | Johnson | Intro to Programming |
    | Alice | Johnson | Data Structures |
    | Bob | Smith | Advanced Calculus |
    | Carol | Davis | English Literature |
    | David | Brown | Intro to Programming |
    | Emily | Miller | Business Ethics |
    | Frank | Wilson | Physics I |
    | Bob | Smith | Data Structures |
    | Grace | Harris | Advanced Calculus |
    | Henry | Clark | English Literature |
    | Ivy | Lee | Business Ethics |
    | John | Walker | Intro to Programming |
    | John | Walker | Data Structures |

2.  **JOIN with Teacher Info: Show each enrollment along with the student name, course name, and teacher’s last name.**

    **Expected Result**  
     | student_first | student_last | course_name | teacher_last |
    |--------------|-------------|----------------------|-------------|
    | Alice | Johnson | Intro to Programming | Adams |
    | Alice | Johnson | Data Structures | Adams |
    | Bob | Smith | Advanced Calculus | Baker |
    | Carol | Davis | English Literature | Collins |
    | David | Brown | Intro to Programming | Adams |
    | Emily | Miller | Business Ethics | Davis |
    | Frank | Wilson | Physics I | Evans |
    | Bob | Smith | Data Structures | Adams |
    | Grace | Harris | Advanced Calculus | Baker |
    | Henry | Clark | English Literature | Collins |
    | Ivy | Lee | Business Ethics | Davis |
    | John | Walker | Intro to Programming | Adams |
    | John | Walker | Data Structures | Adams |

3.  **Filtering: Get only the enrollments for “Intro to Programming.”**

    **Expected Result**
    | first_name | last_name | course_name | grade |
    |-----------|----------|----------------------|------|
    | Alice | Johnson | Intro to Programming | A |
    | David | Brown | Intro to Programming | B |
    | John | Walker | Intro to Programming | A |

4.  **Aggregate Functions: Count how many students are in each course.**

    **Expected Result**
    | course_name | total_students |
    |----------------------|---------------|
    | Physics I | 1 |
    | Business Ethics | 2 |
    | English Literature | 2 |
    | Data Structures | 3 |
    | Intro to Programming | 3 |
    | Advanced Calculus | 2 |

5.  **Subquery: Find students who are enrolled in more than one course.**

    **Expected Result**
    | student_id | first_name | last_name |
    |------------|-----------|----------|
    | 1 | Alice | Johnson |
    | 2 | Bob | Smith |
    | 10 | John | Walker |

6.  **JOIN + Filter by Grade: List students who have received an “A.”**

    **Expected Result**
    | first_name | last_name | course_name | grade |
    |-----------|----------|----------------------|------|
    | John | Walker | Intro to Programming | A |
    | Alice | Johnson | Intro to Programming | A |
    | Carol | Davis | English Literature | A |
    | Ivy | Lee | Business Ethics | A |
    | Emily | Miller | Business Ethics | A |

7.  **List all students and their majors who are enrolled in at least one course offered in Fall 2023.**

    **Expected Result**
    | student_id | first_name | last_name | major |
    |------------|-----------|----------|-------------------|
    | 1 | Alice | Johnson | Computer Science |
    | 2 | Bob | Smith | Mathematics |
    | 3 | Carol | Davis | English |
    | 4 | David | Brown | Computer Science |
    | 5 | Emily | Miller | Business |
    | 6 | Frank | Wilson | Physics |
    | 7 | Grace | Harris | Mathematics |
    | 8 | Henry | Clark | History |
    | 9 | Ivy | Lee | Business |
    | 10 | John | Walker | Computer Science |

8.  **Show each course's name along with the teacher's full name and department.**

    **Expected Result**
    | course_name | teacher_name | department |
    |----------------------|--------------|------------------|
    | Intro to Programming | Laura Adams | Computer Science |
    | Advanced Calculus | Mark Baker | Mathematics |
    | English Literature | Nina Collins | English |
    | Business Ethics | Oliver Davis | Business |
    | Physics I | Paula Evans | Physics |
    | Data Structures | Laura Adams | Computer Science |

9.  **Find the total number of courses each student is enrolled in (across any semester), along with the student’s name.**

    **Expected Result**
    | first_name | last_name | total_courses |
    |-----------|----------|--------------|
    | John | Walker | 2 |
    | Alice | Johnson | 2 |
    | Bob | Smith | 2 |
    | David | Brown | 1 |
    | Frank | Wilson | 1 |
    | Grace | Harris | 1 |
    | Ivy | Lee | 1 |
    | Henry | Clark | 1 |
    | Carol | Davis | 1 |
    | Emily | Miller | 1 |

10. **Show the number of teachers in each department.**

    **Expected Result**
    | department | teacher_count |
    |-------------------|--------------|
    | Computer Science | 1 |
    | English | 1 |
    | Mathematics | 1 |
    | Physics | 1 |
    | Business | 1 |

11. **Find all teachers who do not teach any course. Note: In the sample data, every teacher has at least one course, so this query might return zero rows. But it’s useful for demonstrating an outer join.**

    **Expected Result**
    | teacher_id | first_name | last_name |
    |------------|------------|-----------|
    | | | |

12. **List the first and last names of students who have never received a grade of 'A'. This uses a subquery to exclude students who have at least one 'A'.**

    **Expected Result**
    | first_name | last_name |
    |-----------|----------|
    | Bob | Smith |
    | David | Brown |
    | Frank | Wilson |
    | Grace | Harris |
    | Henry | Clark |

13. **Find all students whose major matches a teacher’s department for at least one course**

    **Expected Result**
    | student_id | first_name | last_name | major | matching_department |
    |------------|-----------|----------|-------------------|--------------------|
    | 1 | Alice | Johnson | Computer Science | Computer Science |
    | 2 | Bob | Smith | Mathematics | Mathematics |
    | 3 | Carol | Davis | English | English |
    | 4 | David | Brown | Computer Science | Computer Science |
    | 5 | Emily | Miller | Business | Business |
    | 6 | Frank | Wilson | Physics | Physics |
    | 7 | Grace | Harris | Mathematics | Mathematics |
    | 9 | Ivy | Lee | Business | Business |
    | 10 | John | Walker | Computer Science | Computer Science |

14. **Get best (highest) letter grade per major**

    **Expected Result**
    | major | best_grade |
    |-------------------|-----------|
    | Business | A |
    | Computer Science | A |
    | English | A |
    | History | B |
    | Mathematics | B |
    | Physics | C |

15. **Find course(s) with the most unassigned grades**

    **Expected Result**
    | course_id | course_name | ungraded_count |
    |-----------|----------------|---------------|
    | 6 | Data Structures | 3 |
