##  Database Objects {#GUID-31BE00A7-7FF9-41CB-852A-F1416912CA9E} 

Oracle Database recognizes objects that are associated with a particular schema and objects that are not associated with any particular schema, as described in the sections that follow. 

###  Schema Objects {#GUID-1B1818AD-6A70-4C2A-8E86-98BECA723FB8} 

A  schema  is a collection of logical structures of data, or schema objects. A schema is owned by a database user and has the same name as that user. Each user owns a single schema. Schema objects can be created and manipulated with SQL and include the following types of objects: 

  * Analytic views 
  * Attribute dimensions 
  * Clusters 
  * Constraints 
  * Database links 
  * Database triggers 
  * Dimensions 
  * External procedure libraries 
  * Hierarchies 
  * Index-organized tables 
  * Indexes 
  * Indextypes 
  * Java classes 
  * Java resources 
  * Java sources 
  * Join groups 
  * Materialized views 
  * Materialized view logs 
  * Mining models 
  * Object tables 
  * Object types 
  * Object views 
  * Operators 
  * Packages 
  * Property Graphs 
  * Sequences 
  * Stored functions 
  * Stored procedures 
  * Synonyms 
  * Tables 
  * Views 
  * Zone maps 



###  Nonschema Objects {#GUID-A0B5BD29-5D01-4946-B19E-D7EC89AC6F65} 

Other types of objects are also stored in the database and can be created and manipulated with SQL but are not contained in a schema: 

  * Contexts 
  * Directories 
  * Editions 
  * Flashback archives 
  * Lockdown profiles 
  * Profiles 
  * Restore points 
  * Roles 
  * Rollback segments 
  * Tablespaces 
  * Tablespace sets 
  * Unified audit policies 
  * Users 



In this reference, each type of object is described in the section devoted to the statement that creates the database object. These statements begin with the keyword ` CREATE ` . For example, for the definition of a cluster, see [ CREATE CLUSTER ](CREATE-CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7) . 

> **note:** See Also: 

[ *Oracle Database Concepts*  ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT010) for an overview of database objects 

You must provide names for most types of database objects when you create them. These names must follow the rules listed in the sections that follow. 
