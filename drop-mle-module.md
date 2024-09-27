[Previous](drop-mle-env.md) [Next](DROP-OPERATOR.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP MLE MODULE

## DROP MLE MODULE

Purpose

You can drop a previously deployed MLE module using `DROP MLE MODULE` .

Syntax

  

![Description of drop_mle_module.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_mle_module.gif)  
[Description of the illustration
drop_mle_module.eps](img_text/drop_mle_module.md)

  

Semantics

Specify `IF EXISTS` to drop an existing MLE module.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

`schema` Specify the schema containing the MLE module. If you do not specify
the schema, then Oracle Database assumes that the module is in your own
schema.

`module_name` refers to the module name.

See Also:

  * [CREATE MLE MODULE](create-mle-module.md#GUID-EF8D8EBC-2313-4C6C-A76E-1A739C304DCC)

  * [ALTER MLE MODULE](alter-mle-module.md#GUID-9CE0DFB6-68BE-427D-AEEB-294C0FD31F8F)


[← Previous](drop-mle-env.md)

[Next →](DROP-OPERATOR.md)
