[Previous](graph-table-shape.md) [Next](json_id-operator.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. [GRAPH_TABLE Operator](graph_table-operator.md)
  4. Value Expressions for GRAPH_TABLE

## Value Expressions for GRAPH_TABLE

Purpose

Value expressions in `WHERE` and `COLUMNS` clauses inside `GRAPH_TABLE`
inherit all the functionality supported in value expressions outside of
`GRAPH_TABLE`. Additionally, inside `GRAPH_TABLE`, the following value
expressions are available:

  * [Property Reference](value-expressions-graph_table.md#GUID-C93B0F61-CC3D-4071-A649-35DD8E31CE78)

  * [Vertex and Edge ID Functions](value-expressions-graph_table.md#GUID-B9E06987-AB0B-4578-A462-2A6B5BF085EA)

  * [Vertex and Edge Equal Predicates](value-expressions-graph_table.md#GUID-8365A435-E525-4CE5-8600-11D203C5C971)

  * [SOURCE and Destination Predicates](value-expressions-graph_table.md#GUID-3CA85A62-A083-4D12-9EFE-CF127BD8A3CD)

  * [Aggregation in GRAPH_TABLE](value-expressions-graph_table.md#GUID-4CC87ADB-39A9-4A4B-8D12-8E9E667DAEC9)

### Property Reference

Purpose

Property references allow for accessing property values of vertices and edges.

Syntax

property_reference::=

  

![Description of property_reference.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/property_reference.gif)  
[Description of the illustration
property_reference.eps](img_text/property_reference.md)

  

property_name::=

![Description of property_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/property_name.gif)  
[Description of the illustration
property_name.eps](img_text/property_name.md)

Semantics

Syntactically, a property access is an element variable followed by a dot (.)
and the name of the property. A property name is an identifier and may thus be
either double quoted or unquoted.

The label expression specified for an element pattern determines which
properties can be referenced:

  * If no label expression is specified, then depending on the type of element variable, either all vertex properties or all edge properties in the graph can be referenced.

  * Otherwise, if a label expression is specified, then the set of properties that can be referenced is the union of the properties of labels belonging to vertex (or edge) tables that have at least one label that satisfies the label expression.

If multiple labels satisfy the label expression but they define the same
property but of a different data type, then such properties may only be
referenced if the data types are union compatible. The resulting value will
then have the union compatible data type.

If multiple labels satisfy the label expression while some labels have a
particular property that other labels do not, then such properties can still
be referenced. The property reference will result in null values for any
vertex or edge that does not have the property.

Examples

Example 1

The following query lists the date of birth of all persons and universities in
the graph:

    
    
    SELECT GT.name, GT.birthday
    FROM GRAPH_TABLE ( students_graph
      MATCH (p IS person|university)
      COLUMNS (p.name, p.dob AS birthday)
    ) GT
    ORDER BY GT.birthday, GT.name;

Note that since only persons `John`, `Bob`, `Mary`, `Alice` have dates of
birth while universities (`ABC` and `XYZ`) do not, null values are returned
for universities. These appear as empty strings in the output:

    
    
    NAME       BIRTHDAY
    ---------- ---------
    John       13-JUN-63
    Bob        11-MAR-66
    Mary       25-SEP-82
    Alice      01-FEB-87
    ABC
    XYZ
    

Example 2

The following query matches all `PERSON` vertices and returns their `NAME` and
`HEIGHT`:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (n IS person)
      COLUMNS ( n.name, n.height )
    )
    ORDER BY height;
    

The result is:

    
    
    NAME           HEIGHT
    ---------- ----------
    Mary             1.65
    Alice	            1.7
    Bob              1.75
    John              1.8 

Here, even though label `PERSON` does not have property `HEIGHT`, the property
can still be referenced because vertex table `PERSONS` has labels `PERSON`
and` PERSON_HT` and since label `PERSON` matches the label expression, the set
of properties that can be referenced is the union of the properties of labels
`PERSON` and `PERSON_HT`, which includes the property `HEIGHT` of label
`PERSON_HT`.

### Vertex and Edge ID Functions

Purpose

Vertex and edge ID functions allow for obtaining unique identifiers for graph
elements.

Syntax

element_id_function::=

![Description of element_id_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/element_id_function.gif)  
[Description of the illustration
element_id_function.eps](img_text/element_id_function.md)

vertex_id_function::=

  

![Description of vertex_id_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vertex_id_function.gif)  
[Description of the illustration
vertex_id_function.eps](img_text/vertex_id_function.md)

  

edge_id_function::=

  

![Description of edge_id_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/edge_id_function.gif)  
[Description of the illustration
edge_id_function.eps](img_text/edge_id_function.md)

  

element_reference::=

![Description of element_reference.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/element_reference.gif)  
[Description of the illustration
element_reference.eps](img_text/element_reference.md)

Semantics

Syntactically, the `VERTEX_ID` and `EDGE_ID` functions take an element
reference, which should be a vertex reference in case of `VERTEX_ID` and an
edge reference in case of `EDGE_ID`. The two functions generate identifiers
for graph elements that are globally unique within a database.

Content-wise, vertex and edge identifiers are JSON object that contains the
following information:

  * Owner of the graph that the vertex or edge is part of.

  * Name of the graph that the vertex or edge is part of.

  * Element table that the vertex or edge is defined in.

  * Key value of the vertex or edge.

Examples

Example 1

The following query lists the vertex identifiers of friends of Mary:

    
    
    SELECT CAST(p2_id AS VARCHAR2(200)) AS p2_id
    FROM GRAPH_TABLE ( students_graph
      MATCH (p1 IS person) -[e1 IS friends]- (p2 IS person)
      WHERE p1.name = 'Mary'
      COLUMNS (vertex_id(p2) AS p2_id)
    )
    ORDER BY p2_id;

The result is:

    
    
    P2_ID
    --------------------------------------------------------------------------------------------------------
    {"GRAPH_OWNER":"SCOTT","GRAPH_NAME":"STUDENTS_GRAPH","ELEM_TABLE":"PERSONS","KEY_VALUE":{"PERSON_ID":1}}
    {"GRAPH_OWNER":"SCOTT","GRAPH_NAME":"STUDENTS_GRAPH","ELEM_TABLE":"PERSONS","KEY_VALUE":{"PERSON_ID":3}}
    {"GRAPH_OWNER":"SCOTT","GRAPH_NAME":"STUDENTS_GRAPH","ELEM_TABLE":"PERSONS","KEY_VALUE":{"PERSON_ID":4}}

Example 2

The following query uses JSON dot-notation syntax to obtain a set of JSON
objects representing the vertex keys of vertices corresponding to friends of
Mary:

    
    
    SELECT GT.p2_id.KEY_VALUE
    FROM GRAPH_TABLE ( students_graph
      MATCH (p1 IS person) -[e1 IS friends]- (p2 IS person)
      WHERE p1.name = 'Mary'
      COLUMNS (vertex_id(p2) AS p2_id)
    ) GT
    ORDER BY key_value;

The result is:

    
    
    KEY_VALUE
    ----------------------------------------
    {"PERSON_ID":1}
    {"PERSON_ID":3}
    {"PERSON_ID":4}

Example 3

The following query uses the `JSON_VALUE` function to obtain all the element
table names of edges in the graph:

    
    
    SELECT DISTINCT json_value(e_id, '$.ELEM_TABLE') AS elem_table
    FROM GRAPH_TABLE ( students_graph
      MATCH -[e]-
      COLUMNS (edge_id(e) AS e_id)
    )
    ORDER BY elem_table;

The result is:

    
    
    ELEM_TABLE
    ----------------------------------------
    FRIENDS
    STUDENT_OF

### Vertex and Edge Equal Predicates

Purpose

The vertex and edge equal predicates allow for specifying that two vertex
variables (or two edge variables) should or should not bind to the same vertex
(or edge).

Syntax

element_equal_predicate::=

![Description of element_equal_predicate.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/element_equal_predicate.gif)  
[Description of the illustration
element_equal_predicate.eps](img_text/element_equal_predicate.md)

vertex_equal_predicate::=

  

![Description of vertex_equal_predicate.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vertex_equal_predicate.gif)  
[Description of the illustration
vertex_equal_predicate.eps](img_text/vertex_equal_predicate.md)

  

edge_equal_predicate::=

  

![Description of edge_equal_predicate.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/edge_equal_predicate.gif)  
[Description of the illustration
edge_equal_predicate.eps](img_text/edge_equal_predicate.md)

  

Examples

Example 1

The following query finds friends of friends of Mary. Here, the `vertex_equal
predicate` is used to make sure Mary herself is not included in the result.

    
    
    SELECT name
    FROM GRAPH_TABLE ( students_graph
      MATCH (p IS person)
              -[IS friends]- (friend IS person)
                -[IS friends]- (friend_of_friend IS person)
      WHERE p.name = 'Mary' AND NOT vertex_equal(p, friend_of_friend)
      COLUMNS (friend_of_friend.name)
    )
    ORDER BY name;

The result is:

    
    
    NAME
    ----------
    Bob
    John

### SOURCE and Destination Predicates

Purpose

The `SOURCE` and `DESTINATION` predicates allow for testing if a vertex is the
source or the destination of an edge. They are useful, for example, for
determining the direction of edges that are matched via any-directed edge
patterns.

Syntax

source_predicate::=

  

![Description of source_predicate.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/source_predicate.gif)  
[Description of the illustration
source_predicate.eps](img_text/source_predicate.md)

  

destination_predicate::=

  

![Description of destination_predicate.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/destination_predicate.gif)  
[Description of the illustration
destination_predicate.eps](img_text/destination_predicate.md)

  

Semantics

The `SOURCE` predicate takes a vertex and an edge as input and returns `TRUE`
or `FALSE` depending on whether the vertex is (not) the source of the edge.

The `DESTINATION` predicate also takes a vertex and an edge as input and
returns `TRUE` or `FALSE` depending on whether the vertex is (not) the
destination of the edge.

Examples

Example 1

The following query matches `FRIENDS` edges that are either incoming or
outgoing from Mary. For each edge, it return the `NAME` property for the
source of the edge as well as the `NAME` property of the destination of the
edge.

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
           MATCH (p1 IS person) -[e IS friends]- (p2 IS person)
           WHERE p1.name = 'Mary'
           COLUMNS (e.friendship_id,
                    e.meeting_date,
                    CASE WHEN p1 IS SOURCE OF e THEN p1.name ELSE p2.name END AS from_person,
                    CASE WHEN p1 IS DESTINATION OF e THEN p1.name ELSE p2.name END AS to_person))
    ORDER BY friendship_id;
    
    FRIENDSHIP_ID MEETING_DATE FROM_PERSON TO_PERSON
    ------------- ------------ ----------- ---------
                2 19-SEP-00    Mary        Alice
                3 19-SEP-00    Mary        John
                4 10-JUL-01    Bob         Mary
    

Example 2

The following query find friends of friends of John such that the two
`FRIENDS` edges are either both incoming or outgoing.

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
           MATCH (p1 IS person) -[e1 IS friends]- (p2 IS person)
                   -[e2 IS friends]- (p3 IS person)
           WHERE p1.name = 'John'
             AND ((p1 IS SOURCE OF e1 AND p2 IS SOURCE OF e2) OR
                 (p1 IS DESTINATION OF e1 AND p2 IS DESTINATION OF e2))
           COLUMNS (p1.name AS person_1,
                    CASE WHEN p1 IS SOURCE OF e1
                      THEN 'Outgoing' ELSE 'Incoming'
                      END AS e1_direction,
                    p2.name AS person_2,
                    CASE WHEN p2 IS SOURCE OF e2
                      THEN 'Outgoing' ELSE 'Incoming'
                      END AS e2_direction,
                    p3.name AS person_3))
    ORDER BY 1, 2, 3;
    
    PERSON_1   E1_DIRECTION PERSON_2   E2_DIRECTION PERSON_3
    ---------- ------------ ---------- ------------ ----------
    John       Incoming     Mary       Incoming     Bob
    John       Outgoing     Bob        Outgoing     Mary
    

Notice how the path from John via Mary to Alice is not part of the result
since it has an incoming edge followed by an outgoing edge and thus not two
edges in the same direction.

### Aggregation in GRAPH_TABLE

Purpose

Aggregations in `GRAPH_TABLE` are used to compute one or more values for a set
of vertices or edges in a variable-length path. This is done using the same
Aggregate Functions that are also available for non-graph queries.

Syntax

All the aggregate functions that are available for non-graph queries are also
available for graph queries. See Aggregate Functions for the syntax of these
functions.

Aggregate functions can be used in `WHERE` and `COLUMNS` clauses in
`GRAPH_TABLE`, with the restriction that `WHERE` clauses within quantified
patterns may not contain aggregate functions.

Syntactically, the value expressions in the aggregations must contain
references to vertices and edges in the graph pattern, rather than to columns
of tables like in case of regular (non-graph) SQL queries.

Semantics

See [Aggregate Functions](Aggregate-
Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848) for the semantics of
aggregate functions.

The arguments of the aggregate function must reference exactly one vertex or
edge variable via property references and/or vertex and edge ID functions.
Furthermore, the degree of reference must be group, meaning that the vertex or
edge that is referenced must be in a quantified path pattern and the
aggregation must be specified outside of a quantified path pattern. Also see
Element Variable for more details on the contextual interpretation of graph
element references.

The order in which values are aggregated in case of `LISTAGG`, `JSON_ARRAYAGG`
and `XMLAGG` is non-deterministic unless an `ORDER BY` clause is specified.
For example: `LISTAGG(edge1.property1 ORDER BY edge1.property1))`. There is
currently no way to explicitly order by path order in such a way that elements
are ordered in the same order as the vertices or edges in the path. However,
when omitting the `ORDER BY` clause, the current implementation nevertheless
implicitly orders by path order, but it should not be relied upon as this
behavior may change over time.

Restrictions

  * Only `WHERE` clauses that are not within a quantified pattern may contain aggregations. For example, the graph pattern `WHERE` clause as well as non-quantified element pattern `WHERE` clauses may contain aggregations, while parenthesized path pattern `WHERE` clauses may not contain aggregations since parenthesized path patterns currently have a restriction that they must always be quantified. 

  * The arguments of an aggregate function in `GRAPH_TABLE` must reference exactly one vertex or edge variable. They may reference that variable multiple times. 

  * References to the vertex or edge variable must be placed in a property reference or a vertex or edge ID function. For example, `COUNT(edge1)` is not allowed but `COUNT(edge_id(edge1))` and `COUNT(edge1.some_property))` are. 

  * The referenced vertex or edge must have group degree of reference. For example, `MATCH -[e1]-> WHERE SUM(e1.prop) > 10` is not allowed since variable e1 has singleton degree of reference within the `SUM` aggregate, while `MATCH -[e2]->{1,10} WHERE SUM(e2.prop) > 10 and MATCH -[e3]->{1,1} WHERE SUM(e3.prop) > 10` are allowed since variables `e2` and `e3` have group degree of reference within the `SUM` aggregates. 

  * The arguments of an aggregate function in `GRAPH_TABLE` cannot reference anything other than a vertex or edge declared within the graph pattern of the `GRAPH_TABLE`. For example, it is not possible to reference a column that is passed from an outer query. 

  * In case of `LISTAGG`, `JSON_ARRAYAGG` and `XMLAGG` there is no way to specify that the order of elements in the result should be in the order of the vertices or edges in the path, although the current implement nevertheless implicitly orders by path order. 

Examples

Example 1

The following query finds all paths that have a length between 2 and 5 edges
(`{2,5}`), starting from a person named Alice and following both incoming and
outgoing edges labeled friends. Edges along paths should not be traversed
twice (`COUNT(edge_id(e) = COUNT(DISTINCT edge_id(e))`). The query returns all
friendship IDs along paths as well as the length of each path.

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
           MATCH (p IS person) -[e IS friends]-{2,5} (friend IS person)
           WHERE p.name = 'Alice' AND
                 COUNT(edge_id(e)) = COUNT(DISTINCT edge_id(e))
           COLUMNS (LISTAGG(e.friendship_id, ', ') AS friendship_ids,
                    COUNT(edge_id(e)) AS path_length))
    ORDER BY path_length, friendship_ids;
    

Note that in the element pattern `WHERE` clause of the query above, p.name
references a property of a single edge, while `edge_id(e)` within the `COUNT`
aggregates accesses a list of element IDs since the edge variable e is
enclosed by the quantifier `{2,5}`. Similarly, the two property references in
the `COLUMNS` clause access a list of property values and edge ID values.

The result is:

    
    
    FRIENDSHIP_IDS    PATH_LENGTH
    ----------------- -----------
    2, 3              2
    2, 4              2
    2, 3, 1           3
    2, 4, 1           3
    2, 3, 1, 4        4
    2, 4, 1, 3        4
    

Example 2

The following query finds all paths between university `ABC` and university
`XYZ` such that paths have a length of up to 3 edges (`{,3}`). For each path,
a JSON array is returned such that the array contains the `friendship_id`
value for edges labeled friends, and the subject value for edges labeled
`student_of`. Note that the `friendship_id` property is cast to `VARCHAR(100)`
to make it type-compatible with the subject property.

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
           MATCH (u1 IS university) -[e]-{,3} (u2 IS university)
           WHERE u1.name = 'ABC' AND u2.name = 'XYZ'
           COLUMNS (JSON_ARRAYAGG(CASE WHEN e.subject IS NOT NULL THEN e.subject
                                  ELSE CAST(e.friendship_id AS VARCHAR(100)) END) AS path))
    ORDER BY path;
    The result is:
    PATH
    -----------------------
    ["Arts","3","Math"]
    ["Music","4","Math"]
    

Example 3

Example 3 The following query finds all paths that have a length between 2 and
3 edges (`{2,3}`), starting from a person named John and following only
outgoing edges labeled friends and vertices labeled person. Vertices along
paths should not have the same person_id as John (`WHERE p.person_id <>
friend.person_id`).

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
           MATCH (p IS person) ( -[e IS friends]-> (friend IS person)
                                 WHERE p.person_id <> friend.person_id){2,3}
           WHERE p.name = 'John'
           COLUMNS (COUNT(edge_id(e)) AS path_length,
                    LISTAGG(friend.name, ', ') AS names,
                    LISTAGG(e.meeting_date, ', ') AS meeting_dates ))
    ORDER BY path_length;
    

Above, the `COLUMNS` clause contains three aggregates, the first to compute
the length of each path, the second to create a comma-separated list of person
names along paths, and the third to create a comma-separate list of meeting
dates along paths.

The result of the query is:

    
    
    PATH_LENGTH NAMES               MEETING_DATES                                                      
    ----------- ------------------- -----------------------------------                                
              2 Bob, Mary           01-SEP-00, 10-JUL-01                                               
              3 Bob, Mary, Alice    01-SEP-00, 10-JUL-01, 19-SEP-00
    


[← Previous](value-expressions-graph_table.md)

[Next →](json_id-operator.md)
