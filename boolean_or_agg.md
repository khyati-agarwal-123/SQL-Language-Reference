[Previous](boolean_and_agg.md) [Next](CARDINALITY.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. BOOLEAN_OR_AGG

## BOOLEAN_OR_AGG

Syntax

  

![Description of boolean_or_agg.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/boolean_or_agg.gif)  
[Description of the illustration
boolean_or_agg.eps](img_text/boolean_or_agg.md)

  

Purpose

`BOOLEAN_OR_AGG` returns `'TRUE'` if the `boolean_expr` evaluates to true for
at least one row that qualifies. Otherwise it returns `'FALSE'`. You can use
it as an aggregate or analytic function.

Examples

    
    
    SELECT BOOLEAN_OR_AGG(c2)
        FROM t; 
        
    
    
    SELECT BOOLEAN_OR_AGG(c2)
        FROM t
        WHERE c1 = 0;
    
    
    SELECT BOOLEAN_OR_AGG(c2)
        FROM t
        WHERE c2 IS TRUE;
    
    
    SELECT BOOLEAN_OR_AGG(c2)
        FROM t
        WHERE c2 IS TRUE OR c2 IS NULL;
    
    
    SELECT BOOLEAN_OR_AGG(c2)
        FROM t
        WHERE c2 IS NOT FALSE OR c2 IS NULL;
    
    
    SELECT BOOLEAN_OR_AGG(c2)
        FROM t
        WHERE c2 IS NOT TRUE OR c2 IS NULL;
    
    
    SELECT BOOLEAN_OR_AGG(c2 OR c2)
        FROM t
        WHERE c2 IS NOT TRUE OR c2 IS NULL;


[← Previous](boolean_and_agg.md)

[Next →](CARDINALITY.md)
