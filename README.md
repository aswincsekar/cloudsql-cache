# cloudsql-cache

We want to build caching mechanism that takes change data stream from cloudsql databases and stores it in a cache like redis or memcache for later use. Some of the major goals of this project to learn how to implement this pipeline for cloudsql database and how to do this very efficiently and in a scalable manner that can process millions of events every hour.

## Goals

- Should be very efficient
- Should be very cost effective
- Should be highly scalable
- Should be robust to faults in the system


## More on this

We want the cache to be co-located within the vpc as our service to target sub millisecond latency. the service will check on the cache and if the required data is not present then will use other data sources like a db call, whether it should set the cache at that point is up for discussion, we can test both ways

The service should read events from MySQL through the Debezium connector, transforms them into cache-compatible key-value pairs, and updates the cache accordingly. Along with this should provide observability measurements like latency, offset or delay and number of events pending processing.

1. we will be getting change events from DB with the entire row information only filtered for the tables that we want
   1. Debezium
   2. GCP data stream - doesnt not support pubsub or kafka as a destination
2. we can publish to a ordered message queue or event store
   1. pubsub
   2. kafka
3. process the events in the queue by setting the cache
   1. redis
   2. memcache
4. on the service check against the cache and if not present connect to the db and get the value and set the cache
   1. go based service for high concurrency


References:

1. https://debezium.io/documentation/reference/stable/tutorial.html
2. https://debezium.io/documentation/reference/stable/operations/debezium-server.html

Info from debezium

Debezium provides a ready-to-use application that streams change events from a source database to messaging infrastructure like Amazon Kinesis, Google Cloud Pub/Sub, Apache Pulsar, Redis (Stream), or NATS JetStream. For streaming change events to Apache Kafka, it is recommended to deploy the Debezium connectors via Kafka Connect.