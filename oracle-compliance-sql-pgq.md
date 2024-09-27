[Previous](oracle-compliance-sql-mda.md) [Next](Oracle-Compliance-with-
FIPS-127-2.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Oracle and Standard SQL](Oracle-and-Standard-SQL.md)
  3. Oracle Compliance with SQL/PGQ

## Oracle Compliance with SQL/PGQ

Table [Table C-4](oracle-compliance-sql-pgq.md#GUID-2984AEEA-
BB05-4209-B144-57DB2B8D5878__TABLE_TWG_1FW_LBC "SQL/PGQ support") describes
Oracle's support for the features of SQL/PGQ.

Table C-4 Oracle Support for Features of SQL/PGQ

Feature ID | Feature Support  
---|---  
G000, Graph pattern  |  Oracle fully supports this feature.  
G001, Repeatable-elements match mode |  Oracle fully supports this feature.  
G008, Graph pattern WHERE clause |  Oracle fully supports this feature.  
G034, Path concatenation |  Oracle fully supports this feature.  
G035, Quantified paths |  Oracle fully supports this feature.  
G036, Quantified edges  |  Oracle fully supports this feature.  
G037, Questioned paths |  Oracle fully supports this feature.  
G040, Vertex pattern |  Oracle fully supports this feature.  
G042, Basic full edge patterns |  Oracle fully supports this feature.  
G044, Basic abbreviated edge patterns  |  Oracle fully supports this feature.  
G060, Bounded graph pattern quantifiers |  Oracle fully supports this feature.  
G070, Label expression: label disjunction  |  Oracle fully supports this feature.  
G071, Label expression: label conjunction  |  Oracle provides equivalent functionality using label expressions on different graph patterns with the same graph element variable name.  
G073, Label expression: individual label name |  Oracle fully supports this feature.  
G090, Property reference |  Oracle fully supports this feature.  
G100, `ELEMENT_ID` function  |  Oracle provides equivalent functionality using `EDGE_ID` and `VERTEX_ID` operators.   
G112, `IS SOURCE` and `IS DESTINATION` predicate  |  Oracle fully supports this feature.  
G114, `SAME` predicate  |  Oracle provides equivalent functionality using `VERTEX_EQUAL` and `EDGE_EQUAL` predicates.   
G120, Within-match aggregates |  Oracle fully supports this feature.  
G900, `GRAPH_TABLE` |  Oracle fully supports this feature.  
G904, All properties reference |  Oracle supports this feature in the `COLUMNS` clause.   
G920, DDL-based SQL-property graphs |  Oracle fully supports this feature with the following exception: the keyword `RESTRICT` is not supported for the `DROP PROPERTY GRAPH` statement.   
G924, Explicit key clause for element tables |  Oracle fully supports this feature.  
G925, Explicit label and properties clause for element tables |  Oracle fully supports this feature.  
G926, More than one label for vertex tables |  Oracle fully supports this feature.  
G927, More than one label for edge tables |  Oracle fully supports this feature.  
G928, Value expressions as properties and renaming of properties |  Oracle fully supports this feature.  
G929, Labels and properties: `EXCEPT` list  |  Oracle fully supports this feature.  
G940, Multi-sourced and multi-destined edges |  Oracle fully supports this feature.  
G941, Implicit removal of incomplete edges |  Oracle fully supports this feature.


[← Previous](oracle-compliance-sql-mda.md)

[Next →](Oracle-Compliance-with-FIPS-127-2.md)
