[Previous](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md) [Next](DROP-
LOCKDOWN-PROFILE.md) JavaScript must be enabled to correctly display this
content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP LIBRARY 

## DROP LIBRARY

Purpose

Use the `DROP` `LIBRARY` statement to remove an external procedure library
from the database.

See Also:

[CREATE LIBRARY](CREATE-
LIBRARY.md#GUID-F042ABC9-2BF5-4E65-9D52-216D6228B288) for information on
creating a library

Prerequisites

You must have the `DROP` `ANY` `LIBRARY` system privilege.

Syntax

drop_library::=

![Description of drop_library.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_library.gif)  
[Description of the illustration drop_library.eps](img_text/drop_library.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

library_name

Specify the name of the external procedure library being dropped.

Examples

Dropping a Library: Example

The following statement drops the `ext_lib` library:

    
    
    DROP LIBRARY ext_lib;


[← Previous](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)

[Next →](DROP-LOCKDOWN-PROFILE.md)
