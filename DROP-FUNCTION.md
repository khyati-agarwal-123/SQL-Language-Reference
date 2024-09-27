[Previous](DROP-FLASHBACK-ARCHIVE.md) [Next](DROP-HIERARCHY.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP FUNCTION 

## DROP FUNCTION

Purpose

Functions are defined using PL/SQL. Refer to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS99993) for complete information on creating,
altering, and dropping functions.

Use the `DROP` `FUNCTION` statement to remove a standalone stored function
from the database.

Note:

Do not use this statement to remove a function that is part of a package.
Instead, either drop the entire package using the `DROP` `PACKAGE` statement
or redefine the package without the function using the `CREATE` `PACKAGE`
statement with the `OR` `REPLACE` clause.

Prerequisites

The function must be in your own schema or you must have the `DROP` `ANY`
`PROCEDURE` system privilege.

Syntax

drop_function::=

![Description of drop_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_function.gif)  
[Description of the illustration
drop_function.eps](img_text/drop_function.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the function. If you omit `schema`, then Oracle
Database assumes the function is in your own schema.

function_name

Specify the name of the function to be dropped.

Oracle Database invalidates any local objects that depend on, or call, the
dropped function. If you subsequently reference one of these objects, then the
database tries to recompile the object and returns an error if you have not
re-created the dropped function.

If any statistics types are associated with the function, then the database
disassociates the statistics types with the `FORCE` option and drops any user-
defined statistics collected with the statistics type.

See Also:

  * [Oracle Database Concepts ](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT1859)for more information on how Oracle Database maintains dependencies among schema objects, including remote objects 

  * [ASSOCIATE STATISTICS](ASSOCIATE-STATISTICS.md#GUID-BD02BA6A-32A7-4093-A6B6-BAE860C0F834) and [DISASSOCIATE STATISTICS](DISASSOCIATE-STATISTICS.md#GUID-6E9A7D93-E28A-469D-97AB-2BECC2EF3C43) for more information on statistics type associations 

Examples

Dropping a Function: Example

The following statement drops the function `SecondMax` in the sample schema
`oe` and invalidates all objects that depend upon `SecondMax`:

    
    
    DROP FUNCTION oe.SecondMax; 

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01377) for the example that creates the `SecondMax`
function


[← Previous](DROP-FLASHBACK-ARCHIVE.md)

[Next →](DROP-HIERARCHY.md)
