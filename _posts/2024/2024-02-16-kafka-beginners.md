---
layout: post
title:  "Kafka - Beginners"
date:   2024-02-16
categories: infra
permalink: /:categories/kafka-beginners
---


<p style="text-align: justify;">This post is based on this kafka course <a href="https://www.udemy.com/course/apache-kafka/">[Kafka for Beginners]</a>. Here is exposed some concepts to help the first understanding and a fast consult.</p>

<p style="text-align: justify;">Here are simple examples of using Kafka for the first time. To have some practices you can read: <a href="https://www.conduktor.io/kafka/kafka-cli-tutorial/">[Conduktor - Tutorial]</a>; <a href="https://www.conduktor.io/get-started/">[Conduktor - get-started]</a>; <a href="https://kafka.apache.org/quickstart">[Apache Kafka - quickstart]</a>. Here <a href="https://upstash.com/">[Upstash - Kafka playground]</a> is a platform where you can create your playground for your tests.</p>

<p style="text-align: justify;"><b><u>Start kafka locally</u></b></p>
{% highlight ruby %}
$ zookeeper-server-start /opt/homebrew/Cellar/kafka/3.6.1/libexec/config/zookeeper.properties
$ kafka-server-start /opt/homebrew/Cellar/kafka/3.6.1/libexec/config/server.properties
{% endhighlight %}


<br />
<h2>Introduction</h2>

<p style="text-align: justify;">Here is the scenario where kafka can fit: </p>
<ul>
  <li><b>Problem: </b>Integration among multiple sources and targets</li>
  <li><b>Difficulties: </b>Protocol, Data format, data schema and evolution</li>
  <li><b>Solution: </b>Kafka decoupling data stream and systems. Kafka works as a data integration layer. 
    <ul>
      <li>High performance, scalable, elastic, distributed, resilient, fault tolerant</li>
      <li>Used as a transportation machanism</li>
      <li>Capabilities: publish/subscribe streams of events; store streams of events; process streams of events</li>
    </ul>
  </li>
</ul>

<blockquote>Kafka is an open-source distributed event streaming platform consisting of servers and clients. Event streaming is the practice of capturing data in real-time from event sources. Apache Kafka is used primarily to build real-time data streaming pipelines.  <a href="https://www.conduktor.io/kafka/what-is-apache-kafka/">[Conduktor]</a><a href="https://kafka.apache.org/">[Apache Kafka]</a></blockquote>


<br />
<h2>Fundamentals</h2>

<p style="text-align: justify;"><em>The fundamentals concepts was collected from <a href="https://www.conduktor.io/kafka/what-is-apache-kafka/#Part-2:-Definition-of-Core-Apache-Kafka-Concepts-9">[1]</a><a href="https://www.conduktor.io/kafka/kafka-fundamentals/">[2]</a></em></p>

<p style="text-align: justify;"><u><b>Event</b></u><br />
Fact that happened in the business and recorded (read/write) in Kafka. An event has key, value (message content), timestamp, metadata, compression type, headers, partition and offset.</p>

<p style="text-align: justify;"><u><b>Broker</b></u></p>
<ul>
  <li>It is a kafka server</li>
  <li>A set of these servers form the storage layer</li>
  <li>Each broker is identified with its ID</li>
</ul>  

<p style="text-align: justify;"><u><b>Kafka cluster</b></u></p>
<ul>
  <li>It is a set of brokers (servers) working together</li>
  <li>Data is distributed across all brokers</li>
  <li>A client can connect to any broker in the cluster </li>
  <li>Every broker in the cluster has information (metadata) about all the other brokers, topics and partition</li>
  <li><b>Bootstrap Server:</b> the broker in the cluster</li>
  <li>The metadata returned from bootstrap server to the clinent make possible them to know which broker to connect</li>
</ul>

<p style="text-align: justify;"><u><b>Kafka Connect</b></u><br />
Import and export data as event streams to integrate Kafka with your existing systems and other Kafka clusters <a href="https://www.confluent.io/product/connectors/">[Connectors]</a></p>


<p style="text-align: justify;"><u><b>Topics</b></u></p>
<ul>
  <li>Store the events in the broker like a directory</li>
  <li>A topic is identidied by the name <a href="https://cnr.sh/essays/how-paint-bike-shed-kafka-topic-naming-conventions">[Convention]</a></li>
  <li>A kafka cluster can have many topics</li>
  <li>It acepts any kind of message format</li>
  <li>You cannot query topics</li>
  <li>Kafka topics are immutable. It's not possible change or delete data in kafka. The message is discarted by setting the configuration per-topic</li>
  <li>It is different of RabbitMQ and ActiveMQ that use queues which scale to millions of consumers and allow delete messages once processed</li>
</ul>

<p style="text-align: justify;"><u><b>Partitions: </b></u></p>
<ul>
  <li>A topic can be split in particions located on different Kafka brokers</li>
  <li>Each topic-partition receives its own sub-directory with the associated name of the topic</li>
  <li>Each broker contains a topic partition</li>
  <li><b>Offset:</b> incremental id given to messages inside the partition as it is written into a partition
    <ul>
      <li>It represent the position of a message within a Kafka Partition</li>
      <li>Messages within partition are ordered by the offset</li>
      <li>Offset of different partitions have no relation</li>
      <li>No garantee of order among the partitions</li>
      <li>Offsets are commited as soon as messages are received (consumed)</li>
      <li>Offsets are not re-used</li>
    </ul>
  </li>
  <li>A data is assigned randomly to a partition (round robin) unless a key is provided (hash strategy)</li>
  <li>Message with the same key goes to the same partition</li>
  <li>Each partition can have multiple reader</li>
  <li><b>Leader of partition:</b> only one broker can be a leader for a partition</li>
  <li><b>Kafka partitionerM:</b> logic to decide which partition to send a record</li>
</ul>

<p style="text-align: justify;"><u><b>Topic replication factor</b></u></p>
<ul>
  <li>Copy of the data across the brokers </li>
  <li>Specified at topic creation time</li>
  <li>It is done at the level of topic-partitions</li>
  <li>A replication factor of 1 means no replication (development purposes)</li>
  <li>Topics should have replication factor > 1 (localhost is only 1 but it is development purpose) </li> 
  <li>Common replication factor: 3 (good balance between broker loss and replication overhead)</li>
  <li><b>In-Sync Replicas (ISR):</b> replica is up to date with the leader broker for a partition</li>
</ul>
<br />
{% highlight ruby %}
// If try to create a topic that not exist, we will see a WARNING and the topic is created
// By default, the topic is created with 1 partition and 1 replication factor
// You cannot create replication factor higher than the number of broker. Then, localhost can only be created with replication 1

// local
$ kafka-topics --bootstrap-server localhost:9092 --create --topic first_topic 

// remote
$ kafka-topics --command-config playground.config --bootstrap-server HOST_URL:9092 --create --topic first_topic --partitions 3 --replication-factor 2

$ kafka-topics --bootstrap-server localhost:9092 --list
$ kafka-topics --command-config playground.config --bootstrap-server HOST_URL:9092 --list  

$ kafka-topics --bootstrap-server localhost:9092 --topic first_topic --describe
$ kafka-topics --command-config playground.config --bootstrap-server HOST_URL:9092 --topic first_topic --describe

$ kafka-topics --command-config playground.config --bootstrap-server HOST_URL:9092 --topic second_topic --delete
{% endhighlight %}

<p style="text-align: justify;"><u><b>Producers</b></u></p>
<ul>
  <li>Client applications that publish (write) events to Kafka</li>
  <li>The producers know in advance which particion to write to and which kafka broker</li>
  <li>Transform object to byte before send to kafka</li>
  <li>Kafka producers only write data to the current leader broker for a partition</li>
  <li>Retry: in case of failures it can retry (default 100ms). In this case, the message can be sent out of order</li>
  <li><b>Idempotent:</b> even the message have been sent more than once, kafka will not have duplicate commits (messages)</li>
  <li><b>Acknowledgment (acks):</b> number of replicas the message must be written before to be be considered successful
    <ul>
      <li><u>acks=0</u>: no response from kafka. In case of any error it is unknow and the data is lost</li>
      <li><u>acks=1</u>: response from the leader regardless of replicas. If an ack is not received, the producer may retry the request. If the leader broker is not working and the replicas is not updated, we have a data loss</li>
      <li><u>acks=all</u>: response from the leader only after the message is accepted by all in-sync replicas (ISR)</li>
      <li>Bast practice: acks=all and min.insync.replicas=2</li>
    </ul>
  </li>
</ul>
<br />
{% highlight ruby %}
// send local
$ kafka-console-producer --bootstrap-server localhost:9092 --topic first_topic 
> Hello World local

// send remote without key
$ kafka-console-producer --producer.config playground.config --bootstrap-server HOST_URL:9092 --topic first_topic --producer-property acks=all
> Hello World Remote

// send with key
kafka-console-producer --producer.config playground.config --bootstrap-server HOST_URL:9092 --topic first_topic --property parse.key=true --property key.separator=:
>My key:my value
>name:Maria
{% endhighlight %}

<p style="text-align: justify;"><u><b>Consumers</b></u></p>
<ul>
  <li>Subscribe to (read and process) events from Kafka</li>
  <li>Pull event data from one or more Kafka topics</li>
  <li>Consumers know which partition to read</li>
  <li>Consumers can read from one or more partitions</li>
  <li>Data is read in order from the same partition (from a lower offset to a higher offset - cannot read data backwards) </li>
  <li>The message order is not guaranteed when the data is read from more than one partition</li>
  <li>By default, Kafka consumers will only consume data that was produced after it first connected to Kafka</li>
  <li>Deserialization has to be done in the same format it was serialized in. </li>
  <li>In case switch a topic data format, the best practice is to create a new topic</li>
  <li>Consumers can commit offiset by the enable.auto.commit=true property every auto.commit.interval.ms (5 seconds by default) when .poll() is called.</li>
</ul>
<br />
{% highlight ruby %}
$ kafka-console-consumer --bootstrap-server localhost:9092 --topic second_topic
$ kafka-console-consumer --consumer.config playground.config --bootstrap-server HOST_URL:9092 --topic second_topic
{% endhighlight %}

<p style="text-align: justify;"><u><b>Consumer groups</b></u></p>
<ul>
  <li>Group of Consumers that performing the same "logical job"</li>
  <li>Identified by group.id</li>
  <li>Each consumer in a group is going to read from one partition</li> 
  <li>Benefit: coordinate to split the work of reading from different partitions and ensure the load balancing (GroupCoordinator and a ConsumerCoordinator)</li>
  <li>Relation: 1 Topic assigned to 1 Consumer | 1 Consumer assigned to multiple Partition</li>
  <li>For more consumers than partitions then consumers will remain inactive</li>
  <li>Offiset help the remaining Kafka consumers know where to restart reading and processing messages in case of fail</li>
  <li>Always a new consumer is added to a group then consumer group rebalance happens</li>
  <li>When a consumer leaves a group its partitions are revoked and re-assigned</li>
  <li>Consumer Groups and Partition Rebalance: Eager Rebalance ; Cooperative Rebalance</li>
</ul>

<p style="text-align: justify;"><u><b>Kafka message serializer</b></u><br />
Kafka only acept and send bytes. it tranforms object in bytes. Use only value and key. The producer use this to serialize the data to send to kafka.</p>

<p style="text-align: justify;"><u><b>Zookeeper</b></u></p>
<ul>
  <li>It tracks cluster state, membership, and leadership</li>
  <li>It determines which broker is the leader of a given partition and topic and perform leader elections</li>
  <li>Send notification to kafka in case of change</li>
  <li>It does not store consumer offsets with kafka</li>
  <li>It stores configurations for topics and permissions</li>
</ul>

<p style="text-align: justify;"><u><b>Kafka KRaft</b></u><br />
Created to overcome performance bottleneck with Zookeeper</p>  

<p style="text-align: justify;"><u><b>The Schema Registry </b></u><br />
It helps register data schemas in Apache Kafka and ensure that producers and consumers will be compatible with each other while evolving. It supports the Apache Avro, Protobuf and JSON-schema data formats.</p>


<p style="text-align: justify;"><u><b>Batch</b></u></p>
<ul>
  <li>If producer try to send a lot of message in parallel (e.g max.in.flight.requests.per.connection=5) kafka is smart enought to start batching them</li>
  <li>It helps to increase throughput and maintaning low latency</li>
  <li>linger.ms: property to define how long to wait until send a batch</li>
</ul>

<p style="text-align: justify;"><u><b>Example in Java</b></u></p>
<li>Producer: send a message to the topic to your kafka playground <a href="https://github.com/conduktor/kafka-beginners-course/blob/main/kafka-basics/src/main/java/io/conduktor/demos/kafka/ProducerDemo.java">[ProducerDemo]</a></li>
<li>Consumer: retrieve a message from the topic in your kafka playground <a href="https://github.com/conduktor/kafka-beginners-course/blob/main/kafka-basics/src/main/java/io/conduktor/demos/kafka/ConsumerDemo.java">[ConsumerDemo]</a></li>

<p style="text-align: justify;"><u><b>Summary which use</b></u></p>
<ul>
  <li>From Source database to kafka: Kafca Connect Source</li>
  <li>Produce data directly to kafka: Kafka Producer</li>
  <li>Kafka to Kafka transformation: Kafka Streams/ KSQL</li>
  <li>From kafka to a database: Kafka Connect Sink</li>
  <li>To use direct the mesage: Kafka Consumer</li>
</ul>
