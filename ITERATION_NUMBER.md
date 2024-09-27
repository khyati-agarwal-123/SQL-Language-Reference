[Previous](INSTR.md) [Next](JSON_ARRAY.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ITERATION_NUMBER 

## ITERATION_NUMBER

Syntax

![Description of iteration_number.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/iteration_number.gif)  
[Description of the illustration
iteration_number.eps](img_text/iteration_number.md)

Purpose

The `ITERATION_NUMBER` function can be used only in the `model_clause` of the
`SELECT` statement and then only when `ITERATE(``number``)` is specified in
the `model_rules_clause`. It returns an integer representing the completed
iteration through the model rules. The `ITERATION_NUMBER` function returns 0
during the first iteration. For each subsequent iteration, the
`ITERATION_NUMBER` function returns the equivalent of `iteration_number` plus
one.

See Also:

[model_clause](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2172805) and "[Model
Expressions](Model-
Expressions.md#GUID-83D3FD56-8346-4D3F-A49E-5FE41FE19257)" for the syntax
and semantics

Examples

The following example assigns the sales of the Mouse Pad for the years 1998
and 1999 to the sales of the Mouse Pad for the years 2001 and 2002
respectively:

    
    
    SELECT country, prod, year, s
      FROM sales_view_ref
      MODEL
        PARTITION BY (country)
        DIMENSION BY (prod, year)
        MEASURES (sale s)
        IGNORE NAV
        UNIQUE DIMENSION
        RULES UPSERT SEQUENTIAL ORDER ITERATE(2)
          (
            s['Mouse Pad', 2001 + ITERATION_NUMBER] =
              s['Mouse Pad', 1998 + ITERATION_NUMBER]
          )
      ORDER BY country, prod, year;
    
    COUNTRY       PROD                                         YEAR           S
    ----------    -----------------------------------      --------   ---------
    France        Mouse Pad                                    1998     2509.42
    France        Mouse Pad                                    1999     3678.69
    France        Mouse Pad                                    2000     3000.72
    France        Mouse Pad                                    2001     2509.42
    France        Mouse Pad                                    2002     3678.69
    France        Standard Mouse                               1998     2390.83
    France        Standard Mouse                               1999     2280.45
    France        Standard Mouse                               2000     1274.31
    France        Standard Mouse                               2001     2164.54
    Germany       Mouse Pad                                    1998     5827.87
    Germany       Mouse Pad                                    1999     8346.44
    Germany       Mouse Pad                                    2000     7375.46
    Germany       Mouse Pad                                    2001     5827.87
    Germany       Mouse Pad                                    2002     8346.44
    Germany       Standard Mouse                               1998     7116.11
    Germany       Standard Mouse                               1999     6263.14
    Germany       Standard Mouse                               2000     2637.31
    Germany       Standard Mouse                               2001     6456.13
     
    18 rows selected.
    

The preceding example requires the view `sales_view_ref`. Refer to "[The MODEL
clause: Examples](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2171160)" to create this view.


[← Previous](INSTR.md)

[Next →](JSON_ARRAY.md)
