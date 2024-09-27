[Previous](NLS_LOWER.md) [Next](NLSSORT.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. NLS_UPPER 

## NLS_UPPER

Syntax

![Description of nls_upper.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nls_upper.gif)  
[Description of the illustration nls_upper.eps](img_text/nls_upper.md)

Purpose

`NLS_UPPER` returns `char`, with all letters uppercase.

Both `char` and `'nlsparam'` can be any of the data types `CHAR`, `VARCHAR2`,
`NCHAR`, `NVARCHAR2`, `CLOB`, or `NCLOB`. The string returned is of `VARCHAR2`
data type if `char` is a character data type and a LOB if `char` is a LOB data
type. The return string is in the same character set as `char`.

The `'nlsparam'` can have the same form and serve the same purpose as in the
`NLS_INITCAP` function.

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation determination rules for `NLS_UPPER`, and for the collation
derivation rules, which define the collation assigned to the character return
value of this function

Examples

The following example returns a string with all the letters converted to
uppercase:

    
    
    SELECT NLS_UPPER('groÃe') "Uppercase"
      FROM DUAL;
    
    Upper
    -----
    GROÃE
    
    SELECT NLS_UPPER('groÃe', 'NLS_SORT = XGerman') "Uppercase" 
      FROM DUAL;
    
    Upperc
    ------
    GROSSE

See Also:

[NLS_INITCAP](NLS_INITCAP.md#GUID-42C1581B-B5AA-4D4C-A489-BC5B38A754FD)


[← Previous](NLS_LOWER.md)

[Next →](NLSSORT.md)
