[Previous](drop-mle-module.md) [Next](DROP-OUTLINE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP OPERATOR 

## DROP OPERATOR

Purpose

Use the `DROP` `OPERATOR` statement to drop a user-defined operator.

See Also:

  * [CREATE OPERATOR](CREATE-OPERATOR.md#GUID-62676C58-6F57-4572-8C09-7984A8E3EE9F) and [ALTER OPERATOR](ALTER-OPERATOR.md#GUID-F00A0AC8-36C8-4EAC-A9BB-B3D42C5EEEDE) for information on creating and modifying operators 

  * "[User-Defined Operators](User-Defined-Operators.md#GUID-6025E56E-8429-42E2-B5A6-6048B5D1AF25)" and [Oracle Database Data Cartridge Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADDCI2100) for more information on operators in general 

  * [ALTER INDEXTYPE](ALTER-INDEXTYPE.md#GUID-BFA7E29C-7905-4811-9119-B20FD8EA18F2) for information on dropping an operator of a user-defined indextype 

Prerequisites

The operator must be in your schema or you must have the `DROP` `ANY`
`OPERATOR` system privilege.

Syntax

drop_operator::=

![Description of drop_operator.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_operator.gif)  
[Description of the illustration
drop_operator.eps](img_text/drop_operator.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the operator. If you omit `schema`, then Oracle
Database assumes the operator is in your own schema.

operator

Specify the name of the operator to be dropped.

FORCE

Specify `FORCE` to drop the operator even if it is currently being referenced
by one or more schema objects, such as indextypes, packages, functions,
procedures, and so on. The database marks any such dependent objects
`INVALID`. Without `FORCE`, you cannot drop an operator if any schema objects
reference it.

Examples

Dropping a User-Defined Operator: Example

The following statement drops the operator `eq_op`:

    
    
    DROP OPERATOR eq_op;
    

Because the `FORCE` clause is not specified, this operation will fail if any
of the bindings of this operator are referenced by an indextype.


[← Previous](drop-mle-module.md)

[Next →](DROP-OUTLINE.md)
