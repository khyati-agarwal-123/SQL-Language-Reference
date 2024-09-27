[Previous](vector_norm.md) [Next](VSIZE.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VECTOR_SERIALIZE

## VECTOR_SERIALIZE

Syntax

  

![Description of vector_serialize.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_serialize.gif)  
[Description of the illustration
vector_serialize.eps](img_text/vector_serialize.md)

  

Purpose

`VECTOR_SERIALIZE` is synonymous with `FROM_VECTOR.`

See [FROM_VECTOR](from_vector.md#GUID-AA60B3CB-FCB7-4944-9E06-976C272855B1)
for semantics and examples.

Examples

    
    
    SELECT VECTOR_SERIALIZE(VECTOR('[1.1,2.2,3.3]',3,FLOAT32));
    
    
    VECTOR_SERIALIZE(VECTOR('[1.1,2.2,3.3]',3,FLOAT32))
    ---------------------------------------------------------------
    [1.10000002E+000,2.20000005E+000,3.29999995E+000]
    
    1 row selected.
    
    
    
    SELECT VECTOR_SERIALIZE(VECTOR('[1.1, 2.2, 3.3]',3,FLOAT32) RETURNING VARCHAR2(1000));
    
    
    VECTOR_SERIALIZE(VECTOR('[...]',3,FLOAT32)RETURNINGVARCHAR2(1000))
    ------------------------------------------------------------------
    [1.10000002E+000,2.20000005E+000,3.29999995E+000]
    
    1 row selected.
    
    
    SELECT VECTOR_SERIALIZE(VECTOR('[1.1, 2.2, 3.3]',3,FLOAT32) RETURNING CLOB);
    
    
    VECTOR_SERIALIZE(VECTOR('[1.1, 2.2, 3.3]',3,FLOAT32)RETURNINGCLOB)
    --------------------------------------------------------
    [1.10000002E+000,2.20000005E+000,3.29999995E+000] 
    
    1 row selected.
    

See Also:

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)

  * [Vector Distance Metrics of the AI Vector Search User's Guide.](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=VECSE-GUID-DBC136C1-7C63-4B7F-902B-2289FF375560)


[← Previous](vector_norm.md)

[Next →](VSIZE.md)
