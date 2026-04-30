# Simple Queue Service

### What is it?
* a message queue service

### Why do we use it?
* to queue messages from one service producing them, to another service consuming them
* the queue holds the messages until they are ready to be consumed
* helps decouple and remove dependencies between individual applications
    * for example, say lambda #1 needs to send messages to lambda #2 for further processing
    * if lambda #1 directly invokes lambda #2, then failures in lambda #1 can prevent lambda #2 from ever picking up those messages
        * lambda #1 could experience throttling issues or exceptions that result in data loss
        * it's also an issue if lambda #2 is slower than lambda #1, so stalls in lambda #2 would stall lambda #1
    * if instead lambda #1 sent the messages to an SQS queue, the two lambdas can process messages independently. One of them can fail, and the message would not be lost because it'd go back to the queue.



## Features
* pull-based: apps pull from the queue
* messages can have up to 256 KB of text in any format
* messages kept in queue up to 14 days

### Visibility Timeout
* amount of time that an application gets to process message from SQS queue
* if the message is not completely processed by the time the visibility timeout expires, then the message appears in the queue again to be reprocessed
* guarantees messages will be processed at least once
* default: 30 seconds
* max: 12 hours

## Types of Queues

### Standard Queues (Default)
* ordering: best effort
    * messages are generally delivered in the same order they were sent
    * occasionally because of the high throughput, may deliver duplicates of a message
    * occasionally because of the high throughput, some messages might be delivered out of order
* guarantees message is delivered at least once
* limit nearly unlimited TPS (transactions per second)


### FIFO queues
* ordering: first-in, first-out
    * strictly perserved
* exactly-once processing
    * each message is delivered once and remains available until a consumer processes and deletes it
    * no duplicates delivered
* limit: 300 TPS (transactions per second)

#### Use Cases
* bank transactions (can't afford to have transactions duplicated or out-of-order)


### SQS Delay Queues
* allows you to postpone delivery of messages to another queue for a few seconds
* those messages end up in the delay queue where they stay invisible to consumers during the delay period
* default delay: 0
* max delay: 900 seconds (15 minutes)
* For standard queues, only affects new messages arriving in queue
* For FIFO queues, also affects messages already in queue

#### Use Cases
* large distributed apps may need delay in processing
    * e.g online retailer wanting a delay of a few seconds so that their sales databases can update before sending out a confirmation on transaction to customers

## Settings

### Short Polling vs Long Polling

#### Short Polling
* returns response immediately even if message queue being polled is empty
* problem: can result in many empty responses while queue is empty (that you pay for)

#### Long Polling
* periodically polls queue
* only returns message after message arrives in queue or the long poll times out
* can save money, usually the preferable option


## Best Practices

### For large SQS messages: Use S3
* large SQS messages are over 256 KB, up to 2 GB
* use S3 to store messages
* You need
    * Amazon SQS extended client library for Java: allows you to specify when to store messages in S3
        * can send message which references a message object stored in S3
        * get and delete a message object from S3
    * AWS SDK for Java
