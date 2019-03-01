# Google Cloud BigQuery

[https://cloud.google.com/bigquery/](https://cloud.google.com/bigquery/)



<https://static.googleusercontent.com/media/research.google.com/de//pubs/archive/36632.pdf>
<https://bigquery.cloud.google.com>



Because BigData is clusters-less, the dataset can be shared with anybody with the same companies domain.
When they want to do a query they can. BigQuery enables data collaboration in the company. Queries can be shared.

- BigQuery is a Data Warehouse Service (OLAP)
- BigQuery is a columnar database
- Cant not be used for transaction processing (OLTP)
- BigQuery has a bit higher latency than BigTable
- BigQuery is a Query Engine that separates storage from compute
- It allows us to query large datasets in seconds
- Open BigQuery from a Web browser with an interactive Data Exploration Interface
- Capture and Analyze Data in Real-time
- Analyze Petabytes of Data in Minutes or Seconds
  (in real-time)
- <https://bigquery.cloud.google.com/>
- An interactive way to analyze Petabytes of Data in Queries are in Standard SQL
- No machines or clusters required
- Near-real-time analysis 
- No-ops
  - No cluster managing required
  - Just run the query
- Durable (replicated), inexpensive storage:
  - The data is replicated in multiple places. You know every time a query runs. 
- Immutable audit logs
  - It is visible when someone uses the dataset
- Queries can be shared, a way of collaboration 
- Query very large datasets in seconds
- Interactive ad-hoc analysis of petabyte-scale databases
- Familiar SQL 2011 query language
- Many ways to ingest, transform, load, export data to/from BigQuery
- Nested and repeated fields, user-defined functions in JavaScript
- Is using Epoch time, returns values based on the UTC time zone 

## Similar to Similar to Hive

## Ressources

https://cloud.google.com/biggquery/docs

https://cloud.google.com/biggquery/docs/tutorials

https://cloud.google.com/biggquery/pricing

https://cloud.google.com/biggquery/client-libraries



## Pricing and performance

- We pay for the amount of data that we process
- Pay for use
- Google offers a flat rate plan for Big Query
- If you want to save money limit the columns where you want to run queries on
  - we are charged for the columns where our query runs
- To pay less we can optimize queries
  - Less work → Faster query
  - What defines work?
    - I/O bytes that get read
    - Shuffle -  How many bytes are pass to the next stage
    - Materialization - How many bytes did you write
    - CPU work - For example for user-defined functions
  - Done project unnecessary columns
    - They waste I/O and materialization
  - Filter early and often with where clauses
  - Do biggest joins first and smaller joins later
  - Build-in functions are faster than JavaScript UDFs
    - Use JavaScript UDFs only as last option
  - Table partitioning is a cost-effective way to manage data

## How is BigQuery storage its data?

- Big queries storage is columnar
- Each column in separate compressed encrypted files
- Replicated 3+ times
- No indexes, no keys no partitions required

## Pricing Categories

- Storage

  - Amount of data in a table
  - Ingest range of streaming data
  - Automatic discount for old data????

- Processing

  - On-demand OR Flat-rate plans
  - On-demand based on the amount of data processed
  - 1 TB/ month free

- Free

  - Loading
  - Exporting
  - Queries on metadata
  - Cached queries
  - Queries with errors

  

## What is a Dataset?

- A dataset is a collection of tables
- A dataset consists of multiple tables
- A dataset contains views
- Datasets can define access control
  - On a dataset basis not on a table basis



## What is a table?

- A table is a collection of columns
- Views are virtual tables
- BigQuery can work with tables that are external
  - cause BigQuery separates its storage from its computation



## What are views?

- Views can be used to restrict control to the dataset 
- A view is a select (specific rows and columns can be selected)
- This views can be used in other datasets



## User-defined functions

- Allow SQL queries to use programming logic
- Allow functionality not supported by standard SQL
  - Loops
- User-defined functions are written in SQL or JavaScript
- User-defined functions are temporary for the current query
- User-defined functions output is limited to <= 5MB
- 6 concurrent JavaScript UDF queries per project are allowed
- A query can have up to 50 UDF



## What is a job?

- A job is working on a dataset
- It is potential long-running



## BigQuery Data Types

- String

- Int

- Float

- Bool

- Array

- Struct

  - Container or ordered fields

- Timestamp

  

## Loading data into BigQuery

- BigQuery is the end of many roads in GCP
- Loading data into BigQuery can be done via
  - CLI (gsutil)
  - WebUI
  - API
  - Load a CSV file into a BigQuery table using the web UI
  - Load a JSON file into a BigQuery table using the CLI
- The following formats are supported
  - CSV
  - JSON
  - AVRO
- Files on disk or Cloud Storage
- Stream Data
- Federated Datasource



## Queries in BigData

- [bigquery.cloud.google.com](http://bigquery.cloud.google.com)
- [cloud.google.com/bigquery/query-reference](http://cloud.google.com/bigquery/query-reference)
- To run a query we can use the web console
- If you want to use standard SQL we have to turn off the google SQL with Show Options
- Save to Google Sheets
  - Results can be downloaded (Export)
  - CSV
  - JSON
  - Save it as table
- Subqueries can be used
- Validate
  - With the validate button we can validate the query an can get an idea of our costs
- Explanation
  - is a way to analyze query performance



## BigQuery and Dataproc together

Can be combined together with Dataproc, output results from Dataproc to BigQuery to get benefits of interactive analysis.
Dataproc clusters are pre-installed with the Cloud Storage Connector.



## Sample Use Case

- Read Data from BigQuery
- Process it in Spark on Dataproc
- Return the Results to BigQuery

### Solution

1. Setup a BigQuery Connector on the Dataproc Cluster
   - The BigQuery Data is imported as RDD
   - The Connector is a Java Library with read/write access
2. Process Data in Memory for Speed with the usage of Pandas Dataframes
   1. Load Big Query Data into a Pandas Dataframe
      (The Data is in memory, keep in mind it is limited in Size)



## Open topics

### Nested and repeated fields



### UDF's

