[Previous](TO_NUMBER.md) [Next](TO_TIMESTAMP.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_SINGLE_BYTE 

## TO_SINGLE_BYTE

Syntax

![Description of to_single_byte.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_single_byte.gif)  
[Description of the illustration
to_single_byte.eps](img_text/to_single_byte.md)

Purpose

`TO_SINGLE_BYTE` returns `char` with all of its multibyte characters converted
to their corresponding single-byte characters. `char` can be of data type
`CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2`. The value returned is in the same
data type as `char`.

Any multibyte characters in `char` that have no single-byte equivalents appear
in the output as multibyte characters. This function is useful only if your
database character set contains both single-byte and multibyte characters.

This function does not support `CLOB` data directly. However, `CLOB`s can be
passed in as arguments through implicit data conversion.

See Also:

  * "[Data Type Comparison Rules](Data-Type-Comparison-Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187)" for more information. 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `TO_SINGLE_BYTE`

Examples

The following example illustrates going from a multibyte `A` in UTF8 to a
single byte ASCII `A`:

    
    
    SELECT TO_SINGLE_BYTE( CHR(15711393)) FROM DUAL; 
    
    T 
    - 
    A 


[← Previous](TO_NUMBER.md)

[Next →](TO_TIMESTAMP.md)
