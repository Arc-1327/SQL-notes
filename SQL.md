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
 


















      
 



























