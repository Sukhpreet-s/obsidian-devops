- serverless query service using SQL language to query S3 bucket
- Used commonly with Quicksight to create dashboards

#### Performance Improvements
- Use columnar data
	- Apache parquet or ORC format is recommended.
	- Use Glue to convert to the desired format.
- Compress data for smaller retrievals
- Partition based on virtual columns (/year=1991/month=1/date=1)
- Use larger files to minimize overhead.


#### Federated Query
- Athena can query pretty much anywhere.
- Using the Data Source Connector (using lambda)