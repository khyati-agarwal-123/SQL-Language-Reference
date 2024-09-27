[Previous](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md) [Next](CREATE-
LIBRARY.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE JSON RELATIONAL DUALITY VIEW

## CREATE JSON RELATIONAL DUALITY VIEW

Purpose

JSON-relational duality views expose data in relational tables as JSON
documents. The documents are materialized on demand, not stored as such.
Duality views give your data a conceptual and an operational duality as it is
organized both relationally and hierarchically. You can base different duality
views on data stored in one or more of the same tables, providing different
JSON hierarchies over the same, shared data. This means that applications can
access (create, query, modify) the same data as a collection of JSON documents
or as a set of related tables and columns, and both approaches can be employed
at the same time.

A flex column in a table underlying a JSON-relational duality view lets you
add and redefine fields of the document object produced by that table. This
provides a certain kind of schema flexibility to a duality view, and to the
documents it supports. For more information on flex columns in a table
underlying a JSON-relational duality view see [JSON Data Stored in JSON-
Relational Duality Views](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=JSNVU-GUID-DB782F3B-F115-4D75-B0BC-9FE06725309F) of the
JSON-Relational Duality Developer's Guide

You define a duality view against a set of tables related by primary key (PK),
foreign key (FK) or unique key constraints (UK). The following rules apply:

  * The constraints must be declared in the database but need not be enforced (can be `RELY`` DISABLE` constraints). 

  * The relationships type can be 1-to-1, 1-to-N and N-to-M (using a mapping table with two FKs). The N-to-M relationship can be thought of as the combination of 1-to-N and 1-to-1 relationship

  * Columns of two or more tables with 1-to-1 or N-to-1 relationships can be merged into the same JSON object via `UNNEST`. Otherwise a nested JSON object is created. 

  * Tables with a 1-to-N relationship create a nested JSON array. 

  * A duality view has only one column of type `JSON`. 

  * Each row in the duality view is one JSON object, which is typically a hierarchy of nested objects and arrays.

  * Each application object is built from values originating from one or multiple rows from the underlying tables of that view. Typically, each table contributes to one (nested) JSON object.

Note:

The SQL data types allowed for a column in a table underlying a duality view
are `BINARY_DOUBLE`, `BINARY_FLOAT`, `BLOB`, `BOOLEAN`, `CHAR`, `CLOB`,
`DATE`, `JSON`, `INTERVAL DAY TO SECOND`, `INTERVAL YEAR TO MONTH`, `NCHAR`,
`NCLOB`, `NUMBER`, `NVARCHAR2`, `VARCHAR2`, `RAW`, `TIMESTAMP`, `TIMESTAMP
WITH TIME ZONE`, and `VECTOR`. An error is raised if you specify any other
column data type.

See Also:

[JSON-Relational Duality Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=JSNVU-GUID-CE7227BF-B4AF-4024-A578-ED52795F4525)

Syntax

create_json_relational_duality_view::=

  

![Description of create_json_relational_duality_view.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_json_relational_duality_view.gif)  
[Description of the illustration
create_json_relational_duality_view.eps](img_text/create_json_relational_duality_view.md)

  

object_gen_clause::=

  

![Description of object_gen_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/object_gen_clause.gif)  
[Description of the illustration
object_gen_clause.eps](img_text/object_gen_clause.md)

  

key_value_clause::=

  

![Description of key_value_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/key_value_clause.gif)  
[Description of the illustration
key_value_clause.eps](img_text/key_value_clause.md)

  

flex_clause::=

  

![Description of flex_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/flex_clause.gif)  
[Description of the illustration flex_clause.eps](img_text/flex_clause.md)

  

column_tags_clause::=

  

![Description of column_tags_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/column_tags_clause.gif)  
[Description of the illustration
column_tags_clause.eps](img_text/column_tags_clause.md)

  

duality_view_subquery::=

  

![Description of duality_view_subquery.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/duality_view_subquery.gif)  
[Description of the illustration
duality_view_subquery.eps](img_text/duality_view_subquery.md)

  

table_tags_clause::=

  

![Description of table_tags_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/table_tags_clause.gif)  
[Description of the illustration
table_tags_clause.eps](img_text/table_tags_clause.md)

  

graphql_query_for_DV::=

![Description of graphql_query_for_dv.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/graphql_query_for_dv.gif)  
[Description of the illustration
graphql_query_for_dv.eps](img_text/graphql_query_for_dv.md)

root_query_field::=

  

![Description of root_query_field.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/root_query_field.gif)  
[Description of the illustration
root_query_field.eps](img_text/root_query_field.md)

  

( [directives::=](create-json-relational-duality-view.md#GUID-64B579AD-
BF97-4B27-BF22-94C1FB6FD6DF__SECTION_VXB_R2Z_FYB), [selection_set::=](create-
json-relational-duality-view.md#GUID-64B579AD-
BF97-4B27-BF22-94C1FB6FD6DF__SECTION_GJN_GGZ_FYB))

root_query_field_name::=

![Description of root_query_field_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/root_query_field_name.gif)  
[Description of the illustration
root_query_field_name.eps](img_text/root_query_field_name.md)

directives::=

![Description of directives.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/directives.gif)  
[Description of the illustration directives.eps](img_text/directives.md)

directive::=

![Description of directive.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/directive.gif)  
[Description of the illustration directive.eps](img_text/directive.md)

arguments::=

![Description of arguments.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/arguments.gif)  
[Description of the illustration arguments.eps](img_text/arguments.md)

argument::=

![Description of argument.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/argument.gif)  
[Description of the illustration argument.eps](img_text/argument.md)

name::=

  

![Description of name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/name.gif)  
[Description of the illustration name.eps](img_text/name.md)

  

name_start::=

![Description of name_start.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/name_start.gif)  
[Description of the illustration name_start.eps](img_text/name_start.md)

name_continue::=

![Description of name_continue.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/name_continue.gif)  
[Description of the illustration
name_continue.eps](img_text/name_continue.md)

letter::=

![Description of letter.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/letter.gif)  
[Description of the illustration letter.eps](img_text/letter.md)

upper_letter::=

![Description of upper_letter.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/upper_letter.gif)  
[Description of the illustration upper_letter.eps](img_text/upper_letter.md)

lower_letter::=

![Description of lower_letter.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lower_letter.gif)  
[Description of the illustration lower_letter.eps](img_text/lower_letter.md)

digit::=

![Description of digit.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/digit.gif)  
[Description of the illustration digit.eps](img_text/digit.md)

selection_set::=

  

![Description of selection_set.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/selection_set.gif)  
[Description of the illustration
selection_set.eps](img_text/selection_set.md)

  

selection_list::=

![Description of selection_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/selection_list.gif)  
[Description of the illustration
selection_list.eps](img_text/selection_list.md)

selection::=

![Description of selection.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/selection.gif)  
[Description of the illustration selection.eps](img_text/selection.md)

field::=

  

![Description of field.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/field.gif)  
[Description of the illustration field.eps](img_text/field.md)

  

( [directives::=](create-json-relational-duality-view.md#GUID-64B579AD-
BF97-4B27-BF22-94C1FB6FD6DF__SECTION_VXB_R2Z_FYB), [selection_set::=](create-
json-relational-duality-view.md#GUID-64B579AD-
BF97-4B27-BF22-94C1FB6FD6DF__SECTION_GJN_GGZ_FYB))

alias::=

![Description of alias.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alias.gif)  
[Description of the illustration alias.eps](img_text/alias.md)

query_field_name::=

![Description of query_field_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/query_field_name.gif)  
[Description of the illustration
query_field_name.eps](img_text/query_field_name.md)

query_scalar_field_name::=

![Description of query_scalar_field_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/query_scalar_field_name.gif)  
[Description of the illustration
query_scalar_field_name.eps](img_text/query_scalar_field_name.md)

query_object_field_name::=

![Description of query_object_field_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/query_object_field_name.gif)  
[Description of the illustration
query_object_field_name.eps](img_text/query_object_field_name.md)

fragment_spread::=

![Description of fragment_spread.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/fragment_spread.gif)  
[Description of the illustration
fragment_spread.eps](img_text/fragment_spread.md)

fragment_name

![Description of fragment_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/fragment_name.gif)  
[Description of the illustration
fragment_name.eps](img_text/fragment_name.md)

quoted_name::=

![Description of quoted_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/quoted_name.gif)  
[Description of the illustration quoted_name.eps](img_text/quoted_name.md)

lower_case_name::=

  

![Description of lower_case_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lower_case_name.gif)  
[Description of the illustration
lower_case_name.eps](img_text/lower_case_name.md)

  

name_continue_lower::=

![Description of name_continue_lower.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/name_continue_lower.gif)  
[Description of the illustration
name_continue_lower.eps](img_text/name_continue_lower.md)

field_name::=

![Description of field_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/field_name.gif)  
[Description of the illustration field_name.eps](img_text/field_name.md)

scalar_field_name::=

![Description of scalar_field_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/scalar_field_name.gif)  
[Description of the illustration
scalar_field_name.eps](img_text/scalar_field_name.md)

object_field_name::=

![Description of object_field_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/object_field_name.gif)  
[Description of the illustration
object_field_name.eps](img_text/object_field_name.md)

object_field_name_lower::=

  

![Description of object_type_name_lower.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/object_type_name_lower.gif)  
[Description of the illustration
object_type_name_lower.eps](img_text/object_type_name_lower.md)

  

schema_name_lower::=

![Description of schema_name_lower.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/schema_name_lower.gif)  
[Description of the illustration
schema_name_lower.eps](img_text/schema_name_lower.md)

simple_object_type_name_lower::=

![Description of simple_object_type_name_lower.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/simple_object_type_name_lower.gif)  
[Description of the illustration
simple_object_type_name_lower.eps](img_text/simple_object_type_name_lower.md)

Semantics

The JSON realtional duality view (DV) has only one column of data type `JSON`.
The column contains the JSON object which is a representation of a application
object. The column name is always `DATA`.

The duality view is read-only by default. Read-only means that the following
annotations are in effect: `NOINSERT`, `NODELETE`, `NOUPDATE`.

OR REPLACE

Specify `OR REPLACE` to re-create the view if it already exists. You can use
this clause to change the definition of an existing view without dropping, re-
creating, and regranting object privileges previously granted on it.

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the view does not exist, a new view is created at the end of the statement.

  * If the view exists, this is the view you have at the end of the statement. A new one is not created because the older one is detected.

You can have only one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a
time. Using both in the same statement results in the following error:

`ORA-11541`: `REPLACE` and `IF NOT EXISTS` cannot coexist in the same DDL
statement.

Using `IF EXISTS` with `CREATE` results in `ORA-11543`: Incorrect `IF NOT
EXISTS` clause for `CREATE` statement

table_tags_clause

You can mark the view as updatable using the following keyword inside a `WITH`
clause:

  * `WITH INSERT`

  * `WITH UPDATE`

  * `WITH DELETE`

You can combine keywords together by separting them with a comma, for example:
`WITH INSERT, UPDATE`

column_tags_clause

You can mark individual columns with `WITH UPDATE` or `WITH NOUPDATE`. This
supercedes table-level annotation.

Column Properties for Updatability

If the `FROM` clause is marked with such keywords, then this sets the default
for all columns of the table in the `FROM` clause. You can change the default
setting on an individual column. If a the `FROM` clause is specified as `WITH`
(`INSERT`, `UPDATE`, `DELETE`) and a column overrides this default with
`NOUPDATE`, then updates are not allowed.

Column Properties for ETAGs

Individual columns as well as a `FROM` clause can be specified to take part in
the `CHECK` `ETAG` calculation or not. An `ETAG` is a hash value for all the
columns' values in one JSON object and is used to detect changes. A column
without `ETAG` can be changed without this change impacting other operations.
By default all columns participate in `ETAG` calculation. Using `NOCHECK`
`ETAG` a column can be excluded from `ETAG` calculation.

graphql_query_for DV

`graphql_query_for_DV` is a special kind of shorthand query operation
definition in GraphQL.

  * The `root_query_field` is the single top-level selection field of this shorthand query. 

For brevity, `graphql_query_for_dv` omits the pair of curly brackets of the
top-level`selection_set` of a general shorthand query operation.

  * `selection_set` syntax augments the selection set defined in the GraphQL specification with the option of optional square brackets around the selection list. 
  * `selection` in `selection_list` can be only `field` or `fragment_spread` . 

  * `field` `directives` : conform to the GraphQL specification. Only supported custom directives are allowed. @skip and @include are NOT supported. 

  * `argument` conforms to the GraphQL specification. 

  * `root_query_field_name` corresponds to the root table. 

  * `name` has the same syntax as the GraphQL specification. 

  * `quoted_name`: The field names in a GraphQL query for DV allow quoted and un-quoted names. As a convention, un-quoted field names are in lower case only. `any_char` is any character allowed in a quoted identifier in SQL . 

  * `scalar_field_name` corresponds to a column name of a table. 

  * `object_field_name` corresponds to a related table name. In addition you can use quoted names, and fully qualified table names with dot-concatenation. 

Examples

See Also:

[Introduction To Car-Racing Duality Views
Example](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=JSNVU-GUID-8F192730-7885-40CF-96BE-7D6DC094A838) of the
JSON-Relational Duality Developer's Guide.

Example 1: Create a Duality View of Orders

The following example is a view of an orders view object `ORDERS_OV` with the
following information:

  * Order information such as order status from the `Orders` table 

  * A `CustomerInfo` singleton descendant consisting of customer details from the `Customer` table 

  * An `OrderItems` array descendant consisting of a list of order items from the `OrderItems` table. 

  * Each order item, in turn, consists of `ItemInfo` and `ShipmentInfo` singletons from the `Products` and `Shipment` tables respectively. 

    
    
    CREATE OR REPLACE JSON RELATIONAL DUALITY VIEW ORDERS_OV AS
    SELECT JSON { 'OrderId'   : ord.order_id, 
                  'OrderTime' : ord.order_datetime,
    	        'OrderStatus' : ord.order_status,
                  'CustomerInfo' : 
    			  (SELECT JSON{'CustomerId'    : cust.customer_id,
    	    	                      'CustomerName'  : cust.full_name,
                                      'CustomerEmail' : cust.email_address }	                                                                         
    			   FROM CUSTOMERS cust 
                         WHERE cust.customer_id = ord.customer_id),	
                  'OrderItems' : (SELECT JSON_ARRAYAGG(
    					JSON { 'OrderItemId' : oi.line_item_id,
                                           'Quantity'    : oi.quantity, 					  			
                                           'ProductInfo' : <subquery from product>        
                                    	 'ShipmentInfo' : <subquery from shipments>)                                                                                           
                                }) 
                                FROM ORDER_ITEMS oi		
                                WHERE ord.order_id = oi.order_id) 
    }
    FROM ORDERS ord;

Example 2: Create an Updatable View

To make the view updatable, one has to add `INSERT` or `UPDATE` or `DELETE` or
any combination of these to either the `FROM` clause or individual column. The
following allows to update the order, only read the customer and insert and
update (not delete) order items.

    
    
    CREATE OR REPLACE JSON RELATIONAL DUALITY VIEW ORDERS_OV AS
    SELECT JSON { 'OrderId'     : ord.order_id, 
                  'OrderTime'.  : ord.order_datetime,
    	         'OrderStatus' : ord.order_status,
                  'CustomerInfo' : 
    		     (SELECT JSON{'CustomerId'    : cust.customer_id,
    	    	                  'CustomerName'  : cust.full_name,
                                 'CustomerEmail' : cust.email_address WITH NOCHECK}	                                                                         
    			   FROM CUSTOMERS c WITH CHECK
                         WHERE cust.customer_id = ord.customer_id),	
                  'OrderItems' : (SELECT JSON_ARRAYAGG(
    					JSON { 'OrderItemId' : oi.line_item_id,
                                           'Quantity'    : oi.quantity, 
                                           'ProductInfo' : <subquery from product>     
                                           'ShipmentInfo' : <subquery from shipments>)                                                                                           
                                }) 
                                FROM ORDER_ITEMS oi WITH INSERT, UPDATE		
                                WHERE ord.order_id = oi.order_id) 
    }
    FROM ORDERS ord WITH INSERT, UPDATE, DELETE;


[← Previous](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)

[Next →](CREATE-LIBRARY.md)
