##  TO_BLOB (bfile) {#GUID-232A1599-53C9-464B-904F-4DBA336B4EBC} 

Syntax 

*to_blob_bfile* ::= 

![Description of to_blob_bfile.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_blob_bfile.gif)[ Description of the illustration to_blob_bfile.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/to_blob_bfile.md)

Purpose 

` TO_BLOB ` (bfile) converts a ` BFILE ` value to a ` BLOB ` value. 

For *mime_type* , specify the MIME type to be set on the ` BLOB ` value returned by this function. If you omit *mime_type* , then a MIME type will not be set on the ` BLOB ` value. 

Example 

The following hypothetical example returns the ` BLOB ` of a ` BFILE ` column value ` media_col ` in table ` media_tab ` . It sets the MIME type to ` JPEG ` on the resulting ` BLOB ` . 
    
    
    ```
    SELECT TO_BLOB(media_col, 'JPEG') FROM media_tab;
    
    ```
