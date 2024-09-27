[Previous](TO_BLOB-bfile.md) [Next](to_boolean.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_BLOB (raw)

## TO_BLOB (raw)

Syntax

to_blob::=

![Description of to_blob.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_blob.gif)  
[Description of the illustration to_blob.eps](img_text/to_blob.md)

Purpose

Note:

All forms of `LONG` data types (`LONG`, `LONG RAW`, `LONG VARCHAR`, `LONG
VARRAW`) were deprecated in Oracle8i Release 8.1.6. For succeeding releases,
the `LONG` data type was provided for backward compatibility with existing
applications. In new applications developed with later releases, Oracle
strongly recommends that you use `CLOB` and `NCLOB` data types for large
amounts of character data.

`TO_BLOB` (raw) converts `LONG` `RAW` and `RAW` values to `BLOB` values.

From within a PL/SQL package, you can use `TO_BLOB` (raw) to convert `RAW` and
`BLOB` values to `BLOB`.

Examples

The following hypothetical example returns the `BLOB` of a `RAW` column value:

    
    
    SELECT TO_BLOB(raw_column) blob FROM raw_table;
    
    BLOB
    -----------------------
    00AADD343CDBBD


[← Previous](TO_BLOB-bfile.md)

[Next →](to_boolean.md)
