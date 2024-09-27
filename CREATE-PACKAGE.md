[Previous](CREATE-OUTLINE.md) [Next](CREATE-PACKAGE-BODY.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE PACKAGE 

## CREATE PACKAGE

Purpose

Packages are defined using PL/SQL. Therefore, this section provides some
general information but refers to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01371) for details of syntax and semantics.

Use the `CREATE` `PACKAGE` statement to create the specification for a stored
package, which is an encapsulated collection of related procedures, functions,
and other program objects stored together in the database. The package
specification declares these objects. The package body, specified
subsequently, defines these objects.

See Also:

  * [CREATE PACKAGE BODY](CREATE-PACKAGE-BODY.md#GUID-E571E5A3-1C4B-4246-BF26-0E4348BEB6D6) for information on specifying the implementation of the package 

  * [CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306) and [CREATE PROCEDURE](CREATE-PROCEDURE.md#GUID-771879D8-BBFD-4D87-8A6C-290102142DA3) for information on creating standalone functions and procedures 

  * [ALTER PACKAGE](ALTER-PACKAGE.md#GUID-47471C4C-03AB-4D78-A295-3D58C91102E0) and [DROP PACKAGE](DROP-PACKAGE.md#GUID-FAE96214-2ED0-4130-8ACA-A077C7A90B23) for information on modifying and dropping a package 

  * [Oracle Database Development Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADFNS009) and [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS139) for detailed discussions of packages and how to use them 

Prerequisites

To create or replace a package in your own schema, you must have the `CREATE`
`PROCEDURE` system privilege. To create or replace a package in another user's
schema, you must have the `CREATE` `ANY` `PROCEDURE` system privilege.

To embed a `CREATE` `PACKAGE` statement inside an Oracle Database precompiler
program, you must terminate the statement with the keyword `END-EXEC` followed
by the embedded SQL statement terminator for the specific language.

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01371) for more information

Syntax

Packages are defined using PL/SQL. Therefore, the syntax diagram in this book
shows only the SQL keywords. Refer to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01371) for the PL/SQL syntax, semantics, and
examples.

create_package::=

![Description of create_package.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_package.gif)  
[Description of the illustration
create_package.eps](img_text/create_package.md)

(`plsql_package_source`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS2180).)

Semantics

OR REPLACE

Specify `OR` `REPLACE` to re-create the package specification if it already
exists. Use this clause to change the specification of an existing package
without dropping, re-creating, and regranting object privileges previously
granted on the package. If you change a package specification, then Oracle
Database recompiles it.

Users who had previously been granted privileges on a redefined package can
still access the package without being regranted the privileges.

If any function-based indexes depend on the package, then the database marks
the indexes `DISABLED`.

See Also:

[`ALTER` `PACKAGE`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SQLRF00811) for information on recompiling package
specifications

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the package does not exist, a new package is created at the end of the statement.

  * If the package exists, this is the package you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

[ EDITIONABLE | NONEDITIONABLE ]

Use these clauses to specify whether the package is an editioned or
noneditioned object if editioning is enabled for the schema object type
`PACKAGE` in `schema`. The default is `EDITIONABLE`. For information about
editioned and noneditioned objects, see [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS99923).

plsql_package_source

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS2180) for the syntax and semantics of the
`plsql_package_source`, including examples.


[← Previous](CREATE-OUTLINE.md)

[Next →](CREATE-PACKAGE-BODY.md)
