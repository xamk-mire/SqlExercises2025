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

3. **Learning to use pgAdmin**
   - Here is a great tutorial video that covers the basics of **pgAdmin**: [pgAdmin Tutorial - How to Use pgAdmin](https://www.youtube.com/watch?v=WFT5MaZN6g4)
   - You can follow the tutorial using **pgAmdin** in your own computer

4. **Create a New Database**
   - In pgAdmin, expand the server tree and right-click on **Databases** to create a new database for the exercises, and name it as **SqlExercises**.

---

## Part 2: Create the Required Tables

1. **Movies Table**  
   Create a table named `movies` with columns for `id`, `name`, and `year`. In pgAdmin, navigate to your database, open the Query Tool, and run the following SQL:

   ```sql
   CREATE TABLE movies (
     id   INT PRIMARY KEY,
     name VARCHAR(100) NOT NULL,
     year INT NOT NULL
   );
   ```

2. **Employees Table**  
   Create another table named `employees` with columns for `id`, `name`, `salary`, and `company`:

   ```sql
   CREATE TABLE employees (
        id      INT PRIMARY KEY,
        forename    VARCHAR(50) NOT NULL,
        surname  VARCHAR(50) NOT NULL,
        salary  INT,
        company VARCHAR(50)
    );
   ```

---

## Part 3: Insert Sample Data

1. **Insert Data into Movies**  
   Run the following inserts:

   ```sql
   INSERT INTO movies (id, name, year) VALUES
    (1, 'Snow White', 1937),
    (2, 'Fantasia',   1940),
    (3, 'Pinocchio',  1940),
    (4, 'Dumbo',      1941),
    (5, 'Bambi',      1942);
   ```

2. **Insert Data into Employees**  
   Run the following inserts:

   ```sql
   INSERT INTO employees (id, forename, salary, company) VALUES
    (1, 'Uolevi',   'Korhonen',  5000, 'Google'),
    (2, 'Maija',    'Virtanen',  6000, 'Google'),
    (3, 'Liisa',    'Lahtinen',  2000, 'Amazon'),
    (4, 'Kaaleppi', 'Korhonen',  7500, 'Microsoft');
    (5, 'Pekka',    'Virtanen',  6000, 'Google');
    (6, 'Liisa',    'Lahtinen',  7500, 'Microsoft');
    (7, 'Kaaleppi', 'Korhonen',   7500, 'Amazon');
   ```

---

## Part 4: SQL Query Exercises

> [!NOTE]
> Exercises 1-10 use the **movies** table

### 1. **Get names of all the movies**

   **Expected Result**  
   | name |
   |-------------|
   | Snow White |
   | Fantasia |
   | Pinocchio |
   | Dumbo |
   | Bambi |



### 2. **Get names and publication years for all movies**

   **Expected Result**  
   | name | year |
   |------------|------|
   | Snow White | 1937 |
   | Fantasia | 1940 |
   | Pinocchio | 1940 |
   | Dumbo | 1941 |
   | Bambi | 1942 |



### 3. **Get names of all the movies published in 1940**

   **Expected Result**  
   | name |
   |-----------|
   | Fantasia |
   | Pinocchio |



### 4. **Get names of all the movies published before 1950**

   **Expected Result**  
   | name |
   |------------|
   | Snow White |
   | Fantasia |
   | Bambi |


### 5. **Get the names of the movies published between 1940 and 1950**  

   **Expected Result**  
   | name      |
   |-----------|
   | Fantasia  |
   | Bambi     |


### 6. **Get the names of the movies published before 1950 and after 1980**  

   **Expected Result**  
   | name       |
   |------------|
   | Snow White |
   | Fantasia   |
   | Bambi      |


### 7. **Get the names of the movies which were not published in 1940**  

   **Expected Result**  
   | name       |
   |------------|
   | Dumbo      |
   | Bambi      |


### 8. **Get the names of all the movies in alphabetical order**  

   **Expected Result**  
   | name       |
   |------------|
   | Bambi      |
   | Dumbo      |
   | Fantasia   |
   | Pinocchio  |
   | Snow White |


### 9. **Get the names of all the movies in reverse alphabetical order**  

   **Expected Result**  
   | name       |
   |------------|
   | Snow White |
   | Pinocchio  |
   | Fantasia   |
   | Dumbo      |
   | Bambi      |


### 10. **Get the names and publication years of movies, primarily in reverse order according to the publication year and secondarily in alphabetical order**  

   **Expected Result**  
   | name       | year |
   |------------|------|
   | Bambi      | 1942 |
   | Dumbo      | 1941 |
   | Fantasia   | 1940 |
   | Pinocchio  | 1940 |
   | Snow White | 1937 |

---

> [!NOTE]
> Exercises 11-20 use the **employees** table


### 11. **Get all different forenames**

   **Expected Result**  
   | forename   |
   |------------|
   | Uolevi     |
   | Maija      |
   | Pekka      |
   


### 13. **Get all the different names**  

   **Expected Result**  
   | forename   | surname  |
   |------------|----------|
   | Uolevi     | Korhonen |
   | Maija      | Virtanen |
   | Pekka      | Virtanen |


### 13. **Get the amount of employees**

   **Expected Result**  
   | count |
   |-------|
   | 7     |


### 14. **Get the amount of employees whose salary is over 2000**  

   **Expected Result**  
   | count |
   |-------|
   | 6     |


### 15. **Get the sum of the employees' salaries**
  
   **Expected Result**  
   | sum   |
   |-------|
   | 41500 |


### 16. **Get the greatest salary** 
 
   **Expected Result**  
   | max  |
   |------|
   | 7500 |


### 17. **Get the amount of different companies** 
 
   **Expected Result**  
   | count |
   |-------|
   | 3     |


### 18. **Get the amount of employees for each company** 
 
   **Expected Result**  
   | company    | count |
   |------------|-------|
   | Amazon     | 2     |
   | Google     | 3     |
   | Microsoft  | 2     |


### 19. **Get the largest salary of an employee for each company** 
 
   **Expected Result**  
   | company    | max_salary |
   |------------|------------|
   | Amazon     | 7500       |
   | Google     | 6000       |
   | Microsoft  | 7500       |


### 20. **Get the greatest salary from those companies, where the salary is at least 5000**  
   *(i.e., only include companies that have at least one employee with salary >= 5000, then get the greatest salary for each.)*  

   **Expected Result**  
   | company    | max_salary |
   |------------|------------|
   | Amazon     | 7500       |
   | Google     | 6000       |
   | Microsoft  | 7500       |
```
