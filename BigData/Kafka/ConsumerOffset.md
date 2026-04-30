# Consumer Offset

### What is it?
* a value that tracks the messages consumed by consumers in a consumer group [^1]
* applies to a partition within a topic, from which a consumer reads data

### How it works
* Consumer offsets starts at index 0
* total_messages_read_by_consumer = consumer_offset + 1
    * e.g consumer_offset = 9; total_messages_read_by_consumer = 10

### Why do we have it?
* avoid consuming the same messages again by tracking which messages were already consumed
    * especially useful if the consumer group goes down and back up, and now needs to pick off where it left off

### How to implement
* For Kafka version >= 0.9, store offsets in Kafka brokers


## Reset Consumer Offset

### Why?
* sometimes consumers may have errors when consuming a message from Kafka, and the messages need to be reconsumed because they were incompletely processed [^2]

### Options

#### --shift-by

Increments the offset position.
```
kafka-consumer-groups.sh --bootstrap-server kafka-host:9092 --group my-group --reset-offsets --shift-by 10 
--topic sales_topic --execute
```

#### --to-datetime
Reset the offset to what it was at specified datetime
```
kafka-consumer-groups.sh --bootstrap-server kafka-host:9092 --group my-group --reset-offsets
--to-datetime 2020-11-01T00:00:00Z --topic sales_topic --execute
```

#### --to-earliest
Reset offset to oldest offset available in the topic

```
kafka-consumer-groups.sh --bootstrap-server kafka-host:9092 --group my-group --reset-offsets --to-earliest 
--topic sales_topic --execute
```

#### to-latest
Reset offsets to most recent offset in the topic

```
kafka-consumer-groups.sh --bootstrap-server kafka-host:9092 --group my-group --reset-offsets --to-latest 
--topic sales_topic --execute
```


[^1]: https://www.bigdatainrealworld.com/what-is-consumer-offset-and-the-purpose-of-consumer-offset-in-kafka/

[^2]: https://www.bigdatainrealworld.com/how-to-change-or-reset-consumer-offset-in-kafka/