[Previous](domain_display.md) [Next](domain_order.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. DOMAIN_NAME

## DOMAIN_NAME

Syntax

  

![Description of domain_name_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/domain_name_function.gif)  
[Description of the illustration
domain_name_function.eps](img_text/domain_name_function.md)

  

Purpose

`DOMAIN_NAME` returns the fully qualified name of the domain associated with
`expr`. This returns `NULL` if expr is associated with a domain.

When calling `DOMAIN_NAME` for multicolumn domains, all values of `expr`
should be from the same domain. It returns `NULL` if the number of `expr`
arguments are different from the number of domain columns or they are in a
different order in the domain.

See Also:

  * [Domain Functions](Single-Row-Functions.md#GUID-AEF8F898-493F-4BE8-86E6-06241BB78AB0)

Examples

The following example creates the domain `DAY_OF_WEEK` in the schema `HR` and
associates it with the column `HR.CALENDAR_DATES.DAY_OF_WEEK_ABBR`. Passing
this column to `DOMAIN_NAME` returns the fully qualified name of the domain.

The query casts the string "`MON`" to `DAY_OF_WEEK` to get the domain name.

All other calls to `DOMAIN_NAME` return `NULL`.

    
    
    CREATE DOMAIN hr.day_of_week AS CHAR(3 CHAR);
    
    
    CREATE TABLE hr.calendar_dates (
      calendar_date    DATE,
      day_of_week_abbr hr.day_of_week
    );
    
    
    INSERT INTO hr.calendar_dates 
    VALUES(DATE'2023-05-01', 'MON');
    
    
    SELECT day_of_week_abbr, 
           DOMAIN_NAME(day_of_week_abbr) domain_column, 
           DOMAIN_NAME(calendar_date) nondomain_column, 
           DOMAIN_NAME(CAST('MON' AS hr.day_of_week)) domain_value,
           DOMAIN_NAME('MON') nondomain_value
      FROM hr.calendar_dates;
      
    DAY_OF_WEEK_ABBR DOMAIN_COLUMN  NONDOMAIN_COLUMN DOMAIN_VALUE   NONDOMAIN_VALUE    
    ---------------- -------------- ---------------- -------------- ---------------
    MON              HR.DAY_OF_WEEK <null>           HR.DAY_OF_WEEK <null> 

The following example creates the multicolumn domain `CURRENCY` in the schema
`CO`. The columns `AMOUNT` and `CURRENCY_CODE` in `CO.ORDER_ITEMS` are
associated with this domain.

In the query, the arguments for `DOMAIN_NAME` only match the domain definition
for the domain_cols expression. This returns the fully qualified name of the
domain. All other calls to `DOMAIN_NAME` have a mismatch between its arguments
and the domain columns so return `NULL`:

    
    
    CREATE DOMAIN co.currency AS (
      amount        AS NUMBER(10, 2)
      currency_code AS CHAR(3 CHAR)
    );
    
    
    CREATE TABLE co.order_items (
      order_id      INTEGER,
      product_id    INTEGER,
      amount        NUMBER(10, 2),
      currency_code CHAR(3 CHAR),
      DOMAIN co.currency(amount, currency_code)
    );
    
    
    INSERT INTO co.order_items
    VALUES (1, 1, 9.99, 'USD');
    
    
    SELECT order_id,
           product_id,
           DOMAIN_NAME(amount, currency_code) domain_cols,
           DOMAIN_NAME(currency_code, amount) domain_cols_wrong_order,
           DOMAIN_NAME(order_id, product_id) nondomain_cols,
           DOMAIN_NAME(amount) domain_cols_subset
      FROM co.order_items
      ORDER BY domain_cols;
      
      ORDER_ID PRODUCT_ID DOMAIN_COLS     DOMAIN_COLS_WRONG_ORDER   NONDOMAIN_COLS  DOMAIN_COLS_SUBSET  
    ---------- ---------- --------------- ------------------------- --------------- --------------------
             1          1 CO.CURRENCY     <null>                    <null>          <null> 


[← Previous](domain_display.md)

[Next →](domain_order.md)
