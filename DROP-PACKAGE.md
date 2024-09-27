[Previous](DROP-OUTLINE.md) [Next](DROP-PLUGGABLE-DATABASE.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP PACKAGE 

## DROP PACKAGE

Purpose

Packages are defined using PL/SQL. Refer to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS99992) for complete information on creating,
altering, and dropping packages.

Use the `DROP` `PACKAGE` statement to remove a stored package from the
database. This statement drops the body and specification of a package.

Note:

Do not use this statement to remove a single object from a package. Instead,
re-create the package without the object using the `CREATE` `PACKAGE` and
`CREATE` `PACKAGE` `BODY` statements with the `OR` `REPLACE` clause.

Prerequisites

The package must be in your own schema or you must have the `DROP` `ANY`
`PROCEDURE` system privilege.

Syntax

drop_package::=

![Description of drop_package.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_package.gif)  
[Description of the illustration drop_package.eps](img_text/drop_package.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

BODY

Specify `BODY` to drop only the body of the package. If you omit this clause,
then Oracle Database drops both the body and specification of the package.

When you drop only the body of a package but not its specification, the
database does not invalidate dependent objects. However, you cannot call one
of the procedures or stored functions declared in the package specification
until you re-create the package body.

schema

Specify the schema containing the package. If you omit `schema`, then the
database assumes the package is in your own schema.

package

Specify the name of the package to be dropped.

Oracle Database invalidates any local objects that depend on the package
specification. If you subsequently reference one of these objects, then the
database tries to recompile the object and returns an error if you have not
re-created the dropped package.

If any statistics types are associated with the package, then the database
disassociates the statistics types with the `FORCE` clause and drops any user-
defined statistics collected with the statistics types.

See Also:

[ASSOCIATE STATISTICS](ASSOCIATE-STATISTICS.md#GUID-
BD02BA6A-32A7-4093-A6B6-BAE860C0F834) and [DISASSOCIATE
STATISTICS](DISASSOCIATE-
STATISTICS.md#GUID-6E9A7D93-E28A-469D-97AB-2BECC2EF3C43)

Examples

Dropping a Package: Example

The following statement drops the specification and body of the `emp_mgmt`
package, invalidating all objects that depend on the specification. See
[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01381) for the example that creates this package.

    
    
    DROP PACKAGE emp_mgmt; 


[← Previous](DROP-OUTLINE.md)

[Next →](DROP-PLUGGABLE-DATABASE.md)
