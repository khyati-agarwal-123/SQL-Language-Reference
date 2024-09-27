[Previous](TO_NCHAR-datetime.md) [Next](TO_NCLOB.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_NCHAR (number) 

## TO_NCHAR (number)

Syntax

to_nchar_number::=

![Description of to_nchar_number.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_nchar_number.gif)  
[Description of the illustration
to_nchar_number.eps](img_text/to_nchar_number.md)

Purpose

`TO_NCHAR` (number) converts `n` to a string in the national character set.
The value `n` can be of type `NUMBER`, `BINARY_FLOAT`, or `BINARY_DOUBLE`. The
function returns a value of the same type as the argument. The optional `fmt`
and `'nlsparam'` corresponding to `n` can be of `DATE`, `TIMESTAMP`,
`TIMESTAMP` `WITH` `TIME` `ZONE`, `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE`,
`INTERVAL` `MONTH` `TO` `YEAR`, or `INTERVAL` `DAY` `TO` `SECOND` data type.

See Also:

  * "[Security Considerations for Data Conversion](Data-Type-Comparison-Rules.md#GUID-6A02902A-1EF1-41E4-9494-381488BD272F)"

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of this function 

Examples

The following example converts the `customer_id` values from the sample table
`oe.orders` to the national character set:

    
    
    SELECT TO_NCHAR(customer_id) "NCHAR_Customer_ID"  FROM orders 
       WHERE order_status > 9
       ORDER BY "NCHAR_Customer_ID";
    
    NCHAR_Customer_ID
    ----------------------------------------
    102
    103
    148
    148
    149


[← Previous](TO_NCHAR-datetime.md)

[Next →](TO_NCLOB.md)
