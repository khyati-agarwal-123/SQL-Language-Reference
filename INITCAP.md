[Previous](HEXTORAW.md) [Next](inner_product.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. INITCAP 

## INITCAP

Syntax

![Description of initcap.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/initcap.gif)  
[Description of the illustration initcap.eps](img_text/initcap.md)

Purpose

`INITCAP` returns `char`, with the first letter of each word in uppercase, all
other letters in lowercase. Words are delimited by white space or characters
that are not alphanumeric.

`char` can be of any of the data types `CHAR`, `VARCHAR2`, `NCHAR`, or
`NVARCHAR2`. The return value is the same data type as `char`. The database
sets the case of the initial characters based on the binary mapping defined
for the underlying character set. For linguistic-sensitive uppercase and
lowercase, refer to
[NLS_INITCAP](NLS_INITCAP.md#GUID-42C1581B-B5AA-4D4C-A489-BC5B38A754FD).

This function does not support `CLOB` data directly. However, `CLOB`s can be
passed in as arguments through implicit data conversion.

See Also:

  * "[Data Type Comparison Rules](Data-Type-Comparison-Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187)" for more information. 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `INITCAP`

Examples

The following example capitalizes each word in the string:

    
    
    SELECT INITCAP('the soap') "Capitals"
      FROM DUAL; 
    
    Capitals
    ---------
    The Soap


[← Previous](HEXTORAW.md)

[Next →](inner_product.md)
