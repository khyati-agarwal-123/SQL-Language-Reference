[Previous](data-quality-operators.md) [Next](graph-reference.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. GRAPH_TABLE Operator

## GRAPH_TABLE Operator

Purpose

The `GRAPH_TABLE` operator can be used as a table expression in a `FROM`
clause. It takes a graph as input against which it matches a specified graph
pattern. It then outputs a set of solutions in tabular form.

This topic consists of the following sub-topics:

  * [Graph Reference](graph-reference.md#GUID-873488F0-58D1-4B9D-94B1-F4967B1785DD)

  * [Graph Pattern](graph-pattern.md#GUID-1F1E8BC1-CEBB-43A2-B66A-C7D9BB24D88C)

  * [Graph Table Shape](graph-table-shape.md#GUID-93202EC2-D2F3-45B0-869D-4C03057EB1A5)

  * [Value Expressions for GRAPH_TABLE](value-expressions-graph_table.md#GUID-30B0844D-329B-4A95-BEA1-953AF9F3ED7C)

Syntax

graph_table::=

  

![Description of graph_table.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/graph_table.gif)  
[Description of the illustration graph_table.eps](img_text/graph_table.md)

  

([graph_reference ::=](graph-
reference.md#GUID-873488F0-58D1-4B9D-94B1-F4967B1785DD__GUID-95FA262E-2E7B-4457-9B62-CBB97ED19E56),
[graph_pattern ::=](graph-
pattern.md#GUID-1F1E8BC1-CEBB-43A2-B66A-C7D9BB24D88C__GUID-2AE8A195-AE59-491B-B2F2-03C6204D33F0),
[graph_table_shape ::=](graph-table-
shape.md#GUID-93202EC2-D2F3-45B0-869D-4C03057EB1A5__GUID-25DD691C-4599-47C5-9122-B59ACCD03DBB))

Semantics

The` GRAPH_TABLE` operator starts with the keyword `GRAPH_TABLE` and consists
of the following three parts that are placed between parentheses:

  * `graph_reference`: a reference to a graph to perform the pattern matching on. Note that any graph first needs to be created through a `CREATE PROPERTY GRAPH` statement before it can be referenced in a `GRAPH_TABLE`. 

  * `graph_pattern`: a graph pattern consisting of vertex and edge patterns together with search conditions. The pattern is matched against the graph to obtain a set of solutions. 

  * `graph_table_shape`: a `COLUMNS` clause that projects the solutions into a tabular form. 

A `FROM` clause in SQL may contain any number of `GRAPH_TABLE` operators as
well as other types of table expressions. This allows for joining data from
multiple graphs or for joining graph data with tabular, JSON, XML, or other
types of data.

Examples

Setting Up Sample Data

This example creates a property graph, `students_graph`, using `persons`,`
university`, `friendships`, and `students` as the underlying database tables
for the graph.

The following statements first create the necessary tables and fill them with
sample data:

    
    
    CREATE TABLE university (
        id NUMBER GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1),
        name VARCHAR2(10),
        CONSTRAINT u_pk PRIMARY KEY (id));
    INSERT INTO university (name) VALUES ('ABC');
    INSERT INTO university (name) VALUES ('XYZ');
    
    
    
    CREATE TABLE persons (
         person_id NUMBER GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT
         BY 1),
         name VARCHAR2(10),
         birthdate DATE,
         height FLOAT DEFAULT ON NULL 0,
         person_data JSON,
         CONSTRAINT person_pk PRIMARY KEY (person_id)
       );
    
    INSERT INTO persons (name, height, birthdate, person_data)
           VALUES ('John', 1.80, to_date('13/06/1963', 'DD/MM/YYYY'), '{"department":"IT","role":"Software Developer"}');
    
    INSERT INTO persons (name, height, birthdate, person_data)
           VALUES ('Mary', 1.65, to_date('25/09/1982', 'DD/MM/YYYY'), '{"department":"HR","role":"HR Manager"}');
    
    INSERT INTO persons (name, height, birthdate, person_data)
           VALUES ('Bob', 1.75, to_date('11/03/1966', 'DD/MM/YYYY'), '{"department":"IT","role":"Technical Consultant"}');
    
    INSERT INTO persons (name, height, birthdate, person_data)
           VALUES ('Alice', 1.70, to_date('01/02/1987', 'DD/MM/YYYY'), '{"department":"HR","role":"HR Assistant"}');
    
    
    CREATE TABLE students (
          s_id NUMBER GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1),
          s_univ_id NUMBER,
          s_person_id NUMBER,
          subject VARCHAR2(10),
          
          CONSTRAINT stud_pk PRIMARY KEY (s_id),
          CONSTRAINT stud_fk_person FOREIGN KEY (s_person_id) REFERENCES persons(person_id),
          CONSTRAINT stud_fk_univ FOREIGN KEY (s_univ_id) REFERENCES university(id)
        );
    
    
    INSERT INTO students(s_univ_id, s_person_id,subject, height) VALUES (1,1,'Arts');
    INSERT INTO students(s_univ_id, s_person_id,subject, height) VALUES (1,3,'Music');
    INSERT INTO students(s_univ_id, s_person_id,subject, height) VALUES (2,2,'Math');
    INSERT INTO students(s_univ_id, s_person_id,subject, height) VALUES (2,4,'Science');
    
    
    
    CREATE TABLE friendships (
        friendship_id NUMBER GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1),
        person_a NUMBER,
        person_b NUMBER,
        meeting_date DATE,
        CONSTRAINT fk_person_a_id FOREIGN KEY (person_a) REFERENCES persons(person_id),
        CONSTRAINT fk_person_b_id FOREIGN KEY (person_b) REFERENCES persons(person_id),
        CONSTRAINT fs_pk PRIMARY KEY (friendship_id)
    );
    
    INSERT INTO friendships (person_a, person_b, meeting_date) VALUES (1, 3, to_date('01/09/2000', 'DD/MM/YYYY'));
    INSERT INTO friendships (person_a, person_b, meeting_date) VALUES (2, 4, to_date('19/09/2000', 'DD/MM/YYYY'));
    INSERT INTO friendships (person_a, person_b, meeting_date) VALUES (2, 1, to_date('19/09/2000', 'DD/MM/YYYY'));
    INSERT INTO friendships (person_a, person_b, meeting_date) VALUES (3, 2, to_date('10/07/2001', 'DD/MM/YYYY'));
    

The following statement creates a graph on top of the tables:

    
    
    CREATE PROPERTY GRAPH students_graph
      VERTEX TABLES (
        persons KEY (person_id)
          LABEL person
            PROPERTIES (person_id, name, birthdate AS dob)
          LABEL person_ht
            PROPERTIES (height),
        university KEY (id)
      )
      EDGE TABLES (
        friendships AS friends
          KEY (friendship_id)
          SOURCE KEY (person_a) REFERENCES persons(person_id)
          DESTINATION KEY (person_b) REFERENCES persons(person_id)
          PROPERTIES (friendship_id, meeting_date),
        students AS student_of
          SOURCE KEY (s_person_id) REFERENCES persons(person_id)
          DESTINATION KEY (s_univ_id) REFERENCES university(id)
          PROPERTIES (subject)
      );

This creates the following graph:

  

![Description of student_graph.png
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/student_graph.png)  
[Description of the illustration
student_graph.png](img_text/student_graph.md)

  

Example: GRAPH_TABLE Query

The following query matches a pattern on graph `students_graph` to find
friends of a person named John:

    
    
    SELECT *
    FROM GRAPH_TABLE ( students_graph
      MATCH (a IS person) -[e IS friends]- (b IS person)
      WHERE a.name = 'John'
      COLUMNS (b.name)
    );
    

In the query:

  * `(a IS person)` is a vertex pattern that matches vertices labeled person and binds the solutions to a variable `a`. 

  * `-[e IS friends]-` is an edge pattern that matches either incoming or outgoing edges labeled friends and binds the solutions to a variable `e`. 

  * `(b IS person)` is another vertex pattern that matches vertices labeled person and binds the solutions to a variable `b`. 

  * `WHERE a.name = 'John'` is a search condition that accesses the property `name` from vertices bound to variable a to compare against the value `John`. 

  * `COLUMNS (b.name)` specifies to return the property `name` of vertex `b` as part of the output table. 

The output is:

    
    
    NAME
    ----------
    Mary
    Bob
    

See Also:

  * [SQL Property Graph](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SPGDG-GUID-B813BA1B-AEA0-4C70-8094-739FFC0E805B)

  * For property graph definitions and terminology , see [CREATE PROPERTY GRAPH](create-property-graph.md#GUID-37364ADB-E89C-4D92-A431-F2544FEDB218). 


[← Previous](data-quality-operators.md)

[Next →](graph-reference.md)
