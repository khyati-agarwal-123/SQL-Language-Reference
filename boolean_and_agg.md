##  BOOLEAN_AND_AGG {#GUID-AF3C1A26-C7A1-4BD2-B15C-86B761D4D8D9} 

Syntax 

  


![Description of boolean_and_agg.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/boolean_and_agg.gif)[ Description of the illustration boolean_and_agg.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/boolean_and_agg.md)

  


Purpose 

` BOOLEAN_AND_AGG ` returns ` 'TRUE' ` if the *boolean_expr* evaluates to true for every row that qualifies. Otherwise it returns ` 'FALSE' ` . You can use it as an aggregate or analytic function. 

Examples 
    
    
    ```
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t;
    ```
    
    
    ```
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c1 = 0;
    ```
    
    
    ```
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c2 IS FALSE;
    ```
    
    
    ```
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c2 IS FALSE OR c2 IS NULL;
    ```
    
    
    ```
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c2 IS NOT TRUE OR c2 IS NULL;
    ```
    
    
    ```
    SELECT BOOLEAN_AND_AGG(c2)
        FROM t
        WHERE c2 IS NOT FALSE OR c2 IS NULL;
    ```
    
    
    ```
    SELECT BOOLEAN_AND_AGG(c2 OR c2 OR (c2))
        FROM t
        WHERE c2 IS NOT FALSE OR c2 IS NULL;
    ```
