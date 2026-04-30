# SNS: Simple Notification Service

### Used for
* Send messages from application to subscribers
    * e.g push notifications to devices like Apple, Google, Windows, Android
    * SMS text message and email
    * trigger lambda, which could also publish to another SNS topic

### How SNS works
* **Publish and Subscribe Model**: applications *publish* messages to a topic, consumers **subscribe** and receive message from topic

### How it differs from SQS
* SNS is push based, SQS is pulled based
    * SQS queue holds the messages in a queue until a consumer pulls it from the queue (e.g a lambda trigger)
    * SNS immediately forwards messages to a topic from which it then goes to the consumer

