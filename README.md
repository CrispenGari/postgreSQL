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
