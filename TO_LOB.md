[Previous](TO_DSINTERVAL.md) [Next](TO_MULTI_BYTE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_LOB 

## TO_LOB

Syntax

![Description of to_lob.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_lob.gif)  
[Description of the illustration to_lob.eps](img_text/to_lob.md)

Purpose

Note:

All forms of `LONG` data types (`LONG`, `LONG RAW`, `LONG VARCHAR`, `LONG
VARRAW`) were deprecated in Oracle8i Release 8.1.6. For succeeding releases,
the `LONG` data type was provided for backward compatibility with existing
applications. In new applications developed with later releases, Oracle
strongly recommends that you use `CLOB` and `NCLOB` data types for large
amounts of character data.

`TO_LOB` converts `LONG` or `LONG` RAW values in the column `long_column` to
LOB values. You can apply this function only to a `LONG` or `LONG` `RAW`
column, and only in the select list of a subquery in an `INSERT` statement.

Before using this function, you must create a LOB column to receive the
converted `LONG` values. To convert `LONG` values, create a `CLOB` column. To
convert `LONG` RAW values, create a `BLOB` column.

You cannot use the `TO_LOB` function to convert a `LONG` column to a LOB
column in the subquery of a `CREATE` `TABLE` ... `AS` `SELECT` statement if
you are creating an index-organized table. Instead, create the index-organized
table without the `LONG` column, and then use the `TO_LOB` function in an
`INSERT` ... `AS` `SELECT` statement.

You cannot use this function within a PL/SQL package. Instead use the
`TO_CLOB` (character) or `TO_BLOB` (raw) functions.

See Also:

  * the `modify_col_properties` clause of [ALTER TABLE](ALTER-TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877) for an alternative method of converting `LONG` columns to LOB 

  * [INSERT](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423) for information on the subquery of an `INSERT` statement 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of this function 

Examples

The following syntax shows how to use the `TO_LOB` function on your `LONG`
data in a hypothetical table `old_table`:

    
    
    CREATE TABLE new_table (col1, col2, ... lob_col CLOB);
    INSERT INTO new_table (select o.col1, o.col2, ... TO_LOB(o.old_long_col)
       FROM old_table o;


[← Previous](TO_DSINTERVAL.md)

[Next →](TO_MULTI_BYTE.md)
