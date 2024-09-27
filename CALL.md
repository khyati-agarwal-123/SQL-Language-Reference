[Previous](AUDIT-Unified-Auditing.md) [Next](COMMENT.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: ALTER SYNONYM to COMMENT](SQL-Statements-ALTER-SYNONYM-to-COMMENT.md)
  3. CALL 

## CALL

Purpose

Use the `CALL` statement to execute a routine (a standalone procedure or
function, or a procedure or function defined within a type or package) from
within SQL.

Note:

The restrictions on user-defined function expressions specified in "[Function
Expressions](Function-
Expressions.md#GUID-C47F0B7D-9058-481F-815E-A31FB21F3BD5)" apply to the
`CALL` statement as well.

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS002) for information on creating such routine

Prerequisites

You must have `EXECUTE` privilege on the standalone routine or on the type or
package in which the routine is defined.

Syntax

call::=

![Description of call.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/call.gif)  
[Description of the illustration call.eps](img_text/call.md)

routine_clause::=

![Description of routine_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/routine_clause.gif)  
[Description of the illustration
routine_clause.eps](img_text/routine_clause.md)

object_access_expression::=

![Description of object_access_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/object_access_expression.gif)  
[Description of the illustration
object_access_expression.eps](img_text/object_access_expression.md)

Semantics

You can execute a routine in two ways. You can issue a call to the routine
itself by name, by using the `routine_clause`, or you can invoke a routine
inside the type of an expression, by using an `object_access_expression`.

routine_clause

Specify the name of the function or procedure being called, or a synonym that
resolves to a function or procedure.

When you call a member function or procedure of a type, if the first argument
(`SELF`) is a null `IN` `OUT` argument, then Oracle Database returns an error.
If `SELF` is a null `IN` argument, then the database returns null. In both
cases, the function or procedure is not invoked.

Restriction on Functions

If the routine is a function, then the `INTO` clause is required.

schema

Specify the schema in which the standalone routine, or the package or type
containing the routine, resides. If you do not specify `schema`, then Oracle
Database assumes the routine is in your own schema.

type or package

Specify the type or package in which the routine is defined.

@dblink

In a distributed database system, specify the name of the database containing
the standalone routine, or the package or function containing the routine. If
you omit `dblink`, then Oracle Database looks in your local database.

See Also:

"[Calling a Procedure:
Example](CALL.md#GUID-6CD7B9C4-E5DC-4F3C-9B6A-876AD2C63545__I2119950)" for
an example of calling a routine directly

object_access_expression

If you have an expression of an object type, such as a type constructor or a
bind variable, then you can use this form of expression to call a routine
defined within the type. In this context, the `object_access_expression` is
limited to method invocations.

See Also:

"[Object Access Expressions](Object-Access-Expressions.md#GUID-
FA69A056-12A6-420F-A106-EE252386CC43)" for syntax and semantics of this form
of expression, and "[Calling a Procedure Using an Expression of an Object
Type: Example](CALL.md#GUID-6CD7B9C4-E5DC-4F3C-9B6A-876AD2C63545__I2119934)"
for an example of calling a routine using an expression of an object type

argument

Specify one or more arguments to the routine, if the routine takes arguments.
You can use positional, named, or mixed notation for `argument`. For example,
all of the following notations are correct:

    
    
    CALL my_procedure(arg1 => 3, arg2 => 4) 
    
    
    
    CALL my_procedure(3, 4) 
    
    CALL my_procedure(3, arg2 => 4) 

Restrictions on Applying Arguments to Routines

The `argument` is subject to the following restrictions:

  * The data types of the parameters passed by the `CALL` statement must be SQL data types. They cannot be PL/SQL-only data types such as `BOOLEAN`. 

  * An `argument` cannot be a pseudocolumn or either of the object reference functions `VALUE` or `REF`. 

  * Any `argument` that is an `IN` `OUT` or `OUT` argument of the routine must correspond to a host variable expression. 

  * The number of arguments, including any return argument, is limited to 1000.

  * You cannot bind arguments of character and raw data types (`CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`, `RAW`, `LONG` `RAW`) that are larger than 4K. 

INTO :host_variable

The `INTO` clause applies only to calls to functions. Specify which host
variable will store the return value of the function.

:indicator_variable

Specify the value or condition of the host variable.

See Also:

Pro*C/C++ Programmer's Guide for more information on [host
variables](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPCC3197) and [indicator
variables](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPCC3205)

Examples

Calling a Procedure: Example

The following statement removes the Entertainment department (created in
"[Inserting Sequence Values:
Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2102477)")
using uses the `remove_dept` procedure. See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01381) for the example that creates this procedure.

    
    
    CALL emp_mgmt.remove_dept(162); 

Calling a Procedure Using an Expression of an Object Type: Example

The following examples show how call a procedure by using an expression of an
object type in the `CALL` statement. The example uses the `warehouse_typ`
object type in the order entry sample schema `OE`:

    
    
    ALTER TYPE warehouse_typ
          ADD MEMBER FUNCTION ret_name
          RETURN VARCHAR2
          CASCADE;
    
    CREATE OR REPLACE TYPE BODY warehouse_typ
          AS MEMBER FUNCTION ret_name
          RETURN VARCHAR2
          IS
             BEGIN
                RETURN self.warehouse_name;
             END;
          END;
    /
    VARIABLE x VARCHAR2(25);
    
    CALL warehouse_typ(456, 'Warehouse 456', 2236).ret_name()
       INTO :x;
    
    PRINT x;
    X
    --------------------------------
    Warehouse 456
    

The next example shows how to use an external function to achieve the same
thing:

    
    
    CREATE OR REPLACE FUNCTION ret_warehouse_typ(x warehouse_typ) 
      RETURN warehouse_typ
      IS
        BEGIN
          RETURN x;
        END;
    /
    CALL ret_warehouse_typ(warehouse_typ(234, 'Warehouse 234',
       2235)).ret_name()
       INTO :x;
    
    PRINT x;
    
    X
    --------------------------------
    Warehouse 234


[← Previous](AUDIT-Unified-Auditing.md)

[Next →](COMMENT.md)
