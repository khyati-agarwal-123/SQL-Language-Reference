[Previous](create-mle-module.md) [Next](CREATE-OUTLINE.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE OPERATOR 

## CREATE OPERATOR

Purpose

Use the `CREATE` `OPERATOR` statement to create a new operator and define its
bindings.

Operators can be referenced by indextypes and by SQL queries and DML
statements. The operators, in turn, reference functions, packages, types, and
other user-defined objects.

See Also:

[Oracle Database Data Cartridge Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADDCI2100) and [Oracle Database
Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=CNCPT1859) for a discussion of these dependencies and of
operators in general

Prerequisites

To create an operator in your own schema, you must have the `CREATE`
`OPERATOR` system privilege. To create an operator in another schema, you must
have the `CREATE` `ANY` `OPERATOR` system privilege. In either case, you must
also have the `EXECUTE` object privilege on the functions and operators
referenced.

Syntax

create_operator::=

![Description of create_operator.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_operator.gif)  
[Description of the illustration
create_operator.eps](img_text/create_operator.md)

binding_clause::=

![Description of binding_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/binding_clause.gif)  
[Description of the illustration
binding_clause.eps](img_text/binding_clause.md)

implementation_clause::=

![Description of implementation_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/implementation_clause.gif)  
[Description of the illustration
implementation_clause.eps](img_text/implementation_clause.md)

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

Semantics

OR REPLACE

Specify `OR` `REPLACE` to replace the definition of the operator schema
object.

Restriction on Replacing an Operator

You can replace the definition only if the operator has no dependent objects,
such as indextypes supporting the operator.

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the operator does not exist, a new operator is created at the end of the statement.

  * If the operator exists, this is the operator you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

schema

Specify the schema containing the operator. If you omit `schema`, then the
database creates the operator in your own schema.

operator

Specify the name of the operator to be created. The name must satisfy the
requirements listed in "[Database Object Naming Rules](Database-Object-Names-
and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

binding_clause

Use the `binding_clause` to specify one or more parameter data types
(`parameter_type`) for binding the operator to a function. The signature of
each bindingâthe sequence of the data types of the arguments to the
corresponding functionâmust be unique according to the rules of overloading.

The `parameter_type` can itself be an object type. If it is, then you can
optionally qualify it with its schema.

Restriction on Binding Operators

You cannot specify a `parameter_type` of `REF`, `LONG`, or `LONG` `RAW`.

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS00807) for more information about overloading

RETURN Clause

Specify the return data type for the binding.

The `return_type` can itself be an object type. If so, then you can optionally
qualify it with its schema.

Restriction on Binding Return Data Type

You cannot specify a `return_type` of `REF`, `LONG`, or `LONG` `RAW`.

SHARING

Use the sharing clause if you want to create the object in an application root
in the context of an application maintenance. This type of object is called an
application common object and it can be shared with the application PDBs that
belong to the application root.

You can specify how the object is shared using one of the following sharing
attributes:

  * `METADATA` \- A metadata link shares the metadata, but its data is unique to each container. This type of object is referred to as a metadata-linked application common object. 

  * `NONE` \- The object is not shared and can only be accessed in the application root. 

implementation_clause

Use this clause to describe the implementation of the binding.

ANCILLARY TO Clause

Use the `ANCILLARY` `TO` clause to indicate that the operator binding is
ancillary to the specified primary operator binding (`primary_operator`). If
you specify this clause, then do not specify a previous binding with just one
number parameter.

context_clause

Use the `context_clause` to describe the functional implementation of a
binding that is not ancillary to a primary operator binding.

WITH INDEX CONTEXT, SCAN CONTEXT

Use this clause to indicate that the functional evaluation of the operator
uses the index and a scan context that is specified by the implementation
type.

COMPUTE ANCILLARY DATA

Specify `COMPUTE` `ANCILLARY` `DATA` to indicate that the operator binding
computes ancillary data.

WITH COLUMN CONTEXT

Specify `WITH` `COLUMN` `CONTEXT` to indicate that Oracle Database should pass
the column information to the functional implementation for the operator.

If you specify this clause, then the signature of the function implemented
must include one extra `ODCIFuncCallInfo` structure.

See Also:

[Oracle Database Data Cartridge Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADDCI024) for instructions on using the
`ODCIFuncCallInfo` routine

using_function_clause

The `using_function_clause` lets you specify the function that provides the
implementation for the binding. The `function_name` can be a standalone
function, packaged function, type method, or a synonym for any of these.

If the function is subsequently dropped, then the database marks all dependent
objects `INVALID`, including the operator. However, if you then subsequently
issue an `ALTER` `OPERATOR` ... `DROP` `BINDING` statement to drop the
binding, then subsequent queries and DML will revalidate the dependent
objects.

Examples

Creating User-Defined Operators: Example

This example creates a very simple functional implementation of equality and
then creates an operator that uses the function. For a more complete set of
examples, see [Oracle Database Data Cartridge Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADDCI2100).

    
    
    CREATE FUNCTION eq_f(a VARCHAR2, b VARCHAR2) RETURN NUMBER AS
    BEGIN
       IF a = b THEN RETURN 1;
       ELSE RETURN 0;
       END IF;
    END;
    /
    
    CREATE OPERATOR eq_op
       BINDING (VARCHAR2, VARCHAR2) 
       RETURN NUMBER 
       USING eq_f; 


[← Previous](create-mle-module.md)

[Next →](CREATE-OUTLINE.md)
