[Previous](RPAD.md) [Next](SCN_TO_TIMESTAMP.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. RTRIM 

## RTRIM

Syntax

![Description of rtrim.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rtrim.gif)  
[Description of the illustration rtrim.eps](img_text/rtrim.md)

Purpose

`RTRIM` removes from the right end of `char` all of the characters that appear
in `set`. This function is useful for formatting the output of a query.

If you do not specify `set`, then it defaults to a single blank. `RTRIM` works
similarly to `LTRIM`.

Both `char` and `set` can be any of the data types `CHAR`, `VARCHAR2`,
`NCHAR`, `NVARCHAR2`, `CLOB`, or `NCLOB`. The string returned is of `VARCHAR2`
data type if `char` is a character data type, `NVARCHAR2` if `char` is a
national character data type, and a LOB if `char` is a LOB data type.

See Also:

  * [LTRIM](LTRIM.md#GUID-81B3D53C-0BBC-4485-B057-C8012CD6E40F)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules, which define the collation `RTRIM` uses to compare characters from `set` with characters from `char`, and for the collation derivation rules, which define the collation assigned to the character return value of this function 

Examples

The following example trims all the right-most occurrences of less than sign
(`<`), greater than sign (`>`) , and equal sign (`=`) from a string:

    
    
    SELECT RTRIM('<=====>BROWNING<=====>', '<>=') "RTRIM Example"
      FROM DUAL;
    
    RTRIM Example
    ---------------
    <=====>BROWNING
    


[← Previous](RPAD.md)

[Next →](SCN_TO_TIMESTAMP.md)
