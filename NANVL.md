[Previous](MONTHS_BETWEEN.md) [Next](NCHR.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. NANVL 

## NANVL

Syntax

![Description of nanvl.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nanvl.gif)  
[Description of the illustration nanvl.eps](img_text/nanvl.md)

Purpose

The `NANVL` function is useful only for floating-point numbers of type
`BINARY_FLOAT` or `BINARY_DOUBLE`. It instructs Oracle Database to return an
alternative value `n1` if the input value `n2` is `NaN` (not a number). If
`n2` is not `NaN`, then Oracle returns `n2`.

This function takes as arguments any numeric data type or any nonnumeric data
type that can be implicitly converted to a numeric data type. Oracle
determines the argument with the highest numeric precedence, implicitly
converts the remaining arguments to that data type, and returns that data
type.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion, "[Floating-Point Numbers](Data-
Types.md#GUID-F579F4B8-EF13-4CAF-9B06-03B076861C41)" for information on
binary-float comparison semantics, and "[Numeric Precedence](Data-
Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812)" for information on
numeric precedence

Examples

Using table `float_point_demo` created for
[TO_BINARY_DOUBLE](TO_BINARY_DOUBLE.md#GUID-0BA2E065-8006-426C-A3CB-1F6B0C8F283C),
insert a second entry into the table:

    
    
    INSERT INTO float_point_demo
      VALUES (0,'NaN','NaN');
    
    SELECT *
      FROM float_point_demo;
    
       DEC_NUM BIN_DOUBLE  BIN_FLOAT
    ---------- ---------- ----------
       1234.56 1.235E+003 1.235E+003
             0        Nan        Nan
    

The following example returns `bin_float` if it is a number. Otherwise, 0 is
returned.

    
    
    SELECT bin_float, NANVL(bin_float,0)
      FROM float_point_demo;
    
     BIN_FLOAT NANVL(BIN_FLOAT,0)
    ---------- ------------------
    1.235E+003         1.235E+003
           Nan                  0


[← Previous](MONTHS_BETWEEN.md)

[Next →](NCHR.md)
