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
        name    VARCHAR(50) NOT NULL,
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
   INSERT INTO employees (id, name, salary, company) VALUES
    (1, 'Uolevi',   5000, 'Google'),
    (2, 'Maija',    6000, 'Google'),
    (3, 'Liisa',    2000, 'Amazon'),
    (4, 'Kaaleppi', 7500, 'Microsoft');
   ```

---

## SQL Query Exercises

1. **Get names of all the movies**

   ```sql
   SELECT name
   FROM movies;
   ```

   **Expected Result**  
   | name |
   |-------------|
   | Snow White |
   | Fantasia |
   | Pinocchio |
   | Dumbo |
   | Bambi |

2. **Get names and publication years for all movies**

   ```sql
   SELECT name, year
   FROM movies;
   ```

   **Expected Result**  
   | name | year |
   |------------|------|
   | Snow White | 1937 |
   | Fantasia | 1940 |
   | Pinocchio | 1940 |
   | Dumbo | 1941 |
   | Bambi | 1942 |

3. **Get names of all the movies published in 1940**

   ```sql
   SELECT name
   FROM movies
   WHERE year = 1940;
   ```

   **Expected Result**  
   | name |
   |-----------|
   | Fantasia |
   | Pinocchio |

4. **Get names of all the movies published before 1950**

   ```sql
   SELECT name
   FROM movies
   WHERE year < 1950;
   ```

   **Expected Result**  
   | name |
   |------------|
   | Snow White |
   | Fantasia |
   | Pinocchio |
   | Dumbo |
   | Bambi |
