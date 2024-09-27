[Previous](ALTER-INDEX.md) [Next](ALTER-INMEMORY-JOIN-GROUP.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER INDEXTYPE 

## ALTER INDEXTYPE

Purpose

Use the `ALTER` `INDEXTYPE` statement to add or drop an operator of the
indextype or to modify the implementation type or change the properties of the
indextype.

Prerequisites

The indextype must be in your own schema or you must have the `ALTER` `ANY`
`INDEXTYPE` system privilege.

To add a new operator, you must have the `EXECUTE` object privilege on the
operator.

To change the implementation type, you must have the `EXECUTE` object
privilege on the new implementation type.

Syntax

alter_indextype::=

  

![Description of alter_indextype1.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_indextype1.eps)  
[Description of the illustration
alter_indextype1.eps](img_text/alter_indextype1.md)

  

([using_type_clause::=](ALTER-INDEXTYPE.md#GUID-
BFA7E29C-7905-4811-9119-B20FD8EA18F2__I2208684), [storage_table_clause](ALTER-
INDEXTYPE.md#GUID-BFA7E29C-7905-4811-9119-B20FD8EA18F2__BABIABHG))

using_type_clause::=

![Description of using_type_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/using_type_clause.gif)  
[Description of the illustration
using_type_clause.eps](img_text/using_type_clause.md)

([array_DML_clause](ALTER-INDEXTYPE.md#GUID-
BFA7E29C-7905-4811-9119-B20FD8EA18F2__BGEBFEFC))

array_DML_clause

![Description of array_dml_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/array_dml_clause.gif)  
[Description of the illustration
array_dml_clause.eps](img_text/array_dml_clause.md)

storage_table_clause

![Description of storage_table_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/storage_table_clause.gif)  
[Description of the illustration
storage_table_clause.eps](img_text/storage_table_clause.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the name of the schema in which the indextype resides. If you omit
`schema`, then Oracle Database assumes the indextype is in your own schema.

indextype

Specify the name of the indextype to be modified.

ADD | DROP

Use the `ADD` or `DROP` clause to add or drop an operator.

No special privilege needed to drop.

  * For `schema`, specify the schema containing the operator. If you omit `schema`, then Oracle assumes the operator is in your own schema. 

  * For `operator`, specify the name of the operator supported by the indextype. 

All the operators listed in this clause must be valid operators.

  * For `parameter_type`, list the types of parameters to the operator. 

using_type_clause

The `USING` clause lets you specify a new type to provide the implementation
for the indextype.

array_DML_clause

Use this clause to modify the indextype to support the array interface for the
`ODCIIndexInsert` method.

type and varray_type

If the data type of the column to be indexed is a user-defined object type,
then you must specify this clause to identify the varray `varray_type` that
Oracle should use to hold column values of `type`. If the indextype supports a
list of types, then you can specify a corresponding list of varray types. If
you omit `schema` for either `type` or `varray_type`, then Oracle assumes the
type is in your own schema.

If the data type of the column to be indexed is a built-in system type, then
any varray type specified for the indextype takes precedence over the ODCI
types defined by the system.

COMPILE

Use this clause to recompile the indextype explicitly. This clause is required
only after some upgrade operations, because Oracle Database normally
recompiles the indextype automatically.

storage_table_clause

This clause has the same behavior when altering an indextype that it has when
you are creating an indextype. Refer to the `CREATE` `INDEXTYPE`
[storage_table_clause](CREATE-
INDEXTYPE.md#GUID-4A7BD0EC-B3E5-4D1D-95C5-C8B52D01D8CE__BABEHBBD) for more
information.

WITH LOCAL PARTITION

This clause has the same behavior when altering an indextype that it has when
you create an indextype. Refer to the `CREATE` `INDEXTYPE` clause [WITH LOCAL
PARTITION](CREATE-
INDEXTYPE.md#GUID-4A7BD0EC-B3E5-4D1D-95C5-C8B52D01D8CE__BABBFIDC) for more
information.

Examples

Altering an Indextype: Example

The following example compiles the `position_indextype` indextype created in
"[Creating an Indextype: Example](CREATE-
INDEXTYPE.md#GUID-4A7BD0EC-B3E5-4D1D-95C5-C8B52D01D8CE__I2169448)".

    
    
    ALTER INDEXTYPE position_indextype COMPILE;


[← Previous](ALTER-INDEX.md)

[Next →](ALTER-INMEMORY-JOIN-GROUP.md)
