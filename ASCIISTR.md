[Previous](ASCII.md) [Next](ASIN.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ASCIISTR 

## ASCIISTR

Syntax

![Description of asciistr.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/asciistr.gif)  
[Description of the illustration asciistr.eps](img_text/asciistr.md)

Purpose

`ASCIISTR` takes as its argument a string, or an expression that resolves to a
string, in any character set and returns an ASCII version of the string in the
database character set. Non-ASCII characters are converted to the form
`\xxxx`, where `xxxx` represents a UTF-16 code unit.

See Also:

  * [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG006) for information on Unicode character sets and character semantics 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `ASCIISTR`

Examples

The following example returns the ASCII string equivalent of the text string
"`ABÃCDE`":

    
    
    SELECT ASCIISTR('ABÃCDE')
      FROM DUAL;
    
    ASCIISTR('
    ----------
    AB\00C4CDE


[← Previous](ASCII.md)

[Next →](ASIN.md)
