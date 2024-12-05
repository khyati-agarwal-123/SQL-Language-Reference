[Previous](MIN.html) [Next](MONTHS_BETWEEN.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. MOD 



## MOD 

Syntax

![Description of mod.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mod.gif)[Descriptionof the illustration mod.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/mod.md)

Purpose

`MOD` returns the remainder of `n2` divided by `n1`. Returns `n2` if `n1` is 0. 

This function takes as arguments any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. Oracle determines the argument with the highest numeric precedence, implicitly converts the remaining arguments to that data type, and returns that data type.

See Also:

[Table 2-9](Data-Type-Comparison-Rules.html#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell indicates implicit conversion of the data types") for more information on implicit conversion and "[Numeric Precedence](Data-Types.html#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812)" for information on numeric precedence 

Examples

The following example returns the remainder of 11 divided by 4:
    
    
    SELECT MOD(11,4) "Modulus"
      FROM DUAL;
    
       Modulus
    ----------
             3
    

This function behaves differently from the classical mathematical modulus function, if the product of `n1` and `n2` is negative. The classical modulus can be expressed using the `MOD` function with this formula: 
    
    
    n2 - n1 * FLOOR(n2/n1)
    

The following table illustrates the difference between the `MOD` function and the classical modulus: 

n2 | n1 | MOD(n2,n1) | Classical Modulus  
---|---|---|---  
11 | 4 | 3 | 3  
11 | -4 | 3 | -1  
-11 | 4 | -3 | 1  
-11 | -4 | -3 | -3  
  
See Also:

[FLOOR (number)](FLOOR.html#GUID-67F61AC7-C097-4397-A122-213157BF584F) and [REMAINDER](REMAINDER.html#GUID-430D4C4A-5779-4EBB-90C5-4D7CA7E73556), which is similar to `MOD`, but uses `ROUND` in its formula instead of `FLOOR`

[← Previous](MIN.md)

[Next →](MONTHS_BETWEEN.md)
