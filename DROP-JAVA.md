[Previous](DROP-INMEMORY-JOIN-GROUP.md) [Next](SQL-Statements-DROP-LIBRARY-
to-DROP-SYNONYM.md) JavaScript must be enabled to correctly display this
content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP JAVA 

## DROP JAVA

Purpose

Use the `DROP` `JAVA` statement to drop a Java source, class, or resource
schema object.

See Also:

  * [CREATE JAVA](CREATE-JAVA.md#GUID-69E13452-1F91-4F98-B154-CF5B1C198387) for information on creating Java objects 

  * [Oracle Database Java Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=JJDEV02000) for more information on resolving Java sources, classes, and resources 

Prerequisites

The Java source, class, or resource must be in your own schema or you must
have the `DROP` `ANY` `PROCEDURE` system privilege. You also must have the
`EXECUTE` object privilege on Java classes to use this command.

Syntax

drop_java::=

![Description of drop_java.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_java.gif)  
[Description of the illustration drop_java.eps](img_text/drop_java.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

JAVA SOURCE

Specify `SOURCE` to drop a Java source schema object and all Java class schema
objects derived from it.

JAVA CLASS

Specify `CLASS` to drop a Java class schema object.

JAVA RESOURCE

Specify `RESOURCE` to drop a Java resource schema object.

object_name

Specify the name of an existing Java class, source, or resource schema object.
Enclose the `object_name` in double quotation marks to preserve lower- or
mixed-case names.

Examples

Dropping a Java Class Object: Example

The following statement drops the Java class `Agent`, created in "[Creating a
Java Class Object: Example](CREATE-
JAVA.md#GUID-69E13452-1F91-4F98-B154-CF5B1C198387__BABHIECB)":

    
    
    DROP JAVA CLASS "Agent";


[← Previous](DROP-INMEMORY-JOIN-GROUP.md)

[Next →](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
