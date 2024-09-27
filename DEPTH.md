[Previous](DENSE_RANK.md) [Next](DEREF.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. DEPTH 

## DEPTH

Syntax

![Description of depth.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/depth.gif)  
[Description of the illustration depth.eps](img_text/depth.md)

Purpose

`DEPTH` is an ancillary function used only with the `UNDER_PATH` and
`EQUALS_PATH` conditions. It returns the number of levels in the path
specified by the `UNDER_PATH` condition with the same correlation variable.

The `correlation_integer` can be any `NUMBER` integer. Use it to correlate
this ancillary function with its primary condition if the statement contains
multiple primary conditions. Values less than 1 are treated as 1.

See Also:

[EQUALS_PATH Condition](XML-
Conditions.md#GUID-51E593FF-9AB0-4E1F-ABF7-5330F82FC0AE), [UNDER_PATH
Condition](XML-Conditions.md#GUID-37EF3738-5751-4888-9397-50EAD8360D6D), and
the related function
[PATH](PATH.md#GUID-91937F98-7718-4F39-9225-1E0229F11F0D)

Examples

The `EQUALS_PATH` and `UNDER_PATH` conditions can take two ancillary
functions, `DEPTH` and `PATH`. The following example shows the use of both
ancillary functions. The example assumes the existence of the XMLSchema
`warehouses.xsd` (created in [Using XML in SQL Statements](Using-XML-in-SQL-
Statements.md#GUID-5FE21EC9-1F66-45F1-9FD8-ECA5336EDC14)).

    
    
    SELECT PATH(1), DEPTH(2)
      FROM RESOURCE_VIEW
      WHERE UNDER_PATH(res, '/sys/schemas/OE', 1)=1
        AND UNDER_PATH(res, '/sys/schemas/OE', 2)=1;
    
    PATH(1)                          DEPTH(2)
    -------------------------------- --------
    . . .
    www.example.com                         1
    www.example.com/xwarehouses.xsd         2
    . . .


[← Previous](DENSE_RANK.md)

[Next →](DEREF.md)
