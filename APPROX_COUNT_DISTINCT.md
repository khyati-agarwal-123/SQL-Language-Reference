[Previous](APPROX_COUNT.md) [Next](APPROX_COUNT_DISTINCT_AGG.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. APPROX_COUNT_DISTINCT

## APPROX_COUNT_DISTINCT

Syntax

![Description of approx_count_distinct.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/approx_count_distinct.gif)  
[Description of the illustration
approx_count_distinct.eps](img_text/approx_count_distinct.md)

Purpose

`APPROX_COUNT_DISTINCT` returns the approximate number of rows that contain a
distinct value for `expr`.

This function provides an alternative to the `COUNT` `(DISTINCT` `expr``)`
function, which returns the exact number of rows that contain distinct values
of `expr`. `APPROX_COUNT_DISTINCT` processes large amounts of data
significantly faster than `COUNT`, with negligible deviation from the exact
result.

For `expr`, you can specify a column of any scalar data type other than
`BFILE`, `BLOB`, `CLOB`, `LONG`, `LONG` `RAW`, or `NCLOB`.

`APPROX_COUNT_DISTINCT` ignores rows that contain a null value for `expr`.
This function returns a `NUMBER`.

See Also:

  * [COUNT](COUNT.md#GUID-AEF08B79-024D-4E3A-B362-9715FB011776) for more information on the `COUNT` `(DISTINCT` `expr``)` function 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules, which define the collation `APPROX_COUNT_DISTINCT` uses to compare character values for `expr`

Examples

The following statement returns the approximate number of rows with distinct
values for `manager_id`:

    
    
    SELECT APPROX_COUNT_DISTINCT(manager_id) AS "Active Managers"
      FROM employees;
    
    Active Managers
    ---------------
                 18
    

The following statement returns the approximate number of distinct customers
for each product:

    
    
    SELECT prod_id, APPROX_COUNT_DISTINCT(cust_id) AS "Number of Customers"
      FROM sales
      GROUP BY prod_id
      ORDER BY prod_id;
    
       PROD_ID Number of Customers
    ---------- -------------------
            13                2516
            14                2030
            15                2105
            16                2367
            17                2093
            18                2975
            19                2630
            20                3791
    . . .


[← Previous](APPROX_COUNT.md)

[Next →](APPROX_COUNT_DISTINCT_AGG.md)
