[Previous](LOWER.md) [Next](LTRIM.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. LPAD

## LPAD

Syntax

![Description of lpad.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lpad.gif)  
[Description of the illustration lpad.eps](img_text/lpad.md)

Purpose

`LPAD` returns `expr1`, left-padded to length `n` characters with the sequence
of characters in `expr2`. This function is useful for formatting the output of
a query.

Both `expr1` and `expr2` can be any of the data types `CHAR`, `VARCHAR2`,
`NCHAR`, `NVARCHAR2`, `CLOB`, or `NCLOB`. The string returned is of `VARCHAR2`
data type if `expr1` is a character data type, `NVARCHAR2` if `expr1` is a
national character data type, and a LOB if `expr1` is a LOB data type. The
string returned is in the same character set as `expr1`. The argument `n` must
be a `NUMBER` integer or a value that can be implicitly converted to a
`NUMBER` integer.

If you do not specify `expr2`, then the default is a single blank. If `expr1`
is longer than `n`, then this function returns the portion of `expr1` that
fits in `n`.

The argument `n` is the total length of the return value as it is displayed on
your terminal screen. In most character sets, this is also the number of
characters in the return value. However, in some multibyte character sets, the
display length of a character string can differ from the number of characters
in the string.

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation derivation rules, which define the collation assigned to the
character return value of `LPAD`

Examples

The following example left-pads a string with the asterisk (*) and period (.)
characters:

    
    
    SELECT LPAD('Page 1',15,'*.') "LPAD example"
      FROM DUAL;
    
    LPAD example
    ---------------
    *.*.*.*.*Page 1


[← Previous](LOWER.md)

[Next →](LTRIM.md)
