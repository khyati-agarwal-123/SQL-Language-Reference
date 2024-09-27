[Previous](ANY_VALUE.md) [Next](APPROX_COUNT_DISTINCT.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. APPROX_COUNT

## APPROX_COUNT

Syntax

![Description of approx_count.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/approx_count.gif)  
[Description of the illustration approx_count.eps](img_text/approx_count.md)

Purpose

`APPROX_COUNT` returns the approximate count of an expression. If you supply
`MAX_ERROR` as the second argument, then the function returns the maximum
error between the actual and approximate count.

You must use this function with a corresponding `APPROX_RANK` function in the
`HAVING` clause. If a query uses `APPROX_COUNT`, `APPROX_SUM`, or
`APPROX_RANK`, then the query must not use any other aggregation functions.

Examples

The following query returns the 10 most common jobs within every department:

    
    
    SELECT department_id, job_id, 
           APPROX_COUNT(*) 
    FROM   employees
    GROUP BY department_id, job_id
    HAVING 
      APPROX_RANK ( 
      PARTITION BY department_id 
      ORDER BY APPROX_COUNT(*) 
      DESC ) <= 10;


[← Previous](ANY_VALUE.md)

[Next →](APPROX_COUNT_DISTINCT.md)
