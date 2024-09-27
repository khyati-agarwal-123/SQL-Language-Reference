[Previous](TO_CLOB-bfile-blob.md) [Next](TO_DATE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_CLOB (character)

## TO_CLOB (character)

Syntax

![Description of to_clob.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_clob.gif)  
[Description of the illustration to_clob.eps](img_text/to_clob.md)

Purpose

`TO_CLOB` (character) converts `NCLOB` values in a LOB column or other
character strings to `CLOB` values. `char` can be any of the data types
`CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`, `CLOB`, or `NCLOB`. Oracle Database
executes this function by converting the underlying LOB data from the national
character set to the database character set.

From within a PL/SQL package, you can use the `TO_CLOB` (character) function
to convert `RAW`, `CHAR`, `VARCHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`, `CLOB`,
or `NCLOB` values to `CLOB` or `NCLOB` values.

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation derivation rules, which define the collation assigned to the
character return value of this function

Examples

The following statement converts `NCLOB` data from the sample `pm.print_media`
table to `CLOB` and inserts it into a `CLOB` column, replacing existing data
in that column.

    
    
    UPDATE PRINT_MEDIA 
       SET AD_FINALTEXT = TO_CLOB (AD_FLTEXTN);


[← Previous](TO_CLOB-bfile-blob.md)

[Next →](TO_DATE.md)
