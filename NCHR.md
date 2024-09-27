[Previous](NANVL.md) [Next](NEW_TIME.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. NCHR 

## NCHR

Syntax

![Description of nchr.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nchr.gif)  
[Description of the illustration nchr.eps](img_text/nchr.md)

Purpose

`NCHR` returns the character having the binary equivalent to `number` in the
national character set. The value returned is always `NVARCHAR2`. This
function is equivalent to using the `CHR` function with the `USING` `NCHAR_CS`
clause.

This function takes as an argument a `NUMBER` value, or any value that can be
implicitly converted to `NUMBER`, and returns a character.

See Also:

  * [CHR](CHR.md#GUID-35FEE007-D49C-4562-A904-041186AC8928)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `NCHR`

Examples

The following examples return the nchar character 187:

    
    
    SELECT NCHR(187)
      FROM DUAL;
    
    N
    -
    > 
    
    SELECT CHR(187 USING NCHAR_CS)
      FROM DUAL;
    
    C
    -
    > 


[← Previous](NANVL.md)

[Next →](NEW_TIME.md)
