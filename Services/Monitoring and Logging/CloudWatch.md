## Metrics
Metrics are available for all the services

### Streams
- Send metrics data to Kinesis Data Firehose or 3rd party service provider like Datadog, Splunk

### Custom Metrics


### Logs Metric Filter
- Create a filter using a pattern on logs.
- Track the filter metric in CloudWatch Dashboard.
- Set up alarm based on the metric

### Types of Logs

- Application logs
	- Usually streamed using CloudWatch Agent from EC2.
	- ECS, Fargate, Lambda, Beanstalk have direct integration with CloudWatch logs.
- Operating system logs
	- Usually streamed to CloudWatch using CloudWatch Agent.
- Access logs
	- list of requests being made
	- usually for load balancer, proxies, web servers


### Alarms
- set alarms based on CloudWatch metric (only one)
- Composite Alarm can be set up with multiple other alarms, by chaining with AND and OR conditions.


### Synthetics Canary

- scripts to monitor your API, URL, websites
- scripts produce the same dummy activities as customers to check everything is loading and working as expected.
- checks availability and latency of the endpoints. Store load time data and screenshots of the UI.
- integrate with Alarms
- Scripts written in Node.js or Python
- Some blueprint available 

##### Canary Recorder (used with Synthetic Recorder)
- record your actions on a website. and automatically create a script to run it automatically.