[Previous](to_nchar-boolean.md) [Next](TO_NCHAR-datetime.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_NCHAR (character) 

## TO_NCHAR (character)

Syntax

to_nchar_char::=

![Description of to_nchar_char.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_nchar_char.gif)  
[Description of the illustration
to_nchar_char.eps](img_text/to_nchar_char.md)

Purpose

`TO_NCHAR` (character) converts a character string, `CHAR`, `VARCHAR2`,
`CLOB`, or `NCLOB` value to the national character set. The value returned is
always `NVARCHAR2`. This function is equivalent to the `TRANSLATE` ... `USING`
function with a `USING` clause in the national character set.

See Also:

  * "[Data Conversion](Data-Type-Comparison-Rules.md#GUID-6DB331B5-0F34-4215-9A20-16AEA9D7FF4B)" and [TRANSLATE ... USING](TRANSLATE-USING.md#GUID-EC8DE4D2-4F24-456D-A2E7-AD8F82E3A148)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of this function 

Examples

The following example converts `VARCHAR2` data from the `oe.customers` table
to the national character set:

    
    
    SELECT TO_NCHAR(cust_last_name) FROM customers
       WHERE customer_id=103;
    
    TO_NCHAR(CUST_LAST_NAME)
    --------------------------------------------------
    Taylor


[← Previous](to_nchar-boolean.md)

[Next →](TO_NCHAR-datetime.md)
