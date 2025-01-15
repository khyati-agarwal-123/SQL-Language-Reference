##  Set Operators {#GUID-5CB549AF-5A4F-453E-B164-49CAC8F94CBF} 

Set operators combine the results of two component queries into a single result. Queries containing set operators are called compound queries. [ Table 4-5 ](Set-Operators.md#GUID-5CB549AF-5A4F-453E-B164-49CAC8F94CBF__CIHECBJH) lists the SQL set operators. They are fully described with examples in [ The Set Operators ](The-UNION-ALL-INTERSECT-MINUS-Operators.md#GUID-B64FE747-586E-4513-945F-80CB197125EE) . 

**Table: Set Operators** 

Operator  |  Returns   
---|---  
` UNION ` |  All distinct rows selected by either query   
` UNION ALL ` |  All rows selected by either query, including duplicates   
` INTERSECT ` |  All distinct rows selected by both queries   
` INTERSECT ALL ` |  All rows selected by both queries including duplicates   
` MINUS ` |  All distinct rows selected by the first query but not the second   
` MINUS ALL ` |  All rows selected by the first query but not the second including duplicates   
` EXCEPT ` |  All distinct rows selected by the first query but not the second   
` EXCEPT ALL ` |  All rows selected by the first query but not the second including duplicates 
