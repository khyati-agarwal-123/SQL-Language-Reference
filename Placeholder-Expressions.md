[Previous](Object-Access-Expressions.md) [Next](Scalar-Subquery-
Expressions.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Expressions](Expressions.md)
  3. Placeholder Expressions 

## Placeholder Expressions

A placeholder expression provides a location in a SQL statement for which a
third-generation language bind variable will provide a value. You can specify
the placeholder expression with an optional indicator variable. This form of
expression can appear only in embedded SQL statements or SQL statements
processed in an Oracle Call Interface (OCI) program.

placeholder_expression::=

![Description of placeholder_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/placeholder_expression.gif)  
[Description of the illustration
placeholder_expression.eps](img_text/placeholder_expression.md)

Some valid placeholder expressions are:

    
    
    :employee_name INDICATOR :employee_name_indicator_var
    :department_location 

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation derivation rules for the placeholder expression with a character
data type


[← Previous](Object-Access-Expressions.md)

[Next →](Scalar-Subquery-Expressions.md)
