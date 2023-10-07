- Use to collect, process, and analyze real-time data stream.
- Example: Application logs, Metrics, Website clickstreams, IoT telemetry data
- Four services:
	- Kinesis Data Streams: collect, process, analyze
	- Kinesis Data Firehose: load streams in AWS data stores or external as well.
	- Kinesis Data Analytics: analyze data streams with SQL or Apache Flink
	- Kinesis Video Streams: capture, process and store video streams.
- It is Producers and Consumers Model
- Data Streams can be accessed using VPC Endpoints by EC2 instances in private subnets
- Monitor API calls using CloudTrail

#### Pricing Models
- Provisioned Mode
- On-demand Mode


#### Consumer Scaling Architecture
- Use CloudWatch Metric `GetRecords.IteratorAgeMilliseconds`
	- The different between current time and when last record was read
- Setup CloudWatch Alarm on this metric
	- if `IteratorAgeMilliseconds` is > 5 minutes, 
- Trigger ASG scale out event

## Kinesis Firehose
- To load streaming data into S3/Redshift/OpenSearch/3rd party/Custom HTTP
- Fully managed
- Near real-time - Data is sent in batched to the destinations
- Can use Lambda for data transformation before sending to destinations
- No data storage (doesn't support replay ability)


### Kinesis Data Analytics

#### For SQL
Sources: Data Stream, Data Firehose
Use SQL statements to perform analytics
Also, can reference data from S3
Output: 
- Data Stream
- Data Firehose
Use Cases:
- Time series analytics
- Real-time dashboard
- Real-time metrics

#### For Apache Flink (Renamed to Amanzon Managed Service for Apache Flink)
Sources: Data Streams, Amazon MSK (Kafka)
Run Apache Flink application on managed cluster on AWS


### Machine Learning on Kinesis Data Analytics
- RANDOM_CUT_FOREST
- HOTSPOTS



