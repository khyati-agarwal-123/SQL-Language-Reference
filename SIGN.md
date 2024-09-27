[Previous](SET.md) [Next](SIN.md) JavaScript must be enabled to correctly
display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. SIGN 

## SIGN

Syntax

![Description of sign.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sign.gif)  
[Description of the illustration sign.eps](img_text/sign.md)

Purpose

`SIGN` returns the sign of `n`. This function takes as an argument any numeric
data type, or any nonnumeric data type that can be implicitly converted to
`NUMBER`, and returns `NUMBER`.

For value of `NUMBER` type, the sign is:

  * -1 if `n`<0 

  * 0 if `n`=0 

  * 1 if `n`>0 

For binary floating-point numbers (`BINARY_FLOAT` and `BINARY_DOUBLE`), this
function returns the sign bit of the number. The sign bit is:

  * -1 if `n`<0 

  * +1 if `n`>=0 or `n`=`NaN`

Examples

The following example indicates that the argument of the function (`-15`) is
<0:

    
    
    SELECT SIGN(-15) "Sign" FROM DUAL;
    
          Sign
    ----------
            -1


[← Previous](SET.md)

[Next →](SIN.md)
