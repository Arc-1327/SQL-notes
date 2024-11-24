# SQL
## Structured Query Language
* SQL is a standard language to interact with and manage databases.
* Developed by IBM during the 1970s.
* Key functions of SQL:
  - Query, ADD, DELETE, MODIFY
* Data scientists, ML engineers, Software engineers, etc use SQL.
* SQL is a domain-specific and declarative language, not a general-purpose programming language.
* Steps for execution of an SQL statement:
  - SQL statement - query is submitted to the database
  - Parser - understands the query and checks the syntax and semantics of the query
  - Compiler - finds the most effective way to optimize the query and generates code based on it
  - Query Executor - executes the query to fetch or modify the required data
  - Database - performs necessary operations
  - Results - results are sent back to the user
## IMDB Dataset
* IMDB: Website owned by Amazon.com
* Refers to a collection of data on movies, TV shows, actors, etc.
* Example schema of a database - tables and their relationship
  - directors
    - id (primary key)
    - first_name
    - last_name
  - movies
    - id (primary key)
    - name
    - year
    - rank
  - actors
    - id (primary key)
    - first_name
    - last_name
    - gender
  - roles
    - actor_id
    - movie_id
    - role
  - director-genre
    - director_id
    - genre
    - prob
  - movie_directors
    - director_id
    - movie_id
  - movie_genre
    - movie_id
    - genre
      
<br>

* SELECT:
  - Used for retrieving specific data from a table.
  - Examples:
    - SELECT * FROM movies;
    - SELECT name, year FROM movies;
        
<br>

* LIMIT and OFFSET:
  - LIMIT - specifies the maximum number of rows to return.
  - OFFSET- skips the given number of rows.
  - Examples:
    - SELECT name, rankscore FROM movies LIMIT 20; 
    - SELECT name, rankscore FROM movies LIMIT 20 OFFSET 40; 

<br>

* ORDER BY:
  - Used to sort the results of a query.
  - Uses ASC(Ascending) and DESC(Descending).
  - Example: SELECT name, year FROM movies ORDER BY year DESC LIMIT 10;

<br>

* DISTINCT:
  - Retrieves unique values from a column or combination of columns.
  - Examples:
    - SELECT DISTINCT genre FROM movie_genres; 
    - SELECT DISTINCT first_name, last_name FROM directors ORDER BY first_name;
      
<br>

* WHERE and Comparison Operators:
  - Filters the rows based on conditions.
  - Comparison operators: =, <>, !=, <, <=, >, >=
  - Conditions can be TRUE, FALSE, NULL
  - Example: SELECT name, year, rankscore FROM movies WHERE rankscore > 9 ORDER BY rankscore DESC LIMIT 10;
  - NULL: values that do not exist/unknown/missing
  - Examples:
    - SELECT name, year, rankscore FROM movies WHERE rankscore IS NULL;
    - SELECT name, year, rankscore FROM movies WHERE rankscore IS NOT NULL;

<br>

* Logical Operators:
  - Combines multiple conditions using: AND, OR, NOT, ALL, ANY, BETWEEN, EXIST, IN, LIKE, SOME.
  - Examples:
    - SELECT name, year, rankscore 
      FROM movies 
      WHERE rankscore > 9 AND year > 2000;
    - SELECT name, year 
      FROM movies 
      WHERE NOT year <= 2000 
      LIMIT 20;

<br>

## Aggregate Functions:
* Performs calculations on data and returns a single value.
* Examples:
  - SELECT MIN(year) FROM movies;
  - SELECT MAX(year) FROM movies;
  - SELECT COUNT(*) FROM movies;
  - SELECT COUNT(*) FROM movies where year>2000;
  - SELECT COUNT(year) FROM movies;

<br>

* GROUP BY:
  - Groups data based on one or more columns.
  - Often used with Aggregate functions(COUNT, MIN, MAX, or SUM).
  - All null values are grouped together if grouping columns contain NULL values.
  - Example: SELECT year, COUNT(year) AS year_count FROM movies GROUP BY year ORDER BY year_count DESC;

<br>

* HAVING:
  - Filters groups created by GROUP BY functions.
  - Example: SELECT name, year FROM movies HAVING year>2000;
  - HAVING without GROUP BY is the same as WHERE.
  - WHERE is applied to individual rows while HAVING is applied to groups.
  - HAVING is applied after grouping while WHERE is used before grouping.
  - Order of SQL keywords:
    - SELECT * FROM WHERE G-H-O-L;
    - G: GROUP BY
    - H: HAVING
    - O: ORDER BY (ASC and DESC)
    - L: LIMIT (has OFFSET)
  - Example: SELECT year, COUNT(year) AS year_count FROM movies WHERE rankscore > 9 GROUP BY year HAVING year_count > 20 ORDER BY year_count DESC LIMIT 10;

<br>

## JOINS
* Combines data from multiple tables.
* INNER JOIN:
  - Matches the rows in both tables.
  - SELECT A.ID, A.name, B.course
    FROM TableA A
    INNER JOIN TableB B
    ON A.ID = B.ID;
      
* LEFT JOIN:
  - Returns all rows from the left table and matching rows from the right table.
  - SELECT A.ID, A.name, B.course
    FROM TableA A
    LEFT JOIN TableB B
    ON A.ID = B.ID;
      
* RIGHT JOIN:
  - Returns all rows from the right table and matching rows from the left table.
  - SELECT A.ID, A.name, B.course
    FROM TableA A
    RIGHT JOIN TableB B
    ON A.ID = B.ID;

* FULL OUTER JOIN:
  - Returns all rows when there is a match in either table.
  - SELECT A.ID, A.name, B.course
    FROM TableA A
    FULL OUTER JOIN TableB B
    ON A.ID = B.ID;

* NATURAL JOIN:
  - Joins tables using all columns with the same name.
  - SELECT *
    FROM TableA
    NATURAL JOIN TableB;

<br>

## Sub Queries 
* Nested Queries or Inner Queries
* Queries within queries.
* First, the inner query is executed and then the outer query is executed.
* Example: SELECT actor_id FROM roles WHERE movie_id IN (SELECT id FROM movies WHERE name = 'Schindler''s List');
* Comparison operators: IN, NOT IN, EXISTS, NOT EXISTS, ANY, ALL.
* ANY operator returns TRUE if any of the subquery values meet the condition.
* ALL operator returns TRUE if all of the subquery values meet the condition.
* Example: SELECT * FROM movies WHERE rankscore>= ALL (SELECT MAX(rankscore) FROM movies);

<br>

## CRUD Operations:
* CREATE, READ, UPDATE, DELETE (CRUD).
* CREATE:
  - To create tables.
  - CREATE TABLE students
    (id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    grade CHAR(1));
* INSERT:
  - To add rows to a table
  - INSERT INTO students (id, name, age, grade)
    VALUES (1, 'John Doe', 20, 'A'),
    (2, 'Jane Smith', 22, 'B');
* READ: query data using SELECT.
* UPDATE:
  - To modify existing rows
  - UPDATE students
    SET grade = 'A+'
    WHERE id = 2;
* DELETE:
  - To remove rows
  - DELETE FROM students WHERE id = 1;

<br>

* ALTER:
  - To modify table structure
  - ADD a new column:
    - ALTER TABLE students ADD email VARCHAR(100);
  - Rename a column:
    - ALTER TABLE students RENAME COLUMN grade TO final_grade;
* DROP:
  - Deletes the table and its data permanently
  - DROP TABLE students;
* TRUNCATE:
  - Deletes all data but keeps the table structure.
  - TRUNCATE TABLE students;





    




  





























      
 



























