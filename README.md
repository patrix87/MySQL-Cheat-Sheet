# SQL ORDER OF EXECUTION
|Clause|Function|
|-|-|
|FROM, including JOINs|Choose and join tables|
|WHERE|Filter the base data|
|GROUP BY|Aggregates the base data|
|HAVING|Filters the aggregated data|
|SELECT|Returns the final data|
|DISTINCT|Remove duplicated rows|
|UNION|Combines multiple result set|
|ORDER BY|Sort the final data|
|LIMIT|Offset and limit the final data|

# SQL ORDER OF CLAUSES
|Clause|Function|
|-|-|
|SELECT|Select columns|
|DISTINCT|Remove duplicated rows|
|FROM|Select table|
|JOIN|Select another table|
|WHERE|Filter the data|
|GROUP BY|Aggregates the data|
|HAVING|Filters the aggregated data|
|UNION|Combines multiple result set|
|ORDER BY|Sort the final data|
|LIMIT|Offset and limit the final data|

# SQL CLAUSES IN WRITING ORDER

## USE
`USE Database`

Tell SQL to use a specific database.

# SELECT 
Returned columns

`SELECT *` 

`SELECT column + 10 * 2 as 'calculated column'`

`SELECT table.column, other_table.column AS 'column_name', 'string' AS "other column name"`

`SELECT DISTINCT *`

## FROM
Target table

`FROM table`

`FROM database.table`

`FROM table alias`

`FROM (query)`

## JOIN
Join only rows that match conditions in both table.

## INNER JOINS

`JOIN table ON table.column = other_table.column`

`JOIN table alias ON alias.column = table.column`

### SELF JOIN

`FROM same_table a JOIN same_table b ON a.column = b.column`

### MULTIPLE JOINS

`JOIN table a ON a.column = other_table.column`

`JOIN table b ON b.column = a.column`

`JOIN table c ON c.column = other_table.other_column`

### COMPOUND JOIN CONDITIONS

`JOIN table a ON a.column = b.column AND a.other_column = b.other_column`

### USING KEYWORD

`JOIN table a USING (column)`

`JOIN table a USING (column, other_column)`

### NATURAL JOIN
Will try to join on matching columns *discouraged*

`NATURAL JOIN table a`

### IMPLICIT SYNTAX

`FROM table a, table b WHERE a.column = b.column`

## OUTER JOINS

### LEFT JOIN
return all the results from the table on the left *(above)* of the JOIN and only the matching columns from the table on the right.

`LEFT JOIN table a ON a.column = b.column`

### RIGHT JOIN

return all the results from the table on the right *(above)* of the JOIN and only the matching columns from the table on the left.

`RIGHT JOIN table a ON a.column = b.column`

### SELF OUTER JOINS

`FROM same_table a LEFT JOIN same_table b ON a.column = b.column`

## CROSS JOINS
return all combinations of both table. EG colors and size combo.

`FROM table a CROSS JOIN table b`

### IMPLICIT SYNTAX

`FROM table a, table b`

## WHERE
Conditions

`WHERE column = 1`

`WHERE column like "string"`

`WHERE column = 3 AND other_column = 2`

`WHERE column IN ('value','other_value')`

`WHERE column BETWEEN 1 AND 10` *inclusive

`WHERE column REGEXP '([A-Z])\w+'`


## GROUP BY
Group by column

`GROUP BY column`

## ORDER BY
Order values based on a column

`ORDER BY column`

`ORDER BY column DESC`

`ORDER BY column DESC, other_column`

## LIMIT
Limit the number of returns

`LIMIT 1000`

Skip 500, return 100

`LIMIT 500,100`

# INSERT

## INSERT STATEMENT

### Based on column name
```sql
INSERT INTO table (
    firstname,
    lastname
)
VALUES (
    'value',
    'other value'
)
```

### Based on column order
```sql
INSERT INTO table
VALUES (
    DEFAULT,
    'value',
    'other value',
    NULL
)
```

### Multiple values
```sql
INSERT INTO table (
    name,
    password
)
VALUES  (bob, qwerty123),
        (alfred, chatton), 
        (john,xXRocker!Xx)
```

### Multiple tables
```sql
INSERT INTO table (firstname, lastname)
VALUES (bob, tremblay)

INSERT INTO order_id (client_id)
VALUES (LAST_INSERT_ID())
```
*both table have auto-increment id*


# DATA TYPES

## String Data Types
|Data type|Description|
|-|-|
|CHAR(size)|A FIXED length string (can contain letters, numbers, and special characters). The size parameter specifies the column length in characters - can be from 0 to 255. Default is 1|
|VARCHAR(size)|A VARIABLE length string (can contain letters, numbers, and special characters). The size parameter specifies the maximum column length in characters - can be from 0 to 65535|
|BINARY(size)|Equal to CHAR(), but stores binary byte strings. The size parameter specifies the column length in bytes. Default is 1|
|VARBINARY(size)|Equal to VARCHAR(), but stores binary byte strings. The size parameter specifies the maximum column length in bytes.|
|TINYBLOB|For BLOBs (Binary Large OBjects). Max length: 255 bytes|
|TINYTEXT|Holds a string with a maximum length of 255 characters|
|TEXT(size)|Holds a string with a maximum length of 65,535 bytes|
|BLOB(size)|For BLOBs (Binary Large OBjects). Holds up to 65,535 bytes of data|
|MEDIUMTEXT|Holds a string with a maximum length of 16,777,215 characters|
|MEDIUMBLOB|For BLOBs (Binary Large OBjects). Holds up to 16,777,215 bytes of data|
|LONGTEXT|Holds a string with a maximum length of 4,294,967,295 characters|
|LONGBLOB|For BLOBs (Binary Large OBjects). Holds up to 4,294,967,295 bytes of data|
|ENUM(val1, val2, val3, ...)|A string object that can have only one value, chosen from a list of possible values. You can list up to 65535 values in an ENUM list. If a value is inserted that is not in the list, a blank value will be inserted. The values are sorted in the order you enter them|
|SET(val1, val2, val3, ...)|A string object that can have 0 or more values, chosen from a list of possible values. You can list up to 64 values in a SET list|

## Numeric Data Types
|Data type|Description|
|-|-|
|BIT(size)|A bit-value type. The number of bits per value is specified in size. The size parameter can hold a value from 1 to 64. The default value for size is 1.|
|TINYINT(size)|A very small integer. Signed range is from -128 to 127. Unsigned range is from 0 to 255. The size parameter specifies the maximum display width (which is 255)|
|BOOL|Zero is considered as false, nonzero values are considered as true.|
|BOOLEAN|Equal to BOOL|
|SMALLINT(size)|A small integer. Signed range is from -32768 to 32767. Unsigned range is from 0 to 65535. The size parameter specifies the maximum display width (which is 255)|
|MEDIUMINT(size)|A medium integer. Signed range is from -8388608 to 8388607. Unsigned range is from 0 to 16777215. The size parameter specifies the maximum display width (which is 255)|
|INT(size)|A medium integer. Signed range is from -2147483648 to 2147483647. Unsigned range is from 0 to 4294967295. The size parameter specifies the maximum display width (which is 255)|
|INTEGER(size)|Equal to INT(size)|
|BIGINT(size)|A large integer. Signed range is from -9223372036854775808 to 9223372036854775807. Unsigned range is from 0 to 18446744073709551615. The size parameter specifies the maximum display width (which is 255)|
|FLOAT(size, d)|A floating point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. This syntax is deprecated in MySQL 8.0.17, and it will be removed in future MySQL versions|
|FLOAT(p)|A floating point number. MySQL uses the p value to determine whether to use FLOAT or DOUBLE for the resulting data type. If p is from 0 to 24, the data type becomes FLOAT(). If p is from 25 to 53, the data type becomes DOUBLE()|
|DOUBLE(size, d)|A normal-size floating point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter|
|DOUBLE PRECISION(size, d)| |
|DECIMAL(size, d)|An exact fixed-point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. The maximum number for size is 65. The maximum number for d is 30. The default value for size is 10. The default value for d is 0.|
|DEC(size, d)|Equal to DECIMAL(size,d)|

Note: All the numeric data types may have an extra option: UNSIGNED or ZEROFILL. If you add the UNSIGNED option, MySQL disallows negative values for the column. If you add the ZEROFILL option, MySQL automatically also adds the UNSIGNED attribute to the column.

## Date and Time Data Types
|Data type|Description|
|-|-|
|DATE|A date. Format: YYYY-MM-DD. The supported range is from '1000-01-01' to '9999-12-31'|
|DATETIME(fsp)|A date and time combination. Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'. Adding DEFAULT and ON UPDATE in the column definition to get automatic initialization and updating to the current date and time|
|TIMESTAMP(fsp)|A timestamp. TIMESTAMP values are stored as the number of seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC. Automatic initialization and updating to the current date and time can be specified using DEFAULT CURRENT_TIMESTAMP and ON UPDATE CURRENT_TIMESTAMP in the column definition|
|TIME(fsp)|A time. Format: hh:mm:ss. The supported range is from '-838:59:59' to '838:59:59'|
|YEAR|A year in four-digit format. Values allowed in four-digit format: 1901 to 2155, and 0000. MySQL 8.0 does not support year in two-digit format.|


# ANNEXES

## COMPARAISON OPERATORS

|Comparison Operator|Description|
|-|-|
|=|Equal|
|<=>|Equal (Safe to compare NULL values)|
|<>|Not Equal|
|!=|Not Equal|
|>|Greater Than|
|>=|Greater Than or Equal|
|<|Less Than|
|<=|Less Than or Equal|
|IN ( )|Matches a value in a list|
|NOT|Negates a condition|
|AND|2 or more conditions to be met|
|OR|Any one of the conditions are met|
|BETWEEN|Within a range (inclusive)|
|IS NULL|NULL value|
|IS NOT NULL|Non-NULL value|
|LIKE|Pattern matching with % and _|
|REGEXP|Regular Expression matching|

## WILDCARDS

|Wildcard|Explanation|
|-|-|
|%|Allows you to match any string of any length (including zero length)|
|_|Allows you to match on a single character|
