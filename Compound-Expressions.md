[Previous](analytic-view-measure-expressions.html) [Next](CASE-Expressions.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)
  2. [ Expressions](Expressions.html)
  3. Compound Expressions 



## Compound Expressions 

A compound expression specifies a combination of other expressions.

compound_expression::= 

![Description of compound_expression.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/compound_expression.gif)[Description of the illustration compound_expression.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/compound_expression.html)You can use any built-in function as an expression ([Function Expressions](Function-Expressions.html#GUID-C47F0B7D-9058-481F-815E-A31FB21F3BD5)). However, in a compound expression, some combinations of functions are inappropriate and are rejected. For example, the `LENGTH` function is inappropriate within an aggregate function. 

The `PRIOR` operator is used in `CONNECT` `BY` clauses of hierarchical queries. 

The `COLLATE` operator determines the collation for an expression. This operator overrides the collation that the database would have derived for the expression using standard collation derivation rules. 

See Also:

  * [Operator Precedence](About-SQL-Operators.html#GUID-FEF44762-F45C-41D9-B380-F6A61AD25338)

  * [Hierarchical Queries](Hierarchical-Queries.html#GUID-0118DF1D-B9A9-41EB-8556-C6E7D6A5A84E)

  * [COLLATE Operator](COLLATE-Operator.html#GUID-1B8CE3B0-77FC-455C-8400-6F81CF188D7B)




Some valid compound expressions are:
    
    
    ('CLARK' || 'SMITH') 
    LENGTH('MOOSE') * 57 
    SQRT(144) + 72 
    my_fun(TO_CHAR(sysdate,'DD-MMM-YY'))
    name COLLATE BINARY_CI

[← Previous](analytic-view-measure-expressions.md)

[Next →](CASE-Expressions.md)
