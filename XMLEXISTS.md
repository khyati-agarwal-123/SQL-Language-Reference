[Previous](XMLELEMENT.md) [Next](XMLFOREST.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. XMLEXISTS 

## XMLEXISTS

Syntax

![Description of xmlexists.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmlexists.gif)  
[Description of the illustration xmlexists.eps](img_text/xmlexists.md)

XML_passing_clause::=

![Description of xml_passing_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xml_passing_clause.gif)  
[Description of the illustration
xml_passing_clause.eps](img_text/xml_passing_clause.md)

Purpose

`XMLExists` checks whether a given XQuery expression returns a nonempty XQuery
sequence. If so, the function returns `TRUE`; otherwise, it returns `FALSE`.
The argument `XQuery_string` is a literal string, but it can contain XQuery
variables that you bind using the `XML_passing_clause`.

The `expr` in the `XML_passing_clause` is an expression returning an `XMLType`
or an instance of a SQL scalar data type that is used as the context for
evaluating the XQuery expression. You can specify only one `expr` in the
`PASSING` clause without an identifier. The result of evaluating each `expr`
is bound to the corresponding identifier in the `XQuery_string`. If any `expr`
that is not followed by an `AS` clause, then the result of evaluating that
expression is used as the context item for evaluating the `XQuery_string`. If
`expr` is a relational column, then its declared collation is ignored by
Oracle XML DB.

See Also:

[Oracle XML DB Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADXDB0400) for more information on uses for this function
and examples


[← Previous](XMLELEMENT.md)

[Next →](XMLFOREST.md)
