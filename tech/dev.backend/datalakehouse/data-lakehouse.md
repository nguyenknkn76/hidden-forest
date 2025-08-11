# Datalake ,Data Warehouse, and Lakehouse

## Data Warehouse

- work with structured data (**schema-on-write** ~ clean data before put it to dbms) 
- etl process (extract - transform - load)
  - extract
  - transform: raw data -> staging area (do something here)
  - load: load to data warehouse 
- 2 architecture types: top-down, bottom-up
```sql
+----------------------------+
|      Data Sources          |
| (ERP, CRM, Apps, APIs)     |
+------------+---------------+
             |
     ETL/ELT Pipeline
             |
             v
+----------------------------+
|      Data Warehouse        |
| (Schema-on-Write)          |
| Optimized for Analytics    |
+------------+---------------+
             |
             v
+----------------------------+
|  BI Tools (Tableau, PowerBI)|
+----------------------------+
```

## Datalake

- Schama-on-read
- elt process (extract - load - transform)
- tech stack base: 
  - old: Hadoop (HDFS) and MapReduce/Spark
  - new: cloud obj storage (Amazon S3, GGC Storage)
- data swarmp issues

```sql
+------------------------------+
|        Data Sources          |
|  (IoT, Logs, DB dumps, API)  |
+--------------+---------------+
               |
               v
+------------------------------+
|          Data Lake           |
| (HDFS, S3, Azure Blob, GCS)  |
|  Raw / Semi-structured /     |
|  Unstructured Data           |
+--------------+---------------+
               |
               v
+------------------------------+
|   Processing Layer           |
| (Spark, Hive, Presto, etc.)  |
+------------------------------+
```

## Data Lakehouse

- core tech: 
  - property: datalake + metadata layer
  - open table format 
- Medadallion architecture (bronze, silver, gold)
- Decoupling of storage and compute 

```sql
+----------------------------+
|      Data Sources          |
+------------+---------------+
             |
             v
+----------------------------+
|     Data Lakehouse         |
| (Delta Lake, Iceberg, Hudi)|
| Unified Storage + ACID     |
| Supports BI + ML           |
+------------+---------------+
             |
        Query Layer
   (SparkSQL, BI tools)
```

> NOTE:
> + keyword: BI tools, 
