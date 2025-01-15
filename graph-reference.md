##  Graph Reference {#GUID-873488F0-58D1-4B9D-94B1-F4967B1785DD} 

Purpose 

Each GRAPH_TABLE starts with a graph reference that references the graph to perform the pattern matching on. 

Syntax 

*graph_reference* ::= 

  


![Description of graph_reference.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/graph_reference.gif)[ Description of the illustration graph_reference.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/graph_reference.md)

  


*graph_name* ::= 

  


![Description of graph_name.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/graph_name.gif)[ Description of the illustration graph_name.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/graph_name.md)

  


Semantics 

A graph name may be qualified with a schema name to allow for querying graphs created by other users. 

Example 1 

The following query counts the number of persons in the students_graph owned by user scott: 
    
    
    ```
    
    SELECT COUNT(*)
    FROM GRAPH_TABLE ( scott.students_graph
      MATCH (a IS person)
      COLUMNS (a.name)
    );
    ```

The output is: 
    
    
    ```
    
      COUNT(*)
    ----------
          4
    ```
