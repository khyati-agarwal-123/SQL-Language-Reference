[Previous](Hierarchical-Queries.md) [Next](Sorting-Query-Results.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Queries and Subqueries](SQL-Queries-and-Subqueries.md)
  3. The Set Operators

## The Set Operators

You can combine multiple queries using the set operators `UNION`, `UNION`
`ALL`, `INTERSECT`, `INTERSECT` `ALL`, `EXCEPT`, `EXCEPT` `ALL`, `MINUS`, and
`MINUS` `ALL`. All set operators have equal precedence. If a SQL statement
contains multiple set operators, then Oracle Database evaluates them from the
left to right unless parentheses explicitly specify another order.

The corresponding expressions in the select lists of the component queries of
a compound query must match in number and must be in the same data type group
(such as numeric or character).

If component queries select character data, then the data type of the return
values are determined as follows:

  * If both queries select values of data type `CHAR` of equal length, then the returned values have data type `CHAR` of that length. If the queries select values of `CHAR` with different lengths, then the returned value is `VARCHAR2` with the length of the larger `CHAR` value. 

  * If either or both of the queries select values of data type `VARCHAR2`, then the returned values have data type `VARCHAR2`. 

If component queries select numeric data, then the data type of the return
values is determined by numeric precedence:

  * If any query selects values of type `BINARY_DOUBLE`, then the returned values have data type `BINARY_DOUBLE`. 

  * If no query selects values of type `BINARY_DOUBLE` but any query selects values of type `BINARY_FLOAT`, then the returned values have data type `BINARY_FLOAT`. 

  * If all queries select values of type `NUMBER`, then the returned values have data type `NUMBER`. 

In queries using set operators, Oracle does not perform implicit conversion
across data type groups. Therefore, if the corresponding expressions of
component queries resolve to both character data and numeric data, Oracle
returns an error.

The `INTERSECT` operator with the keyword `ALL` returns the result of two or
more `SELECT` statements in which rows appear in all result sets. Null values
that are common across the component queries of `INTERSECT` `ALL` are returned
at the end of the result set.

The `MINUS` operator with the keyword `ALL` returns the result of two `SELECT`
statements in which rows appear in the first result set but not in the second
result set.

If the first query has `x` nulls and the second query has `y` nulls, and `x`
is greater than `y`, then `x` minus `y` NULLS are returned at the end of the
result query set. `MINUS` `ALL` returns no rows if the result set returned by
the first `SELECT`statement is a subset of the result set returned by the
second `SELECT`.

The `EXCEPT` operator is a synonym for `MINUS` and has the exact same
semantics. `EXCEPT ALL` returns rows that are present in the first result set
but not in the second. However, duplicates may be present in the final result.

`EXCEPT` `ALL`, `MINUS` `ALL` `INTERSECT` `ALL` return equivalent instead of
the original value, when ` NLS_SORT=BINARY_CI[AI]` is acceptable for the SQL
standard.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion and "[Numeric Precedence](Data-
Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812)" for information on
numeric precedence

Examples for Valid and Invalid Data Type Conversions for Set Operators

The following query is valid:

    
    
    SELECT 3 FROM DUAL
       INTERSECT
    SELECT 3f FROM DUAL;
    

This is implicitly converted to the following compound query:

    
    
    SELECT TO_BINARY_FLOAT(3) FROM DUAL
       INTERSECT
    SELECT 3f FROM DUAL;
    

The following query returns an error:

    
    
    SELECT '3' FROM DUAL
       INTERSECT
    SELECT 3f FROM DUAL;

Restrictions on the Set Operators

The set operators are subject to the following restrictions:

  * The set operators are not valid on columns of type `BLOB`, `CLOB`, `BFILE`, `VARRAY`, or nested table. 

  * The `UNION`, `INTERSECT`, `EXCEPT`, and `MINUS` operators are not valid on `LONG` columns. 

  * If the select list preceding the set operator contains an expression, then you must provide a column alias for the expression in order to refer to it in the `order_by_clause`. 

  * You cannot also specify the `for_update_clause` with the set operators. 

  * You cannot specify the `order_by_clause` in the `subquery` of these operators. 

  * You cannot use these operators in `SELECT` statements containing `TABLE` collection expressions. 

Note:

To comply with emerging SQL standards, a future release of Oracle will give
the `INTERSECT` operator greater precedence than the other set operators.
Therefore, you should use parentheses to specify order of evaluation in
queries that use the `INTERSECT` operator with other set operators.

UNION Example

The following statement combines the results of two queries with the `UNION`
operator, which eliminates duplicate selected rows. This statement shows that
you must match data type (using the `TO_CHAR` function) when columns do not
exist in one or the other table:

    
    
    SELECT location_id, department_name "Department", 
       TO_CHAR(NULL) "Warehouse"  FROM departments
       UNION
       SELECT location_id, TO_CHAR(NULL) "Department", warehouse_name 
       FROM warehouses;
    
    LOCATION_ID Department                     Warehouse
    ----------- ------------------------------ ---------------------------
           1400 IT
           1400                                Southlake, Texas
           1500 Shipping
           1500                                San Francisco
           1600                                New Jersey
           1700 Accounting
           1700 Administration
           1700 Benefits
           1700 Construction
           1700 Contracting
           1700 Control And Credit
    ...

UNION ALL Example

The `UNION` operator returns only distinct rows that appear in either result,
while the `UNION` `ALL` operator returns all rows. The `UNION` `ALL` operator
does not eliminate duplicate selected rows:

    
    
    SELECT product_id FROM order_items
    UNION
    SELECT product_id FROM inventories
    ORDER BY product_id;
    
    SELECT location_id  FROM locations 
    UNION ALL 
    SELECT location_id  FROM departments
    ORDER BY location_id;
    

A `location_id` value that appears multiple times in either or both queries
(such as '`1700`') is returned only once by the `UNION` operator, but multiple
times by the `UNION` `ALL` operator.

INTERSECT Example

The following statement combines the results with the `INTERSECT` operator,
which returns only those unique rows returned by both queries:

    
    
    SELECT product_id FROM inventories
    INTERSECT
    SELECT product_id FROM order_items
    ORDER BY product_id;

MINUS Example

The following statement combines results with the `MINUS` operator, which
returns only unique rows returned by the first query but not by the second:

    
    
    SELECT product_id FROM inventories
    MINUS
    SELECT product_id FROM order_items
    ORDER BY product_id;

EXCEPT Example

You can use `EXCEPT` or `MINUS` when you want to exclude a result set from the
final result set. In this example, the result of the second query is ignored.

The following statement combines results with the `EXCEPT` operator, which
returns only unique rows returned by the first query but not by the second:

    
    
    SELECT product_id FROM inventories
    EXCEPT
    SELECT product_id FROM order_items
    ORDER BY product_id;


[← Previous](Hierarchical-Queries.md)

[Next →](Sorting-Query-Results.md)
