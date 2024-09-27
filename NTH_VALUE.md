[Previous](NLSSORT.md) [Next](NTILE.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. NTH_VALUE 

## NTH_VALUE

Syntax

![Description of nth_value.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nth_value.gif)  
[Description of the illustration nth_value.eps](img_text/nth_value.md)

See Also:

"[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)" for information on
syntax, semantics, and restrictions of the `analytic_clause`

Purpose

`NTH_VALUE` returns the `measure_expr` value of the nth row in the window
defined by the `analytic_clause`. The returned value has the data type of the
`measure_expr`.

  * {`RESPECT` | `IGNORE`} `NULLS` determines whether null values of `measure_expr` are included in or eliminated from the calculation. The default is `RESPECT` `NULLS`. 

  * `n` determines the nth row for which the measure value is to be returned. `n` can be a constant, bind variable, column, or an expression involving them, as long as it resolves to a positive integer. The function returns `NULL` if the data source window has fewer than `n` rows. If `n` is null, then the function returns an error. 

  * `FROM` {`FIRST` | `LAST`} determines whether the calculation begins at the first or last row of the window. The default is `FROM` `FIRST`. 

If you omit the `windowing_clause` of the `analytic_clause`, it defaults to
`RANGE` `BETWEEN` `UNBOUNDED` `PRECEDING` `AND` `CURRENT` `ROW`. This default
sometimes returns an unexpected value for `NTH_VALUE` ... `FROM` `LAST` ... ,
because the last value in the window is at the bottom of the window, which is
not fixed. It keeps changing as the current row changes. For expected results,
specify the `windowing_clause` as `RANGE` `BETWEEN` `UNBOUNDED` `PRECEDING`
`AND` `UNBOUNDED` `FOLLOWING`. Alternatively, you can specify the
`windowing_clause` as `RANGE` `BETWEEN` `CURRENT` `ROW` `AND` `UNBOUNDED`
`FOLLOWING`.

See Also:

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG02017) for more information on the use of this function 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the return value of `NTH_VALUE` when it is a character value 

Examples

The following example shows the minimum `amount_sold` value for the second
`channel_id` in ascending order for each `prod_id` between 13 and 16:

    
    
    SELECT prod_id, channel_id, MIN(amount_sold),
        NTH_VALUE(MIN(amount_sold), 2) OVER (PARTITION BY prod_id ORDER BY channel_id
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) nv
      FROM sales
      WHERE prod_id BETWEEN 13 and 16
      GROUP BY prod_id, channel_id;
    
       PROD_ID CHANNEL_ID MIN(AMOUNT_SOLD)         NV
    ---------- ---------- ---------------- ----------
            13          2           907.34      906.2
            13          3            906.2      906.2
            13          4           842.21      906.2
            14          2          1015.94    1036.72
            14          3          1036.72    1036.72
            14          4           935.79    1036.72
            15          2           871.19     871.19
            15          3           871.19     871.19
            15          4           871.19     871.19
            16          2           266.84     266.84
            16          3           266.84     266.84
            16          4           266.84     266.84
            16          9            11.99     266.84
    
    13 rows selected.


[← Previous](NLSSORT.md)

[Next →](NTILE.md)
