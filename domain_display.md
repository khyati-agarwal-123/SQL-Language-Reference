[Previous](domain_check_type.md) [Next](domain_name.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. DOMAIN_DISPLAY

## DOMAIN_DISPLAY

Syntax

  

![Description of domain_display_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/domain_display_function.gif)  
[Description of the illustration
domain_display_function.eps](img_text/domain_display_function.md)

  

Purpose

`DOMAIN_DISPLAY` returns `expr` formatted according to the domain's display
expression. This returns `NULL` if the arguments are not associated with a
domain or the domain has no display expression.

When calling `DOMAIN_DISPLAY` for multicolumn domains, all values of `expr`
should be from the same domain. It returns `NULL` if the number of `expr`
arguments are different from the number of domain columns or they are in a
different order in the domain.

To get the display expression for a non-domain value, cast `expr` to the
domain type. This is only possible for single column domains.

See Also:

  * [Domain Functions](Single-Row-Functions.md#GUID-AEF8F898-493F-4BE8-86E6-06241BB78AB0)

Examples

The following example creates the domain `DAY_OF_WEEK` and associates it with
the column `CALENDAR_DATES.DAY_OF_WEEK_ABBR`. Passing this column to
`DOMAIN_DISPLAY` returns it with the first letter of each word capitalized and
all other letters in lowercase. `DOMAIN_DISPLAY` also returns this format when
casting a string to the domain.

All other calls to `DOMAIN_DISPLAY` pass non-domain values, so return `NULL`.

    
    
    CREATE DOMAIN day_of_week AS CHAR(3 CHAR)
      DISPLAY INITCAP(day_of_week);
    
    
    CREATE TABLE calendar_dates (
      calendar_date DATE,
      day_of_week_abbr day_of_week
    );
    
    
    INSERT INTO calendar_dates 
    VALUES(DATE'2023-05-01', 'MON'), 
          (DATE'2023-05-02', 'tue'), 
          (DATE'2023-05-05', 'fRI');
    
    
    
    SELECT day_of_week_abbr, 
           DOMAIN_DISPLAY(day_of_week_abbr) domain_column, 
           DOMAIN_DISPLAY(calendar_date) nondomain_column,
           DOMAIN_DISPLAY(CAST('MON' AS day_of_week)) domain_value, 
           DOMAIN_DISPLAY('MON') nondomain_value
      FROM calendar_dates;
    
    DAY_OF_WEEK_ABBR DOMAIN_COLUMN NONDOMAIN_COLUMN DOMAIN_VALUE NONDOMAIN_VALUE
    ---------------- ------------- ---------------- ------------ ---------------
    MON              Mon           <null>           Mon          <null>         
    tue              Tue           <null>           Mon          <null>             
    fRI              Fri           <null>           Mon          <null> 

The following example creates the multicolumn domain `CURRENCY` with a display
expression. The columns `AMOUNT` and `CURRENCY_CODE` in `ORDER_ITEMS` are
associated with this domain.

In the query, only the domain_cols expression formats the columns according to
the domain expression. All other calls to `DOMAIN_DISPLAY` have a mismatch
between its arguments and the domain columns so return `NULL`:

    
    
    CREATE DOMAIN currency AS (
      amount        AS NUMBER(10, 2)
      currency_code AS CHAR(3 CHAR)
    )
    DISPLAY CASE currency_code
      WHEN 'USD' THEN '$'
      WHEN 'GBP' THEN 'Â£'
      WHEN 'EUR' THEN 'â¬'
      WHEN 'JPY' THEN 'Â¥'
    END || TO_CHAR(amount, '999,999,999.00');
    
    
    CREATE TABLE order_items (
      order_id      INTEGER,
      product_id    INTEGER,
      amount        NUMBER(10, 2),
      currency_code CHAR(3 CHAR),
      DOMAIN currency(amount, currency_code)
    );
    
    
    INSERT INTO order_items
    VALUES (1, 1,    9.99, 'USD'),
           (2, 2, 1234.56, 'GBP'),
           (3, 3, 4321,    'EUR'),
           (4, 4, 3141592, 'JPY');
    
    
    SELECT order_id,
           product_id,
           DOMAIN_DISPLAY(amount, currency_code) domain_cols,
           DOMAIN_DISPLAY(currency_code, amount) domain_cols_wrong_order,
           DOMAIN_DISPLAY(order_id, product_id) nondomain_cols,
           DOMAIN_DISPLAY(amount) domain_cols_subset
      FROM order_items;
      
      ORDER_ID PRODUCT_ID DOMAIN_COLS      DOMAIN_COLS_WRONG_ORDER NONDOMAIN_COLS DOMAIN_COLS_SUBSET
    ---------- ---------- ---------------- ----------------------- -------------- ------------------
             1          1 $           9.99 <null>                  <null>         <null>            
             2          2 Â£       1,234.56 <null>                  <null>         <null>            
             3          3 â¬       4,321.00 <null>                  <null>         <null>            
             4          4 Â¥   3,141,592.00 <null>                  <null>         <null> 
    


[← Previous](domain_check_type.md)

[Next →](domain_name.md)
