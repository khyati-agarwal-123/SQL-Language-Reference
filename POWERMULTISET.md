[Previous](POWER.md) [Next](POWERMULTISET_BY_CARDINALITY.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. POWERMULTISET 

## POWERMULTISET

Syntax

![Description of powermultiset.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/powermultiset.gif)  
[Description of the illustration
powermultiset.eps](img_text/powermultiset.md)

Purpose

`POWERMULTISET` takes as input a nested table and returns a nested table of
nested tables containing all nonempty subsets (called submultisets) of the
input nested table.

  * `expr` can be any expression that evaluates to a nested table. 

  * If `expr` resolves to null, then Oracle Database returns `NULL`. 

  * If `expr` resolves to a nested table that is empty, then Oracle returns an error. 

  * The element types of the nested table must be comparable. Refer to "[Comparison Conditions](Comparison-Conditions.md#GUID-828576BF-E606-4EA6-B94B-BFF48B67F927)" for information on the comparability of nonscalar types. 

Note:

This function is not supported in PL/SQL.

Examples

First, create a data type that is a nested table of the
`cust_address_tab_type` data type:

    
    
    CREATE TYPE cust_address_tab_tab_typ
      AS TABLE OF cust_address_tab_typ;
    /
    

Now, select the nested table column `cust_address_ntab` from the
`customers_demo` table using the `POWERMULTISET` function:

    
    
    SELECT CAST(POWERMULTISET(cust_address_ntab) AS cust_address_tab_tab_typ)
      FROM customers_demo;
    
    CAST(POWERMULTISET(CUST_ADDRESS_NTAB) AS CUST_ADDRESS_TAB_TAB_TYP)
      (STREET_ADDRESS, POSTAL_CODE, CITY, STATE_PROVINCE, COUNTRY_ID)
    ------------------------------------------------------------------
    CUST_ADDRESS_TAB_TAB_TYP(CUST_ADDRESS_TAB_TYP(CUST_ADDRESS_TYP
      ('514 W Superior St', '46901', 'Kokomo', 'IN', 'US')))
    CUST_ADDRESS_TAB_TAB_TYP(CUST_ADDRESS_TAB_TYP(CUST_ADDRESS_TYP
      ('2515 Bloyd Ave', '46218', 'Indianapolis', 'IN', 'US')))
    CUST_ADDRESS_TAB_TAB_TYP(CUST_ADDRESS_TAB_TYP(CUST_ADDRESS_TYP
      ('8768 N State Rd 37', '47404', 'Bloomington', 'IN', 'US')))
    CUST_ADDRESS_TAB_TAB_TYP(CUST_ADDRESS_TAB_TYP(CUST_ADDRESS_TYP
      ('6445 Bay Harbor Ln', '46254', 'Indianapolis', 'IN', 'US')))
    . . .
    

The preceding example requires the `customers_demo` table and a nested table
column containing data. Refer to "[Multiset Operators](Multiset-
Operators.md#GUID-793FCBB0-A97C-4884-BCAC-DD0542EA746B)" to create this
table and nested table columns.


[← Previous](POWER.md)

[Next →](POWERMULTISET_BY_CARDINALITY.md)
