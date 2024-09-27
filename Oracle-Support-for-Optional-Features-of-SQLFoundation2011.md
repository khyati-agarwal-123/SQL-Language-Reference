[Previous](Oracle-Compliance-To-Core-SQL2011.md) [Next](Oracle-Compliance-
with-SQLCLI2008.md) JavaScript must be enabled to correctly display this
content

  1. [SQL Language Reference ](index.md)
  2. [ Oracle and Standard SQL](Oracle-and-Standard-SQL.md)
  3. Oracle Support for Optional Features of SQL/Foundation

## Oracle Support for Optional Features of SQL/Foundation

Oracle's support for optional features of SQL/Foundation is listed in [Table
C-2](Oracle-Support-for-Optional-Features-of-
SQLFoundation2011.md#GUID-3BA98AEC-FAAD-4F21-A6AD-F696B5D36D56__BJECCJHB
"Column 1 contains the SQL/Foundation optional feature identifier and its
descrption and column 2 describes the Oracle Database support of the
feature."):

Table C-2 Oracle Support for Optional Features of SQL/Foundation

Feature ID  | Feature Support  
---|---  
B012, Embedded C |  Oracle fully supports this feature.  
B013, Embedded COBOL |  Oracle fully supports this feature.  
B021, Direct SQL |  Oracle fully supports this feature, as SQL*Plus.  
B031, Basic dynamic SQL |  Oracle supports dynamic SQL in two styles, documented in the embedded language manuals as "Oracle dynamic SQL" and "ANSI dynamic SQL." ANSI dynamic SQL is an implementation of the standard, with the following restrictions:

  * Oracle supports a subset of the descriptor items.
  * For <input using clause>, Oracle only supports <using input descriptor>.
  * For <output using clause>, Oracle only supports <into descriptor>.
  * Dynamic parameters are indicated by a colon followed by an identifier rather than a question mark.

Oracle dynamic SQL is similar to standard dynamic SQL, with the following
modifications:

  * Parameters are indicated by a colon followed by an identifier, instead of a question mark.
  * Oracle's `DESCRIBE` `SELECT` `LIST` `FOR` statement replaces the standard's `DESCRIBE` `OUTPUT`. 
  * Oracle provides `DECLARE` `STATEMENT` if you want to declare a cursor using a dynamic SQL statement physically prior to the `PREPARE` statement that prepares the dynamic SQL statement. 

  
B032, Extended dynamic SQL |  In ANSI dynamic SQL, Oracle only implements the ability to declare global statements and global cursors from this feature; the rest of the feature is not supported. In Oracle dynamic SQL, Oracle's `DESCRIBE` `BIND` `VARIABLES` is equivalent to the standard's `DESCRIBE` `INPUT`; the rest of this feature is not supported.   
B122, Routine language C |  Oracle supports external routines written in C, though Oracle does not support the standard syntax for creating such routines.  
B128, Routine language SQL |  Oracle supports routines written in PL/SQL, which is Oracle's equivalent to the standard procedural language SQL/PSM.  
F032, `CASCADE` drop behavior  |  In Oracle, a `DROP` command invalidates all of the dropped object's dependent objects. Invalidated objects are effectively unusable until the dropped object is redefined in such a way to allow successful recompilation of the invalidated object.   
F033, `ALTER` `TABLE` statement: `DROP` `COLUMN` clause  |  Oracle provides a `DROP` `COLUMN` clause, but without the `RESTRICT` or `CASCADE` options found in the standard.   
F034, Extended `REVOKE` statement  |  Oracle supports the following parts of this feature:

  * F034-01, `REVOKE` statement performed by other than the owner of a schema object 
  * F034-03, `REVOKE` statement to revoke a privilege that the grantee has `WITH` `GRANT` `OPTION`

Oracle provides equivalent functionality for the following parts of this
feature:

  * `CASCADE`: In Oracle, a `REVOKE` invalidates all dependent objects, which become effectively unusable until the metadata is changed through subsequent `CREATE` and `GRANT` commands enabling the invalidated object to be successfully recompiled. 

  
F052, Intervals and datetime arithmetic |  Oracle only supports the `INTERVAL` `YEAR` `TO` `MONTH` and `INTERVAL` `DAY` `TO` `SECOND` data types.   
F111, Isolations levels other than `SERIALIZABLE` |  In addition to `SERIALIZABLE`, Oracle supports the `READ` `COMMITTED` isolation level.   
F121, Basic diagnostics management |  Much of the functionality of this feature is provided through the SQLCA in embedded languages.  
F191, Referential delete actions |  Oracle supports `ON` `DELETE` `CASCADE` and `ON` `DELETE` `SET` `NULL`.   
F200, `TRUNCATE` `TABLE` |  Oracle fully supports this feature, and extends it by permitting truncation of a table that references itself in a referential integrity constraint, and the ability to cascade to child tables with enabled `ON` `DELETE` `CASCADE` referential constraints.   
F231, Privilege tables |  Oracle makes this information available in the following metadata views:

  * Instead of `TABLE_PRIVILEGES`, use `ALL_TAB_PRIVS`. 
  * Instead of `COLUMN_PRIVILEGES`, use `ALL_COL_PRIVS`. 
  * Oracle does not support `USAGE` privileges so there is no equivalent to `USAGE_PRIVILEGES`. 

  
F281, `LIKE` enhancements  |  Oracle fully supports this feature.  
F291, `UNIQUE` predicate  |  The `IS` `A` `SET` condition may be used to test whether a multiset is a set; that is, each row is unique. Thus, the equivalent of 
    
    
    UNIQUE <table subquery>

is

    
    
    CAST (<table subquery> AS MULTISET) IS A SET  
  
F302, `INTERSECT` table operator  |  Syntactically, Oracle differs from the standard in that `UNION`, `INTERSECT`, and `MINUS` have the same precedence.   
F312, `MERGE` statement  |  The Oracle `MERGE` statement is almost the same as the standard, with these exceptions: 

  * Oracle does not support the optional `AS` keyword before a table alias. 
  * Oracle does not support the ability to rename columns of the table specified in the `USING` clause with a parenthesized list of column names following the table alias. 
  * Oracle does not support the <override clause>.

  
F314, `MERGE` statement with `DELETE` branch  |  Oracle has similar functionality, though in Oracle you must first update a row, after which you can delete it if the revised row meets a condition.  
F321, User authorization |  Oracle provides equivalent functionality for the following subfeatures:

  * Use `SYS_CONTEXT` `('USERENV',` `'SESSION_USER')` instead of `SESSION_USER`
  * Use `SYS_CONTEXT` `('USERENV',` `'CURRENT_USER')` instead of `CURRENT_USER`

Oracle does not support the following subfeatures:

  * `SYSTEM_USER`
  * `SET` `SESSION` `AUTHORIZATION` statement 

  
F341, Usage tables |  Oracle makes this information available in the views `ALL_DEPENDENCIES`, `DBA_DEPENDENCIES`, and `USER_DEPENDENCIES`.   
F381, Extended schema manipulation |  Oracle fully supports the following element of this feature:

  * Oracle supports the standard syntax to add a table constraint using `ALTER` `TABLE`. 

Oracle partially supports the following element of this feature:

  * Oracle supports the standard syntax to drop a table constraint, except that Oracle does not support `RESTRICT`. 

Oracle provides equivalent functionality for the following element of this
feature:

  * To alter the default value of a column, use the `MODIFY` option of `ALTER` `TABLE`. 

Oracle does not support the following parts of this feature:

  * `DROP` `SCHEMA` statement 
  * `ALTER` `ROUTINE` statement 

  
F382, Alter column data type |  Oracle supports this functionality, though with non-standard syntax. As an extension to the standard, Oracle allows you to reduce the size or precision of a column.  
F383, Set column not null clause |  Oracle provides equivalent functionality for the two subfeatures of this feature:

  * To add a `NOT` `NULL` constraint to an existing column, use `ALTER` `TABLE` ... `MODIFY`
  * To drop a `NOT` `NULL` constraint, use `ALTER` `TABLE` to drop the constraint by name 

  
F384, Drop identity property clause |  Oracle provides equivalent functionality using `ALTER` `TABLE` ... `MODIFY` `(`... `DROP` `IDENTITY``)`  
F386, Set identity column generation clause |  Oracle provides equivalent functionality. Oracle's syntax and semantics are the same as the standard, with this exception:

  * Oracle does not support `RESTART`; use `START` `WITH` instead. When restarting an identity column, the values of the other parameters for the identity column are reset to their defaults unless explicitly set in the `ALTER` `TABLE` statement. 

Oracle's `START` `WITH` `LIMIT` `VALUE` option is an extension on the
standard.  
F391, Long identifiers |  Oracle supports identifiers up to 128 characters in length.  
F393, Unicode escapes in literals |  The Oracle `UNISTR` function supports numeric escape sequences for all Unicode characters.   
F394, Optional normal form specification |  This feature adds the keywords `NFC`, `NFD`, `NFKC`, and `NKD` to the `NORMALIZE` function and the `IS` `NORMAL` predicate. Without these keywords, `NFC` is the default (see Feature T061, UCS support). Oracle supports all four normalization forms, with nonstandard syntax, as follows: 

  * For `NFC`, use `COMPOSE`
  * For `NFD`, use `DECOMPOSE` with the `CANONICAL` option 
  * For `NFKD`, use `DECOMPOSE` with the `COMPATIBILITY` option 
  * For `NFKC`, use `DECOMPOSE` with the `CANONICAL` option followed by `COMPOSE`

Oracle does not support the `IS` `NORMAL` predicate.  
F401, Extended joined table |  Oracle supports `FULL` outer joins, `CROSS` joins, and `NATURAL` joins.   
F402, Named column joins for LOBs, arrays and multisets |  Oracle supports named column joins for columns whose declared type is nested table. Oracle does not support named column joins for LOBs or arrays.  
F403, Partitioned join tables |  Oracle supports this feature, except with `FULL` outer joins.   
F411, Time zone specification |  Oracle fully supports `TIMESTAMP` `WITH` `TIME` `ZONE`, but does not support `TIME` `WITH` `TIME` `ZONE`.   
F421, National character |  Oracle fully supports this feature.  
F431, Read-only scrollable cursors |  Oracle fully supports this feature.  
F441, Extended set function support |  Oracle supports the following parts of this feature:

  * The ability in the `WHERE` clause to reference a column that is defined using an aggregate, either in a view or an inline view 
  * `COUNT` without `DISTINCT` of an expression 
  * Aggregates that reference columns that are outer references with respect to the aggregating query. However, Oracle defines the aggregating query as the innermost query containing the aggregate, rather than the innermost query that defines a range variable referenced in the aggregate.

  
F442, Mixed column references in set functions |  Oracle fully supports this feature.  
F461, Named character sets |  Oracle supports many character sets with Oracle-defined names. Oracle does not support any other aspect of this feature.  
F491, Constraint management |  Oracle fully supports this feature.  
F492, Optional table constraint enforcement |  `ENFORCED` in the standard is equivalent to `ENABLE` `VALIDATE` in Oracle. `NOT` `ENFORCED` in the standard is equivalent to `DISABLE` `NOVALIDATE` in Oracle. Other combinations of the `ENABLE` | `DISABLE`, `VALIDATE` | `NOVALIDATE`, and `RELY` | `NORELY` options are extensions of the standard.   
F531, Temporary tables |  Oracle supports `GLOBAL` `TEMPORARY` tables.   
F555, Enhanced seconds precision |  Oracle provides enhanced support for this feature, supporting up to 9 places after the decimal point.  
F561, Full value expressions |  Oracle fully supports this feature.  
F571, Truth value tests |  Oracle's `LNNVL` function is equivalent to the standard's `IS` `NOT` `TRUE` predicate.   
F591, Derived tables |  Oracle supports <derived table>, with the exception of:

  * Oracle does not support the optional `AS` keyword before a table alias. 
  * Oracle does not support <derived column list>.

  
F641, Row and table constructors |  In Oracle, a row constructor may be used in an equality or inequality comparison with another row constructor or with a subquery. Oracle does not support anything else in this feature.  
F690, Collation support |  Oracle's `NLSSORT` function may be used to change the collation of character expressions.   
F693, SQL-sessions and client module collations |  To set a session collation, use `ALTER` `SESSION` `SET` `NLS_COMP` `=` `'LINGUISTIC'` and also set NLS_SORT to your desired collation. Oracle does not support client module collations.   
F695, Translation support |  The Oracle `CONVERT` function can convert between the database character set and the national character set. For other character sets, store the data in the `RAW` data type and use the PL/SQL package function `UTL_RAW`.`CONVERT`. Oracle does not provide the ability to add or drop character set conversions.   
F721, Deferrable constraints |  Oracle fully supports this feature.  
F731, `INSERT` column privileges  |  Oracle fully supports this feature.  
F761, Session management |  Oracle provides the following equivalents for elements of this feature:

  * The equivalent to the standard's `SET` `SESSION` `CHARACTERISTICS` `AS` `TRANSACTION` `SERIALIZABLE` is `ALTER` `SESSION` `SET` `ISOLATION_LEVEL` `=` `SERIALIZABLE`. 
  * The equivalent to the standard's `SET` `SCHEMA` is `ALTER` `SESSION` `SET` `CURRENT_SCHEMA`. 
  * The equivalent to the standard's `SET` `COLLATION` is `ALTER` `SESSION` `SET` `NLS_SORT`. 

  
F763, `CURRENT_SCHEMA` |  Oracle's equivalent is `SYS_CONTEXT` `('USERENV',` `'CURRENT_SCHEMA')`  
F771, Connection management |  Oracle's `CONNECT` statement provides the same functionality as the standard's `CONNECT` statement, though with different syntax. Instead of using the standard's `SET` `CONNECTION`, Oracle provides the `AT` clause to indicate which connection a SQL statement should be performed on. Oracle embedded languages let you disconnect from a connection by using the `RELEASE` option of either `COMMIT` or `ROLLBACK`.   
F781, Self-referencing operations |  Oracle fully supports this feature.  
F801, Full set function |  Oracle fully supports this feature.  
F831, Full cursor update |  Oracle supports the combination of `FOR` `UPDATE` and `ORDER` `BY` clauses in a query.   
F841, `LIKE_REGEX` predicate  |  Oracle's equivalent is `REGEXP_LIKE`. Oracle's pattern syntax lacks some of the features of the standard's. Oracle's match parameter has the same capabilities as the standard's, though with a few spelling differences.   
F842, `OCCURRENCES_REGEX` function  |  Oracle's equivalent is `REGEXP_COUNT`. Oracle's pattern syntax lacks some of the features of the standard's. Oracle's match parameter has the same capabilities as the standard's, though with a few spelling differences.   
F843, `POSITION_REGEX` function  |  Oracle's equivalent is `REGEXP_INSTR`. Oracle's pattern syntax lacks some of the features of the standard's. Oracle's match parameter has the same capabilities as the standard's, though with a few spelling differences.   
F844, `SUBSTRING_REGEX` function  |  Oracle's equivalent is `REGEXP_SUBSTR`. Oracle's pattern syntax lacks some of the features of the standard's. Oracle's match parameter has the same capabilities as the standard's, though with a few spelling differences.   
F845, `TRANSLATE_REGEX` function  |  Oracle's equivalent is `REGEXP_REPLACE`. Oracle's pattern syntax lacks some of the features of the standard's. Oracle's match parameter has the same capabilities as the standard's, though with a few spelling differences.   
F850, Top-level <order by clause> in <query expression> |  Oracle fully supports this feature.  
F851, <order by clause> in subqueries |  Oracle fully supports this feature.  
F852, Top-level <order by clause> in views |  Oracle fully supports this feature.  
F855, Nested <order by clause> in <query expression> |  Oracle fully supports this feature.  
F856, Nested <fetch first clause> in <query expression> |  Oracle fully supports this feature.  
F857, Top-level <fetch first clause> in a <query expression> |  Oracle fully supports this feature.  
F858, <fetch first clause> in subqueries |  Oracle fully supports this feature.  
F859, Top-level <fetch first clause> in views |  Oracle fully supports this feature.  
F860, Dynamic <fetch first row count> in <fetch first clause> |  Oracle fully supports this feature.  
F861, Top-level <result offset clause> in <query expression> |  Oracle fully supports this feature.  
F862, <result offset clause> in subqueries |  Oracle fully supports this feature.  
F863, Nested <result offset clause> in <query expression> |  Oracle fully supports this feature.  
F864, Top-level <result offset clause> in views |  Oracle fully supports this feature.  
F865, Dynamic <offset row count> in <result offset clause> |  Oracle fully supports this feature.  
F866, `FETCH` `FIRST` clause: `PERCENT` option  |  Oracle fully supports this feature.  
F867, `FETCH` `FIRST` clause: `WITH` `TIES` option  |  Oracle fully supports this feature.  
R010, Row pattern recognition: `FROM` clause  |  Oracle fully supports this feature.  
S023, Basic structured types |  Oracle's object types are equivalent to structured types in the standard.  
S024, Enhanced structured types |  Oracle's syntax is non-standard, but provides equivalents for the following:

  * `NOT` `INSTANTIABLE`
  * `STATIC` methods 
  * `RELATIVE`, `MAP`, and `STATE` orderings. The keyword in Oracle for `RELATIVE` orderings is `ORDER`. There is no keyword for `STATE` orderings (this is the default, if no other ordering is defined). Unlike the standard, Oracle does not support `EQUALS` `ONLY` on non-`STATE` orderings. (See also Feature S251, User-defined orderings.) 
  * `SELF` `AS` `RESULT` in the signature of constructor methods 

  
S025, Final structured types |  Oracle's final object types are equivalent to final structured types in the standard.  
S026, Self-referencing structured types |  In Oracle, an object type OT may have a reference that references OT.  
S041, Basic reference types |  Oracle's reference types are equivalent to reference types in the standard. To dereference a reference, dot notation is used, instead of -> as in the standard.  
S043, Enhanced reference types |  Oracle supports the following elements of this feature:

  * `DEREF` operator to return the object referenced by a reference 
  * `SCOPE` clause as a constraint on columns of tables or materialized views 
  * Adding and dropping the scope of a column
  * References that are either system-generated or derived from the primary key (but not from any other list of columns, nor from a list of attributes of the type)

  
S051, Create table of type |  Oracle's object tables are equivalent to tables of structured type in the standard.  
S081, Subtables |  Oracle supports hierarchies of object views, but not of object base tables. To emulate a hierarchy of base tables, create a hierarchy of views on those base tables.  
S091, Basic array support |  Oracle `VARRAY` types are equivalent to array types in the standard. However, Oracle does not support storage of arrays of LOBs. To access a single element of an array using a subscript, you must use PL/SQL. Oracle supports the following aspects of this feature with nonstandard syntax: 

  * To construct an instance of varray type, including an empty array, use the varray type constructor.
  * To unnest a varray in the `FROM` clause, use the `TABLE` operator. 
  * To get the cardinality of a varray, use the `COUNT` method in PL/SQL. 

  
S092, Arrays of user-defined types |  Oracle supports `VARRAY`s of object types.   
S094, Arrays of reference types |  Oracle supports `VARRAY`s of references.   
S095, Array constructors by query |  Oracle supports this using `CAST` (`MULTISET` (`SELECT` ...) `AS` `varray_type``)`. The ability to order the elements of the array using `ORDER` `BY` is not supported.   
S097, Array element assignment |  In PL/SQL, you can assign to array elements, using syntax that is similar to the standard (SQL/PSM).  
S098, `ARRAY_AGG` |  Oracle does not have an aggregate that results in a varray. Instead, the `COLLECT` aggregate may be used to create a multiset, which can be cast to an array of the element type.   
S111, `ONLY` in query expressions  |  Oracle supports the `ONLY` clause for view hierarchies; Oracle does not support hierarchies of base tables.   
S151, Type predicate |  Oracle fully supports this feature.  
S161, Subtype treatment |  Oracle fully supports this feature.  
S162, Subtype treatment for references |  Supported, with a minor syntactic difference: The standard requires parentheses around the referenced type's name; Oracle does not support parentheses in this position.  
S201, SQL-invoked routines on arrays |  PL/SQL provides the ability to pass arrays as parameters and return arrays as the result of functions. Procedures and functions written in C may pass arrays and return arrays as the result of functions using the Oracle Type Translator (OTT).  
S202, SQL-invoked routines on multisets |  A PL/SQL routine may have nested tables as parameters, and may return a nested table. Routines written in C may pass arrays and return arrays as the result of functions using the Oracle Type Translator.  
S232, Array locators |  Oracle Type Translator supports descriptors for arrays, which achieve the same purpose as locators.  
S233, Multiset locators |  Oracle supports locators for nested tables.  
S241, Transform functions |  The Oracle Type Translator provides the same capability as transforms.  
S251, User-defined orderings |  Oracle's object type ordering capabilities correspond to the standard's capabilities as follows:

  * Oracle's `MAP` ordering corresponds to the standard's `ORDER` `FULL` `BY` `MAP` ordering. 
  * Oracle's `ORDER` ordering corresponds to the standard's `ORDER` `FULL` `BY` `RELATIVE` ordering. 
  * If an Oracle object type has neither `MAP` nor `ORDER` declared, then this corresponds to `EQUALS` `ONLY` `BY` `STATE` in the standard. 
  * Oracle does not have unordered object types; you can alter the ordering but you cannot drop it.

  
S261, Specified type method |  The `GetTypeName` method of the `ANYDATA` type may be used to learn the name of a type.   
S271, Basic multiset support |  Multisets in the standard are supported as nested table types in Oracle. The Oracle nested table data type based on a scalar type ST is equivalent, in standard terminology, to a multiset of rows having a single field of type ST and named `column_value`. The Oracle nested table type based on an object type is equivalent to a multiset of structured type in the standard.  Oracle supports the following elements of this feature on nested tables using the same syntax as the standard has for multisets:

  * The `CARDINALITY` function 
  * The `SET` function 
  * The `MEMBER` predicate 
  * The `IS` `A` `SET` predicate 
  * The `COLLECT` aggregate 

All other aspects of this feature are supported with non-standard syntax, as
follows:

  * To create an empty multiset, denoted `MULTISET[]` in the standard, use an empty constructor of the nested table type. 
  * To obtain the sole element of a multiset with one element, denoted `ELEMENT` (<multiset value expression>) in the standard, use a scalar subquery to select the single element from the nested table. 
  * To construct a multiset by enumeration, use the constructor of the nested table type.
  * To construct a multiset by query, use `CAST` with a multiset argument, casting to the nested table type. 
  * To unnest a multiset, use the `TABLE` operator in the `FROM` clause. 

  
S272, Multisets of user-defined types |  Oracle's nested table type permits a multiset of structured types. Oracle does not have distinct types, so a multiset of distinct types is not supported.  
S274, Multisets of reference types |  A nested table type can have one or more columns of reference type.  
S275, Advanced multiset support |  Oracle supports the following elements of this feature on nested tables using the same syntax as the standard has for multisets:

  * The `MULTISET` `UNION`, `MULTISET` `INTERSECTION`, and `MULTISET` `EXCEPT` operators 
  * The `SUBMULTISET` predicate 
  * `=` and `<>` predicates 

Oracle does not support the `FUSION` or `INTERSECTION` aggregates.  
S281, Nested collection types |  Oracle permits nesting of its collection types (varray and nested table).  
S401, Distinct types based on array types |  Oracle's varray types are strongly typed.  
S403, `ARRAY_MAX_CARDINALITY` |  In PL/SQL, the `LIMIT` method of a varray returns its maximum cardinality.   
S404, `TRIM_ARRAY` |  In PL/SQL, the `TRIM` method of a varray can be used to trim the varray.   
T041, Basic LOB data type support |  Oracle supports the following aspects of this feature:

  * The keywords `BLOB`, `CLOB`, and `NCLOB`
  * Concatenation, `UPPER`, `LOWER` on `CLOB`s 

Oracle provides equivalent support for the following aspects of this feature:

  * Use `INSTR` instead of `POSITION`. 
  * Use `LENGTH` instead of `CHAR_LENGTH`. 

Oracle does not support the following aspects of this feature:

  * The keywords `BINARY` `LARGE` `OBJECT`, `CHARACTER` `LARGE` `OBJECT`, and `NATIONAL` `CHARACTER` `LARGE` `OBJECT` as synonyms for `BLOB`, `CLOB`, and `NCLOB`, respectively 
  * <binary string literal>
  * The ability to specify an upper bound on the length of a `BLOB` or `CLOB`
  * Concatenation of `BLOB`s 

  
T042, Extended LOB support |  Oracle fully supports the following element of this feature:

  * `TRIM` function on a `CLOB` argument 

Oracle provides equivalent functionality for the following elements of this
feature:

  * `BLOB` and `CLOB` substring, supported using `SUBSTR`
  * `SIMILAR` predicate, supported using `REGEXPR_LIKE` to perform pattern matching with a Perl-like syntax 

The following elements of this feature are not supported:

  * Comparison predicates with `BLOB` or `CLOB` operands 
  * `CAST` with a `BLOB` or `CLOB` operand 
  * `OVERLAY` (This may be emulated using `SUBSTR` and string concatenation.) 
  * `LIKE` predicate with `BLOB` or `CLOB` operands 

  
T051, Row types |  Oracle object types can be used in place of the standard's row types.  
T061, UCS support |  Oracle provides equivalent functionality for the following elements of this feature:

  * Oracle supports the keyword `CHAR` instead of `CHARACTERS`, and `BYTE` instead of `OCTETS`, in a character data type declaration. 
  * The Oracle `COMPOSE` function is equivalent to the standard's `NORMALIZE` function. 

Oracle does not support the `IS` `NORMALIZED` predicate.  
T071, `BIGINT` data type  |  On many implementations, `BIGINT` refers to a binary integer type with 64 bits, which supports almost 19 decimal digits. The Oracle `NUMBER` type supports 39 decimal digits.   
T111, Updatable joins, unions and columns |  Oracle's updatable join views are similar to the standard's updatable join capabilities. Unlike the standard, Oracle does not require an updatable join view to display the strong candidate key in the `SELECT` list. Although an updatable join view might have more than one key-preserved table, only one of them may be modified using an `UPDATE` or `DELETE`, unlike the standard, which modifies all key-preserved tables of an updatable join.   
T121, `WITH` (excluding `RECURSIVE`) in query expression  |  Oracle fully supports this feature.  
T122, `WITH` (excluding `RECURSIVE`) in subquery  |  Oracle fully supports this feature.  
T131, Recursive query |  Oracle supports the use of a `WITH` clause element that references itself, but without the `RECURSIVE` keyword. Alternatively, Oracle's `START` `WITH` and `CONNECT` `BY` clauses can be used to perform many recursive queries.   
T132, Recursive query in subquery |  Oracle supports the use of a `WITH` clause element that references itself, but without the `RECURSIVE` keyword. Alternatively, Oracle's `START` `WITH` and `CONNECT` `BY` clauses can be used to perform many recursive queries.   
T141, `SIMILAR` predicate  |  Oracle provides `REGEXP_LIKE` for pattern matching with a Perl-like syntax.   
T172, `AS` subquery clause in table definition  |  Oracle's `AS` subquery feature of `CREATE` `TABLE` has substantially the same functionality as the standard, though there are some syntactic differences.   
T174, Identity columns |  Oracle supports this feature, with the following syntactic differences:

  * Oracle uses `NOMINVALUE` and `NOMAXVALUE` instead of the standard's `NO` `MINVALUE` and `NO` `MAXVALUE`. 
  * To restart an identity column, in an `ALTER` `TABLE` `MODIFY` statement, use `START` `WITH` `LIMIT` `VALUE` to restart at the highest value (for an increasing identity column) or the lowest value (for a decreasing identity column); use `START` `WITH` number to restart at a specific number. 

`GENERATED` `BY` `DEFAULT` `ON` `NULL` is an Oracle extension.  
T175, Generated columns |  Oracle supports this feature, with the following restrictions:

  * Generated columns are not supported in temporary tables.
  * The data type of a generated column may not be LOB or XML.

  
T176, Sequence generator support |  Oracle's sequences have the same capabilities as the standard's, though with different syntax.  
T178, Identity columns: simple restart option |  Oracle's `START` `WITH` `LIMIT` `VALUE` is the same as the standard's simple restart if the identity column has not cycled.   
T180, System-versioned tables |  Oracle's Flashback capability is substantially the same as the standard's system-versioned tables. Some key differences are:

  * In Oracle you do not need to designate particular tables for journaling; all tables are journaled.
  * In Oracle, LOB columns need to be individually designated for journaling, because of the potential for large amounts of data. The standard has no analogous provision.
  * In Oracle you need a privilege in order to read historical data.
  * In the standard, journaled tables have columns to record the start and end timestamps for the row. In Oracle, this is provided through pseudocolumns.

  
T181, Application-time period tables |  Oracle supports the following elements of this feature:

  * Application-time period definition during `CREATE` `TABLE`
  * Adding and dropping an application-time period definition using `ALTER` `TABLE` with a minor syntactic difference: Oracle requires parentheses around the period specification; the standard does not support parentheses in this position. 

Oracle extends this feature:

  * With the ability to have more than one application-time period per table.
  * By making the start time and end time columns optional. In this case, Oracle will create these columns implicitly.
  * By allowing `NULL` for the start time column to indicate that the row is considered valid for any point in time before the value of the end time column. 
  * By allowing `NULL` for the end time column to indicate that the row is considered valid for any point in time on or after the value of the start time column. 
  * By querying an application-time period table using the flashback query options `VERSIONS` `PERIOD` `FOR` and `AS` `OF` `PERIOD` `FOR`. 

  
T201, Comparable data types for referential constraints |  Oracle fully supports this feature.  
T211, Basic trigger capability |  Oracle's triggers differ from the standard as follows:

  * Oracle does not provide the optional syntax `FOR` `EACH` `STATEMENT` for the default case, the statement trigger. 
  * Oracle does not support `OLD` `TABLE` and `NEW` `TABLE`; the transition tables specified in the standard (the multiset of before and after images of affected rows) are not available. 
  * The trigger body is written in PL/SQL, which is functionally equivalent to the standard's procedural language PSM, but not the same.
  * In the trigger body, the new and old transition variables are referenced beginning with a colon.
  * Oracle's row triggers are executed as the row is processed, instead of buffering them and executing all of them after processing all rows. The standard's semantics are deterministic, but Oracle's in-flight row triggers are more performant.
  * Oracle's before-row and before-statement triggers can perform DML statements, which is forbidden in the standard. However, Oracle's after-row statements cannot perform DML, while it is permitted in the standard.
  * When multiple triggers apply, the standard says they are executed in order of definition. In Oracle the execution order is nondeterministic, unless specified using `FOLLOWS`. 
  * Oracle uses the system privileges `CREATE` `TRIGGER` and `CREATE` `ANY` `TRIGGER` to regulate creation of triggers, instead of the standard's `TRIGGER` privilege, which is a table privilege. 

  
T212, Enhanced trigger capability |  This feature permits statements triggers, which Oracle supports, as described for feature T211, Basic trigger capability.  
T213, `INSTEAD` `OF` triggers  |  Oracle supports `INSTEAD` `OF` triggers on views, with syntax and semantics agreeing with the standard except as noted for feature T211, Basic trigger capability. Oracle permits an `INSTEAD` `OF` trigger on a view that specified `WITH` `CHECK` `OPTION`, unlike the standard.   
T241, `START` `TRANSACTION` statement  |  Oracle's `SET` `TRANSACTION` statement starts a transaction making it equivalent to the standard's `START` `TRANSACTION` rather than the standard's `SET` `TRANSACTION`. Oracle's `READ` `ONLY` transactions are at `SERIALIZABLE` isolation level.   
T271, Savepoints |  Oracle supports this feature, except:

  * Oracle does not support `RELEASE` `SAVEPOINT`. 
  * Oracle does not support savepoint levels.

  
T285, Enhanced derived column names |  This feature pertains only to derived columns in a `SELECT` list with no column alias and consisting of a SQL parameter reference. In that case, the column name defaults to the parameter name, the same as in the standard.   
T323, Explicit security for external routines |  The Oracle syntax `AUTHID` { `CURRENT` `USER` | `DEFINER` } when used when creating an external function, procedure, or package is equivalent to the standard's `EXTERNAL` `SECURITY` { `DEFINER` | `INVOKER` }.   
T324, Explicit security for SQL routines |  Oracle's syntax `AUTHID` { `CURRENT` `USER` | `DEFINER` } when used when creating a PL/SQL function, procedure, or package is equivalent to the standard's `SQL` `SECURITY` { `DEFINER` | `INVOKER` }.   
T325, Qualified SQL parameter reference |  PL/SQL supports the use of a routine name to qualify a parameter name.  
T326, Table functions |  Oracle provides equivalents for the following elements of this feature:

  * <multiset value constructor by query> is supported using `CAST` (`MULTISET` (<`query expression`>) `AS` <`nested table type`>) 
  * <table function derived table> is supported using the `TABLE` operator in the `FROM` clause with a varray or nested table as the argument 
  * <collection value expression> is equivalent to an Oracle expression resulting in a varray or nested table
  * <returns table type> is equivalent to a PL/SQL function that returns a nested table

  
T331, Basic roles |  Oracle supports this feature, except for `REVOKE` `ADMIN` `OPTION` `FOR` <role name>.   
T341, Overloading of SQL-invoked functions and procedures |  Oracle supports overloading of functions and procedures. However, the rules for handling certain data type combinations are not the same as the standard. For example, the standard permits the coexistence of two functions of the same name differing only in the numeric types of the arguments, whereas Oracle does not permit this.  
T351, Bracketed comments |  Oracle fully supports this feature.  
T431, Extended grouping capabilities |  Oracle fully supports this feature.  
T432, Nested and concatenated `GROUPING` `SETS` |  Oracle supports concatenated `GROUPING` `SETS`, but not nested `GROUPING` `SETS`.   
T433, Multiargument function `GROUPING` |  The Oracle `GROUP_ID` function can be used to conveniently distinguish groups in a grouped query, serving the same purpose as the standard multiargument `GROUPING` function.   
T441, `ABS` and `MOD` functions  |  Oracle supports the `ABS` function. Oracle's `MOD` function is similar to the standard, though the behavior is different if the two arguments are of opposite sign.   
T471, Result sets return value |  PL/SQL ref cursors provide all the functionality of the standard's result set cursors.  
T491, `LATERAL` derived tables  |  Oracle fully supports this feature.  
T501, Enhanced `EXISTS` predicate  |  Oracle fully supports this feature.  
T511, Transaction counts |  Oracle supports the count of transactions committed and rolled back via the system views `V$STATNAME` and `V$SESSTAT`.   
T521, Named arguments in `CALL` statement  |  Oracle fully supports this feature.  
T522, Default values for `IN` parameters of SQL-invoked procedures  |  Oracle fully supports this feature.  
T524, Named arguments in routine invocations other than a `CALL` statement  |  Oracle fully supports this feature.  
T525, Default values for parameters of SQL-invoked functions |  Oracle fully supports this feature.  
T571, Array-returning external SQL-invoked function |  Oracle table functions returning a varray can be defined in external programming languages. When declaring such functions in SQL, use the `CREATE` `FUNCTION` command with the `PIPELINED` `USING` clause.   
T572, Multiset-returning external SQL-invoked function |  Oracle table functions returning a nested table can be defined in external programming languages. When declaring such functions in SQL, use the `CREATE` `FUNCTION` command with the `PIPELINED` `USING` clause. In the body of the function, use the `OCITable` interface. The function must be invoked within the `TABLE` operator in the `FROM` clause.   
T581, Regular expressions substring functions |  Oracle provides the `REGEXP_SUBSTR` function to perform substring operations using regular expression matching.   
T591, `UNIQUE` constraints of possibly null columns  |  Oracle permits a `UNIQUE` constraint on one or more nullable columns. If the `UNIQUE` constraint is on a single column, then the semantics are the same as the standard (the constraint permits any number of rows that are null in the designated column). If the `UNIQUE` constraint is on two or more columns, then the semantics are nonstandard. Oracle permits any number of rows that are null in all the designated columns. Unlike the standard, if a row is non-null in at least one of the designated columns, then another row having the same values in the non-null columns of the constraint is a constraint violation and not permitted.   
T611, Elementary OLAP operations |  Oracle fully supports this feature, except that `DISTINCT` is only supported in conjunction with window partitioning but not with window framing.   
T612, Advanced OLAP operations |  Oracle supports the following elements of this feature: `PERCENT_RANK`, `CUME_DIST`, `WIDTH_BUCKET`, hypothetical set functions, `PERCENTILE_CONT`, `PERCENTILE_DISC`, and `ROW_NUMBER`.  Oracle does not support the following element of this feature:

  * `ROW_NUMBER` without `ORDER` `BY`

  
T613, Sampling |  Oracle uses the keyword `SAMPLE` instead of the standard's keyword, `TABLESAMPLE`. Oracle uses the keyword `BLOCK` instead of the standard's keyword, `SYSTEM`. Oracle uses the absence of the keyword `BLOCK` to indicate a Bernoulli sampling of rows, indicated in the standard by the keyword `BERNOULLI`. Oracle does not support sampling of derived tables or views that are not key-preserving. Oracle does not permit sampling in a subquery of a `DELETE`, `UPDATE` or `MERGE` statement.   
T614, `NTILE` function  |  Oracle fully supports this feature.  
T615, `LEAD` and `LAG` functions  |  Oracle fully supports this feature.  
T616, Null treatment option for `LEAD` and `LAG` functions  |  Oracle fully supports this feature.  
T617, `FIRST_VALUE` and `LAST_VALUE` functions  |  Oracle fully supports this feature.  
T618, `NTH_VALUE` function  |  Oracle fully supports this feature.  
T621, Enhanced numeric functions |  Oracle fully supports this feature, except for the alternate spelling `CEILING` of the `CEIL` function.   
T622, Trigonometric functions |  Oracle fully supports this feature.  
T623, General logarithm function |  Oracle fully supports this feature.  
T625, `LISTAGG` |  Oracle fully supports this feature.  
T641, Multiple column assignment |  The standard syntax to assign to multiple columns is supported if the assignment source is a subquery.  
T652, SQL-dynamic statements in SQL routines. |  PL/SQL supports dynamic SQL.  
T654, SQL-dynamic statements in external routines |  Oracle supports dynamic SQL in embedded C, which may be used to create an external routine.  
T655, Cyclically dependent routines |  PL/SQL supports recursion.  
T811, Basic SQL/JSON constructor functions |  Oracle fully supports this feature, except for the `JSON_ARRAY` constructor by query.   
T812, SQL/JSON: `JSON_OBJECTAGG` |  Oracle fully supports this feature.  
T813, SQL/JSON: `JSON_ARRAYAGG` with `ORDER` `BY` |  Oracle fully supports this feature.  
T821, Basic SQL/JSON query operators |  Oracle fully supports this feature.  
T822, SQL/JSON: `IS` `JSON` `WITH` `UNIQUE` `KEYS` predicate  |  Oracle fully supports this feature.  
T823, SQL/JSON: `PASSING` clause  |  Oracle supports the `PASSING` clause in `JSON_EXISTS`.   
T825, SQL/JSON: `ON` `EMPTY` and `ON` `ERROR` clauses  |  Oracle fully supports this feature, except that:

  * The `ON` `ERROR` clause for `JSON_EXISTS` does not support `UNKNOWN`. 
  * `JSON_TABLE` does not support a column-level `ON` `EMPTY` clause. 

  
T828, `JSON_QUERY` |  Oracle fully supports this feature.  
T829, `JSON_QUERY`: array wrapper options  |  Oracle fully supports this feature.  
T832, SQL/JSON path language: item method |  Oracle fully supports the following item methods:

  * `abs`
  * `ceiling`
  * `double`
  * `floor`

Oracle provides the following comparable support:

  * `date` and `timestamp` are comparable to the standardâs `datetime`

Oracle extends this feature by supporting the following item methods:

  * `length`
  * `lower`
  * `number`
  * `string`
  * `upper`

  
T833, SQL/JSON path language: multiple subscripts |  Oracle fully supports this feature, except that subscripts have to be specified in strictly monotonically increasing order.  
T834, SQL/JSON path language: wildcard member accessor |  Oracle fully supports this feature.  
T835, SQL/JSON path language: filter expression |  Oracle supports the filter expression as the last step of the SQL/JSON path expression in `JSON_EXISTS`.   
T839, Formatted cast of datetimes to/from character strings |  Oracle supports this feature with a minor syntactic difference: Oracle uses a comma instead of the keyword `FORMAT`. 


[← Previous](Oracle-Compliance-To-Core-SQL2011.md)

[Next →](Oracle-Compliance-with-SQLCLI2008.md)
