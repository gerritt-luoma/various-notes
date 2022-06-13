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