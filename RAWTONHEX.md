[Previous](RAWTOHEX.md) [Next](REF.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. RAWTONHEX 

## RAWTONHEX

Syntax

![Description of rawtonhex.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rawtonhex.gif)  
[Description of the illustration rawtonhex.eps](img_text/rawtonhex.md)

Purpose

`RAWTONHEX` converts `raw` to a character value containing its hexadecimal
representation. `RAWTONHEX(``raw``)` is equivalent to
`TO_NCHAR(RAWTOHEX(``raw``))`. The value returned is always in the national
character set.

Note:

`RAWTONHEX` functions differently when used as a PL/SQL built-in function.
Refer to [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS00308) for more information.

Examples

The following hypothetical example returns the hexadecimal equivalent of a
`RAW` column value:

    
    
    SELECT RAWTONHEX(raw_column),
       DUMP ( RAWTONHEX (raw_column) ) "DUMP" 
       FROM graphics; 
    
    RAWTONHEX(RA)           DUMP 
    ----------------------- ------------------------------ 
    7D                      Typ=1 Len=4: 0,55,0,68 


[← Previous](RAWTOHEX.md)

[Next →](REF.md)
