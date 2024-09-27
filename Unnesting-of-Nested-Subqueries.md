[Previous](Using-Subqueries.md) [Next](Selecting-from-the-DUAL-Table.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Queries and Subqueries](SQL-Queries-and-Subqueries.md)
  3. Unnesting of Nested Subqueries 

## Unnesting of Nested Subqueries

The term subquery refers to a sub-query block that appears in the `WHERE` and
`HAVING` clauses. A sub-query that appears in the `FROM` clause is called a
view or derived table.

A `WHERE` clause subquery belongs to one of the following types: `SINGLE-
ROW`,` EXISTS`, `NOT EXISTS`, `ANY`, or `ALL`. A single-row subquery must
return at most one row, whereas the other types of subquery can return zero or
more rows.

`ANY` and `ALL` subqueries are used with relational comparison operators: =,
>,>=, <, <=, and <>.

In SQL, the set operator `IN` is used as a shorthand for =`ANY` and the set
operator `NOT IN `is used as a shorthand for <>`ALL`.

Example: Correlated `EXISTS` Subquery

The subquery in the example is correlated, because the column `C.cust_id`
comes from the table `customers`, that is not defined by the subquery.

    
    
    SELECT C.cust_last_name, C.country_id
            FROM customers C
            WHERE EXISTS (SELECT 1
                  FROM sales S
                  WHERE S.quantity_sold > 1000 and
                        S.cust_id = C.cust_id);

Nested subqueries are those subqueries that appear in the `WHERE` and `HAVING`
clauses of a parent statement like `SELECT`. When Oracle Database evaluates a
statement with a nested subquery, it must evaluate the subquery portion
multiple times and may overlook more efficient access paths or joins.

Subquery unnesting is an optimization that converts a subquery into a join in
the outer query and allows the optimizer to consider subquery tables during
access path, join method, and join order selection. Unnesting either merges
the subquery into the body of the outer query block or turns it into an inline
view.

When a subquery is unnested, it is merged into the statement that contains it,
allowing the optimizer to consider them together when evaluating access paths
and joins. The optimizer can unnest most subqueries, with some exceptions.
Those exceptions include hierarchical subqueries and subqueries that contain a
`ROWNUM` pseudocolumn, one of the set operators, a nested aggregate function,
or a correlated reference to a query block that is not the immediate outer
query block of the subquery.

Assuming no restrictions exist, the optimizer automatically unnests some (but
not all) of the following nested subqueries:

  * Uncorrelated `IN` subqueries 

  * `IN` and `EXISTS` correlated subqueries, as long as they do not contain aggregate functions or a `GROUP` `BY` clause 

You can enable extended subquery unnesting by instructing the optimizer to
unnest additional types of subqueries:

  * You can unnest an uncorrelated `NOT` `IN` subquery by specifying the `HASH_AJ` or `MERGE_AJ` hint in the subquery. 

  * You can unnest other subqueries by specifying the `UNNEST` hint in the subquery. 

See Also:

"[Hints](Comments.md#GUID-D316D545-89E2-4D54-977F-FC97815CD62E)" for
information on hints

Example: Uncorrelated `ANY` Subquery

    
    
    SELECT C.cust_last_name, C.country_id
            FROM customers C        
            WHERE C.cust_id =ANY (SELECT S.cust_id
                          FROM sales S
                          WHERE S.quantity_sold > 1000);
    
    

Example: `NOT EXISTS` Subquery

    
    
    SELECT C.cust_last_name, C.country_id
    FROM customers C
    WHERE NOT EXISTS (SELECT 1
                      FROM sales S, products P
                      WHERE P.prod_id = S.prod_id and
                            P.prod_min_price > 90 and
                            S.cust_id = C.cust_id);
    
    
    


[← Previous](Using-Subqueries.md)

[Next →](Selecting-from-the-DUAL-Table.md)
