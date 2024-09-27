[Previous](CREATE-USER.md) [Next](CREATE-VIEW.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. CREATE VECTOR INDEX

## CREATE VECTOR INDEX

Purpose

Vector indexes speed up vector searches and are either exact search indexes or
approximate search indexes. An exact search gives 100% accuracy at the cost of
heavy compute resources. Approximate search indexes, also called vector
indexes, trade accuracy for performance.

Vectors are grouped or connected together based on similarity, where
similarity is determined by their relative distance to each other. Greedy
searches are done across these groups and connections to find the best,
closest match to the query vector being searched for. A search using a vector
index is called an approximate search.

There are two vector indexes supported in vector search: IVF (Inverted File)
Flat index and HNSW (Hierarchical Navigable Small Worlds) index. IVF Flat
(also simply called IVF) is a partitioned-based index, while HNSW is a graph-
based index. All partition based indexes are classifed as Neighbor Partition
Vector Index, and all graph-based indexes are classifed as In-Memory Neighbor
Graph Vector Index.

See Also:

[Create Vector Indexes](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=VECSE-GUID-8AF956F3-D951-4968-9B79-A6E180E87456) of the
AI Vector Search User's Guide

Syntax

  

![Description of create_vector_index.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_vector_index.gif)  
[Description of the illustration
create_vector_index.eps](img_text/create_vector_index.md)

  

([vector_index_organization_clause::=](create-vector-
index.md#GUID-B396C369-54BB-4098-A0DD-7C54B3A0D66F__SECTION_Q2G_2M3_QBC),[vector_index_parameters_clause::=](create-
vector-
index.md#GUID-B396C369-54BB-4098-A0DD-7C54B3A0D66F__SECTION_MYM_2M3_QBC),[vector_index_parameters_hnsw_clause::=](create-
vector-
index.md#GUID-B396C369-54BB-4098-A0DD-7C54B3A0D66F__SECTION_XJT_2M3_QBC),[vector_index_parameters_ivf_clause::=](create-
vector-
index.md#GUID-B396C369-54BB-4098-A0DD-7C54B3A0D66F__SECTION_OH1_FM3_QBC))

vector_index_organization_clause::=

  

![Description of vector_index_organization_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_index_organization_clause.gif)  
[Description of the illustration
vector_index_organization_clause.eps](img_text/vector_index_organization_clause.md)

  

vector_index_parameters_clause::=

  

![Description of vector_index_parameters_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_index_parameters_clause.gif)  
[Description of the illustration
vector_index_parameters_clause.eps](img_text/vector_index_parameters_clause.md)

  

vector_index_parameters_hnsw_clause::=

  

![Description of vector_index_parameters_hnsw_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_index_parameters_hnsw_clause.gif)  
[Description of the illustration
vector_index_parameters_hnsw_clause.eps](img_text/vector_index_parameters_hnsw_clause.md)

  

vector_index_parameters_ivf_clause::=

  

![Description of vector_index_parameters_ivf_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_index_parameters_ivf_clause.gif)  
[Description of the illustration
vector_index_parameters_ivf_clause.eps](img_text/vector_index_parameters_ivf_clause.md)

  

Semantics

vector_index_parameters_hnsw_clause

HNSW Specific Parameters

`NEIGHBORS` and `M` are equivalent and represent the maximum number of
neighbors a vector can have on any layer. The last vertex has one additional
flexibility that it can have up to 2M neighbors.

`EFCONSTRUCTION` represents the maximum number of closest vector candidates
considered at each step of the search during insertion.

The valid range for HNSW vector index parameters are:

  * `ACCURACY`: > 0 and <= 100 

  * `DISTANCE`: `EUCLIDEAN`, `L2_SQUARED` (aka `EUCLIDEAN_SQUARED`), `COSINE`, `DOT`, `MANHATTAN`, `HAMMING`

  * `TYPE` : `HNSW`

  * `NEIGHBORS`: >0 and <= 2048 

  * `EFCONSTRUCTION`: >0 and <= 65535 

vector_index_parameters_ivf_clause

IVF Parameters

`NEIGHBOR` `PARTITIONS` determines the number of centroid partitions that are
created by the index.

`SAMPLE_PER_PARTITION` decides the total number of vectors that are passed to
the clustering algorithm (number of samples per partition times the number of
neighbor partitions). Note, that passing all the vectors would significantly
increase the total time to create the index. Instead, aim to pass a subset of
vectors that can capture the data distribution.

`MIN_VECTORS_PER_PARTITION` represents the target minimum number of vectors
per partition. Aim to trim out any partition that can end up with fewer than
100 vectors. This may result in lesser number of centroids. Its values can
range from 0 (no trimming of centroids) to num_vectors (would result in 1
neighbor partition).

The valid range for IVF vector index parameters are:

  * `ACCURACY`: > 0 and <= 100 

  * `DISTANCE`: `EUCLIDEAN`, `L2_SQUARED` (aka `EUCLIDEAN_SQUARED`), `COSINE`, `DOT`, `MANHATTAN`, `HAMMING`

  * `TYPE` : `IVF`

  * `NEIGHBOR PARTITIONS`: >0 and <= 10000000 

  * `SAMPLE_PER_PARTITION`: from 1 to (num_vectors/neighbor_partitions) 

  * `MIN_VECTORS_PER_PARTITION`: from 0 (no trimming of centroid partitions) to total number of vectors (would result in 1 centroid partition) 

Examples

    
    
    CREATE VECTOR INDEX galaxies_hnsw_idx ON galaxies (embedding) ORGANIZATION INMEMORY NEIGHBOR GRAPH
    DISTANCE COSINE
    WITH TARGET ACCURACY 95;
    
    
    
    
    CREATE VECTOR INDEX galaxies_hnsw_idx ON galaxies (embedding) ORGANIZATION INMEMORY NEIGHBOR GRAPH
    DISTANCE COSINE
    WITH TARGET ACCURACY 90 PARAMETERS (type HNSW, neighbors 40, efconstruction 500);
    
    
    CREATE VECTOR INDEX galaxies_ivf_idx ON galaxies (embedding) ORGANIZATION NEIGHBOR PARTITIONS
    DISTANCE COSINE
    WITH TARGET ACCURACY 95;
    
    
    
    CREATE VECTOR INDEX galaxies_ivf_idx ON galaxies (embedding) ORGANIZATION NEIGHBOR PARTITIONS
    DISTANCE COSINE
    WITH TARGET ACCURACY 90 PARAMETERS (type IVF, neighbor partitions 10);
    


[← Previous](CREATE-USER.md)

[Next →](CREATE-VIEW.md)
