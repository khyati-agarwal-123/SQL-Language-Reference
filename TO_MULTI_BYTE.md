[Previous](TO_LOB.md) [Next](to_nchar-boolean.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_MULTI_BYTE 

## TO_MULTI_BYTE

Syntax

![Description of to_multi_byte.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_multi_byte.gif)  
[Description of the illustration
to_multi_byte.eps](img_text/to_multi_byte.md)

Purpose

`TO_MULTI_BYTE` returns `char` with all of its single-byte characters
converted to their corresponding multibyte characters. `char` can be of data
type `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2`. The value returned is in the
same data type as `char`.

Any single-byte characters in `char` that have no multibyte equivalents appear
in the output string as single-byte characters. This function is useful only
if your database character set contains both single-byte and multibyte
characters.

This function does not support `CLOB` data directly. However, `CLOB`s can be
passed in as arguments through implicit data conversion.

See Also:

  * "[Data Type Comparison Rules](Data-Type-Comparison-Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187)" for more information. 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `TO_MULTI_BYTE`

Examples

The following example illustrates converting from a single byte `A` to a
multibyte `A` in UTF8:

    
    
    SELECT dump(TO_MULTI_BYTE( 'A')) FROM DUAL; 
    
    DUMP(TO_MULTI_BYTE('A')) 
    ------------------------ 
    Typ=1 Len=3: 239,188,161


[← Previous](TO_LOB.md)

[Next →](to_nchar-boolean.md)
