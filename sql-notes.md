- [SQL Notes](#sql-notes)
  - [Querying](#querying)
  - [Aggregate Functions](#aggregate-functions)
  - [Working with multiple tables](#working-with-multiple-tables)
# SQL Notes

## Querying
- `SELECT`: The `SELECT` operator is what is used to select specific (or all) columns from a table
  ```
  // to select all rows/columns from a table
  SELECT * FROM table_name

  // to select a specific column from a table
  SELECT col_name FROM table_name

  // to select specific column from a table
  SELECT col1_name, col2_name, ... FROM table_name
  ```
- `AS`: The `AS` operator is used to give a column or table a temporary name/alias when reporting the values in the table
- `DISTINCT`: The `DISTINCT`operator is used to only display distinct/unique values within a column to know all of the *different* data as opposed to *all* of the data
  ```
  SELECT DISTINCT col_name
  FROM table_name
  ```
- `WHERE`: The `WHERE` operator is used to place constraints on a column/columns when selecting/viewing rows.  Only rows satisfying the contraints will be returned/shown
  ```
  SELECT *
  FROM table_name
  WHERE col_name > value 
  ```
- `LIKE`: The `LIKE` operator is used to compare data with similar values.  
  - You can use the like operator to find strings that match with specified wild cards
    ```
    SELECT *
    FROM table_name
    WHERE col_name LIKE 'ONE_TWO' // ONE is the beginning of the string, _ is the wild card, TWO is the remainder of the string
    ```
  - `%` is a wildcard that matches anywhere between 0 and infinity characters
    ```
    SELECT *
    FROM table_name
    WHERE col_name LIKE '%s' //returns all strings ending in s
    ```
- `IS/IS NOT NULL`: Values that have not been set within the table are automatically set to `NULL`.  You can use the `IS` and `IS NOT` operators to filter values that have or have not been set
  ```
  SELECT *
  FROM table_name
  WHERE col_name IS NOT NULL
  ```
- `BETWEEN`: The `BETWEEN` operator is used with a `WHERE` call to only return values that are between two other values.  It accepts numbers, text, an dates.  The between returns values that are x <= val <= y
  ```
  SELECT *
  FROM table_name
  WHERE col_name BETWEEN x AND y
  ```
- `AND`: The `AND` clause allows us to combine constraints to make more accurate and specific queries.  For a row to be returned by the query, it must satisfy both side of the `AND` clause
- `OR`: The `OR` clause allows us to return rows if either of the constraints are met
- `ORDER BY`: The `ORDER BY` clause allows us to list our results in a specific order.  The order of sorting is ascending by default.  If you want to go top to bottom, add `DESC` after the column name
  ```
  SELECT *
  FROM table_name
  ORDER BY col_name DESC // remove DESC if ascending is desired
  ```
- `LIMIT`: The `LIMIT` operator allows us to limit the number of rows returned.  
- `CASE`: The `CASE` statement allows us to create different outputs.  This is the SQL version of an if-then statement
  - `CASE` statements can declare a condition by having a `WHEN` `THEN` block.  `WHEN` the condition is met, `THEN` do something.  If not, move onto the next thing
  - You can have as many `WHEN` `THEN` blocks as you want and when you need a catch all remaining, use the `ELSE` block.
  - All `CASE` statements must end with the `END` operator
  - You can name the output of your case block with the `AS` operator appended to the `END` of the block
  ```
  SELECT col_name,
    CASE
      WHEN col_name <condition> THEN <output>
      WHEN col_name <diff cond> THEN <output>
      ELSE <output>
    END AS output_name
  FROM table_name
  ```

## Aggregate Functions
- Aggregate functions are used to perform calculations on our dable.  When a calculation is used on multiple rows it is known as an **aggregate**
- `COUNT()`: The count function is used to count the number of non empty values in a column
  - You can use query operators to make the value being summed more specific
  ```
  SELECT COUNT(*)
  FROM table_name; // returns the number of rows in the table
  ```
- `SUM()`: The sum function is used to sum a column into one single value
  ```
  SELECT SUM(col_name)
  FROM table_name; // returns a number for the sum
- `MAX()`/`MIN()`: The min and max functions return the min/max value from within a column of a table
  ```
  SELECT MIN(col_name)
  FROM table_name;

  SELECT MAX(col_name)
  FROM table_name;
  ```
- `AVG()`: The average function returns the average value of a column of the table
  ```
  SELECT AVG(col_name)
  FROM table_name;
- `ROUND()`: The round function is used to round the values of a column and takes two inputs.  The first input is a column name while the second input is an integer specififying the number of decimal places it should round to.
  ```
  SELECT ROUND(col_name, num)
  FROM table_name
  ```
- Using `GROUP BY` with aggregate functions can be very useful.  If you want to get the average for a column based on the value of another column, you can get the average for every value of column 2
  ```
  SELECT AVG(col_one)
  FROM table_name
  GROUP BY col_two
  ```
- You can even `GROUP BY` based on a calculation
  ```
  SELECT *
  FROM table_name
  GROUP BY ROUND(col_one)
  ```
- `HAVING`: The having statement is similar to the `WHERE` operator but is used for when we want to have a condition based on a function.  These statements always come after `GROUP BY` statements but before `ORDER BY` and `LIMIT` statements
  ```
  SELECT *
  FROM table_name
  HAVING FUNCTION(col_name) <condition>
  ```


## Working with multiple tables
- One of the main principles of SQL is to not repeat data within the database.  You can prevent repetition by placing data into separate tables and referene the data by an ID
- An example of a subscription and order system with users would have tables as such:
  - Orders:
    - order_id
    - customer_id
    - subscription_id
    - purchase_date
  - Subscriptions:
    - subscription_id
    - description
    - price_per_month
    - subscription_length
  - Customers:
    - customer_id
    - customer_name
    - address
- `JOIN`: The join command is used to combine the outputs of two (or more) tables into one output.  To output a specific row of both tables, you can use the `ON` keyword to have a constraint on what rows to output
  ```
  SELECT *
  FROM table_one
  JOIN table_two
    ON table_one.col_name = table_two.col_name
  ```
  - Inner joins: A base join is also known as an inner join.  Inner joins only include rows that match our `ON` condition which can result in missing data
  - `LEFT JOIN`: Left joins keep all rows from the first table regardless of whether there is ssa matching row in the second table
  - `CROSS JOIN`: The Cross join is used to compine all the rows of one table with all the rows of another table regardless of relation.  It will create an output showing every combo of the chosen columns
    ```
    SELECT shirts.shirt_color,
      pants.pants_color
    FROM shirts
    CROSS JOIN pants;
    ```
- `PRIMARY KEY`
  - In the previous example with the orders, subscriptions, and users each table had a unique ID to identify each entry.  This is known as the `Primary key`
  - Primary keys CANNOT be null
  - Each primary key MUST be unique
  - A table cannot have more than one primary key column
- `FOREIGN KEY`
  - When a primary key is referenced from another table it is known as a `Foreign Key`
- `UNION`: A `UNION` is used to stack one table on top of the other.  Both tables must have the same number of columns and have the same data types in each column
  ```
  SELECT *
  FROM table1
  UNION
  SELECT *
  FROM table2;
  ```
- `WITH`: Sometimes we want to combine a table with the result of another operation/query.  We can do this using `WITH`
  ```
  WITH previous_results AS (
    SELECT ...
    ...
    ...
    ...
  )
  SELECT *
  FROM previous_results
  JOIN table_one
    ON _____ = _____;
  ```
  