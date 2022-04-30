
Copyright (C) 2022 Penan Rajput <chetanrajput2777c@gmail.com>


# SQL Cheatsheet
1. Initial Queries
    1. Users functions

        1. List all users: 
            ```
            SELECT User,Host FROM mysql.user;
            ```

        2. Create new user: 
            ```
            CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
            ```


        3. Grant `ALL` access to user for `*` tables: 
            ```
            GRANT ALL ON database.* TO 'user'@'localhost';
            ```

    2. Schema + Data Queries

        1. Show Schema
            ```
            Describe {table_name};
            ```
            
        2. Create new_table similar like old_table
            ```
            CREATE TABLE dup_countries LIKE countries;
            ```
            
        3. Cloning Table
            ```
            CREATE TABLE new_table LIKE original_table;

            INSERT INTO new_table SELECT * FROM original_table;
            ```
            ```
            CREATE TABLE employees_dummy
            SELECT * 
            FROM employees;
            ```
                
    3. Database Queries
        1. show all database
            ```
            show databases;
            ```
        2. create database
            ```
            create database {db_name};
        3. use database
            ```
            use {db_name}
            ```
        4. Deleting databases: 
            ```
            DROP DATABASE [database]; 
    
            ```
1. DDL
    1. Create
        1. syntax
            ```
            create table {table_name}(
            {column_name_1} datatype_1 costraint_1,
            {column_name_2} datatype_2 costraint_2,
            {column_name_3} datatype_3 costraint_3
            );
            ```
        2. create table example-1
            ```
            CREATE TABLE PRODUCTS(
                NAME VARCHAR(20),
                PRICE int(6), 
                QTY int(6), 
                DISCOUNT float(6,4), 
                SELLER VARCHAR(20), 
                RATING INT(1)
                );
            ```
        3. copy from existing table 
            ```
            CREATE TABLE products_3  SELECT DISTINCT * FROM products_2;
            ```
        4. CREATE INDEX generates an index for a table. Indexes are used to retrieve data from a database faster.
            CREATE INDEX idx_name
            ON customers (name);
        
        5. CREATE VIEW creates a virtual table based on the result set of an SQL statement. A view is like a regular table (and can be queried like one), but it is not saved as a permanent table in the database.

            CREATE VIEW [Bob Customers] AS
            SELECT name, age
            FROM customers
            WHERE name = ‘Bob’;

        
    2. Drop
        1. drop existing
            ```
            DROP TABLE {table_name};
            ```
        2. drop if exists
            ```
            DROP TABLE {table_name} if exists;
            ```
        3. Drop database
            DROP DATABASE dataquestDB;
        4. DROP INDEX
            DROP INDEX idx_name;
        
    3. Alter
        1. ADD COLUMN
            ```
            ALTER TABLE PRODUCTS 
            ADD productID INT(8);
            ```    
        1. Adding a column with an unique, auto-incrementing ID
            ```
            ALTER TABLE [table] ADD COLUMN [column] int NOT NULL AUTO_INCREMENT PRIMARY KEY;
            ```
        2. change datatype length
            ```
            ALTER TABLE products_2 
            MODIFY COLUMN productID int(8);

            ```
        3. delete 1 column 
            ```
            ALTER TABLE products
            DROP COLUMN product_id;
            ```
        4. drop two or more columns
            ```
            ALTER TABLE table
            DROP COLUMN column_1,
            DROP COLUMN column_2;
            ```
        5. update column value - way 1
            ```
            ALTER TABLE PRODUCTS 
            ALTER COLUMN RATING INT(2);
            ```
        6. update column value - way 2
            ```
            ALTER TABLE PRODUCTS 
            MODIFY COLUMN SELLER VARCHAR(60);
            ```
        7. Rearrangin the records: 
            ```
            ALTER TABLE foo
            CHANGE COLUMN bar
            bar COLUMN_DEFINITION_HERE
            FIRST;
            ......... AFTER OTHER_COLUMN;
        
            
            /*
            ALTER TABLE products
            CHANGE COLUMN productID 
            productID int(8)
            FIRST;
            */
            ``` 
        8. Removing table columns: 
            ```
            ALTER TABLE [table] DROP COLUMN [column];
            ```
    4. Alter + permanent way
        1. How to sort a MYSQL table in a permanent way?
            ```
            ALTER TABLE tablename ORDER BY columnname ASC;
            ```

        2. How to rename a SQL Column in permanent way ?
            ```
            ALTER TABLE column_name CHANGE oldname newname datatype(size);

            ALTER TABLE customers CHANGE CUST_ID ID int(4);
            ```


    4. truncate = Delete all records in a table: 
        1. syntax
            ```
            truncate table {table_name};    
            ```
2. DML
    1. insert
        1. insert 1 rows
            ```
            INSERT INTO PRODUCTS VALUES("PENAN0",20);
            ```
        2. insert 2+ rows
            ```
            insert into products values
            ("BOOKS",20000,300,20,"EBAY",4.7,16,'2018-12-22'), 
            ("CARDS",2000,34,25.5,"AMAZON INC INTERNATIONAL",5,17,'2018-12-23'), 
            ("TV SETS",770000,200,20,"AMAZON INC. INDIA",4.5,18,'2018-5-2');
            ```
        3. insert in selected columns 1 row
            ```
            insert into products (NAME, PRICE,SELLER, RATING) 
            values ("MOUSE",150,"AMAZON INDIA",5);
            ```

        4. insert in selected columns 2+ row
            ```
            insert into products (NAME,RATING, PRICE,SELLER) 
            values ("SCREEN",3.5,1150,"FLIPKART"), 
            ("BEDSHEETS",4.1,75,"FLIPKART");;
            ```
    2. update
        1. syntax
            ```
            UPDATE tableName 
            SET [columnName = new_value]
            [WHERE condition]
            ```
        2. example 1
            ```
            update products 
            set SELLER="AMAZON" 
            where NAME = "LAPTOP";

            ```
    3. delete
        1. syntax
            ```
            DELETE FROM [table] 
            WHERE [column] = [value];
            ```
 
        1. delete + where
            ```
            DELETE FROM CUSTOMERS
            WHERE CUST_ID=2;
            ```
        2. delete + in 
            ```
            DELETE FROM products_2 
            where qty in (300,200);
                ```
        3. Delete *all records* from a table (without dropping the table itself):  
            ```
            DELETE FROM [table];
            ```

            (This also resets the incrementing counter for auto generated columns like an id column.)


4. DQL
    1. select
        1. Selecting specific records: 
            ```
            SELECT * FROM [table] WHERE [column] = [value];` 
            ```
        2. Basic Math Operations
            ```
            select 25 % 6 AS "MOD ";
            select 25 * 6 AS "MULTIPLICATION";
            select 25 + 6 AS "ADDITION";
            select 25 / 6 AS "DIVISION";
            select 25 - 6 AS "SUBSTRACTION";
            select 25-6, 25*6;
            ```
        3. To generate random integer numbers
            ```
            select round(rand()*100) 
            as "RANDOM RESULT";
            ```
        4. generate concat rows
            ```
            select concat(name,' is of price ',price,' in qty => ',qty,' with discount ',discount,' is brought from ',seller) 
            AS 'DESCRIPTION' 
            from products;
            ```
        5. only left characters to be shown
            ```
            select LEFT(MANUFACTURE_DATE,4) 
            AS "MANUFACTURING DATE" 
            from products;
            ```
        6. example 2
            ```
            select NAME, LEFT(MANUFACTURE_DATE,4) 
            AS "MANUFACTURING DATE",
            SELLER,QTY 
            from products;
            ```

        7. right characters to be shown
            ```
            select NAME, 
            RIGHT(NAME,4) AS "NAME(LAST 4)",
            SELLER,
            QTY 
            from products;
            ```

        8.  Custom column output names: 
            ```
            SELECT [column] AS [custom-column] FROM [table];
            ```
        9. select *
            ```
            SELECT * 
            FROM customers;
            ```
        10. select distince (=without duplicates)
            ```
            SELECT DISTINCT name 
            FROM customers;
            ```
            ```
            SELECT distinct name, email, acception FROM owners WHERE acception = 1 AND date >= 2015-01-01 00:00:00
            ```
        11. SELECT INTO copies the specified data from one table into another.
            SELECT * INTO customers
            FROM customers_backup;

        12. SELECT TOP only returns the top x number or percent from a table.
            SELECT TOP 50 * FROM customers;

          
        13. AS Rename column or table using an _alias_: 
            ```
            SELECT [table1].[column] AS '[value]', [table2].[column] AS '[value]' FROM [table1], [table2];
            ```
        14. WHERE
            (Selectors: `<`, `>`, `!=`; combine multiple selectors with `AND`, `OR`)
        
        15. AND
            SELECT name
            FROM customers
            WHERE name = ‘Bob’ AND age = 55;

            ```
            select * from products where QTY > 400 and RATING > 4;
            ```

        16. OR
            SELECT name
            FROM customers
            WHERE name = ‘Bob’ OR age = 55;

            ```
            select * from products where QTY < 400 or RATING > 4;
            ```


        17. BETWEEN
            SELECT name
            FROM customers
            WHERE age BETWEEN 45 AND 55;


    2. Explain records: 
        ```
        EXPLAIN SELECT * FROM [table];
        ```
5. Date
    1. where + date
        ```
        select * from products 
        where MANUFACTURE_DATE < '2014-01-01';
        ```

6. Time 
    1. MySQL function for datetime input: 
        ```
        NOW()
        ```

7. Commands 

    1. in, not in
        1. in
            ```
            select * from products where rating in (3,5); 
            ```
        4. not in 
            ```
            select * from products where rating not in (3,5);
            ```
    2. IS NULL will return only rows with a NULL value.
            SELECT name
            FROM customers
            WHERE name IS NULL;
    3. IS NOT NULL
            SELECT name
            FROM customers
            WHERE name IS NOT NULL;

    2. LIKE 
        %x — will select all values that begin with x
        %x% — will select all values that include x
        x% — will select all values that end with x
        x%y — will select all values that begin with x and end with y
        _x% — will select all values have x as the second character
        x_% — will select all values that begin with x and are at least two characters long. You can add additional _ characters to extend the length requirement, i.e. x___%

        1. Select records containing `[value]`: 
            ```
            SELECT * FROM [table] WHERE [column] LIKE '%[value]%';
            ```
        

        2. Select records starting with `[value]`: 
            ```
            SELECT * FROM [table] WHERE [column] LIKE '[value]%';
            ```

        3. Select records starting with `val` and ending with `ue`: 
            ```
            SELECT * FROM [table] WHERE [column] LIKE '[val_ue]';
            ```    
            ```
    4. ORDER BY
        1. Select with custom order and only limit: 
            ```
            SELECT * FROM [table] WHERE [column] ORDER BY [column] ASC LIMIT [value];` (Order: `DESC`, `ASC`)
            ```
    
7. Aggregate functions (count, min, max, sum, avg)

    2. SUM Calculate total number of records: 
        ```
        SELECT SUM([column]) FROM [table];
        ```

    3. SUM Count total number of `[column]` and group by 
        ```
        [category-column]`: `SELECT [category-column], SUM([column]) FROM [table] GROUP BY [category-column];
        ```

    4. MAX Get largest value in `[column]`: 
        ```
        SELECT MAX([column]) FROM [table];
        ```


    5. MIN Get smallest value: 
        ```
        SELECT MIN([column]) FROM [table];
        ```

    6. AVG Get average value: 
        ```
        SELECT AVG([column]) FROM [table];
        ```

    7. ROUND(AVG) Get rounded average value and group by 
        ```
        `SELECT [category-column], ROUND(AVG([column]), 2) FROM [table] GROUP BY [category-column];
        ```
    
    8. COUNT() Counting records: 
        ```
        SELECT COUNT([column]) FROM [table];
        ```

    9. COUNT(*) using *, so the total row count for customers would be returned.
        SELECT COUNT(*)
        FROM customers;

    9. COUNT Counting and selecting grouped records: 
        ```
        SELECT *, (SELECT COUNT([column]) FROM [table]) AS count FROM [table] GROUP BY [column];
        ```
8. GROUP BY groups rows with the same values into summary rows  + aggregate function
    SELECT name, AVG(age)
    FROM customers
    GROUP BY name;

9. HAVING performs the same action as the WHERE clause. The difference is that HAVING is used for aggregate functions, whereas WHERE doesn’t work with them.
    SELECT COUNT(customer_id), name
    FROM customers
    GROUP BY name
    HAVING COUNT(customer_id) > 2;

10. ORDER BY
    1. ORDER BY sets the order of the returned results. The order will be ascending by default.

    SELECT name
    FROM customers
    ORDER BY age;
    2. DESC
    DESC will return the results in descending order.

    SELECT name
    FROM customers
    ORDER BY age DESC;

8. JOINs = Multiple tables (Types = INNER, LEFT, RIGHT, FULL)

    1. Select from multiple tables: 
        ```
        SELECT [table1].[column], [table1].[another-column], [table2].[column] FROM [table1], [table2]; 
        ```


    2. Combine rows from different tables: 
        ```
        SELECT * FROM [table1] INNER JOIN [table2] ON [table1].[column] = [table2].[column];
        ```

    3. Combine rows from different tables but do not require the join condition: 
        ```
        SELECT * FROM [table1] LEFT OUTER JOIN [table2] ON [table1].[column] = [table2].[column];
        ```
        (The left table is the first table that appears in the statement.)
    


        4. INNER JOIN
            INNER JOIN selects records that have matching values in both tables.

            SELECT name
            FROM customers
            INNER JOIN orders
            ON customers.customer_id = orders.customer_id;

        5. LEFT JOIN
            LEFT JOIN selects records from the left table that match records in the right table. In the below example the left table is customers.

            SELECT name
            FROM customers
            LEFT JOIN orders
            ON customers.customer_id = orders.customer_id;
        6. RIGHT JOIN
            RIGHT JOIN selects records from the right table that match records in the left table. In the below example the right table is orders.

            SELECT name
            FROM customers
            RIGHT JOIN orders
            ON customers.customer_id = orders.customer_id;

        7. FULL JOIN
            FULL JOIN selects records that have a match in the left or right table. Think of it as the “OR” JOIN compared with the “AND” JOIN (INNER JOIN).

            SELECT name
            FROM customers
            FULL OUTER JOIN orders
        ON customers.customer_id = orders.customer_id;

        8. EXISTS
            EXISTS is used to test for the existence of any record in a subquery.

            SELECT name
            FROM customers
            WHERE EXISTS
            (SELECT order FROM ORDERS WHERE customer_id = 1);












11. Others 
    20. Export a database dump (more info [here](http://stackoverflow.com/a/21091197/1815847)): 
        ```
        mysqldump -u [username] -p [database] > db_backup.sql
        ```

    21. Use `--lock-tables=false` option for locked tables (more info [here](http://stackoverflow.com/a/104628/1815847)).

    22. Import a database dump (more info [here](http://stackoverflow.com/a/21091197/1815847)): 
        ```
        mysql -u [username] -p -h localhost [database] < db_backup.sql
        ```

    23. Logout: 
        ```
        exit;
        ```
