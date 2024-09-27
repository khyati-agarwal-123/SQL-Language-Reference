[Previous](DROP-SEQUENCE.md) [Next](SQL-Statements-DROP-TABLE-to-LOCK-
TABLE.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP SYNONYM 

## DROP SYNONYM

Purpose

Use the `DROP` `SYNONYM` statement to remove a synonym from the database or to
change the definition of a synonym by dropping and re-creating it.

See Also:

[CREATE SYNONYM](CREATE-
SYNONYM.md#GUID-A806C82F-1171-478E-A910-F9C6C42739B2) for more information
on synonyms

Prerequisites

To drop a private synonym, either the synonym must be in your own schema or
you must have the `DROP` `ANY` `SYNONYM` system privilege.

To drop a `PUBLIC` synonym, you must have the `DROP` `PUBLIC` `SYNONYM` system
privilege.

Syntax

drop_synonym::=

drop_synonym::=

![Description of drop_synonym.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_synonym.gif)  
[Description of the illustration drop_synonym.eps](img_text/drop_synonym.md)

Semantics

PUBLIC

You must specify `PUBLIC` to drop a public synonym. You cannot specify
`schema` if you have specified `PUBLIC`.

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the synonym. If you omit `schema`, then Oracle
Database assumes the synonym is in your own schema.

synonym

Specify the name of the synonym to be dropped.

If you drop a synonym for the master table of a materialized view, and if the
defining query of the materialized view specified the synonym rather than the
actual table name, then Oracle Database marks the materialized view unusable.

If an object type synonym has any dependent tables or user-defined types, then
you cannot drop the synonym unless you also specify `FORCE`.

FORCE

Specify `FORCE` to drop the synonym even if it has dependent tables or user-
defined types.

Note:

Oracle does not recommend that you specify `FORCE` to drop object type
synonyms with dependencies. This operation can result in invalidation of other
user-defined types or marking `UNUSED` the table columns that depend on the
synonym. For information about type dependencies, see [Oracle Database Object-
Relational Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADOBJ00402).

Examples

Dropping a Synonym: Example

To drop the public synonym named `customers`, which was created in "[Oracle
Database Resolution of Synonyms: Example](CREATE-
SYNONYM.md#GUID-A806C82F-1171-478E-A910-F9C6C42739B2__I2102145)", issue the
following statement:

    
    
    DROP PUBLIC SYNONYM customers; 


[← Previous](DROP-SEQUENCE.md)

[Next →](SQL-Statements-DROP-TABLE-to-LOCK-TABLE.md)
