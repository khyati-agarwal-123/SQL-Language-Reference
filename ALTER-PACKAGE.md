[Previous](ALTER-OUTLINE.md) [Next](ALTER-PLUGGABLE-DATABASE.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER PACKAGE 

## ALTER PACKAGE

Purpose

Packages are defined using PL/SQL. Therefore, this section provides some
general information but refers to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01371) for details of syntax and semantics.

Use the `ALTER` `PACKAGE` statement to explicitly recompile a package
specification, body, or both. Explicit recompilation eliminates the need for
implicit run-time recompilation and prevents associated run-time compilation
errors and performance overhead.

Because all objects in a package are stored as a unit, the `ALTER` `PACKAGE`
statement recompiles all package objects together. You cannot use the `ALTER`
`PROCEDURE` statement or `ALTER` `FUNCTION` statement to recompile
individually a procedure or function that is part of a package.

Note:

This statement does not change the declaration or definition of an existing
package. To redeclare or redefine a package, use the [CREATE PACKAGE](CREATE-
PACKAGE.md#GUID-40636655-899F-47D0-95CA-D58A71C94A56) or the [CREATE PACKAGE
BODY](CREATE-PACKAGE-BODY.md#GUID-E571E5A3-1C4B-4246-BF26-0E4348BEB6D6)
statement with the `OR` `REPLACE` clause.

Prerequisites

For you to modify a package, the package must be in your own schema or you
must have `ALTER` `ANY` `PROCEDURE` system privilege.

Syntax

alter_package::=

![Description of alter_package.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_package.gif)  
[Description of the illustration
alter_package.eps](img_text/alter_package.md)

(`package_compile_clause`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1887) for the syntax of this clause.)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the package. If you omit `schema`, then Oracle
Database assumes the package is in your own schema.

package_name

Specify the name of the package to be recompiled.

package_compile_clause

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1887) for the syntax and semantics of this clause
and for complete information on creating and compiling packages.

EDITIONABLE | NONEDITIONABLE

Use these clauses to specify whether the package becomes an editioned or
noneditioned object if editioning is later enabled for the schema object type
`PACKAGE` in `schema`. The default is `EDITIONABLE`. For information about
altering editioned and noneditioned objects, see [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS1287).


[← Previous](ALTER-OUTLINE.md)

[Next →](ALTER-PLUGGABLE-DATABASE.md)
