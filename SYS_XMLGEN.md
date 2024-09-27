[Previous](SYS_XMLAGG.md) [Next](SYSDATE.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. SYS_XMLGEN 

## SYS_XMLGEN

Note:

The `SYS_XMLGen` function is deprecated. It is still supported for backward
compatibility. However, Oracle recommends that you use the SQL/XML generation
functions instead. See [Oracle XML DB Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADXDB1620) for more information.

Syntax

![Description of sys_xmlgen.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sys_xmlgen.gif)  
[Description of the illustration sys_xmlgen.eps](img_text/sys_xmlgen.md)

Purpose

`SYS_XMLGen` takes an expression that evaluates to a particular row and column
of the database, and returns an instance of type `XMLType` containing an XML
document. The `expr` can be a scalar value, a user-defined type, or an
`XMLType` instance.

  * If `expr` is a scalar value, then the function returns an XML element containing the scalar value. 

  * If `expr` is a type, then the function maps the user-defined type attributes to XML elements. 

  * If `expr` is an `XMLType` instance, then the function encloses the document in an XML element whose default tag name is `ROW`. 

By default the elements of the XML document match the elements of `expr`. For
example, if `expr` resolves to a column name, then the enclosing XML element
will be the same column name. If you want to format the XML document
differently, then specify `fmt`, which is an instance of the `XMLFormat`
object.

See Also:

"[XML Format Model](Format-
Models.md#GUID-C6EB69EF-74DB-4C10-A02E-210D31616552)" for a description of
the `XMLFormat` type and how to use its attributes to format `SYS_XMLGen`
results

Examples

The following example retrieves the employee email ID from the sample table
`oe.employees` where the `employee_id` value is 205, and generates an instance
of an `XMLType` containing an XML document with an `EMAIL` element.

    
    
    SELECT SYS_XMLGEN(email)      
       FROM employees
       WHERE employee_id = 205;
    
    SYS_XMLGEN(EMAIL)
    -------------------------------------------------------------------
    <?xml version="1.0"?>
    <EMAIL>SHIGGINS</EMAIL>


[← Previous](SYS_XMLAGG.md)

[Next →](SYSDATE.md)
