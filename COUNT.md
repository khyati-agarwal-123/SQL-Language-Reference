[Previous](cosine_distance.md) [Next](COVAR_POP.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. COUNT 

## COUNT

Syntax

![Description of count.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/count.gif)  
[Description of the illustration count.eps](img_text/count.md)

See Also:

[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056) for information on
syntax, semantics, and restrictions

Purpose

`COUNT` returns the number of rows returned by the query. You can use it as an
aggregate or analytic function.

If you specify `DISTINCT`, then you can specify only the
`query_partition_clause` of the `analytic_clause`. The `order_by_clause` and
`windowing_clause` are not allowed.

If you specify `expr`, then `COUNT` returns the number of rows where `expr` is
not null. You can count either all rows, or only distinct values of `expr`.

If you specify the asterisk (*), then this function returns all rows,
including duplicates and nulls. `COUNT` never returns null.

Note:

Before performing a `COUNT` `(DISTINCT` `expr``)`operation on a large amount
of data, consider using one of the following methods to obtain approximate
results more quickly than exact results:

  * Set the `APPROX_FOR_COUNT_DISTINCT` initialization parameter to true before using the `COUNT` `(DISTINCT` `expr``)` function. Refer to [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN-GUID-D2A8A53F-113A-4E6F-AC2E-37139460EF8D) for more information on this parameter. 

  * Use the `APPROX_COUNT_DISTINCT` function instead of the `COUNT` `(DISTINCT` `expr``)` function. Refer to [APPROX_COUNT_DISTINCT](APPROX_COUNT_DISTINCT.md#GUID-50055A05-0187-4481-AFE5-2414F7227713). 

See Also:

  * "[About SQL Expressions](About-SQL-Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)" for information on valid forms of `expr` and [Aggregate Functions](Aggregate-Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules, which define the collation `COUNT` uses to compare character values for the `DISTINCT` clause 

Aggregate Examples

The following examples use `COUNT` as an aggregate function:

    
    
    SELECT COUNT(*) "Total"
      FROM employees;
    
         Total
    ----------
           107
    
    SELECT COUNT(*) "Allstars"
      FROM employees
      WHERE commission_pct > 0;
    
     Allstars
    ---------
           35
    
    SELECT COUNT(commission_pct) "Count"
      FROM employees;
    
         Count
    ----------
            35
    
    SELECT COUNT(DISTINCT manager_id) "Managers"
      FROM employees;
    
      Managers
    ----------
            18

Analytic Example

The following example calculates, for each employee in the `employees` table,
the moving count of employees earning salaries in the range 50 less than
through 150 greater than the employee's salary.

    
    
    SELECT last_name, salary,
           COUNT(*) OVER (ORDER BY salary RANGE BETWEEN 50 PRECEDING AND
                          150 FOLLOWING) AS mov_count
      FROM employees
      ORDER BY salary, last_name;
    
    LAST_NAME                     SALARY  MOV_COUNT
    ------------------------- ---------- ----------
    Olson                           2100          3
    Markle                          2200          2
    Philtanker                      2200          2
    Gee                             2400          8
    Landry                          2400          8
    Colmenares                      2500         10
    Marlow                          2500         10
    Patel                           2500         10
    . . .


[← Previous](cosine_distance.md)

[Next →](COVAR_POP.md)
