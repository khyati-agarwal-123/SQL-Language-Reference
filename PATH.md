[Previous](ORA_INVOKING_USERID.md) [Next](PERCENT_RANK.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. PATH 

## PATH

Syntax

![Description of path.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path.gif)  
[Description of the illustration path.eps](img_text/path.md)

Purpose

`PATH` is an ancillary function used only with the `UNDER_PATH` and
`EQUALS_PATH` conditions. It returns the relative path that leads to the
resource specified in the parent condition.

The `correlation_integer` can be any `NUMBER` integer and is used to correlate
this ancillary function with its primary condition. Values less than 1 are
treated as 1.

See Also:

  * [EQUALS_PATH Condition](XML-Conditions.md#GUID-51E593FF-9AB0-4E1F-ABF7-5330F82FC0AE) and [UNDER_PATH Condition](XML-Conditions.md#GUID-37EF3738-5751-4888-9397-50EAD8360D6D)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `PATH`

Examples

Refer to the related function
[DEPTH](DEPTH.md#GUID-C0107BE4-0003-4329-9CCE-D0671B3F3538) for an example
using both of these ancillary functions of the `EQUALS_PATH` and `UNDER_PATH`
conditions.


[← Previous](ORA_INVOKING_USERID.md)

[Next →](PERCENT_RANK.md)
