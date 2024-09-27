[Previous](CARDINALITY.md) [Next](ceil-datetime.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CAST 

## CAST

Syntax

![Description of cast.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cast.gif)  
[Description of the illustration cast.eps](img_text/cast.md)

domain_validate_clause::=

  

![Description of domain_validate_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/domain_validate_clause.gif)  
[Description of the illustration
domain_validate_clause.eps](img_text/domain_validate_clause.md)

  

Purpose

`CAST` lets you convert built-in data types or collection-typed values of one
type into another built-in data type or collection type. You can cast an
unnamed operand (such as a date or the result set of a subquery) or a named
collection (such as a varray or a nested table) into a type-compatible data
type or named collection. The `type_name` must be the name of a built-in data
type, collection type, or domain name and the operand must be a built-in data
type or must evaluate to a collection value.

For the operand, `expr` can be either a built-in data type, a collection type,
or an instance of an `ANYDATA` type. If `expr` is an instance of an `ANYDATA`
type, then `CAST` tries to extract the value of the `ANYDATA` instance and
return it if it matches the cast target type, otherwise, null will be
returned. `MULTISET` informs Oracle Database to take the result set of the
subquery and return a collection value. [Table
7-1](CAST.md#GUID-5A70235E-1209-4281-8521-B94497AAEF75__G1514003 "The cells
indicate with an X the possible conversions from source to destination data
type using CAST.") shows which built-in data types can be cast into which
other built-in data types. (`CAST` does not support `LONG`, `LONG` `RAW`, or
the Oracle-supplied types.)

`CAST` does not directly support any of the LOB data types. When you use
`CAST` to convert a `CLOB` value into a character data type or a `BLOB` value
into the `RAW` data type, the database implicitly converts the LOB value to
character or raw data and then explicitly casts the resulting value into the
target data type. If the resulting value is larger than the target type, then
the database returns an error.

When you use `CAST` ... `MULTISET` to get a collection value, each select list
item in the query passed to the `CAST` function is converted to the
corresponding attribute type of the target collection element type.

The cells with an 'X' indicate the possible conversions from source to
destination data type using `CAST`.

Table 7-1 Casting Built-In Data Types

Destination Data Type | from BINARY_FLOAT, BINARY_DOUBLE | from CHAR, VARCHAR2 | from NUMBER/INTEGER | from DATETIME / INTERVAL (Note 1) | from RAW | from ROWID, UROWID (Note 2) | from NCHAR, NVARCHAR2 | from BOOLEAN  
---|---|---|---|---|---|---|---|---  
to BINARY_FLOAT, BINARY_DOUBLE |  `X` (Note 3)  |  `X` (Note 3)  |  `X` (Note 3)  |  `--` |  `--` |  `--` |  `X` (Note 3)  |  `X`(Note 4)   
to CHAR, VARCHAR2 |  `X` |  `X` |  `X` |  `X` |  `X` |  `X` |  `--` |  `X` (Note 5)   
to NUMBER/INTEGER |  `X` (Note 3)  |  `X` (Note 3)  |  `X` (Note 3)  |  `--` |  `--` |  `--` |  `X` (Note 3)  |  `X`(Note 4)   
to DATETIME/INTERVAL |  `--` |  `X` (Note 3)  |  `--` |  `X` (Note 3)  |  `--` |  `--` |  `--` |  `--`  
to RAW |  `--` |  `X` |  `--` |  `--` |  `X` |  `--` |  `--` |  `--`  
to ROWID, UROWID |  `--` |  `X` |  `--` |  `--` |  `--` |  `X` |  `--` |  `--`  
to NCHAR, NVARCHAR2 |  `X` |  `--` |  `X` |  `X` |  `X` |  `X` |  `X` |  `X`(Note 5)   
to BOOLEAN |  `X`(Note 4)  |  `X`(Note 6)  |  `x` (Note 4)  |  `--` |  `--` |  `--` |  `X`(Note 6)  |  `X`  
  
Note 1: Datetime/interval includes `DATE`, `TIMESTAMP`, `TIMESTAMP` `WITH`
`TIMEZONE`, `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE`, `INTERVAL` `DAY` `TO`
`SECOND`, and `INTERVAL` `YEAR` `TO` `MONTH`.

Note 2: You cannot cast a `UROWID` to a `ROWID` if the `UROWID` contains the
value of a `ROWID` of an index-organized table.

Note 3: You can specify the `DEFAULT` `return_value` `ON` `CONVERSION` `ERROR`
clause for this type of conversion. You can specify the `fmt` and `nlsparam`
clauses for this type of conversion with the following exceptions: you cannot
specify fmt when converting to `INTERVAL` `DAY` `TO` `SECOND`, and you cannot
specify `fmt` or `nlsparam` when converting to `INTERVAL` `YEAR` `TO` `MONTH`.

Note 4: Casting Between Boolean and Numeric

When casting `BOOLEAN` to numeric :

  * If the boolean value is true, then resulting value is 1. 

  * If the boolean value is false, then resulting value is 0. 

When casting numeric to `BOOLEAN` :

  * If the numeric value is non-zero (e.g., 1, 2, -3, 1.2), then resulting value is true.

  * If the numeric value is zero, then resulting value is false.

Note 5: Casting Between Boolean and Char(n), NCHAR(n)

When casting `BOOLEAN` to `VARCHAR(n)`, `NVARCHAR(n)`

  * If the boolean value is true and `n` is not less than 4, then resulting value is true. 

  * If the boolean value is false and `n` is not less than 5, then resulting value is false. 

  * Otherwise, a data exception error is raised.

Note 6: Casting Character Strings to Boolean

When casting a character string to boolean, you must trim both leading and
trailing spaces of the character string first. If the resulting character
string is one of the accepted literals used to determine a valid boolean
value, then the result is that valid boolean value.

If you want to cast a named collection type into another named collection
type, then the elements of both collections must be of the same type.

See Also:

  * [Boolean Data Type](Data-Types.md#GUID-285FFCA8-390D-4FA9-9A51-47B84EF5F83A)

  * [Implicit Data Conversion](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694) for information on how Oracle Database implicitly converts collection type data into character data and [Security Considerations for Data Conversion](Data-Type-Comparison-Rules.md#GUID-6A02902A-1EF1-41E4-9494-381488BD272F)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the return value of `CAST` when it is a character value 

MULTISET

If the result set of `subquery` can evaluate to multiple rows, then you must
specify the `MULTISET` keyword. The rows resulting from the subquery form the
elements of the collection value into which they are cast. Without the
`MULTISET` keyword, the subquery is treated as a scalar subquery.

Restriction on MULTISET

If you specify the `MULTISET` keyword, then you cannot specify the `DEFAULT`
`return_value` `ON` `CONVERSION` `ERROR`, `fmt`, or `nlsparam` clauses.

DOMAIN

The `DOMAIN` clause specifies that `type_name` is a domain. `type_name` must
be the name of a domain that the user has execute privileges on.

`domain_validate_clause`

This clause is only valid when casting to domain types. It controls whether
domain constraints are applied when converting `expr` to `type_name`. If
`type_name` is a domain with constraints, and `domain_validate_clause` is not
specified, enabled constraints will be applied to `expr`. Any disabled
constraints are ignored.

VALIDATE

All the domain constraints are applied to `expr`, regardless of their state.

NOVALIDATE

None of the domain constraints are applied to `expr`, regardless of their
state.

DEFAULT return_value ON CONVERSION ERROR

This clause allows you to specify the value returned by this function if an
error occurs while converting `expr` to `type_name`. This clause has no effect
if an error occurs while evaluating `expr`.

This clause is valid if `expr` evaluates to a character string of type `CHAR`,
`VARCHAR2`, `NCHAR`, or `NVARCHAR2`, and `type_name` is `BINARY_DOUBLE`,
`BINARY_FLOAT`, `DATE`, `INTERVAL` `DAY` `TO` `SECOND`, `INTERVAL` `YEAR` `TO`
`MONTH`, `NUMBER`, `TIMESTAMP`, `TIMESTAMP` `WITH` `TIME` `ZONE`, or
`TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE`.

The `return_value` can be a string literal, null, constant expression, or a
bind variable, and must evaluate to null or a character string of type `CHAR`,
`VARCHAR2`, `NCHAR`, or `NVARCHAR2`. If `return_value` cannot be converted to
`type_name`, then the function returns an error.

fmt and nlsparam

The `fmt` argument lets you specify a format model and the `nlsparam` argument
lets you specify NLS parameters. If you specify these arguments, then they are
applied when converting `expr` and `return_value`, if specified, to
`type_name`.

You can specify `fmt` and `nlsparam` if `type_name` is one of the following
data types:

  * `BINARY_DOUBLE`

If you specify `BINARY_DOUBLE`, then the optional `fmt` and `nlsparam`
arguments serve the same purpose as for the `TO_BINARY_DOUBLE` function. Refer
to
[TO_BINARY_DOUBLE](TO_BINARY_DOUBLE.md#GUID-0BA2E065-8006-426C-A3CB-1F6B0C8F283C)
for more information.

  * `BINARY_FLOAT`

If you specify `BINARY_FLOAT`, then the optional `fmt` and `nlsparam`
arguments serve the same purpose as for the `TO_BINARY_FLOAT` function. Refer
to
[TO_BINARY_FLOAT](TO_BINARY_FLOAT.md#GUID-66A51BE2-BE4A-4B99-9C37-73B110452D27)
for more information.

  * `DATE`

If you specify `DATE`, then the optional `fmt` and `nlsparam` arguments serve
the same purpose as for the `TO_DATE` function. Refer to
[TO_DATE](TO_DATE.md#GUID-D226FA7C-F7AD-41A0-BB1D-BD8EF9440118) for more
information.

  * `NUMBER`

If you specify `NUMBER`, then the optional `fmt` and `nlsparam` arguments
serve the same purpose as for the `TO_NUMBER` function. Refer to
[TO_NUMBER](TO_NUMBER.md#GUID-D4807212-AFD7-48A7-9AED-BEC3E8809866) for more
information.

  * `TIMESTAMP`

If you specify `TIMESTAMP`, then the optional `fmt` and `nlsparam` arguments
serve the same purpose as for the `TO_TIMESTAMP` function. If you omit `fmt`,
then `expr` must be in the default format of the `TIMESTAMP` data type, which
is determined explicitly by the `NLS_TIMESTAMP_FORMAT` parameter or implicitly
by the `NLS_TERRITORY` parameter. Refer to
[TO_TIMESTAMP](TO_TIMESTAMP.md#GUID-57E09334-E3CC-4CA2-809E-F0909458BCFA)
for more information.

  * `TIMESTAMP` `WITH` `TIME` `ZONE`

If you specify `TIMESTAMP` `WITH` `TIME` `ZONE`, then the optional `fmt` and
`nlsparam` arguments serve the same purpose as for the `TO_TIMESTAMP_TZ`
function. If you omit `fmt`, then `expr` must be in the default format of the
`TIMESTAMP` `WITH` `TIME` `ZONE` data type, which is determined explicitly by
the `NLS_TIMESTAMP_TZ_FORMAT` parameter or implicitly by the `NLS_TERRITORY`
parameter. Refer to
[TO_TIMESTAMP_TZ](TO_TIMESTAMP_TZ.md#GUID-3999303B-89CA-4AA3-9817-458F36ADC9DC)
for more information.

  * `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE`

If you specify `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE` then the optional
`fmt` and `nlsparam` arguments serve the same purpose as for the
`TO_TIMESTAMP` function. If you omit `fmt`, then `expr` must be in the default
format of the `TIMESTAMP` data type, , which is determined explicitly by the
`NLS_TIMESTAMP_FORMAT` parameter or implicitly by the `NLS_TERRITORY`
parameter. Refer to
[TO_TIMESTAMP](TO_TIMESTAMP.md#GUID-57E09334-E3CC-4CA2-809E-F0909458BCFA)
for more information.

Built-In Data Type Examples

The following examples use the `CAST` function with scalar data types. The
first example converts text to a timestamp value by applying the format model
provided in the session parameter `NLS_TIMESTAMP_FORMAT`. If you want to avoid
dependency on this NLS parameter, then you can use the `TO_DATE` as shown in
the second example.

    
    
    SELECT CAST('22-OCT-1997'
           AS TIMESTAMP WITH LOCAL TIME ZONE) 
      FROM DUAL;
    
    SELECT CAST(TO_DATE('22-Oct-1997', 'DD-Mon-YYYY')
           AS TIMESTAMP WITH LOCAL TIME ZONE)
      FROM DUAL;
    

In the preceding example, `TO_DATE` converts from text to `DATE`, and `CAST`
converts from `DATE` to `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE`, interpreting
the date in the session time zone (`SESSIONTIMEZONE`).

    
    
    SELECT product_id, CAST(ad_sourcetext AS VARCHAR2(30)) text
      FROM print_media
      ORDER BY product_id;

The following examples return a default value if an error occurs while
converting the specified value to the specified data type. In these examples,
the conversions occurs without error.

    
    
    SELECT CAST(200
           AS NUMBER
           DEFAULT 0 ON CONVERSION ERROR)
      FROM DUAL;
    
    
    
    SELECT CAST('January 15, 1989, 11:00 A.M.'
           AS DATE
           DEFAULT NULL ON CONVERSION ERROR,
           'Month dd, YYYY, HH:MI A.M.')
      FROM DUAL;
    
    
    SELECT CAST('1999-12-01 11:00:00 -8:00'
           AS TIMESTAMP WITH TIME ZONE
           DEFAULT '2000-01-01 01:00:00 -8:00' ON CONVERSION ERROR,
           'YYYY-MM-DD HH:MI:SS TZH:TZM',
           'NLS_DATE_LANGUAGE = American')
      FROM DUAL;

In the following example, an error occurs while converting `'N/A'` to a
`NUMBER` value. Therefore, the `CAST` function returns the default value of
`0`.

    
    
    SELECT CAST('N/A'
           AS NUMBER
           DEFAULT '0' ON CONVERSION ERROR)
      FROM DUAL;
    

The following example converts data types `VARCHAR2`, `NUMBER` as `BOOLEAN`:

    
    
    SELECT
      CAST ( 'yes' AS BOOLEAN ),
      CAST ( true AS NUMBER ),
      CAST ( false AS VARCHAR2(10) ) ;
    
    CAST('YES'ASBOOLEAN) CAST(TRUEASNUMBER) CAST(FALSE
    -------------------- ------------------ ----------
                    TRUE                  1 FALSE
    

Collection Examples

The `CAST` examples that follow build on the `cust_address_typ` found in the
sample order entry schema, `oe`.

    
    
    CREATE TYPE address_book_t AS TABLE OF cust_address_typ;
    
    CREATE TYPE address_array_t AS VARRAY(3) OF cust_address_typ;
    
    CREATE TABLE cust_address (
      custno            NUMBER, 
      street_address    VARCHAR2(40), 
      postal_code       VARCHAR2(10), 
      city              VARCHAR2(30),
      state_province    VARCHAR2(10), 
      country_id        CHAR(2));
    
    CREATE TABLE cust_short (custno NUMBER, name VARCHAR2(31));
    
    CREATE TABLE states (state_id NUMBER, addresses address_array_t);
    

This example casts a subquery:

    
    
    SELECT s.custno, s.name,
           CAST(MULTISET(SELECT ca.street_address,   
                                ca.postal_code, 
                                ca.city, 
                                ca.state_province, 
                                ca.country_id
                           FROM cust_address ca
                           WHERE s.custno = ca.custno)
           AS address_book_t)
      FROM cust_short s
      ORDER BY s.custno;
    

`CAST` converts a varray type column into a nested table:

    
    
    SELECT CAST(s.addresses AS address_book_t)
      FROM states s 
      WHERE s.state_id = 111;
    

The following objects create the basis of the example that follows:

    
    
    CREATE TABLE projects 
      (employee_id NUMBER, project_name VARCHAR2(10));
    
    CREATE TABLE emps_short 
      (employee_id NUMBER, last_name VARCHAR2(10));
    
    CREATE TYPE project_table_typ AS TABLE OF VARCHAR2(10);
    

The following example of a `MULTISET` expression uses these objects:

    
    
    SELECT e.last_name,
           CAST(MULTISET(SELECT p.project_name
                           FROM projects p 
                           WHERE p.employee_id = e.employee_id
                           ORDER BY p.project_name)
           AS project_table_typ)
      FROM emps_short e
      ORDER BY e.last_name;

The following example casts the string `'yes'` to a boolean value, the boolean
value `true` to a `NUMBER` and the boolean value `false` to `VARCHAR2(10)`:

    
    
    SELECT 
        CAST ( 'yes' AS BOOLEAN ),
        CAST ( true AS NUMBER ),
        CAST ( false AS VARCHAR2(10) );
    
       CAST('YES'ASBOOLEAN) CAST(TRUEASNUMBER) CAST(FALSE
       -------------------- ------------------ ----------
                    TRUE                  1      FALSE
    

Domain Examples

The following example creates the domain `DAY_OF_WEEK` with a disabled check
constraint. The first query omits the `domain_validate_clause`, so uses the
constraint state to determine whether to verify the value. As this is
disabled, the database does not check the value.

The second query uses the `VALIDATE` clause. This applies the constraint to
"`N/A`", even though it's disabled. The value "`N/A`" is not in the list
permitted by the constraints, so `CAST` raises an exception.

    
    
    CREATE DOMAIN day_of_week AS VARCHAR2(3 CHAR)
      CONSTRAINT CHECK (day_of_week IN('MON','TUE','WED','THU','FRI','SAT','SUN'))
      DISABLE;
    
    
    SELECT CAST ( 'N/A' AS day_of_week ) use_constraint_state;
    
    USE_CONSTRAINT_STATE    
    --------------------
    N/A
    
    
    SELECT CAST ( 'N/A' AS day_of_week VALIDATE ) apply_constraints;
    
    ORA-11513: CAST AS DOMAIN has failed due to domain constraints.

The following example creates the domain `DAY_OF_WEEK` with an enabled check
constraint. The first query omits the `domain_validate_clause`, so uses the
constraint state to determine whether to verify the value. As this is enabled,
the database applies the constraint to "`N/A`". This is not in the list of
permitted values so `CAST` raises an error.

The second query uses the `NOVALIDATE` clause. This ignores the constraint
even though it is enabled and the statement completes without error.

    
    
    CREATE DOMAIN day_of_week AS VARCHAR2(3 CHAR)
      CONSTRAINT CHECK (day_of_week IN('MON','TUE','WED','THU','FRI','SAT','SUN'))
      ENABLE;
    
    
    SELECT CAST ( 'N/A' AS day_of_week ) use_constraint_state;
    
    ORA-11513: CAST AS DOMAIN has failed due to domain constraints.
    
    
    SELECT CAST ( 'N/A' AS DOMAIN day_of_week NOVALIDATE ) ignore_constraints;
    
    IGNORE_CONSTRAINTS    
    ------------------
    N/A
    


[← Previous](CARDINALITY.md)

[Next →](ceil-datetime.md)
