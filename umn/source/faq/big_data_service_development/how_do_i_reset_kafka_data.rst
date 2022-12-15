:original_name: mrs_03_1106.html

.. _mrs_03_1106:

How Do I Reset Kafka Data?
==========================

You can reset Kafka data by deleting Kafka topics.

-  Delete a topic: **kafka-topics.sh --delete --zookeeper** *ZooKeeper Cluster service IP address*\ **:2181/kafka --topic topicname**
-  Query all topics: **kafka-topics.sh --zookeeper** *ZooKeeper cluster service IP address*\ **:2181/kafka --list**

After the deletion command is executed, empty topics will be deleted immediately. If a topic has data, the topic will be marked for deletion and will be deleted by Kafka later.
