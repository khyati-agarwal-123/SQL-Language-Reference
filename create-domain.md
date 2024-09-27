[Previous](CREATE-DISKGROUP.md) [Next](CREATE-EDITION.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE DOMAIN

## CREATE DOMAIN

Purpose

Use `CREATE DOMAIN` to create a data use case domain. A use case domain is
high-level dictionary object that belongs to a schema and encapsulates a set
of optional properties and constraints.

You can define table columns to be associated with a domain, thereby
explicitly applying the domain's optional properties and constraints to the
columns.

At minimum, a domain must specify a built-in Oracle datatype. The qualified
domain name should not collide with the qualified user-defined datatypes, or
with Oracle built-in datatypes.

The domain datatype must be a single Oracle datatype. For Oracle character
data type you must specify a maximum length, one of ` VARCHAR2(L
[CHAR|BYTE])`, `NVARCHAR2(L)`, `CHAR(L [CHAR|BYTE])`, or `NCHAR(L)`.

Domain-Specific Expressions and Conditions

A domain expression can be one of simple, datetime, interval, CASE, compound,
or list domain expression :

  * A simple domain expression is one of `string`, `number`,` sequence.CURRVAL`, `sequence.NEXTVAL`, `NULL`, or` schema.domain`. It is similar to simple expressions, except that it references domain names instead of column names. It references domain names as qualified names, names of Oracle built-in domains or uses a `PUBLIC` synonym to a domain. 

  * A datetime domain expression is a datetime expression that references domain expressions only. 

  * An interval domain expression is defined just as a regular interval expression, except that it references domain expressions. For example, `(SYSTIMESTAMP - day_of_week) DAY(9) TO SECOND` is an interval domain expression. 

  * A compound domain expression is any of: `(expr)`, `expr op expr` with op `+, -, *, /, ||, `or `expr COLLATE collation_name`, where `expr` is a domain expression. 

Examples of valid compound domain expressions

    
         'email: ' || EmailAddress
    
        day_of_week + INTERVAL '1' DAY
    
        TO_CHAR(LastFour(SSN))

  * A case domain expression is a like a regular case expression except that it references domain expressions only. 

Examples of valid case domain expressions

    
        CASE 
      WHEN UPPER(DOMAIN_DISPLAY(day_of_week)) IN ('SAT','SUN')
      THEN 'weekend' 
      ELSE 'week day' 
    END 

  * Similar to the definition of use case domain expressions, a domain condition is like a regular SQL condition, except that it references only domain expressions. You can use the keyword `VALUE` in domain expressions instead of the domain name. For example: 
    
        CREATE DOMAIN day_of_week AS CHAR(3 CHAR)
       CONSTRAINT day_of_week_c
         CHECK (UPPER(VALUE) IN ('MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT', 'SUN'))
       DEFERRABLE INITIALLY DEFERRED
       DISPLAY SUBSTR(VALUE, 1, 2);

Prerequisites

To create a domain in your own schema, you must have the `CREATE DOMAIN`
system privilege.

To create a domain in another user's schema, you must have the `CREATE ANY
DOMAIN` system privilege.

Syntax

create_domain::=

  

![Description of create_domain.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_domain.gif)  
[Description of the illustration
create_domain.eps](img_text/create_domain.md)

  

create_single_column_domain::=

  

![Description of create_single_column_domain.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_single_column_domain.gif)  
[Description of the illustration
create_single_column_domain.eps](img_text/create_single_column_domain.md)

  

enum_list::=

  

![Description of enum_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/enum_list.gif)  
[Description of the illustration enum_list.eps](img_text/enum_list.md)

  

enum_item_list::=

  

![Description of enum_item_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/enum_item_list.gif)  
[Description of the illustration
enum_item_list.eps](img_text/enum_item_list.md)

  

enum_alias_list::=

  

![Description of enum_alias_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/enum_alias_list.gif)  
[Description of the illustration
enum_alias_list.eps](img_text/enum_alias_list.md)

  

column_properties_clause::=

  

![Description of column_properties_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/column_properties_clause.gif)  
[Description of the illustration
column_properties_clause.eps](img_text/column_properties_clause.md)

  

create_multi_column_domain::=

  

![Description of create_multi_column_domain.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_multi_column_domain.gif)  
[Description of the illustration
create_multi_column_domain.eps](img_text/create_multi_column_domain.md)

  

create_flexible_domain::=

  

![Description of create_flexible_domain.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_flexible_domain.gif)  
[Description of the illustration
create_flexible_domain.eps](img_text/create_flexible_domain.md)

  

[CASE Expressions](CASE-Expressions.md#GUID-
CA29B333-572B-4E1D-BA64-851FABDBAE96)

result_expr::=

  

![Description of result_expr.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/result_expr.gif)  
[Description of the illustration result_expr.eps](img_text/result_expr.md)

  

default_clause::=

  

![Description of default_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_clause.gif)  
[Description of the illustration
default_clause.eps](img_text/default_clause.md)

  

constraint_clause::=

![Description of constraint_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/constraint_clause.gif)  
[Description of the illustration
constraint_clause.eps](img_text/constraint_clause.md)

annotations_clause::=

For the full syntax and semantics of the `annotations_clause `see
[annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052).

Semantics

USECASE

This keyword is optional and is provided for semantic clarity. It indicates
that the domain is to describe a data use case.

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the domain does not exist, a new domain is created at the end of the statement.

  * If the domain exists, a new one is not created because the older one is detected. 

Using `IF EXISTS` with `CREATE` results in the following error: ` Incorrect IF
NOT EXISTS clause for CREATE statement`.

domain_name

`domain_name` follows the same restrictions as any type name and must not
collide with the name of any object in the domain schema, any Oracle supplied
data type, and any Oracle supplied domain.

These restrictions apply at a PDB-level in a CDB environment.

Note that domains are schema-level catalog objects, and therefore subject to
schema-level object restrictions.

datatype

`datatype` must be an Oracle built-in data type like:

  * `CHAR(L [CHAR|BYTE]), NCHAR(L), VARCHAR(L [CHAR|BYTE]), VARCHAR2(L [CHAR|BYTE]), NVARCHAR2(L) `

  * `NUMBER[p, [s]]`, `FLOAT`, `BINARY_FLOAT`, `BINARY_DOUBLE`

  * `RAW`, `LONG RAW` (extended included) 

  * `DATE`, `TIMESTAMP (WITH (LOCAL) TIME ZONE)`, `INTERVAL`

  * `BFILE`, `BLOB`, `CLOB`, `NCLOB`

  * `JSON` native datatype 

  * `BOOLEAN`

ENUM

Specify `ENUM` to create an enumeration domain. An enumeration domain consists
of a set of names and, optionally, a value corresponding to name. The name has
to be a valid SQL identifier and every specified value must be a literal or a
constant expression. The values can be of any datatype that are supported for
a data use case Domain, but all of them must agree on that datatype.

An enumeration domain has a default check-constraint, a display-expression,
and an order-expression. This check-constraint cannot be dropped using `ALTER
DOMAIN`.

The names inside a enumeration domain can be used wherever a literal is
allowed in a scalar SQL expression, and the domain itself can be used in the`
FROM` clause of a `SELECT` statement as if it were a table.

The collection of names (`name` ) in an enumeration domain must be unique.
There is no limit on number of names (or their aliases) in a enumeration,
besides whatever limits already exist in Oracle SQL.

The datatype of all the values (`value` ) must match. If you do not specify a
value, the default value of the first name is 1, and the value of every other
unspecified name is one more than the previous value.

The expression defining the default must be one of the enumeration names
without any expression besides that.

STRICT

When you specify `STRICT`, table columns linked with the domain must have the
same data type limits as the corresponding domain columns. For example, if the
data type of a domain column is `NUMBER(10)`, you can only associate it with
columns declared as `NUMBER(10)`. Applying the domain to columns of`
NUMBER(9)` or `NUMBER(11)` will raise a type error.

If you omit `STRICT`, you can link the domain to columns with type limits
greater than or equal to the domain's limit. For example, you can apply a non-
strict domain with the data type `NUMBER(10)` to columns with the data type
`NUMBER(20)`.

If you associate a column with a domain without specifying the column's data
type, then it uses `STRICT` semantics.

default_clause

If you specify the `ON NULL` clause, an implicit `NOT NULL` constraint is
added.

default_expression

`default_expression` must be a domain expression and must conform to all the
restrictions on default column expressions of the given datatype, when applied
to domain expressions:

  * `default_expression` cannot contain a SQL function that returns a domain reference, or a nested function invocation, and it cannot be a subquery expression. 

  * The dataype of `default_expression` must match the domain's specified datatype. 

  * As a domain expression, `default_expression` cannot refer to any table or column. It cannot refer to any other domain name. 

  * `default_expression` may refer to `NEXTVAL` and `CURRVAL` for a sequence. It cannot reference a PL/SQL function. 

constraint_clause

Note that domain constraints can have optional names. They are `NOT NULL`,
`NULL` or `CHECK` constraints. Multiple such constraint clauses can be
specified both at the column and domain level.

The `CHECK` conditions as well as expressions in `ALTER DOMAIN` can only refer
to domain columns. If the domain has a single column, the column name is
either the domain name or the keyword `VALUE`, but the same expression cannot
contain both domain name and `VALUE` as column name.

`constraint_name` is optional. When specified, it must not collide with a name
of any other constraint in the domain's schema (in the given PDB if in a CDB
environment). When not specified, a system-generated name will be used. Domain
constraints follow the same rules as table and column-level constraints: a
named table or column-level constraint cannot coincide with the name of any
other constraint in the same schema. Domain constraints can share names with
tables, even in the same schema. They can share names with columns, and it is
possible for a constraint to have the same name as the table or column it is
defined on.

The `CHECK` condition must be a domain logical condition and must conform to
all the restrictions on `CHECK` constraints translated to domain expressions:

  * It can only refer to `domain_name`, like a `CHECK` constraint on a column can only refer to a column. It cannot refer to any columns in any table or view, even within the domain schema. 

  * Subquery or scalar query expressions cannot be used.

  * Condition cannot refer to non-deterministic functions (like `CURRENT_DATE`), or user-defined PL/SQL functions. 

  * `CHECK IS JSON (STRICT)` constraints are allowed. 

`CHECK IS JSON(VALIDATE USING schema_constant_text)` is allowed. You can
specify the JSON schema and use it to validate that the JSON column respects
the schema definition that is specified. `schema_constant_text` can be a
constant literal with the JSON schema text, or a bind variable for the JSON
schema text. The bind must be a runtime constant. It cannot be a domain.

If you use the `IS JSON` constraint without specifying `VALIDATE USING
schema_constraint`, any JSON value will be accepted. But when you specify a
JSON Schema with `VALIDATE USING schema_constraint` , and the entered input
data into the table column does not follow the schema, a JSON schema
validation error is raised.

You can use shorthand syntax to specify the JSON schema with `VALIDATE USING
schema_constant_text`.

Just as for table and column-level constraints, you can specify only one JSON
constraint for a given table column

  * The `CHECK` constraint condition is applied to one value at a time, and it is satisfied if the `CHECK` condition, with `domain_name` substituted by the value, evaluates to `TRUE` or `UNKNOWN`. 

Domain constraints may be enforced in any order.

NULL constraint means that values of the domain are allowed to be NULL, and
this is the default.

When `constraint_state` is not specified, the constraint is `NOT DEFERABLE
INITIALLY IMMEDIATE`.

COLLATE

When collation is specified, it conforms to all the restrictions of column-
level or schema-level collation. The datatype must be a character data type if
collation is specified.

An error will be raised when creating a table with a column marked of a domain
with a collation different than the column's collation.

An error will be raised when altering a column to have a collation different
than the collation of the column's domain.

This should ensure the invariant that all columns of a domain with a collation
specified have the same collation as that of their domain. If no collation is
specified and datatype is collatable, the column's collation will be used if
specified, or otherwise the underlying default datatype collation in the
domain's schema is used.

If no collation is specified and datatype is collatable, the column's
collation will be used if specified.

You can specify the `COLLATE` clause only if the `COMPATIBLE` initialization
parameter is set to 12.2 or greater, and the `MAX_STRING_SIZE` initialization
parameter is set to `EXTENDED`.

display_expression

Use `display_expression` to format the data according to domain
specifications. It can be of any data type allowed as a domain data type.
`display_expression` must be a domain expression that does not contain table
or view columns, subqueries, non-deterministic functions, or PL/SQL functions.
It can refer to `domain_name`. If you do not specify collation for the
expression, then `display_expression` uses the domain's collation, if it is
specified.

order_expression

Use `order_expression` to order and compare values for domain specifications.

`order_expression` must conform to the same restrictions as
display_expressions, and additionally must be of a byte or char-comparable
data type. It returns `order_expression` with `domain_name` replaced by
expression, if `order_expression` is specified for the expression's domain, or
expression otherwise

annotations_clause

For examples of the `annotations_clause` see the examples at the end.

For the full semantics of the annotations clause see
[annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052).

FROM Clause of Create Flexible Domain

`expr` and `comparison_expr` reference domain discriminant columns in the list
`domain_discriminant_column`.

The `FROM` clause for flexible domain is either a `DECODE` or a `CASE`
expression that refers only to discriminant column names (in the list
following `CHOOSE DOMAIN USING`) in the search expressions and has only domain
name followed by a list of columns in the result expressions. The columns in
the result expression must be only columns in the domain column list
(following `CREATE FLEXIBLE DOMAIN`).

Examples

Create Domain year_of_birth

The following example creates the single column domain `year_of_birth`. The
check constraint ensures that the column's value is an integer with a value
greater than or equal to 1900. The display clause formats the output of calls
to `domain_display` to either `19-YY` or `20-YY`, where `YY` is the last two
digits of the value. The order clause sorts calls to `domain_order` in order
by the column value minus 1900.

    
    
    CREATE DOMAIN year_of_birth AS NUMBER(4)
          CONSTRAINT CHECK ( (trunc(year_of_birth) = year_of_birth) and (year_of_birth >= 1900) ) 
          DISPLAY (CASE WHEN year_of_birth < 2000 THEN '19-' ELSE '20-' END) || MOD(year_of_birth, 100)
          ORDER year_of_birth-1900 ;
    

Create Domain day_of_week

The following statement creates the single column domain `day_of_week`. The
check constraint ensures that its values are one of `MON`, `TUE`, `WED`,
`THU`, `FRI`, `SAT`, `SUN`. The initially deferred clause delays validation of
these values until commit time. The order clause ensures the values are sorted
by day of week instead of alphabetically when calling `domain_order`.

    
    
    CREATE DOMAIN day_of_week AS CHAR(3 CHAR)
       CONSTRAINT day_of_week_c
         CHECK (day_of_week IN ('MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT', 'SUN'))   
       INITIALLY DEFERRED
       ORDER CASE day_of_week
          WHEN 'MON' THEN 0
          WHEN 'TUE' THEN 1
          WHEN 'WED' THEN 2
          WHEN 'THU' THEN 3
          WHEN 'FRI' THEN 4
          WHEN 'SAT' THEN 5
          WHEN 'SUN' THEN 6
          ELSE 7
      END;

From 23.3 you can associate columns of data type `CHAR(L CHAR)` with the
domain with any value for `L`.

Create Domain email

The following example creates the sequence `email_seq`. It then creates the
single column domain` email`. This uses the sequence to generate email
addresses in the form `nnn@domain.com` when you insert null into columns with
this domain, where `nnn` are the numbers generated by the sequence. The
constrains ensures that email addresses are of the form `sss@sss.sss`, where
`sss` is any nonwhitespace character.

The display clause formats the output of calls to `domain_display` to`
---sss.sss`, where `sss` is the nonwhitespace characters after the @ sign.

    
    
    CREATE SEQUENCE IF NOT EXISTS email_seq;
    
    CREATE DOMAIN email AS VARCHAR2(30)  
        DEFAULT ON NULL email_seq.NEXTVAL || '@domain.com'
        CONSTRAINT EMAIL_C CHECK (REGEXP_LIKE (email, '^(\S+)\@(\S+)\.(\S+)$'))
        DISPLAY '---' || SUBSTR(email, INSTR(email, '@') + 1);
    

Create a Strict Domain dept_codes

The following statement creates the domain `dept_codes`. The check constraint
ensures its values are greater than 99 excluding 200. It adds the annotation
`Title` with the value "`Domain Annotation`". You can only link this domain
with columns of type `NUMBER(3)`.

    
    
    CREATE DOMAIN dept_codes AS NUMBER(3) STRICT
          CONSTRAINT dept_chk CHECK (dept_codes > 99 AND dept_codes != 200) 
          ANNOTATIONS (Title 'Domain Annotation');

Create Domain hourly_wages

The following statement creates the single column domain `hourly_wages`. It
defaults to 15 when inserting null into columns with this domain. The check
constraint ensures the values are between 7 and 1,000.

The display clause returns its value in the format `$999.99` when calling
`domain_display`. The order clause multiplies its value by negative one, so
sorting by `domain_order` sorts from high to low. It has the annotation
`Title` with the value "`Domain Annotation`".

    
    
    CREATE DOMAIN hourly_wages AS NUMBER(10)
           DEFAULT ON NULL 15
           CONSTRAINT minimal_wage_c
             CHECK (hourly_wages >= 7 and hourly_wages <=1000) ENABLE
           DISPLAY TO_CHAR(hourly_wages, '$999.99')
           ORDER ( -1*hourly_wages )
           ANNOTATIONS (Title 'Domain Annotation');
     

Add Annotations to a Multi Column Domain US_City at Column and Domain Levels

The following statement creates the multicolumn domain `US_city`. This has
three columns: `name`, `state`, and `zip`. All columns have the `Address`
annotation.

The check constraint ensures that the permitted values for state are `CA`,
`AZ`, and `TX` and zip is less than `100000`. The display clause returns calls
to `domain_display` in the format name `||', '|| state ||', '||TO_CHAR(zip)`.

The order clause sorts calls to `domain_order` by the concatenation of state,
then zip, then name. The domain has an object level annotation `Title` with
the value "`Domain Annotation`" and and three column level annotations
`Address` without a value, one for each column.

    
    
    CREATE DOMAIN US_city AS
      (
        name  AS VARCHAR2(30) ANNOTATIONS (Address),
        state AS VARCHAR2(2) ANNOTATIONS (Address),
        zip AS NUMBER ANNOTATIONS (Address)
      )
      CONSTRAINT City_CK CHECK(state in ('CA','AZ','TX') and zip < 100000)
      DISPLAY name||', '|| state ||', '||TO_CHAR(zip)
      ORDER state||', '||TO_CHAR(zip)||', '||name
      ANNOTATIONS (Title 'Domain Annotation');
    

Create a Flexible Domain

The following examples create the flexible domain `expense_details`. To do
this, you must first create the domains `flight_details`, `meals_details`, and
`lodging_details`. These are multicolumn domains with check constraints to
ensure the domain columns store appropriate values for the expense type.

For `flight_details`, this means the `flight_num` are two strings separated by
a dash, and the origin and destination are both three character strings.

For `meals_details`, the restaurant is mandatory, the `meal_type` one of
`Breakfast`, `Lunch` or `Dinner`, and `diner_count` is non-null.

For `lodging_details`, the hotel must be non-null and the `nights_count`
greater than zero.

The flexible domain `expense_details` then chooses between these based on the
value in the typ column.

In the `FROM DECODE` example:

  * if `typ` = `Flight`, it uses the `flight_details` domain. The flexible domain columns `val1`, `val2`, and `val3` map to `flight_num`, `origin`, and `destination` in the` flight_details` domain. 

  * if` typ` = `Meals`, it uses the `meals_details` domain. The flexible domain columns `val1`, `val2`, and `val4` map to` restaurant`, `meal_type`, and `diner_count` respectively in the `meals_details` domain. 

  * if `typ` = `Lodging`, it uses the `lodging_details` domain. The flexible domain columns `val1` and `val4` map to `hotel` and `nights_count` respectively in the `lodging_details` domain. 

In the `FROM CASE` flexible domain:

  * If `typ` starts with letters `A-G`, it uses the `flight_details` domain. 

  * If `typ` = `Meals`, it uses the `meals_details` domain. 

  * If typ starts with `Lodg`, it uses the `lodging_details` domain. 

The column mappings are the same as in the `FROM DECODE` example.

Create Domain flight_details

    
    
    CREATE DOMAIN flight_details AS
      (
       flight_num AS VARCHAR2(100) NOT NULL,
       origin AS VARCHAR2(200)
         CONSTRAINT origin_3_char_c CHECK (LENGTH(origin) = 3),
       destination AS VARCHAR2(200)
         CONSTRAINT dest_3_char_c CHECK (LENGTH(destination) = 3)
      )
      CONSTRAINT flight_c
        CHECK
          (
            flight_num LIKE '%-%' AND
            origin IS NOT NULL AND
            destination IS NOT NULL
          )
      CONSTRAINT origin_dest_different_c
        CHECK (origin <> destination)
      DISPLAY flight_num||', '||origin||', '||destination
      ORDER flight_num||destination;

Create Domain meals_details

    
    
    CREATE DOMAIN meals_details AS
        (
           restaurant AS VARCHAR2(100) NOT NULL,
           meal_type AS VARCHAR2(200),
           diner_count AS NUMBER
        )
        CONSTRAINT meals_c
          CHECK
           (
             restaurant IS NOT NULL AND
             meal_type IN ('Breakfast', 'Lunch', 'Dinner') AND
             diner_count IS NOT NULL
           )
        DISPLAY meal_type||', '||restaurant||', '||diner_count;

Create Domain lodging_details

    
    
     CREATE DOMAIN lodging_details AS
        (
          hotel AS VARCHAR2(100) NOT NULL,
          nights_count AS NUMBER
        )
        CONSTRAINT lodging_c
         CHECK (hotel IS NOT NULL AND nights_count > 0)
        DISPLAY hotel||', '||nights_count;

Create a Flexible Domain expense_details Using FROM DECODE

    
    
    CREATE FLEXIBLE DOMAIN expense_details (val1, val2, val3, val4)
        CHOOSE DOMAIN USING (typ VARCHAR2(10))
        FROM DECODE(typ,
                  'Flight', flight_details(val1, val2, val3),
                  'Meals', meals_details(val1, val2, val4),
                  'Lodging', lodging_details(val1, val4));

Create a Flexible Domain expense_details Using FROM CASE

    
    
    CREATE FLEXIBLE DOMAIN expense_details (val1, val2, val3, val4)
        CHOOSE DOMAIN USING(typ VARCHAR2(10))
        FROM CASE
            WHEN typ BETWEEN 'A' AND 'G' THEN flight_details(val1, val2, val3)
            WHEN typ = 'Meals' THEN meals_details(val1, val2, val4)
            WHEN typ LIKE 'Lodg%' THEN lodging_details(val1, val4)
          END;

Create Domain Specifying a JSON Schema for Validation

The following example creates domain `w2_form` of type `JSON` with a
constraint that checks that the value is a JSON object that complies with the
provided JSON Schema. The check constraint uses `IS JSON VALIDATE USING`
`schema_constant_text`:

    
    
    CREATE DOMAIN w2_form AS JSON 
      CONSTRAINT CHECK (VALUE IS JSON VALIDATE USING '{ 
        "title": "W2_form",
        "type": "object",
        "properties": {
        "social_security_number": {
        "type": "string",
        "description": "The person social security number."
       },
       "wages": {
         "description": "total wages",
         "type": "number",
         "minimum": 0
       },
       "social_security_wages": {
         "type": "number",
         "description": "wages subject to social security tax" 
       },
       "Federal Income Tax Withheld": {
         "type": "number",
         "description": "withheld of tax to federal income tax"
       },
       "Social Security Tax Withheld": {
         "type": "number",
         "description": "withheld of social security tax"
       }
       },
       "required": [
         "social_security_number", 
         "wages", 
         "Federal Income Tax Withheld" 
        ]
       }'
     );
    

The following statement creates table `tax_report` where column `w2_form` is
associated with domain `w2_form` to ensure that its content conforms to the
schema defined in the domain`w2_form`:

    
    
    CREATE TABLE tax_report(id NUMBER, income JSON DOMAIN w2_form);

Before the data is inserted into the income column, it is checked against the
JSON Schema. If the data is not valid, an error is raised.

Example of valid data:

    
    
    INSERT INTO tax_report VALUES 
      (1, '{"wages": 100, "social_security_number": "111", "Federal Income Tax Withheld":10}'
       );
    1 row created

Example of invalid data:

    
    
    INSERT INTO tax_report VALUES 
      (2, '{"wages": 100}'
       );
    ERROR at line 1:
    ORA-40875: JSON schema validation error

Create a Domain Specifying a JSON Schema Using Shorthand Syntax

    
    
    CREATE DOMAIN w2_form AS JSON VALIDATE USING '{
      "title": "W2_form",
      "type": "object",
      "properties": {
        "social_security_number": {
        "type": "string",
        "description": "The person social security number."
      },
      "wages": {
        "description": "total wages",
        "type": "number",
        "minimum": 0
      },
      "social_security_wages": {
        "type": "number",
        "description": "wages subject to social security tax"
      },
      "Federal Income Tax Withheld": {
        "type": "number",
        "description": "withheld of tax to federal income tax"
      },
      "Social Security Tax Withheld": {
        "type": "number",
        "description": "withheld of social security tax"
      }
     },
     "required": [ 
       "social_security_number", 
       "wages", 
       "Federal Income Tax Withheld"
      ]
     }';

Example: Create a Domain with an Annotation Stored as JSON and Query its Value

The following example creates a domain with an annotation `allowed_operations`
specified as a JSON string which contains a nested JSON object:

    
    
    CREATE DOMAIN email AS VARCHAR2(30)  
        CONSTRAINT EMAIL_C CHECK (REGEXP_LIKE (email, '^(\S+)\@(\S+)\.(\S+)$'))
        DISPLAY '---' || SUBSTR(email, INSTR(email, '@') + 1)
        ANNOTATIONS(allowed_operations 
    '{
        "allowed_operations": {
            "title": "Allowed operations",
            "operations": [
                "Sort",
                "Group By",
                "Picklist"
            ]
        }
    }');
    

Now you can run the following query to retrieve values for the annotation
`allowed_operations`:

    
    
    SELECT jt.* FROM user_annotations_usage a,
      JSON_TABLE (annotation_value,
        '$.allowed_operations.operations[*]'
        COLUMNS (value VARCHAR2(50 CHAR) PATH '$')) jt
      WHERE annotation_name = 'ALLOWED_OPERATIONS'
      AND object_name = 'EMAIL' ;
        

The output is:

    
    
    VALUE
    ----------------------------------------
    Sort
    Group By
    Picklist

Example: Create a Domain with an Annotation Stored as JSON and Query its Value

The following example creates a domain with the annotation `display_units`
specified as a JSON string containg an array to store the possible display
units:

    
    
    CREATE DOMAIN temperature AS NUMBER(3)
    ANNOTATIONS (display_units '{ "units": ["celsius", "fahrenheit"] }');
    

Now you can query for the values of the annotation:

    
    
    SELECT jt.* FROM user_annotations_usage,
      JSON_TABLE(annotation_value, '$.units[*]'
        COLUMNS (value VARCHAR2(30 CHAR) PATH '$')) jt
      WHERE annotation_name = 'DISPLAY_UNITS'
      AND object_name = 'TEMPERATURE';

The output is:

    
    
    VALUE
    --------------------------------------------
    celsius
    fahrenheit

Example: JSON Schema Using a Use Case Domain

You can register a JSON schema as a use case domain.

The following example creates domain `dj5` as a JSON schema object:

    
    
    CREATE DOMAIN dj5 AS JSON CONSTRAINT dj5chk
        CHECK (dj5 IS JSON validate
              '{
               "type": "object",
               "properties": {
                 "a": {
                   "type": "number"
                  }
               }
             }'
        );   
    

You can then create a table `jtab` and associate column `jcol` with the domain
`dj5`:

    
    
    CREATE TABLE jtab(
          id   NUMBER PRIMARY KEY,
         jcol JSON DOMAIN dj5
        );
    

Examples for ENUM Domains

Example: Create ENUM Domain order_status

The following example creates an enumeration domain `order_status` with a
collection of names `New`, `Open`, `Shipped`, `Closed`, `Cancelled`:

    
    
    CREATE DOMAIN order_status AS
      ENUM (
        New ,     
        Open ,
        Shipped ,
        Closed ,
        Cancelled
      );
    

Example: Query Enumeration Domain order_status

Unlike a regular domain, the enumeration domain `order_status` can be treated
as a table and queried via `SELECT` as follows:

    
    
    SELECT * FROM order_status;

The result is:

    
    
    ENUM_NAME     ENUM_VALUE
    - - - - -    - - - - - -
    NEW                    1
    OPEN                   2
    SHIPPED                3
    CLOSED                 4
    CANCELLED              5

Example: Enumeration Domain order_status as Datatype of Column:

Like a regular single-column domain, an enumeration domain can be used to
define the data type of a column in a table. In the example below, the
enumeration domain `order_status` is used as the data type of column `status`
in table `orders`:

    
    
    CREATE TABLE orders ( 
         id      NUMBER,
         cust    VARCHAR2(100),
         status  ORDER_STATUS
    );

Using `DESCRIBE` on the `orders` table shows the `status` column as a numeric
column with a single column domain `order_status`:

    
    
    DESCRIBE orders;

The result is:

    
    
    Name    Null ?  Type
    ----    ------  ----
    ID              NUMBER
    CUST            VARCHAR2 (100)
    STATUS          NUMBER SCOTT.ORDER_STATUS

You can construct each row to insert into the the `orders` table using the
appropriate `order_status`:

    
    
    INSERT INTO orders VALUES
      (1, 'Costco', order_status.open ),
      (2, 'BMW', order_status.closed ),
      (3, 'Nestle', order_status.shipped );
    
     3 rows created .

Use the `domain_display` function to list the rows in the `orders` table:

    
    
    SELECT ID, DOMAIN_DISPLAY(STATUS) FROM orders;

The result is:

    
    
    ID        STATUS
    ---       ------
    1         OPEN
    2         CLOSED
    3         SHIPPED

The actual values stored in the status column are the values you associated
with the status when you created the enumerated domain `order_status`, 2 for
`OPEN`, 4 for `CLOSED`, and 3 for `SHIPPED`:

    
    
    SELECT ID, STATUS FROM orders;

The result is:

    
    
    ID        STATUS
    ---       ------
    1         2
    2         4
    3         3

Since the underlying datatype of the status column is a number, you can
directly update the column with a numeric value as long as is passes the
domain check-constraint:

    
    
    UPDATE orders SET STATUS = 2 WHERE STATUS = 5;
    
    1 ROW UPDATED.

Since enumeration names are placeholds for literal values, you can use them
anywhere where SQL allows literals:

    
    
    SELECT 2 * ORDER_STATUS.CANCELLED;

The result is:

    
    
    2*ORDER_STATUS.CANCELLED
    –-----------------------
                          10

Example: Create ENUM Domain days_of_week

The following example creates an enumeration domain `days_of_week` with a
collection of names that comprises the days of the week.

Each value has a pair of names, only the first name of the pair has an
assigned value. There are two names for each value, the full day name and the
first two letters of the day's name. The names `Sunday` and `Su` both have the
value zero. The value then increases by one for each pair of names. So
`Monday` and `Mo` have the value 1, `Tuesday` and `Tu` have the value 2 and so
on up to `Saturday` and `Sa` which have the value 6.

    
    
    CREATE DOMAIN days_of_week AS
      ENUM (
        Sunday     = Su  = 0,     
        Monday     = Mo,
        Tuesday    = Tu,
        Wednesday  = We,
        Thursday   = Th,
        Friday     = Fr,
        Saturday   = Sa
      );
    


[← Previous](CREATE-DISKGROUP.md)

[Next →](CREATE-EDITION.md)
