Dead Letter Queue 
- messages that are not read by consumer within the visibility timeout.
- The message keeps going back to the queue.
- Specify MaximumReceives Threshold, the message is sent to DLQ once threshold is met.
- messages in DLQ are useful for debugging

Redrive to Source
- After debugging the DLQ message and fixing the consumer
- The message can be sent back to the source queue to again sent to consumer.


SNS 
- New DLQ is created for each subscriber of the SNS with redrive policy