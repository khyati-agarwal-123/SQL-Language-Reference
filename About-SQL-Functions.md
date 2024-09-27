[Previous](Functions.md) [Next](Aggregate-Functions.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. About SQL Functions 

## About SQL Functions

SQL functions are built into Oracle Database and are available for use in
various appropriate SQL statements. Do not confuse SQL functions with user-
defined functions written in PL/SQL.

If you call a SQL function with an argument of a data type other than the data
type expected by the SQL function, then Oracle attempts to convert the
argument to the expected data type before performing the SQL function.

See Also:

[About User-Defined Functions](About-User-Defined-
Functions.md#GUID-4EB3E236-8216-471C-BA44-23D87BDFEA67) for information on
user functions and [Data Conversion](Data-Type-Comparison-
Rules.md#GUID-6DB331B5-0F34-4215-9A20-16AEA9D7FF4B) for implicit conversion
of data types

Nulls in SQL Functions

Most scalar functions return null when given a null argument. You can use the
`NVL` function to return a value when a null occurs. For example, the
expression `NVL(commission_pct,0)` returns 0 if `commission_pct` is null or
the value of `commission_pct` if it is not null.

For information on how aggregate functions handle nulls, see [Aggregate
Functions](Aggregate-
Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848).

Syntax for SQL Functions

In the syntax diagrams for SQL functions, arguments are indicated by their
data types. When the parameter `function` appears in SQL syntax, replace it
with one of the functions described in this section. Functions are grouped by
the data types of their arguments and their return values.

Note:

When you apply SQL functions to LOB columns, Oracle Database creates temporary
LOBs during SQL and PL/SQL processing. You should ensure that temporary
tablespace quota is sufficient for storing these temporary LOBs for your
application.

A SQL function may be collation-sensitive, which means that character value
comparison or matching that it performs is controlled by a collation. The
particular collation to use by the function is determined from the collations
of the function's arguments.

If the result of a SQL function has a character data type, the collation
derivation rules define the collation to associate with the result.

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation derivation and determination rules for SQL functions

The syntax showing the categories of functions follows:

function::=

![Description of function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/function.gif)  
[Description of the illustration function.eps](img_text/function.md)

single_row_function::=

![Description of single_row_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/single_row_function.gif)  
[Description of the illustration
single_row_function.eps](img_text/single_row_function.md)

The sections that follow list the built-in SQL functions in each of the groups
illustrated in the preceding diagrams except user-defined functions. All of
the built-in SQL functions are then described in alphabetical order.

See Also:

[About User-Defined Functions](About-User-Defined-
Functions.md#GUID-4EB3E236-8216-471C-BA44-23D87BDFEA67) and [CREATE
FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306)


[← Previous](Functions.md)

[Next →](Aggregate-Functions.md)
