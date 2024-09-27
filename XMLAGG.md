[Previous](WIDTH_BUCKET.md) [Next](XMLCAST.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. XMLAGG 

## XMLAGG

Syntax

![Description of xmlagg.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmlagg.gif)  
[Description of the illustration xmlagg.eps](img_text/xmlagg.md)

Purpose

`XMLAgg` is an aggregate function. It takes a collection of XML fragments and
returns an aggregated XML document. Any arguments that return null are dropped
from the result.

`XMLAgg` is similar to `SYS_XMLAgg` except that `XMLAgg` returns a collection
of nodes but it does not accept formatting using the `XMLFormat` object. Also,
`XMLAgg` does not enclose the output in an element tag as does `SYS_XMLAgg`.

Within the `order_by_clause`, Oracle Database does not interpret number
literals as column positions, as it does in other uses of this clause, but
simply as number literals.

See Also:

[XMLELEMENT](XMLELEMENT.md#GUID-DEA75423-00EA-4034-A246-4A774ADC988E) and
[SYS_XMLAGG](SYS_XMLAGG.md#GUID-BEDD241D-360A-46A2-AEBF-C8B70E465D75)

Examples

The following example produces a `Department` element containing `Employee`
elements with employee job ID and last name as the contents of the elements:

    
    
    SELECT XMLELEMENT("Department",
       XMLAGG(XMLELEMENT("Employee", 
       e.job_id||' '||e.last_name)
       ORDER BY last_name))
       as "Dept_list"     
       FROM employees e
       WHERE e.department_id = 30;
    
    Dept_list
    -------------------------------------------------------------
    <Department>
      <Employee>PU_CLERK Baida</Employee>
      <Employee>PU_CLERK Colmenares</Employee>
      <Employee>PU_CLERK Himuro</Employee>
      <Employee>PU_CLERK Khoo</Employee>
      <Employee>PU_MAN Raphaely</Employee>
      <Employee>PU_CLERK Tobias</Employee>
    </Department>
    

The result is a single row, because `XMLAgg` aggregates the rows. You can use
the `GROUP` `BY` clause to group the returned set of rows into multiple
groups:

    
    
    SELECT XMLELEMENT("Department",
          XMLAGG(XMLELEMENT("Employee", e.job_id||' '||e.last_name)))
       AS "Dept_list"
       FROM employees e
       GROUP BY e.department_id;
    
    Dept_list
    ---------------------------------------------------------
    <Department>
      <Employee>AD_ASST Whalen</Employee>
    </Department>
    
    <Department>
      <Employee>MK_MAN Hartstein</Employee>
      <Employee>MK_REP Fay</Employee>
    </Department>
    
    <Department>
      <Employee>PU_MAN Raphaely</Employee>
      <Employee>PU_CLERK Khoo</Employee>
      <Employee>PU_CLERK Tobias</Employee>
      <Employee>PU_CLERK Baida</Employee>
      <Employee>PU_CLERK Colmenares</Employee>
      <Employee>PU_CLERK Himuro</Employee>
    </Department>
    . . .


[← Previous](WIDTH_BUCKET.md)

[Next →](XMLCAST.md)
