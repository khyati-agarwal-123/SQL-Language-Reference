[Previous](Version-Query-Pseudocolumns.md) [Next](OBJECT_ID-
Pseudocolumn.md) JavaScript must be enabled to correctly display this
content

  1. [SQL Language Reference ](index.md)
  2. [ Pseudocolumns](Pseudocolumns.md)
  3. COLUMN_VALUE Pseudocolumn 

## COLUMN_VALUE Pseudocolumn

When you refer to an `XMLTable` construct without the `COLUMNS` clause, or
when you use the `TABLE` collection expression to refer to a scalar nested
table type, the database returns a virtual table with a single column. This
name of this pseudocolumn is `COLUMN_VALUE`.

In the context of `XMLTable`, the value returned is of data type `XMLType`.
For example, the following two statements are equivalent, and the output for
both shows `COLUMN_VALUE` as the name of the column being returned:

    
    
    SELECT *
      FROM XMLTABLE('<a>123</a>');
    
    COLUMN_VALUE
    ---------------------------------------
    <a>123</a>
    
    SELECT COLUMN_VALUE
      FROM (XMLTable('<a>123</a>'));
    
    COLUMN_VALUE
    ----------------------------------------
    <a>123</a>
    

In the context of a `TABLE` collection expression, the value returned is the
data type of the collection element. The following statements create the two
levels of nested tables illustrated in [Creating a Table: Multilevel
Collection Example](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2139603) to show the
uses of `COLUMN_VALUE` in this context:

    
    
    CREATE TYPE phone AS TABLE OF NUMBER;   
    /
    CREATE TYPE phone_list AS TABLE OF phone;
    /
    

The next statement uses `COLUMN_VALUE` to select from the `phone` type:

    
    
    SELECT t.COLUMN_VALUE
      FROM TABLE(phone(1,2,3)) t;
    
    COLUMN_VALUE
    ------------
               1
               2
               3
    

In a nested type, you can use the `COLUMN_VALUE` pseudocolumn in both the
select list and the `TABLE` collection expression:

    
    
    SELECT t.COLUMN_VALUE
      FROM TABLE(phone_list(phone(1,2,3))) p, TABLE(p.COLUMN_VALUE) t;
    
    COLUMN_VALUE
    ------------
               1
               2
               3
    

The keyword `COLUMN_VALUE` is also the name that Oracle Database generates for
the scalar value of an inner nested table without a column or attribute name,
as shown in the example that follows. In this context, `COLUMN_VALUE` is not a
pseudocolumn, but an actual column name.

    
    
    CREATE TABLE my_customers (
        cust_id       NUMBER,
        name          VARCHAR2(25),
        phone_numbers phone_list,
        credit_limit  NUMBER)
      NESTED TABLE phone_numbers STORE AS outer_ntab
      (NESTED TABLE COLUMN_VALUE STORE AS inner_ntab);

See Also:

  * [XMLTABLE](XMLTABLE.md#GUID-C4A32C58-33E5-4CF1-A1FE-039550D3ECFA) for information on that function 

  * [table_collection_expression::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121871) for information on the `TABLE` collection expression 

  * `ALTER` `TABLE` examples in [Nested Tables: Examples](ALTER-TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2133232)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules for values of the `COLUMN_VALUE` pseudocolumn 


[← Previous](Version-Query-Pseudocolumns.md)

[Next →](OBJECT_ID-Pseudocolumn.md)
