[Previous](XMLEXISTS.md) [Next](XMLISVALID.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. XMLFOREST 

## XMLFOREST

Syntax

![Description of xmlforest.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmlforest.gif)  
[Description of the illustration xmlforest.eps](img_text/xmlforest.md)

Purpose

`XMLForest` converts each of its argument parameters to XML, and then returns
an XML fragment that is the concatenation of these converted arguments.

  * If `value_expr` is a scalar expression, then you can omit the `AS` clause, and Oracle Database uses the column name as the element name. 

  * If `value_expr` is an object type or collection, then the `AS` clause is mandatory, and Oracle uses the specified expression as the enclosing tag. 

You can do this by specifying `c_alias`, which is a string literal, or by
specifying `EVALNAME` `value_expr`. In the latter case, the value expression
is evaluated and the result, which must be a string literal, is used as the
identifier. The identifier does not have to be a column name or column
reference. It cannot be an expression or null. It can be up to 4000 characters
if the initialization parameter `MAX_STRING_SIZE` `=` `STANDARD`, and 32767
characters if `MAX_STRING_SIZE` `=` `EXTENDED`. See "[Extended Data
Types](Data-Types.md#GUID-8EFA29E9-E8D8-40A6-A43E-954908C954A4)" for more
information.

  * If `value_expr` is null, then no element is created for that `value_expr`. 

Examples

The following example creates an `Emp` element for a subset of employees, with
nested `employee_id`, `last_name`, and `salary` elements as the contents of
`Emp`:

    
    
    SELECT XMLELEMENT("Emp", 
       XMLFOREST(e.employee_id, e.last_name, e.salary))
       "Emp Element"
       FROM employees e WHERE employee_id = 204;
    
    Emp Element
    ----------------------------------------------------------------
    <Emp>
      <EMPLOYEE_ID>204</EMPLOYEE_ID>
      <LAST_NAME>Baer</LAST_NAME>
      <SALARY>10000</SALARY>
    </Emp>
    

Refer to the example for [XMLCOLATTVAL](XMLCOLATTVAL.md#GUID-
AE3B6441-74D8-4033-900B-A578A79E5F0A) to compare the output of these two
functions.


[← Previous](XMLEXISTS.md)

[Next →](XMLISVALID.md)
