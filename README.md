# SQL NOTES

### Select query for all columns

```
SELECT * FROM mytable;
```

### Select query for a specific columns

```
SELECT column, another_column, … FROM mytable;
```

### Select query with constraints

```
SELECT column, ... FROM mytable WHERE condition AND/OR another_condition AND/OR …;
```

### % Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE)

```
SELECT * FROM table WHERE column LIKE "abc%";
```

### Select query with unique results

```
SELECT DISTINCT column, … FROM mytable WHERE condition(s);
```

### Select query with ordered results (By default ASC)

```
SELECT column, … FROM mytable WHERE condition(s) ORDER BY column ASC/DESC;
```

### Select query with limited rows

```
SELECT column, … FROM mytable WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

### Select query with INNER JOIN on multiple tables

```
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

### Select query with LEFT/RIGHT/FULL JOINs on multiple tables

```
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

### Select query with constraints on NULL values

```
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
```

### Select query with aggregate functions over all rows

```
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression;
```

## Aggregate Function

- COUNT(\*), COUNT(column)
- MIN(column)
- MAX(column)
- AVG(column)
- SUM(column)

### Select query with HAVING constraint

```
SELECT group_by_column, AGG_FUNC(column_expression) AS aggregate_result_alias, …
FROM mytable
WHERE condition
GROUP BY column
HAVING group_condition;
```

### Order of Execution

```
SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE constraint_expression
    GROUP BY column
    HAVING constraint_expression
    ORDER BY column ASC/DESC
    LIMIT count OFFSET COUNT;
```

- FROM and JOINs -> Where -> Group By -> Having -> Select -> Distinct -> ORDER BY -> LIMIT / OFFSET.

### Insert statement with values for all columns

```
INSERT INTO mytable
VALUES (value_or_expr, another_value_or_expr, …),
       (value_or_expr_2, another_value_or_expr_2, …),
```

```
INSERT INTO mytable
(column, another_column, …)
        VALUES (value_or_expr, another_value_or_expr, …),
        (value_or_expr_2, another_value_or_expr_2, …),
```

### Update statement with values

```
UPDATE mytable
SET column = value_or_expr,
    other_column = another_value_or_expr,
    …
WHERE condition;
```

### Delete statement with condition the rows of the table to delete through the WHERE clause.

```
DELETE FROM mytable
WHERE condition;
```

### Create table statement w/ optional table constraint and default value

```
CREATE TABLE IF NOT EXISTS mytable (
    column DataType TableConstraint DEFAULT default_value,
    another_column DataType TableConstraint DEFAULT default_value,
    …
);
```

### Altering table to add new column(s)

```
ALTER TABLE mytable
ADD column DataType OptionalTableConstraint
    DEFAULT default_value;
```

### Altering table to remove column(s)

```
ALTER TABLE mytable
DROP column_to_be_deleted;
```

### Altering table name

```
ALTER TABLE mytable
RENAME TO new_table_name;
```

### Drop table statement

```
DROP TABLE IF EXISTS mytable;
```

## Normalization

### 1NF

- Using row order to convey information is not permitted.
  - e.g: Display the names in order from tallest to shortest.
- Mixing data types within the same column violates 1NF.
- A table without a **primary key** violates 1NF.
- Storing a repeating group of data items on a single row violates the 1NF.

### 2NF

![Not in 2NF](./player_inventory.png 'Not in 2 NF')

- This must follow 1NF.
- Each non-key attribute must depend on the entire primary key.

![In 2NF](./2NF.png 'IN 2 NF')

### 3NF

![Not in 3NF](./NotIn3NF.png 'Not in 3 NF')
![In 3NF](./3NF.png 'In 3 NF')

### Summary

![Summary](Summary.png 'Summary')
