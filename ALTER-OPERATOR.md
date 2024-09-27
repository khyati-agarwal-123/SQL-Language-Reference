[Previous](alter-mle-module.md) [Next](ALTER-OUTLINE.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER OPERATOR 

## ALTER OPERATOR

Purpose

Use the `ALTER` `OPERATOR` statement to add bindings to, drop bindings from,
or compile an existing operator.

See Also:

[CREATE OPERATOR](CREATE-
OPERATOR.md#GUID-62676C58-6F57-4572-8C09-7984A8E3EE9F)

Prerequisites

The operator must already have been created by a previous `CREATE` `OPERATOR`
statement. The operator must be in your own schema or you must have the
`ALTER` `ANY` `OPERATOR` system privilege. You must have the `EXECUTE` object
privilege on the operators and functions referenced in the `ALTER` `OPERATOR`
statement.

Syntax

alter_operator::=

![Description of alter_operator.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_operator.gif)  
[Description of the illustration
alter_operator.eps](img_text/alter_operator.md)

([add_binding_clause::=](ALTER-
OPERATOR.md#GUID-F00A0AC8-36C8-4EAC-A9BB-B3D42C5EEEDE__I2295578),
[drop_binding_clause::=](ALTER-
OPERATOR.md#GUID-F00A0AC8-36C8-4EAC-A9BB-B3D42C5EEEDE__I2282008))

add_binding_clause::=

![Description of add_binding_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_binding_clause.gif)  
[Description of the illustration
add_binding_clause.eps](img_text/add_binding_clause.md)

([implementation_clause::=](ALTER-
OPERATOR.md#GUID-F00A0AC8-36C8-4EAC-A9BB-B3D42C5EEEDE__I2282020),
[using_function_clause::=](ALTER-
OPERATOR.md#GUID-F00A0AC8-36C8-4EAC-A9BB-B3D42C5EEEDE__I2282031))

implementation_clause::=

![Description of implementation_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/implementation_clause.gif)  
[Description of the illustration
implementation_clause.eps](img_text/implementation_clause.md)

([context_clause::=](ALTER-
OPERATOR.md#GUID-F00A0AC8-36C8-4EAC-A9BB-B3D42C5EEEDE__I2282043))

context_clause::=

![Description of context_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/context_clause.gif)  
[Description of the illustration
context_clause.eps](img_text/context_clause.md)

using_function_clause::=

![Description of using_function_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/using_function_clause.gif)  
[Description of the illustration
using_function_clause.eps](img_text/using_function_clause.md)

drop_binding_clause::=

![Description of drop_binding_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_binding_clause.gif)  
[Description of the illustration
drop_binding_clause.eps](img_text/drop_binding_clause.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the operator. If you omit this clause, then
Oracle Database assumes the operator is in your own schema.

operator

Specify the name of the operator to be altered.

add_binding_clause

Use this clause to add an operator binding and specify its parameter data
types and return type. The signature must be different from the signature of
any existing binding for this operator.

If a binding of an operator is associated with an indextype and you add
another binding to the operator, then Oracle Database does not automatically
associate the new binding with the indextype. If you want to make such an
association, then you must issue an explicit `ALTER` `INDEXTYPE` ... `ADD`
`OPERATOR` statement.

implementation_clause

This clause has the same semantics in `CREATE` `OPERATOR` and `ALTER`
`OPERATOR` statements. For full information, refer to
[implementation_clause](CREATE-
OPERATOR.md#GUID-62676C58-6F57-4572-8C09-7984A8E3EE9F__I2160229) in the
documentation on `CREATE` `OPERATOR`.

context_clause

This clause has the same semantics in `CREATE` `OPERATOR` and `ALTER`
`OPERATOR` statements. For full information, refer to [context_clause](CREATE-
OPERATOR.md#GUID-62676C58-6F57-4572-8C09-7984A8E3EE9F__I2152088) in the
documentation on `CREATE` `OPERATOR`.

using_function_clause

This clause has the same semantics in `CREATE` `OPERATOR` and `ALTER`
`OPERATOR` statements. For full information, refer to
[using_function_clause](CREATE-
OPERATOR.md#GUID-62676C58-6F57-4572-8C09-7984A8E3EE9F__I2152100) in the
documentation on `CREATE` `OPERATOR`.

drop_binding_clause

Use this clause to specify the list of parameter data types of the binding you
want to drop from the operator. You must specify `FORCE` if the binding has
any dependent objects, such as an indextype or an ancillary operator binding.
If you specify `FORCE`, then Oracle Database marks `INVALID` all objects that
are dependent on the binding. The dependent objects are revalidated the next
time they are referenced in a DDL or DML statement or a query.

You cannot use this clause to drop the only binding associated with this
operator. Instead you must use the `DROP` `OPERATOR` statement. Refer to [DROP
OPERATOR](DROP-OPERATOR.md#GUID-48E60BB4-9490-4B8B-B08E-D17EAEBDDD7E) for
more information.

COMPILE

Specify `COMPILE` to cause Oracle Database to recompile the operator.

Examples

Compiling a User-defined Operator: Example

The following example compiles the operator `eq_op` (which was created in
"[Creating User-Defined Operators: Example](CREATE-
OPERATOR.md#GUID-62676C58-6F57-4572-8C09-7984A8E3EE9F__I2099937)"):

    
    
    ALTER OPERATOR eq_op COMPILE;


[← Previous](alter-mle-module.md)

[Next →](ALTER-OUTLINE.md)
