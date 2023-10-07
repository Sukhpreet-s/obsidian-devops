Cron jobs (scheduled scripts)


Rules:
- Source - Triggers an event recorded by EventBridge
- Middleware (EventBridge)
- Destination - EventBridge sends the event response to the output service like Lambda, EC2 ....

#### Rule
- Define rule by defining event pattern, and targets

##### Event filtering
- While creating rules, able to define wildcard filtering for event schema

##### Input Transformer
- While defining the event target, can also define transformation of the event output. 
- Can specify which specific fields to use and how to organize before sending the output

Default Event Bus - Events triggered by AWS Services
Partner Event Bus - Events triggred by AWS SaaS Partners outside of AWS
Custom Event Bus

Able to archive events to replay later. Example: to replay a bug for testing purposes.


##### Schema Registry

##### Resource Based Policy
Allow multiple accounts/regions to send events to one Event Bus in EventBridge.