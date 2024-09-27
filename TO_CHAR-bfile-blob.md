[Previous](to_boolean.md) [Next](to_char-boolean.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_CHAR (bfile|blob) 

## TO_CHAR (bfile|blob)

Syntax

to_char_bfile_blob::=

![Description of to_char_bfile_blob.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_char_bfile_blob.gif)  
[Description of the illustration
to_char_bfile_blob.eps](img_text/to_char_bfile_blob.md)

Purpose

`TO_CHAR` (bfile|blob) converts `BFILE` or `BLOB` data to the database
character set. The value returned is always `VARCHAR2`. If the value returned
is too large to fit into the `VARCHAR2` data type, then the data is truncated.

For `csid`, specify the character set ID of the `BFILE` or `BLOB` data. If the
character set of the `BFILE` or `BLOB` data is the database character set,
then you can specify a value of 0 for `csid`, or omit `csid` altogether.

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation derivation rules, which define the collation assigned to the
character return value of this function

Example

The following hypothetical example takes as its input a `BFILE` column
`media_col` in table `media_tab`, which uses the character set with ID 873.
The example returns a `VARCHAR2` value that uses the database character set.

    
    
    SELECT TO_CHAR(media_col, 873) FROM media_tab;
    


[← Previous](to_boolean.md)

[Next →](to_char-boolean.md)
