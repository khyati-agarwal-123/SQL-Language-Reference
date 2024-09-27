[Previous](PRESENTNNV.md) [Next](PREVIOUS.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. PRESENTV

## PRESENTV

Syntax

![Description of presentv.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/presentv.gif)  
[Description of the illustration presentv.eps](img_text/presentv.md)

Purpose

The `PRESENTV` function can be used only within the `model_clause` of the
`SELECT` statement and then only on the right-hand side of a model rule. It
returns `expr1` when, prior to the execution of the `model_clause`,
`cell_reference` exists. Otherwise it returns `expr2`.

See Also:

  * [model_clause](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2172805) and "[Model Expressions](Model-Expressions.md#GUID-83D3FD56-8346-4D3F-A49E-5FE41FE19257)" for the syntax and semantics 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the return value of `PRESENTV` when it is a character value 

Examples

In the following example, if a row containing sales for the Mouse Pad for the
year 2000 exists, then the sales value for the Mouse Pad for the year 2001 is
set to the sales value for the Mouse Pad for the year 2000. If the row does
not exist, then a row is created with the sales value for the Mouse Pad for
year 20001 set to 0.

    
    
    SELECT country, prod, year, s
      FROM sales_view_ref
      MODEL
        PARTITION BY (country)
        DIMENSION BY (prod, year)
        MEASURES (sale s)
        IGNORE NAV
        UNIQUE DIMENSION
        RULES UPSERT SEQUENTIAL ORDER
        (
          s['Mouse Pad', 2001] =
            PRESENTV(s['Mouse Pad', 2000], s['Mouse Pad', 2000], 0)
        )
      ORDER BY country, prod, year;
    
    COUNTRY       PROD                                         YEAR           S
    ----------    -----------------------------------      --------   ---------
    France        Mouse Pad                                    1998     2509.42
    France        Mouse Pad                                    1999     3678.69
    France        Mouse Pad                                    2000     3000.72
    France        Mouse Pad                                    2001     3000.72
    France        Standard Mouse                               1998     2390.83
    France        Standard Mouse                               1999     2280.45
    France        Standard Mouse                               2000     1274.31
    France        Standard Mouse                               2001     2164.54
    Germany       Mouse Pad                                    1998     5827.87
    Germany       Mouse Pad                                    1999     8346.44
    Germany       Mouse Pad                                    2000     7375.46
    Germany       Mouse Pad                                    2001     7375.46
    Germany       Standard Mouse                               1998     7116.11
    Germany       Standard Mouse                               1999     6263.14
    Germany       Standard Mouse                               2000     2637.31
    Germany       Standard Mouse                               2001     6456.13
    
    16 rows selected.
    

The preceding example requires the view `sales_view_ref`. Refer to "[The MODEL
clause: Examples](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2171160)" to create this view.


[← Previous](PRESENTNNV.md)

[Next →](PREVIOUS.md)
