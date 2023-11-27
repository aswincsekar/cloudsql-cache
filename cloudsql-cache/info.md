## cloudsql-cache

The service should read events from MySQL through the Debezium connector, transforms them into cache-compatible key-value pairs, and updates the cache accordingly. Along with this should provide observability measurements like latency, offset or delay and number of events pending processing.

We have 2 approaches one using PubSub and another using Kafka.

### PubSub Approach

We are going to use debezium server to get events from our database and send them to PubSub



### References

1. https://debezium.io/documentation/reference/stable/operations/debezium-server.html