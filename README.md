#### Getting started
To get started make sure you have sbt installed on your system.

#### Prerequisites
* Kafka.

* Apache Cassandra.
  
#### For running the Trailblazer application:

* Start the Zookeeper server.

* Start the Kafka brokers.

* Start Cassandra DB.

* Create a topic.
```
> bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic <TopicName>
```

**TopicName:** Provide the name of the topic you want to create.  
The default topic name set by the application is **_"temperature"_**.
* Start a console producer
```
> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <TopicName>
```

* Produce some messages, format should be like below:
```
> { "device-id": <String>, "timestamp": <String>, "temperature": <Double> }
```
  
#### Example:
```
> { "device-id": "0x0132", "timestamp": "2018-08-31T21:33:56Z", "temperature": 40.2 }
```

* Export the topic name explicitly in case default topic name is not used, use the following command:<br>
```
export TOPIC_NAME=<TopicName>
```

* Start the application using the following command:
```
sbt runAll
```
* To get the data, invoke the route by providing the timestamp value in Long:
```
https://localhost:9000/api/temperature/time/:timestamp
```
  
#### Example:
```
https://localhost:9000/api/temperature/time/1499070300000
```  
  
* Sample Response
```
  {
    "device-id": "0x0132",
    "timestamp": "2018-08-31T21:33:56Z",
    "temperature": 27.2
  }
```
