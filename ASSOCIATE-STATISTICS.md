[Previous](ANALYZE.md) [Next](AUDIT-Traditional-Auditing.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: ALTER SYNONYM to COMMENT](SQL-Statements-ALTER-SYNONYM-to-COMMENT.md)
  3. ASSOCIATE STATISTICS 

## ASSOCIATE STATISTICS

Purpose

Use the `ASSOCIATE` `STATISTICS` statement to associate a statistics type (or
default statistics) containing functions relevant to statistics collection,
selectivity, or cost with one or more columns, standalone functions, packages,
types, domain indexes, or indextypes.

For a listing of all current statistics type associations, query the
`USER_ASSOCIATIONS` data dictionary view. If you analyze the object with which
you are associating statistics, then you can also query the associations in
the `USER_USTATS` view.

See Also:

[ANALYZE](ANALYZE.md#GUID-535CE98E-2359-4147-839F-DCB3772C1B0E) for
information on the order of precedence with which `ANALYZE` uses associations

Prerequisites

To issue this statement, you must have the appropriate privileges to alter the
base object (table, function, package, type, domain index, or indextype). In
addition, unless you are associating only default statistics, you must have
execute privilege on the statistics type. The statistics type must already
have been defined.

See Also:

[CREATE TYPE](CREATE-TYPE.md#GUID-E72E3EE6-DE95-4F58-8941-E2F76D0EAE80) for
information on defining types

Syntax

associate_statistics::=

![Description of associate_statistics.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/associate_statistics.gif)  
[Description of the illustration
associate_statistics.eps](img_text/associate_statistics.md)

column_association::=

![Description of column_association.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/column_association.gif)  
[Description of the illustration
column_association.eps](img_text/column_association.md)

function_association::=

![Description of function_association.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/function_association.gif)  
[Description of the illustration
function_association.eps](img_text/function_association.md)

using_statistics_type::=

![Description of using_statistics_type.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/using_statistics_type.gif)  
[Description of the illustration
using_statistics_type.eps](img_text/using_statistics_type.md)

default_cost_clause::=

![Description of default_cost_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_cost_clause.gif)  
[Description of the illustration
default_cost_clause.eps](img_text/default_cost_clause.md)

default_selectivity_clause::=

![Description of default_selectivity_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_selectivity_clause.gif)  
[Description of the illustration
default_selectivity_clause.eps](img_text/default_selectivity_clause.md)

storage_table_clause::=

![Description of storage_table_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/storage_table_clause.gif)  
[Description of the illustration
storage_table_clause.eps](img_text/storage_table_clause.md)

Semantics

column_association

Specify one or more table columns. If you do not specify `schema`, then Oracle
Database assumes the table is in your own schema.

function_association

Specify one or more standalone functions, packages, user-defined data types,
domain indexes, or indextypes. If you do not specify `schema`, then Oracle
Database assumes the object is in your own schema.

  * `FUNCTIONS` refers only to standalone functions, not to method types or to built-in functions. 

  * `TYPES` refers only to user-defined types, not to built-in SQL data types. 

Restriction on function_association

You cannot specify an object for which you have already defined an
association. You must first disassociate the statistics from this object.

See Also:

[DISASSOCIATE STATISTICS](DISASSOCIATE-
STATISTICS.md#GUID-6E9A7D93-E28A-469D-97AB-2BECC2EF3C43) "[Associating
Statistics: Example](ASSOCIATE-STATISTICS.md#GUID-
BD02BA6A-32A7-4093-A6B6-BAE860C0F834__I2115932)"

using_statistics_type

Specify the statistics type (or a synonym for the type) being associated with
column, function, package, type, domain index, or indextype. The
`statistics_type` must already have been created.

The `NULL` keyword is valid only when you are associating statistics with a
column or an index. When you associate a statistics type with an object type,
columns of that object type inherit the statistics type. Likewise, when you
associate a statistics type with an indextype, index instances of the
indextype inherit the statistics type.You can override this inheritance by
associating a different statistics type for the column or index.
Alternatively, if you do not want to associate any statistics type for the
column or index, then you can specify `NULL` in the `using_statistics_type`
clause.

Restriction on Specifying Statistics Type

You cannot specify `NULL` for functions, packages, types, or indextypes.

See Also:

[Oracle Database Data Cartridge Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADDCI2110) for information on creating statistics
collection functions

default_cost_clause

Specify default costs for standalone functions, packages, types, domain
indexes, or indextypes. If you specify this clause, then you must include one
number each for CPU cost, I/O cost, and network cost, in that order. Each cost
is for a single execution of the function or method or for a single domain
index access. Accepted values are integers of zero or greater.

default_selectivity_clause

Specify as a percent the default selectivity for predicates with standalone
functions, types, packages, or user-defined operators. The
`default_selectivity_clause` must be a number between 0 and 100. Values
outside this range are ignored.

Restriction on the default_selectivity_clause

You cannot specify `DEFAULT` `SELECTIVITY` for domain indexes or indextypes.

See Also:

"[Specifying Default Cost: Example](ASSOCIATE-STATISTICS.md#GUID-
BD02BA6A-32A7-4093-A6B6-BAE860C0F834__I2115948)"

storage_table_clause

This clause is relevant only for statistics on `INDEXTYPE`.

  * Specify `WITH` `SYSTEM` `MANAGED` `STORAGE` `TABLES` to indicate that the storage of statistics data is to be managed by the system. The type you specify in `statistics_type` should be storing the statistics related information in tables that are maintained by the system. Also, the indextype you specify must already have been created or altered to support the `WITH` `SYSTEM` `MANAGED` `STORAGE` `TABLES` clause. 

  * Specify `WITH` `USER` `MANAGED` `STORAGE` `TABLES` to indicate that the tables that store the user-defined statistics will be managed by the user. This is the default behavior. 

Examples

Associating Statistics: Example

This statement creates an association for the standalone package `emp_mgmt`.
See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01378) for the example that creates this package.

    
    
    ASSOCIATE STATISTICS WITH PACKAGES emp_mgmt DEFAULT SELECTIVITY 10;

Specifying Default Cost: Example

This statement specifies that using the domain index `salary_index`, created
in "[Using Extensible Indexing](Using-Extensible-Indexing.md#GUID-
BEAC690B-1FA4-4B31-9B28-FEAF45A01665)", to implement a given predicate always
has a CPU cost of 100, I/O cost of 5, and network cost of 0.

    
    
    ASSOCIATE STATISTICS WITH INDEXES salary_index DEFAULT COST (100,5,0);
    

The optimizer will use these default costs instead of calling a cost function.


[← Previous](ANALYZE.md)

[Next →](AUDIT-Traditional-Auditing.md)
