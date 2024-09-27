[Previous](Comments.md) [Next](Database-Object-Names-and-Qualifiers.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Basic Elements of Oracle SQL](Basic-Elements-of-Oracle-SQL.md)
  3. Database Objects

## Database Objects

Oracle Database recognizes objects that are associated with a particular
schema and objects that are not associated with any particular schema, as
described in the sections that follow.

### Schema Objects

A schema is a collection of logical structures of data, or schema objects. A
schema is owned by a database user and has the same name as that user. Each
user owns a single schema. Schema objects can be created and manipulated with
SQL and include the following types of objects:

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

### Nonschema Objects

Other types of objects are also stored in the database and can be created and
manipulated with SQL but are not contained in a schema:

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

In this reference, each type of object is described in the section devoted to
the statement that creates the database object. These statements begin with
the keyword `CREATE`. For example, for the definition of a cluster, see
[CREATE CLUSTER](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7).

See Also:

[Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=CNCPT010) for an overview of database objects

You must provide names for most types of database objects when you create
them. These names must follow the rules listed in the sections that follow.


[← Previous](Database-Objects.md)

[Next →](Database-Object-Names-and-Qualifiers.md)
