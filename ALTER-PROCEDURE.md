[Previous](alter-pmem-filestore.md) [Next](ALTER-PROFILE.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER PROCEDURE 

## ALTER PROCEDURE

Purpose

Packages are defined using PL/SQL. Therefore, this section provides some
general information but refers to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS99997) for details of syntax and semantics.

Use the `ALTER` `PROCEDURE` statement to explicitly recompile a standalone
stored procedure. Explicit recompilation eliminates the need for implicit run-
time recompilation and prevents associated run-time compilation errors and
performance overhead.

To recompile a procedure that is part of a package, recompile the entire
package using the `ALTER` `PACKAGE` statement (see [ALTER PACKAGE](ALTER-
PACKAGE.md#GUID-47471C4C-03AB-4D78-A295-3D58C91102E0)).

Note:

This statement does not change the declaration or definition of an existing
procedure. To redeclare or redefine a procedure, use the `CREATE` `PROCEDURE`
statement with the `OR` `REPLACE` clause (see [CREATE PROCEDURE](CREATE-
PROCEDURE.md#GUID-771879D8-BBFD-4D87-8A6C-290102142DA3)).

The `ALTER` `PROCEDURE` statement is quite similar to the `ALTER` `FUNCTION`
statement. Refer to [ALTER FUNCTION](ALTER-
FUNCTION.md#GUID-6FB32876-2DB3-41EB-B0CA-91B163826AB2) for more information.

Prerequisites

The procedure must be in your own schema or you must have `ALTER` `ANY`
`PROCEDURE` system privilege.

Syntax

alter_procedure::=

![Description of alter_procedure.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_procedure.gif)  
[Description of the illustration
alter_procedure.eps](img_text/alter_procedure.md)

(`procedure_compile_clause`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1891) for the syntax of this clause.)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the procedure. If you omit `schema`, then Oracle
Database assumes the procedure is in your own schema.

procedure_name

Specify the name of the procedure to be recompiled.

procedure_compile_clause

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1891) for the syntax and semantics of this clause
and for complete information on creating and compiling procedures.

EDITIONABLE | NONEDITIONABLE

Use these clauses to specify whether the procedure becomes an editioned or
noneditioned object if editioning is later enabled for the schema object type
`PROCEDURE` in `schema`. The default is `EDITIONABLE`. For information about
altering editioned and noneditioned objects, see [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS1287).


[← Previous](alter-pmem-filestore.md)

[Next →](ALTER-PROFILE.md)
