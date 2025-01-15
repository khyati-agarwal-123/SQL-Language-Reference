##  Hierarchical Query Operators {#GUID-4CC13EEB-846A-4254-93FC-E91E678BD302} 

Two operators, ` PRIOR ` and ` CONNECT_BY_ROOT ` , are valid only in hierarchical queries. 

###  PRIOR {#GUID-95F6A554-C6FE-42CD-88A6-7A1C162ED964} 

In a hierarchical query, one expression in the ` CONNECT ` ` BY ` *condition* must be qualified by the ` PRIOR ` operator. If the ` CONNECT ` ` BY ` *condition* is compound, then only one condition requires the ` PRIOR ` operator, although you can have multiple ` PRIOR ` conditions. ` PRIOR ` evaluates the immediately following expression for the parent row of the current row in a hierarchical query. 

` PRIOR ` is most commonly used when comparing column values with the equality operator. (The ` PRIOR ` keyword can be on either side of the operator.) ` PRIOR ` causes Oracle to use the value of the parent row in the column. Operators other than the equal sign (=) are theoretically possible in ` CONNECT ` ` BY ` clauses. However, the conditions created by these other operators can result in an infinite loop through the possible combinations. In this case Oracle detects the loop at run time and returns an error. Refer to [ Hierarchical Queries ](Hierarchical-Queries.md#GUID-0118DF1D-B9A9-41EB-8556-C6E7D6A5A84E) for more information on this operator, including examples. 

###  CONNECT_BY_ROOT {#GUID-875C8985-4AEF-4DF1-BA23-3CDF5BCBCD8E} 

` CONNECT_BY_ROOT ` is a unary operator that is valid only in hierarchical queries. When you qualify a column with this operator, Oracle returns the column value using data from the root row. This operator extends the functionality of the ` CONNECT ` ` BY ` [ ` PRIOR ` ] condition of hierarchical queries. 

Restriction on CONNECT_BY_ROOT 

You cannot specify this operator in the ` START ` ` WITH ` condition or the ` CONNECT ` ` BY ` condition. 

> **note:** See Also: 

[ CONNECT_BY_ROOT Examples ](Hierarchical-Queries.md#GUID-E3D35EF7-33C3-4D88-81B3-00030C47AE56__I2069380)
