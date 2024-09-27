[Previous](NLS_CHARSET_NAME.md) [Next](NLS_COLLATION_NAME.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. NLS_COLLATION_ID 

## NLS_COLLATION_ID

Syntax

![Description of nls_collation_id.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nls_collation_id.gif)  
[Description of the illustration
nls_collation_id.eps](img_text/nls_collation_id.md)

Purpose

`NLS_COLLATION_ID` takes as its argument a collation name and returns the
corresponding collation ID number. Collation IDs are used in the data
dictionary tables and in Oracle Call Interface (OCI). Collation names are used
in SQL statements and data dictionary views

For `expr`, specify the collation name as a `VARCHAR2` value. You can specify
a valid named collation or a pseudo-collation, in any combination of uppercase
and lowercase letters.

This function returns a `NUMBER` value. If you specify an invalid collation
name, then this function returns null.

Examples

The following example returns the collation ID of collation `BINARY_CI`:

    
    
    SELECT NLS_COLLATION_ID('BINARY_CI') 
      FROM DUAL; 
    
    NLS_COLLATION_ID('BINARY_CI')
    -----------------------------
                           147455


[← Previous](NLS_CHARSET_NAME.md)

[Next →](NLS_COLLATION_NAME.md)
