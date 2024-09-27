[Previous](Model-Expressions.md) [Next](Placeholder-Expressions.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Expressions](Expressions.md)
  3. Object Access Expressions 

## Object Access Expressions

An object access expression specifies attribute reference and method
invocation.

object_access_expression::=

![Description of object_access_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/object_access_expression.gif)  
[Description of the illustration
object_access_expression.eps](img_text/object_access_expression.md)

The column parameter can be an object or `REF` column. If you specify `expr`,
then it must resolve to an object type.

When a type's member function is invoked in the context of a SQL statement, if
the `SELF` argument is null, Oracle returns null and the function is not
invoked.

Examples

The following example creates a table based on the sample `oe.order_item_typ`
object type, and then shows how you would update and select from the object
column attributes.

    
    
    CREATE TABLE short_orders (
       sales_rep VARCHAR2(25), item order_item_typ);
    
    UPDATE short_orders s SET sales_rep = 'Unassigned';
    
    SELECT o.item.line_item_id, o.item.quantity FROM short_orders o;


[← Previous](Model-Expressions.md)

[Next →](Placeholder-Expressions.md)
