[Previous](CREATE-FLASHBACK-ARCHIVE.md) [Next](CREATE-HIERARCHY.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE FUNCTION 

## CREATE FUNCTION

Purpose

Functions are defined in PL/SQL. Therefore, this section provides some general
information but refers to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01370) for details of syntax and semantics.

Use the `CREATE` `FUNCTION` statement to create a standalone stored function
or a call specification.

  * A stored function (also called a user function or user-defined function) is a set of PL/SQL statements you can call by name. Stored functions are very similar to procedures, except that a function returns a value to the environment in which it is called. User functions can be used as part of a SQL expression. 

  * A call specification declares a JavaScript method, a Java method or a third-generation language (3GL) routine so that it can be called from PL/SQL. You can also use the `CALL` SQL statement to call such a method or routine. The call specification tells Oracle Database which Java method, JavaScript method, or which named function in which shared library, to invoke when a call is made. It also tells the database what type conversions to make for the arguments and return value. 

Note:

You can also create a function as part of a package using the `CREATE`
`PACKAGE` statement.

See Also:

  * [CREATE PROCEDURE](CREATE-PROCEDURE.md#GUID-771879D8-BBFD-4D87-8A6C-290102142DA3) for a general discussion of procedures and functions, [CREATE PACKAGE](CREATE-PACKAGE.md#GUID-40636655-899F-47D0-95CA-D58A71C94A56) for information on creating packages, [ALTER FUNCTION](ALTER-FUNCTION.md#GUID-6FB32876-2DB3-41EB-B0CA-91B163826AB2) and [DROP FUNCTION](DROP-FUNCTION.md#GUID-5BF63D1C-797E-4FB7-BEAB-B02BD7AADAEF) for information on modifying and dropping a function 

  * [CREATE LIBRARY](CREATE-LIBRARY.md#GUID-F042ABC9-2BF5-4E65-9D52-216D6228B288) for information on shared libraries 

  * [Oracle Database Development Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADFNS010) for more information about registering external functions 

  * [JavaScript Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MLEJS-GUID-EDC075CA-B50E-45D8-8A72-D060C6DB47DB)

  * [CREATE MLE MODULE](create-mle-module.md#GUID-EF8D8EBC-2313-4C6C-A76E-1A739C304DCC)

Prerequisites

To create or replace a function in your own schema, you must have the `CREATE`
`PROCEDURE` system privilege. To create or replace a function in another
user's schema, you must have the `CREATE` `ANY` `PROCEDURE` system privilege.

Syntax

Functions are defined using PL/SQL. Alternatively they can refer to non-PL/SQL
code such as Java, JavaScript, C, and others by means of call specifications.
Therefore, the syntax diagram in this book shows only the SQL keywords. Refer
to Oracle Database PL/SQL Language Reference for the PL/SQL syntax, semantics,
and examples.

create_function::=

![Description of create_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_function.gif)  
[Description of the illustration
create_function.eps](img_text/create_function.md)

(`plsql_function_source`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS2178).)

Semantics

OR REPLACE

Specify `OR` `REPLACE` to re-create the function if it already exists. Use
this clause to change the definition of an existing function without dropping,
re-creating, and regranting object privileges previously granted on the
function. If you redefine a function, then Oracle Database recompiles it.

Users who had previously been granted privileges on a redefined function can
still access the function without being regranted the privileges.

If any function-based indexes depend on the function, then Oracle Database
marks the indexes `DISABLED`.

See Also:

[`ALTER` `FUNCTION`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SQLRF00804) for information on recompiling functions
using SQL

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the function does not exist, a new function is created at the end of the statement.

  * If the function exists, this is the function you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

[ EDITIONABLE | NONEDITIONABLE ]

Use these clauses to specify whether the function is an editioned or
noneditioned object if editioning is enabled for the schema object type
`FUNCTION` in `schema`. The default is `EDITIONABLE`. For information about
editioned and noneditioned objects, see [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS99923).

plsql_function_source

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS2178) for the syntax and semantics of the
`plsql_function_source`, including examples.


[← Previous](CREATE-FLASHBACK-ARCHIVE.md)

[Next →](CREATE-HIERARCHY.md)
