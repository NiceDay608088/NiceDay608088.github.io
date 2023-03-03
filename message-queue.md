
# kafka

## core parameters

```
// heartbeat timeout between client and server
kafka.properties.session.timeout.ms = 25000
// frequency of sending heartbeat
kafka.properties.heartbeat.interval.ms = 3000
// records pulled per request
kafka.consumer.max-poll-records=20
// message processing timeout
kafka.properties.max.poll.interval.ms=60000
```

## rebalancing
Following cases will trigger kafka rebalaning

1. increase or decrease consumer / broker / partitions.
2. not receiving heartbeat in time. (heartbeat.interval.ms)
3. exceed processing time. (max.poll.interval.ms)
4. rebalancing only impact in consumer group.

## partiton vs consumer
1. One partition is only consumed by one consumer in a consumer group. In other words, Consumers in the same consumer group cannot consume the same partition.
2. Consumers from different consumer groups are able to consume the same partition.

