[Previous](physical_attributes_clause.md) [Next](storage_clause.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Common SQL DDL Clauses ](Common-SQL-DDL-Clauses.md)
  3. size_clause 

## size_clause

Purpose

The `size_clause` lets you specify a number of bytes, kilobytes (K), megabytes
(M), gigabytes (G), terabytes (T), petabytes (P), or exabytes (E) in any
statement that lets you establish amounts of disk or memory space.

Syntax

size_clause::=

![Description of size_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/size_clause.gif)  
[Description of the illustration size_clause.eps](img_text/size_clause.md)

Semantics

Use the `size_clause` to specify a number or multiple of bytes. If you do not
specify any of the multiple abbreviations, then the `integer` is interpreted
as bytes.

Note:

Not all multiples of bytes are appropriate in all cases, and context-sensitive
limitations may apply. In the latter case, Oracle issues an error message.


[← Previous](physical_attributes_clause.md)

[Next →](storage_clause.md)
