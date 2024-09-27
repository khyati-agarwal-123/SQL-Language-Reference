[Previous](graph-reference.md) [Next](graph-table-shape.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. [GRAPH_TABLE Operator](graph_table-operator.md)
  4. Graph Pattern

## Graph Pattern

Purpose

A graph pattern consists of a set of vertex and edge patterns together with
search conditions. A graph pattern is matched against a graph to obtain a set
of solutions containing bindings for each vertex and edge variable in the
pattern.

This topic has the following sub-topics:

  * [Path Pattern](graph-pattern.md#GUID-0C83E320-23F7-41C6-87A8-BE7582185789)

  * [Element Pattern](graph-pattern.md#GUID-C8045246-F087-46E4-A707-5BF3D5712196)

  * [Quantified Path Pattern](graph-pattern.md#GUID-111F9A60-3554-46E6-93F1-BC88BF5E1949)

  * [Parenthesized Path Pattern](graph-pattern.md#GUID-395B9EB2-AB62-42B7-8CE5-9ADF2462B2C5)

  * [Graph Pattern WHERE Clause](graph-pattern.md#GUID-6CD2D743-2D7E-4DF7-8E4D-4680F3CB2AF1)

Syntax

graph_pattern::=

  

![Description of graph_pattern.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/graph_pattern.gif)  
[Description of the illustration
graph_pattern.eps](img_text/graph_pattern.md)

  

path_pattern_list::=

  

![Description of path_pattern_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path_pattern_list.gif)  
[Description of the illustration
path_pattern_list.eps](img_text/path_pattern_list.md)

  

Semantics

A graph pattern contains the following parts:

  * `MATCH` keyword. 

  * `path_pattern_list`: a list containing one or more comma-separated path patterns. 

  * `graph_pattern_where_clause`: an optional `WHERE` clause defining a search condition that may reference vertices and edges from the pattern. 

Two path patterns inside the same `GRAPH_TABLE` may share vertex and edge
variables to allow for creating more complex, non-linear patterns. Variables
may also be repeated within a single path pattern to create a cyclic pattern.
If multiple vertex or edge patterns share a variable then all the label
expressions and element pattern `WHERE` clauses in those patterns must satisfy
for binding to the element variable to occur.

If there are no shared variables between two path patterns, then the solution
set is a cross product of the solutions of the individual path patterns.

Restrictions

A vertex variable may not have the same name as an edge variable.

Examples

Example 1

The following query finds cyclic paths from `Mary` via two other persons back
to `Mary`. Only incoming edges are matched (`<-[..]-`).

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (a IS person) <-[e1 IS friends]- (b IS person)
               <-[e2 IS friends]- (c IS person)
                  <-[e3 is friends]- (a IS person)
      WHERE a.name= 'Mary'
      COLUMNS (a.name AS person_a, b.name AS person_b, c.name AS person_c)
    );

Here, the graph pattern consists of a single path pattern that has four vertex
patterns and three edge patterns. The first vertex pattern shares a variable
`a` with the last vertex pattern so that the pattern matches cyclic paths.

Only a single path matches the pattern:

    
    
    PERSON_A   PERSON_B   PERSON_C
    ---------- ---------- ----------
    Mary       Bob        John

Here, the output shows that a path was matched that starts in `Mary` with an
incoming edge to `Bob`, followed by an incoming edge to `John`, followed by an
incoming edge back to `Mary`.

The same query may also be expressed by breaking up the single path pattern
into multiple path patterns as follows:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (a IS person) <-[e1 IS friends]- (b IS person),
            (b) <-[e2 IS friends]- (c IS person),
            (c) <-[e3 is friends]- (a IS person)
      WHERE a.name= 'Mary'
      COLUMNS (a.name AS person_a, b.name AS person_b, c.name AS person_c)
    );

Here, the first path pattern shares variable `b` with the second path pattern,
the second path pattern shares variable `c` with the third path pattern, and
the third path pattern shares variable `a` with the first path pattern.

### Path Pattern

Purpose

A path pattern specifies a linear pattern that matches a string of vertices
and edges. Path patterns are made up of the concatenation of one or more
vertex and edge patterns. Vertex and edge patterns may be quantified as well
as parenthesized.

Syntax

path_pattern::=

  

![Description of path_pattern.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path_pattern.gif)  
[Description of the illustration path_pattern.eps](img_text/path_pattern.md)

  

path_pattern_expression::=

  

![Description of path_pattern_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path_pattern_expression.gif)  
[Description of the illustration
path_pattern_expression.eps](img_text/path_pattern_expression.md)

  

path_term::=

  

![Description of path_term.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path_term.gif)  
[Description of the illustration path_term.eps](img_text/path_term.md)

  

path_factor::=

  

![Description of path_factor.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path_factor.gif)  
[Description of the illustration path_factor.eps](img_text/path_factor.md)

  

path_concatenation::=

  

![Description of path_concatenation.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path_concatenation.gif)  
[Description of the illustration
path_concatenation.eps](img_text/path_concatenation.md)

  

path_primary::=

  

![Description of path_primary.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path_primary.gif)  
[Description of the illustration path_primary.eps](img_text/path_primary.md)

  

Semantics

Syntactically, a path pattern is the concatenation of one or more element
patterns, which are either vertex patterns or edge patterns.

The element patterns of a path pattern are not required to alternate between
vertex and edge patterns; there may be two consecutive edge patterns or two
consecutive vertex patterns. These topologically inconsistent patterns are
understood during pattern matching as follows:

  * Two consecutive vertex patterns bind to the same vertex.

  * Two consecutive edge patterns conceptually have an implicit vertex pattern between them.

Restricitons

Path patterns have the following restrictions:

  * A path pattern may only contain two consecutive vertex patterns if one of the vertex patterns is contained in a parenthesized path pattern while the other one is not.

  * A parenthesized path pattern must be quantified. 

Examples

Example 1

The following query counts the number of vertices in the graph:

    
    
    SELECT COUNT(*)
    FROM GRAPH_TABLE ( students_graph
      MATCH (v)
      COLUMNS (1 AS dummy)
    );

Note that the `COLUMNS` clause needs to contain at least one expression, hence
a dummy value is projected but it is not returned from the query.

The result is:

    
    
      COUNT(*)
    ----------
             6

Example 2

The following query counts the number of edges in the graph:

    
    
    SELECT COUNT(*)
    FROM GRAPH_TABLE ( students_graph
      MATCH -[e]->
      COLUMNS (1 AS dummy)
    );

The result is:

    
    
      COUNT(*)
    ----------
             8

Example 3

The following query finds persons that are two friend hops away from `Mary`,
following either incoming or outgoing friends edges:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (n IS person) -[IS friends]- () -[IS friends]- (m IS person)
      WHERE n.name = 'Mary' AND m.name <> n.name
      COLUMNS (m.name AS fof)
    );

In the path pattern above:

  * (`n IS person`) is a vertex pattern that has a variable `n` and a label expression `IS person`. 

  * `-[IS friends]-` is an any-directed edge pattern that has an implicit variable and a label expression `IS friends`. 

  * `()` is a vertex pattern that has an implicit variable and no label expression such that it matches vertices having any label(s). 

  * `-[IS friends]-` is again an any-directed edge pattern that has an implicit variable and a label expression `IS friends`. 

  * (`n IS person`) is a vertex pattern that has a variable `n` and a label expression `IS person`. 

The result is:

    
    
    FOF
    ----------
    Bob
    John

Note that the query above can also be expressed as:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (n IS person) -[IS friends]- -[IS friends]- (m IS person)
      WHERE n.name = 'Mary' AND m.name <> n.name
      COLUMNS (m.name AS fof)
    );

Here, the vertex pattern between the two edge patterns is implicit.

The same query can be expressed using a quantifier to avoid the repeated
specification of the same edge pattern:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (n IS person) -[IS friends]-{2}(m IS person)
      WHERE n.name = 'Mary' AND m.name <> n.name
      COLUMNS (m.name AS fof)
    );
    

Quantified path patterns may be parenthesized:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (n IS person) (-[IS friends]-){2}(m IS person)
      WHERE n.name = 'Mary' AND m.name <> n.name
      COLUMNS (m.name AS fof)
    );

Note that each of the syntax variations above gives the same result:

    
    
    FOF
    ----------
    Bob
    John

### Element Pattern

Purpose

An element pattern is either a vertex pattern or an edge pattern. The result
of matching an element pattern is the binding of vertices or edges to the
implicitly or explicitly declared variable of the element pattern.

This section comprises the following sections:

  * [Vertex Pattern](graph-pattern.md#GUID-590F45CA-2D6E-42D8-925E-28A9F1B421E3)

  * [Edge Pattern](graph-pattern.md#GUID-B6D2B840-7BC4-4F95-B9D1-B65B7EB826E6)

  * [Element Pattern Filler](graph-pattern.md#GUID-C364215A-E792-4CF3-A352-EA4C2ABC7A29)

  * [Element Variable](graph-pattern.md#GUID-03FAEC9D-A5FE-4D8F-9F20-38556D08932B)

  * [Label Expression](graph-pattern.md#GUID-9671FB35-E95A-40F9-9ABB-7DE879AC46F5)

  * [Element Pattern WHERE Clause](graph-pattern.md#GUID-9AC5083D-1B05-4D62-9C5B-E14AD66C2C10)

Syntax

element_pattern::=

  

![Description of element_pattern.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/element_pattern.gif)  
[Description of the illustration
element_pattern.eps](img_text/element_pattern.md)

  

#### Vertex Pattern

Purpose

A vertex pattern is a pattern that matches vertices in a graph. The result of
such matching is the binding of a set of vertices to the implicitly or
explicitly declared variable of the vertex pattern.

Syntax

vertex_pattern::=

  

![Description of vertex_pattern.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vertex_pattern.gif)  
[Description of the illustration
vertex_pattern.eps](img_text/vertex_pattern.md)

  

Semantics

Visually, a vertex pattern has two parentheses ( ) to mimic a circle since
vertices are typically represented by circles in visualizations of graphs.

Examples

Example 1

The following query counts the number of vertices in the graph:

    
    
    SELECT COUNT(*)
    FROM GRAPH_TABLE ( students_graph
      MATCH (v)
      COLUMNS (1 AS dummy)
    );

Note that the `COLUMNS` clause needs to contain at least one expression, hence
a dummy value is projected but it is not returned from the query.

The result is:

    
    
      COUNT(*)
    ----------
          6

Example 2

The following query matches all persons with a date of birth greater than 1
January 1980:

    
    
    SELECT name, birthday
    FROM GRAPH_TABLE ( students_graph
      MATCH (p IS person WHERE p.dob > DATE '1980-01-01')
      COLUMNS (p.name, p.dob AS birthday)
    )
    ORDER BY birthday;

The result is:

    
    
    NAME	   BIRTHDAY
    ---------- ---------
    Mary	   25-SEP-82
    Alice	  01-FEB-87

#### Edge Pattern

Purpose

An edge pattern is a pattern that matches edges in a graph. The result of such
matching is the binding of a set of edges to the implicitly or explicitly
declared variable of the edge pattern.

Syntax

edge_pattern::=

![Description of edge_pattern.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/edge_pattern.gif)  
[Description of the illustration edge_pattern.eps](img_text/edge_pattern.md)

full_edge_pattern::=

![Description of full_edge_pattern.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/full_edge_pattern.gif)  
[Description of the illustration
full_edge_pattern.eps](img_text/full_edge_pattern.md)

full_edge_pointing_right::=

![Description of full_edge_pointing_right.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/full_edge_pointing_right.gif)  
[Description of the illustration
full_edge_pointing_right.eps](img_text/full_edge_pointing_right.md)

full_edge_pointing_left::=

![Description of full_edge_pointing_left.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/full_edge_pointing_left.gif)  
[Description of the illustration
full_edge_pointing_left.eps](img_text/full_edge_pointing_left.md)

full_edge_any_direction::=

  

![Description of full_edge_any_direction.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/full_edge_any_direction.gif)  
[Description of the illustration
full_edge_any_direction.eps](img_text/full_edge_any_direction.md)

  

abbreviated_edge_pattern::=

![Description of abbreviated_edge_pattern.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/abbreviated_edge_pattern.gif)  
[Description of the illustration
abbreviated_edge_pattern.eps](img_text/abbreviated_edge_pattern.md)

Semantics

Visually, an edge pattern mimics an arrow since edges are typically
represented by arrows in visualizations of graphs. For example, <-[]- or <\-
are incoming edge patterns because they look like incoming arrows, while -[]->
or -> are outgoing edge patterns because they look like outgoing arrows.

An edge_pattern is either a full_edge_pattern or an abbreviated_edge_pattern.
The full edge pattern has an element_pattern_filler with optional element
pattern variable, label expression and element pattern WHERE clause, while the
abbreviated edge pattern provides syntactic sugar in case none of the three
optional filler parts are needed.

The following table summarizes the options:

Table 4-6 Summary of Edge Patterns

Directionality | Full Edge Pattern | Abbreviated Edge Pattern  
---|---|---  
Directed pointing to the right |  -[ ] -> |  ->  
Directed pointing to the left |  <-[ ]- |  <-  
Any-Directed: pointing to the right or the left |  -[ ]- or <-[ ]-> |  -  
  
Note that since the abbreviated syntax does not allow for providing a variable
name, a label expression, or an element pattern `WHERE` clause, abbreviated
edge patterns match with all edges in the graph that have the specified
direction.

Examples

Example 1

The following query counts the number of edges in the graph:

    
    
    SELECT COUNT(*)
    FROM GRAPH_TABLE ( students_graph
      MATCH ->
      COLUMNS (1 AS dummy)
    );

The result is:

    
    
      COUNT(*)
    ----------
          8
    

Example 2

The following query matches all `friends` edges that have a property
`meeting_date` with a value greater than `DATE '2000-01-01'`:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH -[e IS friends WHERE e.meeting_date > DATE '2001-01-01']->
      COLUMNS (e.meeting_date)
    );

The result is:

    
    
    MEETING_D
    ---------
    10-JUL-01

#### Element Pattern Filler

Purpose

Vertex patterns and full edge patterns have a filler for providing an optional
variable declaration, an optional label expression, and an optional `WHERE`
clause.

Syntax

element_pattern_filler::=

  

![Description of element_pattern_filler.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/element_pattern_filler.gif)  
[Description of the illustration
element_pattern_filler.eps](img_text/element_pattern_filler.md)

  

Semantics

Vertex patterns and full edge patterns and have a filler containing the
following parts:

  * An optional `element_variable_declaration` for providing a variable name for the element pattern so that the element can be referenced elsewhere, for example in `WHERE` and `COLUMNS` clauses. If no variable name is specified, a variable is implicit and cannot be referenced. 

  * An optional `is_label_expression` for defining a label expression. Vertices and edges only match if they satisfy the specified label expression. 

  * An optional `element_pattern_where_clause` for defining an in-lined search condition. Vertices and edges only match if they satisfy the specified search condition. 

Examples

Example 1

The following query finds persons that are two friend hops away from `Mary`,
following either incoming or outgoing friends edges:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (n IS person WHERE n.name = 'Mary')
              -[e IS friends WHERE e.meeting_date > DATE '2001-01-01']-
                () -[IS friends]- (m IS person)
      WHERE m.name <> n.name
      COLUMNS (m.name, e.meeting_date)
    );

In the path pattern above:

  * (`n IS person WHERE n.name = 'Mary'`) is a vertex pattern that has a variable `n`, a label expression `IS person` and an element pattern `WHERE` clause `WHERE n.name = 'Mary'`. 

  * `-[e IS friends WHERE e.meeting_date > DATE '2001-01-01']-` is an any-directed edge pattern that has a variable `e`, a label expression `IS friends` and an element pattern `WHERE` clause `WHERE e.meeting_date > DATE '2001-01-01'`. 

  * `()` is a vertex pattern that has an implicit variable and neither has a label expression nor an element pattern `WHERE` clause. 

  * `-[IS friends]-` is an any-directed edge pattern that has an implicit variable, a label expression `IS friends` but no element pattern `WHERE` clause. 

  * (`n IS person`) is a vertex pattern that has a variable `n`, a label expression` IS person` but no element pattern `WHERE` clause. 

The result is:

    
    
    NAME       MEETING_D
    ---------- ---------
    John       10-JUL-01

#### Element Variable

Purpose

Element variables are either vertex or edge variables. During pattern
matching, the variables will bind to sets of vertices or edges in the graph.
Element variables can be referenced from other places in the query to access
data of vertices and edges, such as their property values.

Syntax

element_variable_declaration::=

  

![Description of element_variable_declaration.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/element_variable_declaration.gif)  
[Description of the illustration
element_variable_declaration.eps](img_text/element_variable_declaration.md)

  

element_variable::=

  

![Description of element_variable.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/element_variable.gif)  
[Description of the illustration
element_variable.eps](img_text/element_variable.md)

  

Semantics

Syntactically, an `element_variable_declaration` is an identifier and can thus
be either double quoted or unquoted. Declaring an element variable is optional
and if no element variable is declared then the element pattern has an
implicit variable with an (implicit) unique name. Implicit variables cannot be
referenced elsewhere in the query.

Multiple vertex patterns may declare the same element variable and multiple
edge patterns may also declare the same element variable. In such cases, there
are not multiple variables but there is a single variable that is shared by
the different vertex or edge patterns.

Declared variables are visible within the `GRAPH_TABLE` in which they are
declared. They may be referenced in `WHERE` and `COLUMNS` clauses defined in
the same `GRAPH_TABLE`.

If an element variable is declared in a quantified path pattern, then it may
bind to more than one vertex or edge within a single solution to the pattern.
References are interpreted contextually: if the reference occurs outside the
quantified path pattern, then the reference is to the complete list of graph
elements that are bound to the element variable. In this circumstance, the
element variable is said to have group degree of reference. However, if the
reference does not cross a quantifier, then the reference has singleton degree
of reference.

For example, in `(X) -[E WHERE E.P > 1]->{1,10} (Y) WHERE SUM(E.P) < 100` the
edge variable `E` is referenced twice: once in the edge pattern and once
outside the edge pattern. Within the edge pattern, `E` has singleton degree of
reference and the property reference `E`.`P` references a property of a single
edge. On the other hand, the reference within the `SUM` aggregate has group
degree of reference (because of the quantifier `{1,10}`) and references the
list of edges that are bound to `E`.

Restrictions

  * A vertex pattern may not declare a variable with the same name as an edge pattern.

  * A quantified path pattern may not declare a variable with the same name as an element variable declared outside of the quantified path pattern.

Examples

Example 1

The following query finds friends of friends of John following incoming or
outgoing edges that have a property` meeting_date` with a value greater than
`DATE '2000-09-015'`:

    
    
    SELECT DISTINCT name
    FROM GRAPH_TABLE ( students_graph
      MATCH (a IS person) -[e IS friends WHERE e.meeting_date > DATE '2000-09-15']-{2} ("b" IS person)
      WHERE a.name = 'John' AND a.name <> "b".name
      COLUMNS ("b".name)
    );

In the query above, `a` and `"b"` are vertex variables, `e` is an edge
variable and `e.meeting_date`, `a.name` and `"b".name` are property references
that access a property value of the referenced vertex or edge.

The result shows that John has two such friends of friends:

    
    
    NAME
    ----------
    Bob
    Alice
    

Example 2

The following query finds friends of Mary and the universities that Mary and
her friends went to:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (p1 IS person) -[e1 IS friends]- (p2 IS person)
          , (p1) -[IS student_of]-> (u1 IS university)
          , (p2) -[IS student_of]-> (u2 IS university)
      WHERE p1.name = 'Mary'
      COLUMNS (p1.name, p2.name AS friend, e1.meeting_date, u1.name AS univ_1, u2.name AS univ_2)
    );

In the query above, `p1`, `p2`, `u1` and `u2` are vertex variables, while `e1`
is an edge variable. The pattern `-[IS student_of]-> `appears twice and
implicitly declares two unique variables that cannot be referenced.
Furthermore, there are two vertex patterns that share variable `p1` and there
are two vertex patterns that share variable `p2`. Vertices will only bind to
such variable if both vertex patterns match.

The result shows that Mary has three friends, one of which goes to the same
university `XYZ`, while two other friends go to a different university `ABC`:

    
    
    NAME       FRIEND     MEETING_D UNIV_1     UNIV_2
    ---------- ---------- --------- ---------- ----------
    Mary       John       19-SEP-00 XYZ        ABC
    Mary       Bob        10-JUL-01 XYZ        ABC
    Mary       Alice      19-SEP-00 XYZ        XYZ

Example 3

The following query finds all paths that have a length between 2 and 5 edges
(`{2,5}`), starting from a person named Alice and following both incoming and
outgoing edges labeled `friends`. Edges along paths should not be traversed
twice (`COUNT(e.friendship_id`) =` COUNT(DISTINCT e.friendship_id`)). The
query returns all friendship IDs along paths as well as the length of each
path.

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
           MATCH (p IS person) -[e IS friends]-{2,5} (friend IS person)
           WHERE p.name = 'Alice' AND
                 COUNT(e.friendship_id) = COUNT(DISTINCT e.friendship_id)
           COLUMNS (LISTAGG(e.friendship_id, ', ') AS friendship_ids,
                    COUNT(e.friendship_id) AS path_length));
    

Note that in the element pattern `WHERE` clause of the query above, `p.name`
references a property of a single edge, while` e.friendship_id` within the
`COUNT` aggregate accesses a list of property values since the edge variable
`e` is enclosed by the quantifier `{2,5}`. Similarly, the two property
references in the `COLUMNS` clause both access a list of property values.

The result is:

    
    
    FRIENDSHIP_IDS    PATH_LENGTH
    ----------------- -----------
    2, 3              2
    2, 4              2
    2, 3, 1           3
    2, 4, 1           3
    2, 3, 1, 4        4
    2, 4, 1, 3        4

#### Label Expression

Purpose

Label expressions are used to limit the search to only vertices or edges of a
specific type.

Syntax

is_label_declaration::=

  

![Description of is_label_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/is_label_expression.gif)  
[Description of the illustration
is_label_expression.eps](img_text/is_label_expression.md)

  

label_expression::=

  

![Description of label_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/label_expression.gif)  
[Description of the illustration
label_expression.eps](img_text/label_expression.md)

  

label_disjunction::=

  

![Description of label_disjunction.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/label_disjunction.gif)  
[Description of the illustration
label_disjunction.eps](img_text/label_disjunction.md)

  

label::=

  

![Description of label.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/label.gif)  
[Description of the illustration label.eps](img_text/label.md)

  

Semantics

Syntactically, an `is_label_declaration` starts with the keyword `IS` followed
by a `label_expression`, which is either a `label` or a `label_disjunction`
denoted by a vertical bar |. A label itself is an identifier and can thus be
double quoted or unquoted.

An element pattern matches only vertices and edges that satisfy the label
expression. If the label expression is omitted, then all vertices and edges
are matched irrespective of their labels.

Examples

Example 1

The following query matches all vertices labeled person or university and
retrieves their name and date of birth properties:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (x IS person|university)
      COLUMNS (x.name, x.dob)
    )
    ORDER BY name;

The result is:

    
    
    NAME       DOB
    ---------- ---------
    ABC
    Alice      01-FEB-87
    Bob        11-MAR-66
    John       13-JUN-63
    Mary       25-SEP-82
    XYZ

Above, since universities do not have a date of birth, a null value is
returned and shows up as empty string in the `DOB` column.

Example 2

The following query matches outgoing edges labeled `student_of` or `friends`
from a person named Mary to a vertex `m` that is labeled `university` or
`"PERSON"`:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (n IS person) -[e IS student_of|friends]-> (m IS university|"PERSON")
      WHERE n.name = 'Mary'
      COLUMNS (e.subject, e.meeting_date, m.name)
    )
    ORDER BY subject, meeting_date, name;

The result is:

    
    
    SUBJECT    MEETING_D NAME
    ---------- --------- ----------
    Math                 XYZ
               19-SEP-00 Alice
               19-SEP-00 John

#### Element Pattern WHERE Clause

Purpose

The element pattern `WHERE` clause specifies a search condition that is
syntactically placed inside a vertex or an edge pattern and that needs to be
satisfied by the vertex or edge for the pattern to match.

Syntax

element_pattern_where_clause::=

  

![Description of element_pattern_where_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/element_pattern_where_clause.gif)  
[Description of the illustration
element_pattern_where_clause.eps](img_text/element_pattern_where_clause.md)

  

Semantics

Syntactically, the `element_pattern_where_clause` starts with the keyword
`WHERE` and is followed by a `search_condition`, which is an arbitrary boolean
value expression.

The element pattern `WHERE` clause may reference any graph element variable in
the graph pattern. If the variable has group degree of reference, then the
reference must be inside the arguments of an aggregate function. See
[Aggregation in GRAPH_TABLE](value-expressions-
graph_table.md#GUID-4CC87ADB-39A9-4A4B-8D12-8E9E667DAEC9). There is no
requirement that the search condition must reference the variable of the
element pattern itself, but for improved query readability it is generally
recommended that it always does such that any search condition that does not
reference the element variable is placed in the graph pattern `WHERE` clause
instead.

Examples

Example 1

The following query finds all friends of John whom he met after `15 September
2000`:

    
    
    SELECT Gt.name
    FROM GRAPH_TABLE ( students_graph
      MATCH (a IS person WHERE a.name = 'John')
              -[e IS friends WHERE e.meeting_date > DATE '2000-09-15']-
                (b IS person)
      COLUMNS (b.name)
    ) GT;

The example above contains two element pattern `WHERE` clauses:

  * `WHERE a.name` = `'John'`

  * `WHERE e.meeting_date > DATE '2000-09-15'`. 

The result is:

    
    
    NAME
    ----------
    Mary

### Quantified Path Pattern

Purpose

Quantified path patterns allow for repeated matching of a path pattern,
typically for the purpose of matching variable-length paths. The specified
quantifier determines a minimum and maximum for the number of times to match
the path pattern.

Syntax

quantified_path_primary::=

  

![Description of quantifier_path_primary.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/quantifier_path_primary.gif)  
[Description of the illustration
quantifier_path_primary.eps](img_text/quantifier_path_primary.md)

  

graph_pattern_quantifier::=

  

![Description of graph_pattern_quantifier.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/graph_pattern_quantifier.gif)  
[Description of the illustration
graph_pattern_quantifier.eps](img_text/graph_pattern_quantifier.md)

  

fixed_quantifier::=

  

![Description of fixed_quantifier.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/fixed_quantifier.gif)  
[Description of the illustration
fixed_quantifier.eps](img_text/fixed_quantifier.md)

  

general_quantifier::=

  

![Description of general_quantifier.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/general_quantifier.gif)  
[Description of the illustration
general_quantifier.eps](img_text/general_quantifier.md)

  

lower_bound::=

  

![Description of lower_bound.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lower_bound.gif)  
[Description of the illustration lower_bound.eps](img_text/lower_bound.md)

  

upper_bound::=

  

![Description of upper_bound.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/upper_bound.gif)  
[Description of the illustration upper_bound.eps](img_text/upper_bound.md)

  

Semantics

A `quantified_path_primary` is a path_primary together with a quantifier.
Here, the path primary must be either an edge pattern or a parenthesized path
pattern.

A graph_pattern_quantifier is either:

  * A `fixed_quantifier`, which is an unsigned integer placed between curly braces. The integer value specifies an exact number of times the pattern should be matched. In other words, the lower bound on the number of times to match the pattern is the same as the upper bound. 

  * A `general_quantifier`, which has an optional `lower_bound`, a comma (,) and a mandatory `upper_bound`, all of which are placed between curly braces. Lower and upper bound are unsigned integers and specify a minimum and a maximum number of times to match the path pattern. If no lower bound is specified, then the lower bound is zero (0). 

The following table summarizes the options:

Table 4-7 Quantifier Table

Quantifier | Meaning  
---|---  
`{ n }` |  Exactly `n`  
`{ n, m }` |  Between `n` and `m` (inclusive)   
`{ , m }` |  Between zero (0) and `m` (inclusive)   
  
Restrictions

The following restrictions apply to quantified path patterns:

  * The path primary that is quantified must be either an edge pattern or a parenthesized path pattern. For example, vertex patterns cannot be quantified unless they appear together with at least one edge pattern inside a parenthesized path pattern.

  * The lower bound should be between 0 and 10 (inclusive), while the upper bound should be between 1 and 10 (inclusive) and greater than or equal to the lower bound.

  * Nested quantifiers are not allowed.

Examples

Example 1

The following query finds friends of friends of John following incoming or
outgoing edges that have a property `meeting_date` with a value greater than
`DATE '2000-090-15'`:

    
    
    SELECT DISTINCT name
    FROM GRAPH_TABLE ( students_graph
      MATCH (a IS person)
              -[e IS friends WHERE e.meeting_date > DATE '2000-09-15']-{2}
                (b IS person)
      WHERE a.name = 'John' AND a.name <> b.name
      COLUMNS (b.name)
    );

In the query above, the path pattern `-[e IS friends WHERE e.meeting_date >
DATE '2000-09-15']-` is quantified with the fixed quantifier `{2}` to indicate
that the edge pattern should match exactly twice.

The result is:

    
    
    NAME
    ----------
    Bob
    Alice

The same query may be written using a parenthesized path pattern too. The
following are all syntactic alternatives, the latter two use a parenthesized
path pattern:

  * `-[e IS friends WHERE e.meeting_date > DATE '2000-09-15']-{2}`

  * `(-[e IS friends WHERE e.meeting_date > DATE '2000-09-15']-){2}`

  * `(-[e IS friends]- WHERE e.meeting_date > DATE '2000-09-15'){2}`

Example 2

The following query finds persons that can be reached from Mary within three
hops, following only persons that are taller than Mary.

    
    
    SELECT DISTINCT name, height
    FROM GRAPH_TABLE ( students_graph
      MATCH (a IS person|person_ht)
               (-[e IS friends]- (x IS person_ht) WHERE x.height > a.height) {,3}
                 (b IS person|person_ht)
      WHERE a.name = 'Mary'
      COLUMNS (b.name, b.height)
    )
    ORDER BY height;
    
    The result is:
    NAME           HEIGHT
    ---------- ----------
    Mary             1.65
    Alice             1.7
    Bob              1.75
    John              1.8

Note that the reason Mary is included in the result is because the specified
quantifier `{,3}` has a lower bound of zero such that the quantified pattern
is allowed to match zero times in which case variables `a` and `b` bind to the
same vertex corresponding to Mary.

Example 3

The following query finds all paths between university `ABC` and university
`XYZ` such that paths have a length of up to 3 edges (`{,3}`). For each path,
a JSON array is returned such that the array contains the `friendship_id`
value for edges labeled `friends`, and the subject value for edges labeled
`student_of`. Note that the `friendship_id` property is cast to `VARCHAR(100)`
to make it type-compatible with the subject property.

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
           MATCH (u1 IS university) -[e]-{,3} (u2 IS university)
           WHERE u1.name = 'ABC' AND u2.name = 'XYZ'
           COLUMNS (JSON_ARRAYAGG(CASE WHEN e.subject IS NOT NULL THEN e.subject
                                  ELSE CAST(e.friendship_id AS VARCHAR(100)) END) AS path));

The result is:

    
    
    PATH
    -----------------------
    ["Arts","3","Math"]
    ["Music","4","Math"]

### Parenthesized Path Pattern

Purpose

Parenthesized path patterns allow for defining more complex quantified path
pattern expressions.

Syntax

parenthesized_path_pattern_expression::=

  

![Description of parenthesized_path_pattern_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parenthesized_path_pattern_expression.gif)  
[Description of the illustration
parenthesized_path_pattern_expression.eps](img_text/parenthesized_path_pattern_expression.md)

  

parenthesized_path_pattern_where_clause::=

![Description of parenthesized_path_pattern_where_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parenthesized_path_pattern_where_clause.gif)  
[Description of the illustration
parenthesized_path_pattern_where_clause.eps](img_text/parenthesized_path_pattern_where_clause.md)

Semantics

A `parenthesized_path_pattern_expression` is a `path_pattern_expression`
together with an optional `parenthesized_path_pattern_where_clause`, placed in
between parentheses.

Parenthesized path patterns allow for the quantification of any path pattern
expression that contains at least one edge pattern. Without parentheses, only
a single edge pattern can be quantified.

The parenthesized path pattern `WHERE` clause may reference vertex and edge
variables declared in the parenthesized path pattern itself as well as vertex
and edge variables declared outside of the parenthesized path pattern. If the
variable has group degree of reference, then the reference must be inside the
arguments of an aggregate function. See [Aggregation in GRAPH_TABLE](value-
expressions-graph_table.md#GUID-4CC87ADB-39A9-4A4B-8D12-8E9E667DAEC9).

Restrictions

The following restrictions apply to parenthesized path pattern expressions:

  * Each parenthesized path pattern needs to be quantified.

  * There can only be a single level of parentheses. Nesting of parenthesized path patterns is not allowed.

Examples

Example 1

The following query finds persons that can be reached from Bob within one to
three hops (`{1,3}`) such that for each consecutive pair of persons along the
path, the first person has a date of birth that is smaller than the date of
birth of the second person.

    
    
    SELECT DISTINCT name, birthday
    FROM GRAPH_TABLE ( students_graph
      MATCH
       (a IS person)
         ( (x) -[e IS friends]- (y IS person) 
           WHERE x.dob < y.dob ){1,3}
             (b IS person)
      WHERE a.name = 'Bob'
      COLUMNS (b.name, b.dob AS birthday)
    )
    ORDER BY birthday;
    

The result is:

    
    
    NAME       BIRTHDAY
    ---------- ---------
    Mary       25-SEP-82
    Alice      01-FEB-87

Example 2

The following query finds all paths that have a length between 2 and 3 edges
({2,3}), starting from a person named John and following only outgoing edges
labeled friends and vertices labeled person. Vertices along paths should not
have the same person_id as John (WHERE p.person_id <> friend.person_id).

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
           MATCH (p IS person) ( -[e IS friends]-> (friend IS person)
                                 WHERE p.person_id <> friend.person_id){2,3}
           WHERE p.name = 'John'
           COLUMNS (COUNT(e.friendship_id) AS path_length,
                    LISTAGG(friend.name, ', ') AS names,
                    LISTAGG(e.meeting_date, ', ') AS meeting_dates ));
    

Above, the `COLUMNS` clause contains three aggregates, the first to compute
the length of each path, the second to create a comma-separated list of person
names along paths, and the third to create a comma-separate list of meeting
dates along paths.

The result of the query is:

    
    
    PATH_LENGTH NAMES               MEETING_DATES                                                      
    ----------- ------------------- -----------------------------------                                
              2 Bob, Mary           01-SEP-00, 10-JUL-01                                               
              3 Bob, Mary, Alice    01-SEP-00, 10-JUL-01, 19-SEP-00

### Graph Pattern WHERE Clause

Purpose

The graph pattern `WHERE` clause specifies a search condition that is
syntactically placed at the end of the graph pattern and that needs to be
satisfied by the complete graph pattern in order for the graph pattern to
match.

Syntax

graph_pattern_where_clause::=

![Description of graph_pattern_where_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/graph_pattern_where_clause.gif)  
[Description of the illustration
graph_pattern_where_clause.eps](img_text/graph_pattern_where_clause.md)

Semantics

Syntactically, the graph pattern `WHERE` clause starts with the keyword
`WHERE` and is followed by a `search_condition`, which is an arbitrary boolean
value expression.

The graph pattern `WHERE` clause may reference any element variables in the
graph pattern. If the variable has group degree of reference, then the
reference must be inside the arguments of an aggregate function. See
[Aggregation in GRAPH_TABLE](value-expressions-
graph_table.md#GUID-4CC87ADB-39A9-4A4B-8D12-8E9E667DAEC9) .

Examples

Example 1

The following query finds all friends of John whom he met after 15 September
2000:

    
    
    SELECT Gt.name
    FROM GRAPH_TABLE ( students_graph
      MATCH (a IS person) -[e IS friends]- (b IS person)
      WHERE a.name = 'John' AND e.meeting_date > DATE '2000-09-15'
      COLUMNS (b.name)
    ) GT;

Note that the two conditions are placed together in the graph pattern `WHERE`
clause to form a single search that needs to be satisfied by the pattern:
`WHERE a.name = 'John' AND e.meeting_date > DATE '2000-09-15'`.

The result is:

    
    
    NAME
    ----------
    Mary


[← Previous](graph-pattern.md)

[Next →](graph-table-shape.md)
