[Previous](MEDIAN.md) [Next](MOD.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. MIN 

## MIN

Syntax

![Description of min.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/min.gif)  
[Description of the illustration min.eps](img_text/min.md)

See Also:

"[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)" for information on
syntax, semantics, and restrictions

Purpose

`MIN` returns minimum value of `expr`. You can use it as an aggregate or
analytic function.

See Also:

  * "[About SQL Expressions](About-SQL-Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)" for information on valid forms of `expr`, "[Floating-Point Numbers](Data-Types.md#GUID-F579F4B8-EF13-4CAF-9B06-03B076861C41)" for information on binary-float comparison semantics, and "[Aggregate Functions](Aggregate-Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848)"

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules, which define the collation `MIN` uses to compare character values for `expr`, and for the collation derivation rules, which define the collation assigned to the return value of this function when it is a character value 

Aggregate Example

The following statement returns the earliest hire date in the `hr.employees`
table:

    
    
    SELECT MIN(hire_date) "Earliest"
      FROM employees;
     
    Earliest
    ---------
    13-JAN-01

Analytic Example

The following example determines, for each employee, the employees who were
hired on or before the same date as the employee. It then determines the
subset of employees reporting to the same manager as the employee, and returns
the lowest salary in that subset.

    
    
    SELECT manager_id, last_name, hire_date, salary,
           MIN(salary) OVER(PARTITION BY manager_id ORDER BY hire_date
             RANGE UNBOUNDED PRECEDING) AS p_cmin
      FROM employees
      ORDER BY manager_id, last_name, hire_date, salary;
    
    MANAGER_ID LAST_NAME                 HIRE_DATE     SALARY     P_CMIN
    ---------- ------------------------- --------- ---------- ----------
           100 Cambrault                 15-OCT-07      11000       6500
           100 De Haan                   13-JAN-01      17000      17000
           100 Errazuriz                 10-MAR-05      12000       7900
           100 Fripp                     10-APR-05       8200       7900
           100 Hartstein                 17-FEB-04      13000       7900
           100 Kaufling                  01-MAY-03       7900       7900
           100 Kochhar                   21-SEP-05      17000       7900
           100 Mourgos                   16-NOV-07       5800       5800
           100 Partners                  05-JAN-05      13500       7900
           100 Raphaely                  07-DEC-02      11000      11000
           100 Russell                   01-OCT-04      14000       7900
    
    . . .


[← Previous](MEDIAN.md)

[Next →](MOD.md)
