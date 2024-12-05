[Previous](CEIL.html) [Next](checksum.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. CHARTOROWID 



## CHARTOROWID 

Syntax

![Description of chartorowid.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/chartorowid.gif)[Descriptionof the illustration chartorowid.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/chartorowid.md)

Purpose

`CHARTOROWID` converts a value from `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2` data type to `ROWID` data type. 

This function does not support `CLOB` data directly. However, `CLOB`s can be passed in as arguments through implicit data conversion. 

See Also:

[Data Type Comparison Rules](Data-Type-Comparison-Rules.html#GUID-1563C817-86BF-430B-99AB-322EE2E29187) for more information. 

Examples

The following example converts a character rowid representation to a rowid. (The actual rowid is different for each database instance.)
    
    
    SELECT last_name
      FROM employees
      WHERE ROWID = CHARTOROWID('AAAFd1AAFAAAABSAA/');
     
    LAST_NAME
    -------------------------
    Greene

[← Previous](CEIL.md)

[Next →](checksum.md)
