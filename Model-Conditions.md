[Previous](Logical-Conditions.md) [Next](Multiset-Conditions.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Conditions](Conditions.md)
  3. Model Conditions 

## Model Conditions

Model conditions can be used only in the `MODEL` clause of a `SELECT`
statement.

### IS ANY Condition

The `IS` `ANY` condition can be used only in the `model_clause` of a `SELECT`
statement. Use this condition to qualify all values of a dimension column,
including `NULL`.

is_any_condition::=

![Description of is_any_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/is_any_condition.gif)  
[Description of the illustration
is_any_condition.eps](img_text/is_any_condition.md)

The condition always returns a Boolean value of `TRUE` in order to qualify all
values of the column.

See Also:

[model_clause](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2172805) and [Model Expressions](Model-
Expressions.md#GUID-83D3FD56-8346-4D3F-A49E-5FE41FE19257) for information

Example

The following example sets sales for each product for year 2000 to 0:

    
    
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
          s[ANY, 2000] = 0
        )
      ORDER BY country, prod, year;
    
    COUNTRY       PROD                                         YEAR           S
    ----------    -----------------------------------      --------   ---------
    France        Mouse Pad                                    1998     2509.42
    France        Mouse Pad                                    1999     3678.69
    France        Mouse Pad                                    2000           0
    France        Mouse Pad                                    2001     3269.09
    France        Standard Mouse                               1998     2390.83
    France        Standard Mouse                               1999     2280.45
    France        Standard Mouse                               2000           0
    France        Standard Mouse                               2001     2164.54
    Germany       Mouse Pad                                    1998     5827.87
    Germany       Mouse Pad                                    1999     8346.44
    Germany       Mouse Pad                                    2000           0
    Germany       Mouse Pad                                    2001     9535.08
    Germany       Standard Mouse                               1998     7116.11
    Germany       Standard Mouse                               1999     6263.14
    Germany       Standard Mouse                               2000           0
    Germany       Standard Mouse                               2001     6456.13
     
    16 rows selected.
    

The preceding example requires the view `sales_view_ref`. Refer to [The MODEL
clause: Examples](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2171160) to create this view.

### IS PRESENT Condition

is_present_condition::=

The `IS` `PRESENT` condition can be used only in the `model_clause` of a
`SELECT` statement. Use this condition to test whether the cell referenced is
present prior to the execution of the `model_clause`.

![Description of is_present_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/is_present_condition.gif)  
[Description of the illustration
is_present_condition.eps](img_text/is_present_condition.md)

The condition returns `TRUE` if the cell exists prior to the execution of the
`model_clause` and `FALSE` if it does not.

See Also:

[model_clause](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2172805) and [Model Expressions](Model-
Expressions.md#GUID-83D3FD56-8346-4D3F-A49E-5FE41FE19257) for information

Example

In the following example, if sales of the Mouse Pad for year 1999 exist, then
sales of the Mouse Pad for year 2000 is set to sales of the Mouse Pad for year
1999. Otherwise, sales of the Mouse Pad for year 2000 is set to 0.

    
    
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
          s['Mouse Pad', 2000] =
            CASE WHEN s['Mouse Pad', 1999] IS PRESENT
                 THEN s['Mouse Pad', 1999]
                 ELSE 0
            END
        )
      ORDER BY country, prod, year;
    
    COUNTRY       PROD                                         YEAR           S
    ----------    -----------------------------------      --------   ---------
    France        Mouse Pad                                    1998     2509.42
    France        Mouse Pad                                    1999     3678.69
    France        Mouse Pad                                    2000     3678.69
    France        Mouse Pad                                    2001     3269.09
    France        Standard Mouse                               1998     2390.83
    France        Standard Mouse                               1999     2280.45
    France        Standard Mouse                               2000     1274.31
    France        Standard Mouse                               2001     2164.54
    Germany       Mouse Pad                                    1998     5827.87
    Germany       Mouse Pad                                    1999     8346.44
    Germany       Mouse Pad                                    2000     8346.44
    Germany       Mouse Pad                                    2001     9535.08
    Germany       Standard Mouse                               1998     7116.11
    Germany       Standard Mouse                               1999     6263.14
    Germany       Standard Mouse                               2000     2637.31
    Germany       Standard Mouse                               2001     6456.13
    16 rows selected.
    

The preceding example requires the view `sales_view_ref`. Refer to [The MODEL
clause: Examples](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2171160) to create this view.


[← Previous](Model-Conditions.md)

[Next →](Multiset-Conditions.md)
