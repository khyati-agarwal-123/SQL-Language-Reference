[Previous](AVG.md) [Next](BIN_TO_NUM.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. BFILENAME 

## BFILENAME

Syntax

![Description of bfilename.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/bfilename.gif)  
[Description of the illustration bfilename.eps](img_text/bfilename.md)

Purpose

`BFILENAME` returns a `BFILE` locator that is associated with a physical LOB
binary file on the server file system.

  * '`directory`' is a database object that serves as an alias for a full path name on the server file system where the files are actually located. 

  * '`filename`' is the name of the file in the server file system. 

You must create the directory object and associate a `BFILE` value with a
physical file before you can use them as arguments to `BFILENAME` in a SQL or
PL/SQL statement, `DBMS_LOB` package, or OCI operation.

You can use this function in two ways:

  * In a DML statement to initialize a `BFILE` column 

  * In a programmatic interface to access `BFILE` data by assigning a value to the `BFILE` locator 

The directory argument is case sensitive. You must ensure that you specify the
directory object name exactly as it exists in the data dictionary. For
example, if an `"Admin"` directory object was created using mixed case and a
quoted identifier in the `CREATE` `DIRECTORY` statement, then when using the
`BFILENAME` function you must refer to the directory object as `'Admin'`. You
must specify the filename argument according to the case and punctuation
conventions for your operating system.

See Also:

  * [Oracle Database SecureFiles and Large Objects Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADLOB012) and [Oracle Call Interface Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNOCI030) for more information on LOBs and for examples of retrieving `BFILE` data 

  * [CREATE DIRECTORY](CREATE-DIRECTORY.md#GUID-8E9C569A-1B06-42C4-9586-0EF83437001A)

Examples

The following example inserts a row into the sample table `pm.print_media`.
The example uses the `BFILENAME` function to identify a binary file on the
server file system in the directory `/demo/schema/product_media`. The example
shows how the directory database object `media_dir` was created in the `pm`
schema.

    
    
    CREATE DIRECTORY media_dir AS '/demo/schema/product_media';
    
    INSERT INTO print_media (product_id, ad_id, ad_graphic)
      VALUES (3000, 31001, BFILENAME('MEDIA_DIR', 'modem_comp_ad.gif'));


[← Previous](AVG.md)

[Next →](BIN_TO_NUM.md)
