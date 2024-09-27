[Previous](ALTER-INMEMORY-JOIN-GROUP.md) [Next](SQL-Statements-ALTER-
LIBRARY-to-ALTER-SESSION.md) JavaScript must be enabled to correctly display
this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER JAVA 

## ALTER JAVA

Purpose

Use the `ALTER` `JAVA` statement to force the resolution of a Java class
schema object or compilation of a Java source schema object. (You cannot call
the methods of a Java class before all its external references to Java names
are associated with other classes.)

See Also:

[Oracle Database Java Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=JJDEV02000) for more information on resolving Java
classes and compiling Java sources

Prerequisites

The Java source or class must be in your own schema, or you must have the
`ALTER` `ANY` `PROCEDURE` system privilege. You must also have the `EXECUTE`
object privilege on Java classes.

Syntax

alter_java::=

![Description of alter_java.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_java.gif)  
[Description of the illustration alter_java.eps](img_text/alter_java.md)

([invoker_rights_clause::=](ALTER-
JAVA.md#GUID-6B211750-3247-4D71-9533-3DD8F66640CD__I2208708))

invoker_rights_clause::=

![Description of invoker_rights_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/invoker_rights_clause.gif)  
[Description of the illustration
invoker_rights_clause.eps](img_text/invoker_rights_clause.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

JAVA SOURCE

Use `ALTER` `JAVA` `SOURCE` to compile a Java source schema object.

JAVA CLASS

Use `ALTER` `JAVA` `CLASS` to resolve a Java class schema object.

object_name

Specify a previously created Java class or source schema object. Use double
quotation marks to preserve lower- or mixed-case names.

RESOLVER

The `RESOLVER` clause lets you specify how schemas are searched for referenced
fully specified Java names, using the mapping pairs specified when the Java
class or source was created.

See Also:

[CREATE JAVA](CREATE-JAVA.md#GUID-69E13452-1F91-4F98-B154-CF5B1C198387) and
"[Resolving a Java Class: Example](ALTER-
JAVA.md#GUID-6B211750-3247-4D71-9533-3DD8F66640CD__I2136137)"

RESOLVE | COMPILE

`RESOLVE` and `COMPILE` are synonymous keywords. They let you specify that
Oracle Database should attempt to resolve the primary Java class schema
object.

  * When applied to a class, resolution of referenced names to other class schema objects occurs. 

  * When applied to a source, source compilation occurs.

invoker_rights_clause

The `invoker_rights_clause` lets you specify whether the methods of the class
execute with the privileges and in the schema of the user who defined it or
with the privileges and in the schema of `CURRENT_USER`.

This clause also determines how Oracle Database resolves external names in
queries, DML operations, and dynamic SQL statements in the member functions
and procedures of the type.

AUTHID CURRENT_USER

Specify `CURRENT_USER` if you want the methods of the class to execute with
the privileges of `CURRENT_USER`. This clause is the default and creates an
invoker-rights class.

This clause also specifies that external names in queries, DML operations, and
dynamic SQL statements resolve in the schema of `CURRENT_USER`. External names
in all other statements resolve in the schema in which the methods reside.

AUTHID DEFINER

Specify `DEFINER` if you want the methods of the class to execute with the
privileges of the user who defined the class.

This clause also specifies that external names resolve in the schema where the
methods reside.

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS008) for information on how `CURRENT_USER` is
determined

Examples

Resolving a Java Class: Example

The following statement forces the resolution of a Java class:

    
    
    ALTER JAVA CLASS "Agent"
       RESOLVER (("/usr/bin/bfile_dir/*" pm)(* public))
       RESOLVE;


[← Previous](ALTER-INMEMORY-JOIN-GROUP.md)

[Next →](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
