[Previous](GREATEST.md) [Next](GROUPING.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. GROUP_ID 

## GROUP_ID

Syntax

![Description of group_id.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/group_id.gif)  
[Description of the illustration group_id.eps](img_text/group_id.md)

Purpose

`GROUP_ID` distinguishes duplicate groups resulting from a `GROUP` `BY`
specification. It is useful in filtering out duplicate groupings from the
query result. It returns an Oracle `NUMBER` to uniquely identify duplicate
groups. This function is applicable only in a `SELECT` statement that contains
a `GROUP` `BY` clause.

If `n` duplicates exist for a particular grouping, then `GROUP_ID` returns
numbers in the range 0 to `n`-1.

Examples

The following example assigns the value `1` to the duplicate
`co.country_region` grouping from a query on the sample tables `sh.countries`
and `sh.sales`:

    
    
    SELECT co.country_region, co.country_subregion,
           SUM(s.amount_sold) "Revenue", GROUP_ID() g
      FROM sales s, customers c, countries co
      WHERE s.cust_id = c.cust_id
        AND c.country_id = co.country_id
        AND s.time_id = '1-JAN-00'
        AND co.country_region IN ('Americas', 'Europe')
      GROUP BY GROUPING SETS ( (co.country_region, co.country_subregion),
                               (co.country_region, co.country_subregion) )
      ORDER BY co.country_region, co.country_subregion, "Revenue", g;
    
    COUNTRY_REGION       COUNTRY_SUBREGION                 Revenue          G
    -------------------- ------------------------------ ---------- ----------
    Americas             Northern America                    944.6          0
    Americas             Northern America                    944.6          1
    Europe               Western Europe                     566.39          0
    Europe               Western Europe                     566.39          1
    

To ensure that only rows with `GROUP_ID` < 1 are returned, add the following
`HAVING` clause to the end of the statement :

    
    
    HAVING GROUP_ID() < 1


[← Previous](GREATEST.md)

[Next →](GROUPING.md)
