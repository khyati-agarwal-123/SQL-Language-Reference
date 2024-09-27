[Previous](Hierarchical-Query-Operators.md) [Next](Multiset-Operators.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. Set Operators 

## Set Operators

Set operators combine the results of two component queries into a single
result. Queries containing set operators are called compound queries. [Table
4-5](Set-Operators.md#GUID-5CB549AF-5A4F-453E-B164-49CAC8F94CBF__CIHECBJH
"The first column lists the set operators and the second column describes what
is returned by a query containing the operator.") lists the SQL set operators.
They are fully described with examples in [The Set Operators](The-UNION-ALL-
INTERSECT-MINUS-Operators.md#GUID-B64FE747-586E-4513-945F-80CB197125EE).

Table 4-5 Set Operators

Operator | Returns  
---|---  
`UNION` |  All distinct rows selected by either query  
`UNION ALL` |  All rows selected by either query, including duplicates  
`INTERSECT ` |  All distinct rows selected by both queries  
`INTERSECT ALL` |  All rows selected by both queries including duplicates  
`MINUS ` |  All distinct rows selected by the first query but not the second  
`MINUS ALL ` |  All rows selected by the first query but not the second including duplicates  
`EXCEPT ` |  All distinct rows selected by the first query but not the second  
`EXCEPT ALL` |  All rows selected by the first query but not the second including duplicates


[← Previous](Hierarchical-Query-Operators.md)

[Next →](Multiset-Operators.md)
