[Previous](Arithmetic-Operators.md) [Next](Concatenation-Operator.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. COLLATE Operator

## COLLATE Operator

The `COLLATE` operator determines the collation for an expression. This
operator enables you to override the collation that the database would have
derived for the expression using standard collation derivation rules.

`COLLATE` is a postfix unary operator. It has the same precedence as other
unary operators, but it is evaluated after all prefix unary operators have
been evaluated.

You can apply this operator to expressions of type `VARCHAR2`, `CHAR`, `LONG`,
`NVARCHAR`, or `NCHAR`.

The `COLLATE` operator takes one argument, `collation_name`, for which you can
specify a named collation or pseudo-collation. If the collation name contains
a space, then you must enclose the name in double quotation marks.

[Table 4-3](COLLATE-
Operator.md#GUID-1B8CE3B0-77FC-455C-8400-6F81CF188D7B__CIHDBHCB "The first
column lists the single COLLATE operator, the second column describes it, and
the third column provides an example.") describes the `COLLATE` operator.

Table 4-3 COLLATE Operator

Operator | Purpose | Example  
---|---|---  
`COLLATE` `collation_name` |  Determines the collation for an expression | 
    
    
    SELECT last_name
      FROM employees
      ORDER BY last_name COLLATE GENERIC_M;  
  
See Also:

  * [Compound Expressions](Compound-Expressions.md#GUID-533C7BA0-C8B4-4323-81EA-1379657AF64A) for information on using the `COLLATE` operator in a compound expression 

  * [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-4146F48A-FB6F-4593-8098-BDF45404EB24) for more information on the `COLLATE` operator 


[← Previous](Arithmetic-Operators.md)

[Next →](Concatenation-Operator.md)
