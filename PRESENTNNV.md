[Previous](PREDICTION_SET.md) [Next](PRESENTV.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. PRESENTNNV

## PRESENTNNV

Syntax

![Description of presentnnv.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/presentnnv.gif)  
[Description of the illustration presentnnv.eps](img_text/presentnnv.md)

Purpose

The `PRESENTNNV` function can be used only in the `model_clause` of the
`SELECT` statement and then only on the right-hand side of a model rule. It
returns `expr1` when `cell_reference` exists prior to the execution of the
`model_clause` and is not null when `PRESENTNNV` is evaluated. Otherwise it
returns `expr2`. This function differs from `NVL2` in that `NVL2` evaluates
the data at the time it is executed, rather than evaluating the data as it was
prior to the execution of the `model_clause`.

See Also:

  * [model_clause](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2172805) and "[Model Expressions](Model-Expressions.md#GUID-83D3FD56-8346-4D3F-A49E-5FE41FE19257)" for the syntax and semantics 

  * [NVL2](NVL2.md#GUID-414D6E81-9627-4163-8AC2-BD24E57742AE) for comparison 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the return value of `PRESENTNNV` when it is a character value 

Examples

In the following example, if a row containing sales for the Mouse Pad for the
year 2002 exists, and the sales value is not null, then the sales value
remains unchanged. If the row exists and the sales value is null, then the
sales value is set to 10. If the row does not exist, then the row is created
with the sales value set to 10.

    
    
    SELECT country, prod, year, s
      FROM sales_view_ref
      MODEL
        PARTITION BY (country)
        DIMENSION BY (prod, year)
        MEASURES (sale s)
        IGNORE NAV
        UNIQUE DIMENSION
        RULES UPSERT SEQUENTIAL ORDER
        ( s['Mouse Pad', 2002] = 
            PRESENTNNV(s['Mouse Pad', 2002], s['Mouse Pad', 2002], 10)
        )
      ORDER BY country, prod, year;
    
    COUNTRY       PROD                                         YEAR           S
    ----------    -----------------------------------      --------   ---------
    France        Mouse Pad                                    1998     2509.42
    France        Mouse Pad                                    1999     3678.69
    France        Mouse Pad                                    2000     3000.72
    France        Mouse Pad                                    2001     3269.09
    France        Mouse Pad                                    2002          10
    France        Standard Mouse                               1998     2390.83
    France        Standard Mouse                               1999     2280.45
    France        Standard Mouse                               2000     1274.31
    France        Standard Mouse                               2001     2164.54
    Germany       Mouse Pad                                    1998     5827.87
    Germany       Mouse Pad                                    1999     8346.44
    Germany       Mouse Pad                                    2000     7375.46
    Germany       Mouse Pad                                    2001     9535.08
    Germany       Mouse Pad                                    2002          10
    Germany       Standard Mouse                               1998     7116.11
    Germany       Standard Mouse                               1999     6263.14
    Germany       Standard Mouse                               2000     2637.31
    Germany       Standard Mouse                               2001     6456.13
    
    18 rows selected.
    

The preceding example requires the view `sales_view_ref`. Refer to
"[Examples](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2066378)"
to create this view.


[← Previous](PREDICTION_SET.md)

[Next →](PRESENTV.md)
