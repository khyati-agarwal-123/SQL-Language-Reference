[Previous](ROW_NUMBER.md) [Next](ROWIDTONCHAR.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ROWIDTOCHAR 

## ROWIDTOCHAR

Syntax

![Description of rowidtochar.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rowidtochar.gif)  
[Description of the illustration rowidtochar.eps](img_text/rowidtochar.md)

Purpose

`ROWIDTOCHAR` converts a rowid value to `VARCHAR2` data type. The result of
this conversion is always 18 characters long.

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation derivation rules, which define the collation assigned to the
character return value of `ROWIDTOCHAR`

Examples

The following example converts a rowid value in the `employees` table to a
character value. (Results vary for each build of the sample database.)

    
    
    SELECT ROWID FROM employees 
       WHERE ROWIDTOCHAR(ROWID) LIKE '%JAAB%'
       ORDER BY ROWID;
    
    ROWID
    ------------------
    AAAFfIAAFAAAABSAAb


[← Previous](ROW_NUMBER.md)

[Next →](ROWIDTONCHAR.md)
