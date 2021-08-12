## PostgreSQL Database.

This repository document a quick and fast journey of learning PostgreSQL database, that is if you are familiar with SQL commands.

### PostgreSQL Commands.

For help go and type the following command.

```
postgres=# help
```

1. Clearing the console

```
\! cls
```

2. Starting a Server

```
psql -U <user> # default is postgres
```

3. Selecting the database.

```
\c <database_name>
```

### Creating a database.

To create a database run the following command:

```sql
CREATE DATABASE <database_name>;
```

### Executing commands from a file.

To execute commands from a file on the terminal

1. Run the following command

```
\i <file_name>
<!-- Example -->
\i createdatabase.sql
```

- Note that if there are a lot of commands in the SQL file they will be executed sequentially meaning one after the other in order.

### Creating table

- We want to create a table users that will store information of users.
- All the SQL commands will be also found in the `01_Day1` folder.

```sql
CREATE TABLE users(
    id BIGSERIAL NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    email VARCHAR(150),
    password VARCHAR(100) NOT NULL,
    date_of_birth DATE NOT NULL,
    gender VARCHAR(20) NOT NULL,
    country_code VARCHAR(10) NOT NULL,
    country VARCHAR(100) NOT NULL,
    PRIMARY KEY(id)
)
```

### Inserting data into a table.

- Again we are going to generate some fake data using the [mockaroo](https://www.mockaroo.com/)
- We are going to download the sql file so that we will execute it from the Command line using the command

```
\i users.sql
```

### Describing a table

To describe (DESC) a table we run the following command:

```
\d <table name>
```

### Describing a database

To describe (DESC) a database we run the following command:

```
\d <database name>
```

1. SELECT

```sql
SELECT <columns> FROM <table_name>;
```

2. Column Aliases

```sql
SELECT first_name, last_name as surname FROM <table_name>

-- OR

SELECT first_name || ' ' || last_name AS full_name from <table_name>
```

- The second command is `Assigning a column alias to an expression example`. [docs](postgresqltutorial.com/postgresql-column-alias/)

3. ORDER BY
   Orders the results in either ascending or descending order.

```sql
SELECT * FROM <table_name> ORDER BY <column_name> [ASC | DESC] [NULLS FIRST | NULLS LAST];
```

4. DISTINCT
   Removes duplicate rows from a result set returned by a query.

```sql
SELECT
   DISTINCT column1
FROM
   table_name;

-- You can also specify multiple columns for example
SELECT
   DISTINCT ON (column1) column_alias,
   column2
FROM
   table_name
```

5. WHERE
   Filters rows that satisy a given condition.

```sql
SELECT select_list
FROM table_name
WHERE condition;
```

- For operators click [here](https://www.postgresqltutorial.com/postgresql-where/)

6. LIKE and ILIKE
   LIKE and ILIKE operators to query data using pattern matchings. The difference between the two is that the `LIKE` matches cases and the `ILIKE` ignores the case.

World cards:

- Percent sign `( %)` matches any sequence of zero or more characters.
- Underscore sign `(_)` matches any single character.

```sql
SELECT
	'foo' LIKE 'foo', -- true
	'foo' LIKE 'f%', -- true
	'foo' LIKE '_o_', -- true
	'bar' LIKE 'b_'; -- false
```

```sql
SELECT
	'foo' ILIKE 'Foo', -- true
	'foo' ILIKE 'F%', -- true
	'foo' ILIKE '_o_', -- true
	'bar' ILIKE 'b_'; -- false
```

- `~~` -> LIKE
- `~~*` -> ILIKE
- `!~~` -> NOT LIKE
- `!~~*` -> NOT iLIKE

7. LIMIT

- LIMIT is an optional clause of the SELECT statement that constrains the number of rows returned by the query.

```sql
SELECT * FROM <table_name> WHERE <condition> LIMIT = <row_count>;
```

8. FETCH

```sql
OFFSET start { ROW | ROWS }
FETCH { FIRST | NEXT } [ row_count ] { ROW | ROWS } ONLY
Code language: SQL (Structured Query Language) (sql)
-- Examples

SELECT
    film_id,
    title
FROM
    film
ORDER BY
    title
FETCH FIRST 1 ROW ONLY;

--
SELECT
    film_id,
    title
FROM
    film
ORDER BY
    title
FETCH FIRST 5 ROW ONLY;
--
SELECT
    film_id,
    title
FROM
    film
ORDER BY
    title
FETCH FIRST ROW ONLY;

--
SELECT
    film_id,
    title
FROM
    film
ORDER BY
    title
OFFSET 5 ROWS
FETCH FIRST 5 ROW ONLY;

-- PRACTICAL EXAMPLE
SELECT email, first_name from users ORDER BY email DESC OFFSET 5 ROWS FETCH FIRST 5 ROW ONLY;
```

9. IN and NOT IN
   This operator in the WHERE clause to check if a value matches any value in a list.

```SQL
SELECT * FROM <table_name> WHERE
<column_name> IN (value_1, value_2, ...);

-- Example
 SELECT first_name, country FROM users WHERE country IN ('Zimbabwe', 'China', 'South Africa') ORDER BY country DESC;
```

10. BETWEEN and NOT BETWEEN
    This operator to match a value against a range of values.

```sql
SELECT
	customer_id,
	payment_id,
	amount
FROM
	payment
WHERE
	amount BETWEEN 8 AND 9;
```

11. IS NULL and IS NOT NULL

```SQL
SELECT * FROM USERS WHERE email IS NULL;
```

12. HAVING

```SQL
SELECT
	customer_id,
	SUM (amount)
FROM
	payment
GROUP BY
	customer_id
HAVING
	SUM (amount) > 200;
```

13. SQL Joins

![img](https://www.postgresqltutorial.com/wp-content/uploads/2018/12/PostgreSQL-Joins-768x465.png)

- We are going to create sample tables and insert the data ito it. SQL commands will be found `02_Day_2/tables.sql` to execute it we run the following command:

```
\i 02_Day_2/tables.sql
```

`table a`:

```
- Apple
- Orange
- Banana
- Cucumber
```

`table b`:

```
- Orange
- Apple
- Watermelon
- Pear
```

a. INNER JOIN

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
INNER JOIN basket_b
    ON fruit_a = fruit_b;
```

![img](https://www.postgresqltutorial.com/wp-content/uploads/2018/12/PostgreSQL-Join-Inner-Join.png)

b. LEFT JOIN

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
LEFT JOIN basket_b
    ON fruit_a = fruit_b;
```

![img](https://www.postgresqltutorial.com/wp-content/uploads/2018/12/PostgreSQL-Join-Left-Join.png)

c. LEFT OUTER JOIN

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
LEFT OUTER JOIN basket_b
     ON fruit_a = fruit_b
WHERE b IS NULL
```

d. RIGHT JOIN
This is the opposite of the LEFT JOIN.
![img](https://www.postgresqltutorial.com/wp-content/uploads/2018/12/PostgreSQL-Join-Right-Join.png)
e. RIGHT OUTER JOIN
This is the opposite of the LEFT JOIN.
![img](https://www.postgresqltutorial.com/wp-content/uploads/2018/12/PostgreSQL-Join-Right-Join-with-Where.png)
f. FULL OUTER JOIN

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
FULL OUTER JOIN basket_b
    ON fruit_a = fruit_b;
```

![img](https://www.postgresqltutorial.com/wp-content/uploads/2018/12/PostgreSQL-Join-Full-Outer-Join.png)

g. FULL OUTER JOIN

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
FULL JOIN basket_b
   ON fruit_a = fruit_b
WHERE a IS NULL OR b IS NULL;
```

![img](https://www.postgresqltutorial.com/wp-content/uploads/2018/12/PostgreSQL-Join-Full-Outer-Join-with-Where.png)

14. Table Aliases

```sql
SELECT
    e.first_name employee,
    m .first_name manager
FROM
    employee e
INNER JOIN employee m
    ON m.employee_id = e.manager_id
ORDER BY manager;
```

### References

- [postgresqltutorial](https://www.postgresqltutorial.com)
