
Copyright (C) 2022 Penan Rajput 

<chetanrajput2777c@gmail.com>


# SQL Cheatsheet
## SINGLE TABLE QUERIES
1. Initial Queries (User, Schema, DB)
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
2. Datatype
    1. NUMERIC
        1. INT: Whole numbers
        2. Float(m, d) : decimal numbers (approx)
        3. decimal(m, d) : decimal numbers (precise)
    2. NON-NUMERIC
        1. CHAR(N) : Fixed length character
        2. VARCHAR(N) : Varying length character
        3. ENUM('M','F') : Value from a defined list
        4. BOOLEAN : True of False values
    3. DATA AND TIME TYPES
        1. DATE : Date (YYYY-MM-DD)
        2. DATETIME : Date and the time (YYYY-MM-DD HH-MM-SS)
        3. TIME : Time (HHH-MM-SS)
        4. YEAR : Year (YYYY)
 

2. DDL (create, alter, drop, truncate)
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
            ```
            CREATE INDEX idx_name
            ON customers (name);
            ```
        
        5. CREATE VIEW creates a virtual table based on the result set of an SQL statement. A view is like a regular table (and can be queried like one), but it is not saved as a permanent table in the database.
            ```
            CREATE VIEW [Bob Customers] AS
            SELECT name, age
            FROM customers
            WHERE name = ‘Bob’;
            ```

        
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
            ALTER TABLE [table] 
            ADD COLUMN [column] int NOT NULL AUTO_INCREMENT PRIMARY KEY;
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
        9. COLUMN NAME CHANGE
            ```
            ```
    4. Alter + permanent way
        1. How to sort a MYSQL table in a permanent way?
            1. Syntax
                ```
                ALTER TABLE tablename ORDER BY columnname ASC;
                ```
            2. Ex-1

        2. How to rename a SQL Column in permanent way ?
            1. Syntax
                ```
                ALTER TABLE {column_name} 
                CHANGE {oldname} {newname} {datatype(size)};
                ```
            1. Ex-1 
                ```
                ALTER TABLE customers 
                CHANGE CUST_ID ID int(4);
                ```
        3.  Change datatype DATA TYPE
            1. Syntax
                ```
                ALTER TABLE {table_name} 
                MODIFY COLUMN {column_name} {new_datatype(new_size)};
                ```
                
            2. Ex 1
                ```
                ALTER TABLE products_2 
                MODIFY COLUMN productID int(8);
                ```
            


    4. truncate = Delete all records in a table: 
        1. syntax
            ```
            TRUNCATE table {table_name};    
            ```
2. DML (insert, update, delete)
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


4. DQL (select)

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
            ```
            SELECT * INTO customers
            FROM customers_backup;
            ```

        12. SELECT TOP only returns the top x number or percent from a table.
            ```
            SELECT TOP 50 * FROM customers;
            ```

          
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
    ```
    select * from products 
    where MANUFACTURE_DATE < '2014-01-01';
    ```

6. Time 
    1. Current Time: 
        ```
        SELECT NOW()
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
        ```
        SELECT name
        FROM customers
        WHERE name IS NULL;
        ```
    3. IS NOT NULL
        ```
        SELECT name
        FROM customers
        WHERE name IS NOT NULL;
        ```
    2. LIKE 
        ```
        %x — will select all values that begin with x
        %x% — will select all values that include x
        x% — will select all values that end with x
        x%y — will select all values that begin with x and end with y
        _x% — will select all values have x as the second character
        x_% — will select all values that begin with x and are at least two characters long. You can add additional _ characters to extend the length requirement, i.e. x___%
        ```

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
        ```
        SELECT name, AVG(age)
        FROM customers
        GROUP BY name;
        ```

    9. HAVING is used with group by only \
    HAVING checks condition. \
    select -> where,  \
    group by -> order by
        ```
        SELECT COUNT(customer_id), name
        FROM customers
        GROUP BY name
        HAVING COUNT(customer_id) > 2;
        ```

    10. ORDER BY
        1. ORDER BY sets the order of the returned results. The order will be ascending by default.
            ```
            SELECT name
            FROM customers
            ORDER BY age;
            ```
        2. DESC
        DESC will return the results in descending order.
            ```
            SELECT name
            FROM customers
            ORDER BY age DESC;
            ```

## MULTIPLE TABLE QUERIES

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
        ```
        SELECT name
        FROM customers
        INNER JOIN orders
        ON customers.customer_id = orders.customer_id;
        ```

    5. LEFT JOIN
        LEFT JOIN selects records from the left table that match records in the right table. In the below example the left table is customers.
        ```
        SELECT name
        FROM customers
        LEFT JOIN orders
        ON customers.customer_id = orders.customer_id;
        ```
    6. RIGHT JOIN
        RIGHT JOIN selects records from the right table that match records in the left table. In the below example the right table is orders.
        ```
        SELECT name
        FROM customers
        RIGHT JOIN orders
        ON customers.customer_id = orders.customer_id;
        ```

    7. FULL JOIN
        FULL JOIN selects records that have a match in the left or right table. Think of it as the “OR” JOIN compared with the “AND” JOIN (INNER JOIN).
        ```
        SELECT name
        FROM customers
        FULL OUTER JOIN orders
        ON customers.customer_id = orders.customer_id;
        ```

    8. EXISTS
        EXISTS is used to test for the existence of any record in a subquery.
        ```
        SELECT name
        FROM customers
        WHERE EXISTS
        (SELECT order FROM ORDERS WHERE customer_id = 1);
        ```


10. CONSTRAINTS & KEYS

    show all constraints
    ```
        select * from information_schema.table_constraints
        where constraint_schema = 'db_name';
    ```
    ```
    Constraints are commonly used in SQL are :

    1. NOT NULL - Ensures that a column cannot have a NULL value

    2. UNIQUE - Ensures that all values in a column are different

    3. PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table (UNIQUE + NOT NULL)

    4. FOREIGN KEY - Prevents actions that would destroy links between tables

    5. CHECK - Ensures that the values in a column satisfies a specific condition

    6. DEFAULT - Sets a default value for a column if no value is specified

    7. CREATE INDEX - Used to create and retrieve data from the database very quickly
    ```
    1. NOT NULL
        1. on CREATE TABLE
            ```
            CREATE TABLE Persons (
            ID int NOT NULL,
            LastName varchar(255) NOT NULL,
            FirstName varchar(255) NOT NULL,
            Age int
            );
            ```
        2. on ALTER TABLE
            ```
            ALTER TABLE Persons
            MODIFY Age int NOT NULL;
            ```
    2. UNIQUE
        1. on CREATE TABLE
            ```
            CREATE TABLE Persons (
            ID int NOT NULL UNIQUE,
            LastName varchar(255) NOT NULL,
            FirstName varchar(255),
            Age int
            );
            ```

            ```
            CREATE TABLE Persons (
            ID int NOT NULL,
            LastName varchar(255) NOT NULL,
            FirstName varchar(255),
            Age int,
            UNIQUE (ID)
            );
            ```

            ```
            CREATE TABLE Persons (
            ID int NOT NULL,
            LastName varchar(255) NOT NULL,
            FirstName varchar(255),
            Age int,
            CONSTRAINT UC_Person UNIQUE (ID,LastName)
            );
            ```
        2. on ALTER TABLE
            1. without constraint_name

                ```
                ALTER TABLE Persons
                ADD UNIQUE ({column_name});
                ```
            2. EX-1
                
                ```
                ALTER TABLE Persons
                ADD UNIQUE (ID);
                ```

            3. with constraint_name

                ```
                ALTER TABLE Persons
                ADD CONSTRAINT {constraint_name} 
                UNIQUE (column_name1, column_name2);
                ```
            4. EX-2
                 ```
                ALTER TABLE Persons
                ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);
                ```
        3. DROP a UNIQUE Constraint
            1. by INDEX 

                ```
                ALTER TABLE Persons
                DROP INDEX UC_Person;
                ```

           2. by CONSTRAINT

                ```
                ALTER TABLE Persons
                DROP CONSTRAINT UC_Person;
                ```
            
    1. PRIMARY KEYS
        1. IMPLICITELY on create table
            ```
            CREATE TABLE Persons (
            ID int NOT NULL,
            LastName varchar(255) NOT NULL,
            FirstName varchar(255),
            Age int,
            PRIMARY KEY (ID)
            );
            ```

            ```
            CREATE TABLE Persons (
            ID int NOT NULL PRIMARY KEY,
            LastName varchar(255) NOT NULL,
            FirstName varchar(255),
            Age int
            );
            ```

            ```
            CREATE TABLE Persons (
            ID int NOT NULL,
            LastName varchar(255) NOT NULL,
            FirstName varchar(255),
            Age int,
            CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)
            );
            ```
        2. EXPLICITELY on alter table
            ```
            ALTER TABLE Persons
            ADD PRIMARY KEY (ID);
            ```

            ```
            ALTER TABLE Persons
            ADD CONSTRAINT PK_Person PRIMARY KEY (ID,LastName);
            ```
        3.  DROP a PRIMARY KEY Constraint
            ```
            ALTER TABLE Persons
            DROP PRIMARY KEY;
            ```

            ```
            ALTER TABLE Persons
            DROP CONSTRAINT PK_Person;
            ```

    4. FOREIGN KEY
        1. on CREATE TABLE
            ```
            CREATE TABLE Orders (
                OrderID int NOT NULL,
                OrderNumber int NOT NULL,
                PersonID int,
                PRIMARY KEY (OrderID),
                FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
            );
            ```

             ```
            CREATE TABLE Orders (
            OrderID int NOT NULL PRIMARY KEY,
            OrderNumber int NOT NULL,
            PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
            );
            ```

            ```
            CREATE TABLE Orders (
            OrderID int NOT NULL,
            OrderNumber int NOT NULL,
            PersonID int,
            PRIMARY KEY (OrderID),
            CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
            REFERENCES Persons(PersonID)
            );
             ```

        2. on ALTER TABLE
            1. without constraint_name
                ```
                ALTER TABLE Orders
                ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
                ```
            2. with costraint_name
                ```
                ALTER TABLE Orders
                ADD CONSTRAINT {constraint_name}
                FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
                ```
            3. Ex - 1
                ```
                ALTER TABLE Orders
                ADD CONSTRAINT FK_PersonOrder
                FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
                ```

        3. DROP a FOREIGN KEY Constraint
            1. by FOREIGN KEY {constraint_name}
                ```
                ALTER TABLE Orders
                DROP FOREIGN KEY {constraint_name};
                ```
            2. Ex 1
                  ```
                ALTER TABLE Orders
                DROP FOREIGN KEY FK_PersonOrder;
                ```

            2. by CONSTRAINT {constraint_name}
                 ```
                ALTER TABLE Orders
                DROP CONSTRAINT {constraint_name};
                ```
            4. Ex 1
                ```
                ALTER TABLE Orders
                DROP CONSTRAINT FK_PersonOrder;
                ```


    5. CHECK
        1. on CREATE TABLE
            ```
            CREATE TABLE Persons (
                ID int NOT NULL,
                LastName varchar(255) NOT NULL,
                FirstName varchar(255),
                Age int,
                CHECK (Age>=18)
            );
            ```

            ```
            CREATE TABLE Persons (
                ID int NOT NULL,
                LastName varchar(255) NOT NULL,
                FirstName varchar(255),
                Age int CHECK (Age>=18)
            );
            ```


            ```
            CREATE TABLE Persons (
                ID int NOT NULL,
                LastName varchar(255) NOT NULL,
                FirstName varchar(255),
                Age int,
                City varchar(255),
                CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
            );
            ```
        2. on ALTER TABLE
            ```
            ALTER TABLE Persons
            ADD CHECK (Age>=18);
            ```

            ```
            ALTER TABLE Persons
            ADD CONSTRAINT CHK_PersonAge CHECK (Age>=18 AND City='Sandnes');
            ```
        3. DROP a CHECK Constraint
            ```
            ALTER TABLE Persons
            DROP CONSTRAINT CHK_PersonAge;
            ```
        
            ```
            ALTER TABLE Persons
            DROP CHECK CHK_PersonAge;
            ```
    6. DEFAULT
        1. on CREATE TABLE
            ```
            CREATE TABLE Persons (
                ID int NOT NULL,
                LastName varchar(255) NOT NULL,
                FirstName varchar(255),
                Age int,
                City varchar(255) DEFAULT 'Sandnes'
            );
            ```

            ```
            CREATE TABLE Orders (
                ID int NOT NULL,
                OrderNumber int NOT NULL,
                OrderDate date DEFAULT GETDATE()
            );
            ```
        2. on ALTER TABLE
            ```
            ALTER TABLE Persons
            ALTER City SET DEFAULT 'Sandnes';
            ```
            ```
            ALTER TABLE Persons
            ADD CONSTRAINT df_City
            DEFAULT 'Sandnes' FOR City;
            ```
            ```
            ALTER TABLE Persons
            ALTER COLUMN City SET DEFAULT 'Sandnes';
            ```
            ```
            ALTER TABLE Persons
            MODIFY City DEFAULT 'Sandnes';
            ```
        3. DROP a DEFAULT Constraint
            ```
            ALTER TABLE Persons
            ALTER City DROP DEFAULT;
            ```
            ```
            ALTER TABLE Persons
            ALTER COLUMN City DROP DEFAULT;
            ```
            ```
            ALTER TABLE Persons
            ALTER COLUMN City DROP DEFAULT;
            ```
    7. INDEX = used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.
        1. CREATE INDEX Syntax = Creates an index on a table. Duplicate values are allowed:
            ```
            CREATE INDEX index_name
            ON table_name (column1, column2, ...);
            ```

        2. CREATE UNIQUE INDEX Syntax = Creates a unique index on a table. Duplicate values are not allowed:

            ```
            CREATE UNIQUE INDEX index_name
            ON table_name (column1, column2, ...);
            ```
        3. CREATE INDEX Example
            The SQL statement below creates an index named "idx_lastname" on the "LastName" column in the "Persons" table:

            ```
            CREATE INDEX idx_lastname
            ON Persons (LastName);
            ```

            If you want to create an index on a combination of columns, you can list the column names within the parentheses, separated by commas:

            ```
            CREATE INDEX idx_pname
            ON Persons (LastName, FirstName)
            ```
        4. DROP INDEX Statement

            ```
            DROP INDEX index_name ON table_name;
            ```


            ```
            DROP INDEX table_name.index_name;
            ```


            ```
            DROP INDEX index_name;
            ```


            ```
            ALTER TABLE table_name
            DROP INDEX index_name;
            ```
    8.  AUTO INCREMENT
        1. Syntax  
            ```
            CREATE TABLE Persons (
                Personid int NOT NULL AUTO_INCREMENT,
                LastName varchar(255) NOT NULL,
                FirstName varchar(255),
                Age int,
                PRIMARY KEY (Personid)
            );
            ```
        2. on ALTER TABLE
            ```
            ALTER TABLE Persons AUTO_INCREMENT=100;
            ```


10. Operators -> Set Operations
    1. UNION operator
        1. UNION = only distinct values
            1. Syntax
                ```
                SELECT column_name(s) FROM table1
                UNION
                SELECT column_name(s) FROM table2;
                ```
            2. Ex 1
                ```
                SELECT City FROM Customers
                UNION
                SELECT City FROM Suppliers
                ORDER BY City;
                ```
        2. UNION ALL = + allows duplicate values
            1. Syntax
                ```
                SELECT column_name(s) FROM table1
                UNION ALL
                SELECT column_name(s) FROM table2;
                ```
            2. Ex 1
                ```
                SELECT City FROM Customers
                UNION ALL
                SELECT City FROM Suppliers
                ORDER BY City;
                ```
        3. UNION + WHERE
            1. Ex 1
                ```
                SELECT City, Country FROM Customers
                WHERE Country='Germany'
                UNION
                SELECT City, Country FROM Suppliers
                WHERE Country='Germany'
                ORDER BY City;
                ```
        4. UNION ALL + WHERE
            1. Ex 1
                ```
                SELECT City, Country FROM Customers
                WHERE Country='Germany'
                UNION ALL
                SELECT City, Country FROM Suppliers
                WHERE Country='Germany'
                ORDER BY City;
                ```
    2. INTERSECT
        1. Syntax
            ```
            SELECT column1 [, column2 ]
            FROM table1 [, table2 ]
            [WHERE condition]

            INTERSECT

            SELECT column1 [, column2 ]
            FROM table1 [, table2 ]
            [WHERE condition]
            ```
        2. Ex 1
            ```
            SELECT  ID, NAME, AMOUNT, DATE
                FROM CUSTOMERS
                LEFT JOIN ORDERS
                ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID

            INTERSECT

            SELECT  ID, NAME, AMOUNT, DATE
                FROM CUSTOMERS
                RIGHT JOIN ORDERS
                ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
            ```

    3. MINUS



11. SUBQUERIES
    1. Single Row
        ```
        SELECT id, last_name, salary
        FROM employee
        WHERE salary = (
            SELECT MAX(salary)
            FROM employee
        );
        ```

    2. Multi Row 
        ```
        SELECT id, last_name, salary
        FROM employee
        WHERE salary IN (
            SELECT salary
            FROM employee
            WHERE last_name LIKE 'C%'
        );
        ```

12. Operators
    ```
    ALL	-> TRUE if all of the subquery values meet the condition	

    AND	-> TRUE if all the conditions separated by AND is TRUE	

    ANY	-> TRUE if any of the subquery values meet the condition	

    BETWEEN	-> TRUE if the operand is within the range of comparisons	

    EXISTS	-> TRUE if the subquery returns one or more records	

    IN -> TRUE if the operand is equal to one of a list of expressions	
    
    LIKE -> TRUE if the operand matches a pattern	

    NOT	-> Displays a record if the condition(s) is NOT TRUE	

    OR -> TRUE if any of the conditions separated by OR is TRUE	

    SOME -> TRUE if any of the subquery values meet the condition

    ```


13. VIEW [[GFG Link]](https://www.geeksforgeeks.org/sql-views/)
    1. Basics
        1. Create View - Syntax

            ```
            CREATE VIEW <VIEW_NAME> AS SELECT <COLUMN_NAME(S)> FROM <TABLE_NAME>;
            ```

        2. Create - EXAMPLE 1
            ```
            CREATE VIEW <view_name> AS 
            SELECT <Column_Names(S)> 
            FROM <Table_Name> 
            WHERE <Condition>;
            ```
        3. Drop View -  Syntax
            ```
            DROP VIEW <View_Name>;
            ```
        4. Drop View - Example
            ```
            DROP VIEW MarksView;
            ```
        5. Updating View - Syntax
        [[GFG Link]](https://www.geeksforgeeks.org/sql-views/#:~:text=DROP%20VIEW%20MarksView%3B-,UPDATING%20VIEWS,-There%20are%20certain)
    2. Create 
14. PRACTICAL HACKS
    1. Maintain order of search
        ```
        ORDER BY CASE ItemId
            WHEN 9 THEN 1
            WHEN 1 THEN 2
            ELSE        3
            END;
        ```
        Reference Links: <br />
            1. https://stackoverflow.com/questions/15155930/how-do-i-preserve-the-order-of-a-sql-query-using-the-in-command <br />
            2. https://stackoverflow.com/questions/866465/order-by-the-in-value-list  <br />
            3. https://stackoverflow.com/questions/2813884/how-do-you-keep-the-order-using-select-where-in

    2. Find values Not in Second Table

        ```
        drop table if exists t_left, t_right;

        create table t_left (value integer);
        create table t_right (value integer);

        insert into t_left values(50), (60);
        insert into t_right values(50);
        ```

        LEFT JOIN with IS NULL
        ```
        SELECT  l.*
        FROM    t_left l
        LEFT JOIN
                t_right r
        ON      r.value = l.value
        WHERE   r.value IS NULL;
        ```


        NOT IN
        ```
        SELECT  l.*
        FROM    t_left l
        WHERE   l.value NOT IN
                (
                SELECT  value
                FROM    t_right r
                );
        ```


        NOT EXISTS
        ```
        SELECT  l.*
        FROM    t_left l
        WHERE   NOT EXISTS
                (
                SELECT  NULL
                FROM    t_right r
                WHERE   r.value = l.value
                );
        ```
                
                
                
        EXCEPT
        ```
        SELECT l.* FROM
        t_left l
        EXCEPT
        SELECT r.value FROM
        t_right r;
        ```

        OUTPUT
        ```
        value
        60
        ```
        
        REFERENCE LINKS

        1. https://dba.stackexchange.com/questions/37627/identifying-which-values-do-not-match-a-table-row/37628#37628?newreg=2040ae28dfd141978710f03d2fa6630f
        2. https://dba.stackexchange.com/questions/83684/except-operator-vs-not-in
        3. https://stackoverflow.com/questions/2973558/select-a-value-where-it-doesnt-exist-in-another-table
        4. https://stackoverflow.com/questions/12048633/sql-query-to-find-record-with-id-not-in-another-table
        5. https://stackoverflow.com/questions/28945251/sql-server-select-n-from-values0-0-0-0-tn


Some Important Notes
1. [Slideshare - SQL vs MySQL vs Oracle Syntax Difference](https://www.slideshare.net/SteveStarc/sql-mysqloracle) 
2. [IDE MS SQL SERVER](https://onecompiler.com/sqlserver)
3. [Temp Table Creation for Experiment](https://stackoverflow.com/questions/1564956/how-can-i-select-from-list-of-values-in-sql-server)
