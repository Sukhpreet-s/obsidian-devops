- Manage ETL (extract, transform, and load) service
- serverless
- for data analytics

Convert data into Parquet format


Data Catalog: catalog of datasets
- Glue Data Crawler connected to S3, RDS, DynamoDB
- crawls and writes all the data to Glue Data Catalog
- then used by Glue Jobs to perform ETL
- Other services can use Data Catalog
	- Amazon Athena - data discovery
	- Redshift Spectrum
	- EMR 

Other features;
- Glue job bookmark - prevent re-processing old data
- Glue Elastic Views:
	- Combine and replicate data across multiple data stores using SQL
	- no code
	- creates virtual table
- Glue DataBrew - Clean and normalize data using pre-build transformations
- Glue Studio - GUI to create, run and monitor ETL jobs
- Glue Streaming ETL - read data using (streaming service, instead of running as batch job) Kinesis Data Streaming, Kafka, MSK