[Previous](LPAD.md) [Next](MAKE_REF.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. LTRIM 

## LTRIM

Syntax

![Description of ltrim.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ltrim.gif)  
[Description of the illustration ltrim.eps](img_text/ltrim.md)

Purpose

`LTRIM` removes from the left end of `char` all of the characters contained in
`set`. If you do not specify `set`, then it defaults to a single blank. Oracle
Database begins scanning `char` from its first character and removes all
characters that appear in `set` until reaching a character not in `set` and
then returns the result.

Both `char` and `set` can be any of the data types `CHAR`, `VARCHAR2`,
`NCHAR`, `NVARCHAR2`, `CLOB`, or `NCLOB`. The string returned is of `VARCHAR2`
data type if `char` is a character data type, `NVARCHAR2` if `char` is a
national character data type, and a LOB if `char` is a LOB data type.

See Also:

  * [RTRIM](RTRIM.md#GUID-95A7DAFB-F7AB-48F4-BE24-64B3C7A840AA)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules, which define the collation `LTRIM` uses to compare characters from `set` with characters from `char`, and for the collation derivation rules, which define the collation assigned to the character return value of this function 

Examples

The following example trims all the left-most occurrences of less than sign
(`<`), greater than sign (`>`) , and equal sign (`=`) from a string:

    
    
    SELECT LTRIM('<=====>BROWNING<=====>', '<>=') "LTRIM Example"
      FROM DUAL;
    
    LTRIM Example
    ---------------
    BROWNING<=====>
    


[← Previous](LPAD.md)

[Next →](MAKE_REF.md)
