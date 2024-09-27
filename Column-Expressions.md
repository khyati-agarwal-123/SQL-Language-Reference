[Previous](CASE-Expressions.md) [Next](CURSOR-Expressions.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Expressions](Expressions.md)
  3. Column Expressions 

## Column Expressions

A column expression, which is designated as `column_expression` in subsequent
syntax diagrams, is a limited form of `expr`. A column expression can be a
simple expression, compound expression, function expression, boolean
expression, or expression list, but it can contain only the following forms of
expression:

  * Columns of the subject table â the table being created, altered, or indexed

  * Constants (strings or numbers)

  * Deterministic functions â either SQL built-in functions or user-defined functions

No other expression forms described in this chapter are valid. In addition,
compound expressions using the `PRIOR` keyword are not supported, nor are
aggregate functions.

You can use a column expression for these purposes:

  * To create a function-based index. 

  * To explicitly or implicitly define a virtual column. When you define a virtual column, the defining `column_expression` must refer only to columns of the subject table that have already been defined, in the current statement or in a prior statement. 

The combined components of a column expression must be deterministic. That is,
the same set of input values must return the same set of output values.

See Also:

[Simple Expressions](Simple-
Expressions.md#GUID-0E033897-60FB-40D7-A5F3-498B0FCC31B0), [Compound
Expressions](Compound-
Expressions.md#GUID-533C7BA0-C8B4-4323-81EA-1379657AF64A), [Function
Expressions](Function-
Expressions.md#GUID-C47F0B7D-9058-481F-815E-A31FB21F3BD5), and [Expression
Lists](Expression-Lists.md#GUID-5CC8FC75-813B-44AA-8737-D940FA887D1E) for
information on these forms of `expr`


[← Previous](CASE-Expressions.md)

[Next →](CURSOR-Expressions.md)
