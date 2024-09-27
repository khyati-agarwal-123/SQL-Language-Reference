[Previous](ALTER-FLASHBACK-ARCHIVE.md) [Next](ALTER-HIERARCHY.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER FUNCTION 

## ALTER FUNCTION

Purpose

Functions are defined using PL/SQL. Therefore, this section provides some
general information but refers to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS99999) for details of syntax and semantics.

Use the `ALTER` `FUNCTION` statement to recompile an invalid standalone stored
function. Explicit recompilation eliminates the need for implicit run-time
recompilation and prevents associated run-time compilation errors and
performance overhead.

This statement does not change the declaration or definition of an existing
function. To redeclare or redefine a function, use the `CREATE` `FUNCTION`
statement with the `OR` `REPLACE` clause. See [CREATE FUNCTION](CREATE-
FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306).

Prerequisites

The function must be in your own schema or you must have `ALTER` `ANY`
`PROCEDURE` system privilege.

Syntax

alter_function::=

![Description of alter_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_function.gif)  
[Description of the illustration
alter_function.eps](img_text/alter_function.md)

(`function_compile_clause`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1872) for the syntax of this clause.)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the function. If you omit `schema`, then Oracle
Database assumes the function is in your own schema.

function_name

Specify the name of the function to be recompiled.

function_compile_clause

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1872) for the syntax and semantics of this clause
and for complete information on creating and compiling functions.

EDITIONABLE | NONEDITIONABLE

Use these clauses to specify whether the function becomes an editioned or
noneditioned object if editioning is later enabled for the schema object type
`FUNCTION` in `schema`. The default is `EDITIONABLE`. For information about
altering editioned and noneditioned objects, see [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS1287).


[← Previous](ALTER-FLASHBACK-ARCHIVE.md)

[Next →](ALTER-HIERARCHY.md)
