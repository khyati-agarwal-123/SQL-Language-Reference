[Previous](TO_BINARY_FLOAT.md) [Next](TO_BLOB-raw.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_BLOB (bfile) 

## TO_BLOB (bfile)

Syntax

to_blob_bfile::=

![Description of to_blob_bfile.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_blob_bfile.gif)  
[Description of the illustration
to_blob_bfile.eps](img_text/to_blob_bfile.md)

Purpose

`TO_BLOB` (bfile) converts a `BFILE` value to a `BLOB` value.

For `mime_type`, specify the MIME type to be set on the `BLOB` value returned
by this function. If you omit `mime_type`, then a MIME type will not be set on
the `BLOB` value.

Example

The following hypothetical example returns the `BLOB` of a `BFILE` column
value `media_col` in table `media_tab`. It sets the MIME type to `JPEG` on the
resulting `BLOB`.

    
    
    SELECT TO_BLOB(media_col, 'JPEG') FROM media_tab;
    


[← Previous](TO_BINARY_FLOAT.md)

[Next →](TO_BLOB-raw.md)
