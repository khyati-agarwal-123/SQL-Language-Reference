[Previous](BIT_XOR_AGG.md) [Next](boolean_or_agg.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. BOOLEAN_AND_AGG

## BOOLEAN_AND_AGG

Syntax

  

![Description of boolean_and_agg.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/boolean_and_agg.gif)  
[Description of the illustration
boolean_and_agg.eps](img_text/boolean_and_agg.md)

  

Purpose

`BOOLEAN_AND_AGG` returns `'TRUE'` if the `boolean_expr` evaluates to true for
every row that qualifies. Otherwise it returns `'FALSE'`. You can use it as an
aggregate or analytic function.

Examples

    
    
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t;
    
    
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c1 = 0;
    
    
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c2 IS FALSE;
    
    
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c2 IS FALSE OR c2 IS NULL;
    
    
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c2 IS NOT TRUE OR c2 IS NULL;
    
    
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c2 IS NOT FALSE OR c2 IS NULL;
    
    
    SELECT BOOLEAN_AND_AGG(c2 OR c2 OR (c2))
        FROM t
        WHERE c2 IS NOT FALSE OR c2 IS NULL;


[← Previous](BIT_XOR_AGG.md)

[Next →](boolean_or_agg.md)
