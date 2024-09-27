[Previous](create-pmem-filestore.md) [Next](CREATE-PROFILE.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE PROCEDURE 

## CREATE PROCEDURE

Purpose

Procedures are defined using PL/SQL. Therefore, this section provides some
general information but refers to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01373) for details of syntax and semantics.

Use the `CREATE` `PROCEDURE` statement to create a standalone stored procedure
or a call specification.

A procedure is a group of PL/SQL statements that you can call by name. A call
specification (sometimes called call spec) declares a Java method, a
JavaScript method, or a third-generation language (3GL) routine so that it can
be called from SQL and PL/SQL. The call spec tells Oracle Database which Java
method, JavaScript function, or third-generation language (3GL) routine to
invoke when a call is made. It also tells the database what type conversions
to make for the arguments and return value.

Stored procedures offer advantages in the areas of development, integrity,
security, performance, and memory allocation.

See Also:

  * [JavaScript Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MLEJS-GUID-EDC075CA-B50E-45D8-8A72-D060C6DB47DB)

  * [CREATE MLE MODULE](create-mle-module.md#GUID-EF8D8EBC-2313-4C6C-A76E-1A739C304DCC)

  * [CREATE MLE ENV](create-mle-env.md#GUID-419C81FD-338D-495F-85CD-135D4D316718)

  * [Oracle Database Development Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADFNS009) for more information on stored procedures, including how to call stored procedures and for information about registering external procedures. 

  * [CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306) for information specific to functions, which are similar to procedures in many ways. 

  * [CREATE PACKAGE](CREATE-PACKAGE.md#GUID-40636655-899F-47D0-95CA-D58A71C94A56) for information on creating packages. The `CREATE` `PROCEDURE` statement creates a procedure as a standalone schema object. You can also create a procedure as part of a package. 

  * [ALTER PROCEDURE](ALTER-PROCEDURE.md#GUID-24A5796F-7D97-49D4-8448-7E541CB73AC6) and [DROP PROCEDURE](DROP-PROCEDURE.md#GUID-D7F2B5AD-DEEE-466B-B6D3-B765EB897DCB) for information on modifying and dropping a standalone procedure. 

  * [CREATE LIBRARY](CREATE-LIBRARY.md#GUID-F042ABC9-2BF5-4E65-9D52-216D6228B288) for more information about shared libraries. 

Prerequisites

To create or replace a procedure in your own schema, you must have the
`CREATE` `PROCEDURE` system privilege. To create or replace a procedure in
another user's schema, you must have the `CREATE` `ANY` `PROCEDURE` system
privilege.

To invoke a call spec, you may need additional privileges, for example, the
`EXECUTE` object privilege on the C library for a C call spec.

To embed a `CREATE` `PROCEDURE` statement inside an Oracle precompiler
program, you must terminate the statement with the keyword `END-EXEC` followed
by the embedded SQL statement terminator for the specific language.

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS009) or [Oracle Database Java Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=JJDEV13255) for more information

Syntax

Procedures are defined using PL/SQL. Alternatively they can refer to non-
PL/SQL code such as Java, JavaScript, C, and others by means of call
specifications. Therefore, the syntax diagram in this book shows only the SQL
keywords. Refer to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01373) for the PL/SQL syntax, semantics, and
examples.

create_procedure::=

![Description of create_procedure.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_procedure.gif)  
[Description of the illustration
create_procedure.eps](img_text/create_procedure.md)

(`plsql_procedure_source`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1527).)

Semantics

OR REPLACE

Specify `OR` `REPLACE` to re-create the procedure if it already exists. Use
this clause to change the definition of an existing procedure without
dropping, re-creating, and regranting object privileges previously granted on
it. If you redefine a procedure, then Oracle Database recompiles it.

Users who had previously been granted privileges on a redefined procedure can
still access the procedure without being regranted the privileges.

If any function-based indexes depend on the procedure, then Oracle Database
marks the indexes `DISABLED`.

See Also:

[ALTER PROCEDURE](ALTER-
PROCEDURE.md#GUID-24A5796F-7D97-49D4-8448-7E541CB73AC6) for information on
recompiling procedures

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the procedure does not exist, a new procedure is created at the end of the statement.

  * If the procedure exists, this is the procedure you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

[ EDITIONABLE | NONEDITIONABLE ]

Use these clauses to specify whether the procedure is an editioned or
noneditioned object if editioning is enabled for the schema object type
`PROCEDURE` in `schema`. The default is `EDITIONABLE`. For information about
editioned and noneditioned objects, see [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS99923).

plsql_procedure_source

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1527) for the syntax and semantics of the
`plsql_procedure_source`.


[← Previous](create-pmem-filestore.md)

[Next →](CREATE-PROFILE.md)
