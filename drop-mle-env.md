[Previous](DROP-MATERIALIZED-ZONEMAP.md) [Next](drop-mle-module.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP MLE ENV

## DROP MLE ENV

Purpose

Drop an exisiting environment with `DROP MLE ENV`.

Prerequisites

You must have the `DROP ANY MLE` privilege to drop an environment in schemas
other than your own. No privilege is needed to drop an environment in your own
schema.

Syntax

  

![Description of drop_mle_env.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_mle_env.gif)  
[Description of the illustration drop_mle_env.eps](img_text/drop_mle_env.md)

  

Semantics

Specify `IF EXISTS` to drop an existing MLE environment.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

See Also:

  * [CREATE MLE ENV](create-mle-env.md#GUID-419C81FD-338D-495F-85CD-135D4D316718)

  * [ALTER MLE ENV](alter-mle-env.md#GUID-AF0D1253-6FEF-44A7-BEA3-9F24AEFF17C1)

  * [CREATE MLE MODULE](create-mle-module.md#GUID-EF8D8EBC-2313-4C6C-A76E-1A739C304DCC)


[← Previous](DROP-MATERIALIZED-ZONEMAP.md)

[Next →](drop-mle-module.md)
