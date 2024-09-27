[Previous](STDDEV_POP.md) [Next](SUBSTR.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. STDDEV_SAMP 

## STDDEV_SAMP

Syntax

![Description of stddev_samp.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/stddev_samp.gif)  
[Description of the illustration stddev_samp.eps](img_text/stddev_samp.md)

See Also:

"[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)" for information on
syntax, semantics, and restrictions

Purpose

`STDDEV_SAMP` computes the cumulative sample standard deviation and returns
the square root of the sample variance. You can use it as both an aggregate
and analytic function.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. The
function returns the same data type as the numeric data type of the argument.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

This function is same as the square root of the `VAR_SAMP` function. When
`VAR_SAMP` returns null, this function returns null.

See Also:

  * "[Aggregate Functions](Aggregate-Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848)" and [VAR_SAMP](VAR_SAMP.md#GUID-314D5831-0E26-4ABF-9F46-35F78F97DA52)

  * "[About SQL Expressions](About-SQL-Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)" for information on valid forms of `expr`

Aggregate Example

Refer to the aggregate example for
[STDDEV_POP](STDDEV_POP.md#GUID-4F804DE5-7E20-4E08-A1BA-32DBB167B34B).

Analytic Example

The following example returns the sample standard deviation of salaries in the
`employees` table by department:

    
    
    SELECT department_id, last_name, hire_date, salary, 
       STDDEV_SAMP(salary) OVER (PARTITION BY department_id 
          ORDER BY hire_date 
          ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cum_sdev 
       FROM employees
       ORDER BY department_id, last_name, hire_date, salary, cum_sdev;
    
    DEPARTMENT_ID LAST_NAME       HIRE_DATE     SALARY   CUM_SDEV
    ------------- --------------- --------- ---------- ----------
               10 Whalen          17-SEP-03       4400
               20 Fay             17-AUG-05       6000 4949.74747
               20 Hartstein       17-FEB-04      13000
               30 Baida           24-DEC-05       2900 4035.26125
               30 Colmenares      10-AUG-07       2500 3362.58829
               30 Himuro          15-NOV-06       2600  3649.2465
               30 Khoo            18-MAY-03       3100 5586.14357
               30 Raphaely        07-DEC-02      11000
    . . .
              100 Greenberg       17-AUG-02      12008  2126.9772
              100 Popp            07-DEC-07       6900 1804.13155
              100 Sciarra         30-SEP-05       7700 1929.76233
              100 Urman           07-MAR-06       7800 1788.92504
              110 Gietz           07-JUN-02       8300 2621.95194
              110 Higgins         07-JUN-02      12008
                  Grant           24-MAY-07       7000


[← Previous](STDDEV_POP.md)

[Next →](SUBSTR.md)
