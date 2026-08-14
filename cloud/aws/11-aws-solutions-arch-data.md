# AWS Data & Analytics

- [AWS Data \& Analytics](#aws-data--analytics)
  - [AWS Athena](#aws-athena)
    - [Performance](#performance)
  - [Redshift](#redshift)
    - [Redshift spectrum](#redshift-spectrum)
  - [OpenSearch](#opensearch)
  - [EMR](#emr)
  - [QuickSight](#quicksight)
  - [Glue](#glue)
  - [Lake formation](#lake-formation)
  - [Amazon managed services for Apache Flink](#amazon-managed-services-for-apache-flink)
  - [MSK: Managed Streaming for Apache Kafka](#msk-managed-streaming-for-apache-kafka)


## AWS Athena
Serverless query service to analyze S3 buckets. It uses SQL (via Presto).
Used in combination with Amazon Quicksight to create reports/dashboards.
Fix amount per TB scanned. 

### Performance
Use columnar data type & compress data for cost-savings (Apache parquet or ORC, use Glue to convert it).

Partition datasets for easy querying.

Use large files to minimize overhead (>128 MB).

Using a federeated query you can run SQl across al data stored (even on-premises) using a Data source connector (running in a Lambda).

## Redshift
Based on PostgreSQL for analytics and data warehousing with scalability to PB of data.

* Direct integrated with Amazon quicksight or Tableau.
* Columnar storage of data & paralel query engine.
* Provisioned or serverless cluster modes.
* Leader node for query planning + compute node for work the queries.
* There is a multiAZ mode for some cluster modes.
* Snapshots are stored in S3, which are incremental ways. (every 8 hours / 5 GB)
* Snapshots can be copied to another AWS region.

Data can be inserted from Kinesis Data firehose, from an S3 bucket or using the JDBC driver from an EC2 instance(batches).

### Redshift spectrum
Query data without loading from an S3 using an already instanciated redshift cluster.

## OpenSearch
You can search any field, even for partially matches. Use as complement to another DBs. Via plugin can enable SQL support. Comes with visualization dashboards.

Also has managed cluster or serverless cluster.

Integration with cognito, IAM & integration.

## EMR
Elastic MapReduce. Creates Hadoop cluster (Big Data) to analyze & process.

Used for machine learging & Apache spark, HBase, Presto, Flink.

Master + Core node + Task node (optional) to build a long-running cluster or transient(tmp) cluster

On-demand, reserved & spot-instances(for task nodes) available for this service. 

## QuickSight
Serverless machine powered BI to create interactive dashboards connected to datasources(RDS, Aurora, RedShift, S3, data sources(csv, json, etc) or 3rd party sources or on-premises DBs w/ JDBC).

It uses SPICE (in-memory computation engine) is used if the data is imported.
Enterprise edition has CLS(column-level security).

## Glue
Managed service for Extract, transdor and load (ETL) service. Fully serverless.

Using AWS Glue data crawler is used to crete a Data Catalog.

* Job bookmarks: prevent re-processing old data.
* DataBrew: Clean & normalize data.
* Studio: GUI to create, run & monitor jobs.
* Straming ETL: Use streaming compatible with kinesis.

## Lake formation
Central place to have all you data for analytics purposes. It handels discover, cleanse, transforms and ingest data into a data lake stored in S3. Is built on top of AWS glue.

* Combined structured & un-structred data in the lake.
* Out-of-the-box blueprints.
* fine-grained access control.
* centralized permissions for access control at row & column-level security.

Athena, Redshift, EMR can be used the data lake information.

## Amazon managed services for Apache Flink
Apache Flink is used for processing data streams in real-time. It allows to run any apache Flink application on a managed AWS cluster.

It can read data from Kinesis Data streams or MSK.
Cannot read from Amazon Data firehose.

## MSK: Managed Streaming for Apache Kafka
Alternative to Amazon Kinesis. Deply Kafka in one-click. It requires a MSK consumer, which can be Lambda functions, AWS Glue, Apache Flink or a custom application.

Can be serverless!

