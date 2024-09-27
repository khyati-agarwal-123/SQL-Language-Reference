[Previous](UID.md) [Next](UPPER.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. UNISTR 

## UNISTR

Syntax

![Description of unistr.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/unistr.gif)  
[Description of the illustration unistr.eps](img_text/unistr.md)

Purpose

`UNISTR` takes as its argument a text literal or an expression that resolves
to character data and returns it in the national character set. The national
character set of the database can be either AL16UTF16 or UTF8. `UNISTR`
provides support for Unicode string literals by letting you specify the
Unicode encoding value of characters in the string. This is useful, for
example, for inserting data into `NCHAR` columns.

The Unicode encoding value has the form '\xxxx' where 'xxxx' is the
hexadecimal value of a character in UCS-2 encoding format. Supplementary
characters are encoded as two code units, the first from the high-surrogates
range (U+D800 to U+DBFF), and the second from the low-surrogates range (U+DC00
to U+DFFF). To include the backslash in the string itself, precede it with
another backslash (\\\\).

For portability and data preservation, Oracle recommends that in the `UNISTR`
string argument you specify only ASCII characters and the Unicode encoding
values.

See Also:

  * [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG006) for information on Unicode and national character sets 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `UNISTR`

Examples

The following example passes both ASCII characters and Unicode encoding values
to the `UNISTR` function, which returns the string in the national character
set:

    
    
    SELECT UNISTR('abc\00e5\00f1\00f6') FROM DUAL;
    
    UNISTR
    ------
    abcÃ¥Ã±Ã¶


[← Previous](UID.md)

[Next →](UPPER.md)
