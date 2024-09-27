[Previous](APPROX_SUM.md) [Next](ASCIISTR.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ASCII 

## ASCII

Syntax

![Description of ascii.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ascii.gif)  
[Description of the illustration ascii.eps](img_text/ascii.md)

Purpose

`ASCII` returns the decimal representation in the database character set of
the first character of `char`.

`char` can be of data type `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2`. The
value returned is of data type `NUMBER`. If your database character set is
7-bit ASCII, then this function returns an ASCII value. If your database
character set is EBCDIC Code, then this function returns an EBCDIC value.
There is no corresponding EBCDIC character function.

This function does not support `CLOB` data directly. However, `CLOB`s can be
passed in as arguments through implicit data conversion.

See Also:

[Data Type Comparison Rules](Data-Type-Comparison-
Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187) for more information

Examples

The following example returns employees whose last names begin with the letter
L, whose ASCII equivalent is 76:

    
    
    SELECT last_name
      FROM employees
      WHERE ASCII(SUBSTR(last_name, 1, 1)) = 76
      ORDER BY last_name;
     
    LAST_NAME
    -------------------------
    Ladwig
    Landry
    Lee
    Livingston
    Lorentz


[← Previous](APPROX_SUM.md)

[Next →](ASCIISTR.md)
