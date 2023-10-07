- Audit, governance and compliance for your account
- history of events/API calls made within your account (logs)
- A trail can be applied to All Regions (default) or single Region.
- can send logs to CW logs or S3

Management Events
- Operations performed on AWS resources
- Example: configuring security, routing data, setting up logging
- by default these are logged.
- can separate read from write events
Data Events
- S3 object level active (put, delete, modify)
- by default not logged (high volume events)
CloudTrail Insights Events
- detects unusual activities
- analyzes normal management to create baseline and then analyze write type of events to detect anomalies
- events can be sent to S3 or EventBridge.

Event Retention
- default 90 days
- log to S3 for long-term retention and use Athena to analyze

EventBridge Integration
- All CloudTrail events are sent to EventBridge