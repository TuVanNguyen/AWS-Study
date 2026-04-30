# Kafka

### What
* a stream processing platform [^1]

### Features
* publisher-subsciber pattern
    * producers publish events to Kafka topic at constant rate
    * any number of consumers can publish events to Kafka topic, and process those events
    * producers and consumers are decoupled, so they can act independently
* pull-based model
    * Retain messages for configurable amount of time, after consumers have retrieved the messages
    * 


## Compared To RabbitMQ

| | Kafka | RabbitMQ |
|-|-------|----------|
| Design | dumb broker, smart consumer[^2] | smart broker, dumb consumer |
| Message Retention | based on retention time set on the topic | None, messages removed as soon as they are consumed and acknowledged |
| Volume Impact on Performance| designed to store and stream large volume with little impact| as volume in queues increase, performance slows | 
| Performance | ~100,000 messages/second | ~20,000 messages/second; slows as volume increases |
| Scaling | horizontally: add more machines | vertically: add power to machines |
| Monitoring | Confluent, Datadog, etc | in-built |



### Dumb-Broker-Smart-Consumer vs Smart-Broker-Dumb-Consumer
* the dumb broker provides a message buffer, while smart consumers read from the buffer and track message consumption
    * consumption managed by consumers entirely
    * can configure consumers to read messages from the beginning or from a certain offset
* smart broker tracks consumer state, and the dumb consumers consume at roughly same pace
    * the broker supports routing rules that can get complex


[^1]: https://www.bigdatainrealworld.com/stream-processing-vs-message-processing-whats-the-difference/

[^2]: https://www.bigdatainrealworld.com/differences-between-rabbitmq-and-kafka/