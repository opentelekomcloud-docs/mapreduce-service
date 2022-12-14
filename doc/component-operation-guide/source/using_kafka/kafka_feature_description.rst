:original_name: mrs_01_2312.html

.. _mrs_01_2312:

Kafka Feature Description
=========================

Kafka Idempotent Feature
------------------------

Feature description: The function of creating idempotent producers is introduced in Kafka 0.11.0.0. After this function is enabled, producers are automatically upgraded to idempotent producers. When producers send messages with the same field values, brokers automatically detect whether the messages are duplicate to avoid duplicate data. Note that this feature can only ensure idempotence in a single partition. That is, an idempotent producer can ensure that no duplicate messages exist in a partition of a topic. Only idempotence on a single session can be implemented. The session refers to the running of the producer process. That is, idempotence cannot be ensured after the producer process is restarted.

Method for enabling this feature:

#. Add **props.put("enable.idempotence", true)** to the secondary development code.
#. Add **enable.idempotence = true** to the client configuration file.

Kafka Transaction Feature
-------------------------

Feature description: Kafka 0.11 introduces the transaction feature. The Kafka transaction feature indicates that a series of producer message production and consumer offset submission operations are in the same transaction, or are regarded as an atomic operation. Message production and offset submission succeed or fail at the same time. This feature provides transactions at the Read Committed isolation level to ensure that multiple messages are written to the target partition atomically and that the consumer can view only the transaction messages that are successfully submitted. The transaction feature of Kafka is used in the following scenarios:

#. Multiple pieces of data sent by a producer can be encapsulated in a transaction to form an atomic operation. All messages are successfully sent or fail to be sent.
#. read-process-write mode: Message consumption and production are encapsulated in a transaction to form an atomic operation. In a streaming application, a service usually needs to receive messages from the upstream system, process the messages, and then send the processed messages to the downstream system. This corresponds to message consumption and production.

Example of secondary development code:

.. code-block::

   // Initialize the configuration and enable the transaction feature.
   Properties props = new Properties();
   props.put("enable.idempotence", true);
   props.put("transactional.id", "transaction1");
   ...

   KafkaProducer producer = new KafkaProducer<String, String>(props);

   // init transaction
   producer.initTransactions();
   try {
       // Start a transaction.
       producer.beginTransaction();
       producer.send(record1);
       producer.send(record2);
       // Stop a transaction.
       producer.commitTransaction();
   } catch (KafkaException e) {
       // Abort a transaction.
       producer.abortTransaction();
   }

Nearby Consumption
------------------

Feature description: In versions earlier than Kafka 2.4.0, the production and consumption of the client are leader copies oriented to each partition. Follower copies are used only for data redundancy and do not provide services for external systems. As a result, the leader copy has high pressure. In addition, in cross-DC and cross-rack consumption scenarios, a large volume of data is transmitted between DCs and between racks. In Kafka 2.4.0 and later versions, the Kafka kernel can consume data from follower replicas, which greatly reduces the data transmission volume and reduces the network bandwidth pressure in cross-DC and cross-rack scenarios. The community opens the ReplicaSelector API to support this feature. By default, MRS Kafka provides two methods to use this API.

#. **RackAwareReplicaSelector**: indicates that replicas in the same rack are preferentially consumed (nearby consumption in a rack).
#. **AzAwareReplicaSelector**: indicates that copies from nodes in the same AZ are preferentially consumed (nearby consumption in an AZ).

The following uses **RackAwareReplicaSelector** as an example to describe how to consume the closest replica.

.. code-block::

   public class RackAwareReplicaSelector implements ReplicaSelector {

       @Override
       public Optional<ReplicaView> select(TopicPartition topicPartition,
                                           ClientMetadata clientMetadata,
                                           PartitionView partitionView) {
           if (clientMetadata.rackId() != null && !clientMetadata.rackId().isEmpty()) {
               Set<ReplicaView> sameRackReplicas = partitionView.replicas().stream()
                       // Filter the replicas that are in the same rack as the client.
                       .filter(replicaInfo -> clientMetadata.rackId().equals(replicaInfo.endpoint().rack()))
                       .collect(Collectors.toSet());
               if (sameRackReplicas.isEmpty()) {
                   // If no replicas are in the same rack as the client, the leader replica is returned.
                   return Optional.of(partitionView.leader());
               } else {
                   // It shows that a replica that is in the same rack as the client exists.
                   if (sameRackReplicas.contains(partitionView.leader())) {
                       // If the client and the leader replica are in the same rack, the leader replica returns first.
                       return Optional.of(partitionView.leader());
                   } else {
                       // Otherwise, the latest replica synchronized with the leader is returned.
                       return sameRackReplicas.stream().max(ReplicaView.comparator());
                   }
               }
           } else {
               // If the rack information is not contained in the client request, the leader replica is returned first.
               return Optional.of(partitionView.leader());
           }
       }
   }

Method for enabling this feature:

#. Server: Update the **replica.selector.class** configuration item based on different features.

   -  To enable "nearby consumption in a rack", set this parameter to **org.apache.kafka.common.replica.RackAwareReplicaSelector**.
   -  To enable "nearby consumption in an AZ", set this parameter to **org.apache.kafka.common.replica.AzAwareReplicaSelector**.

#. Client: Add the **client.rack** configuration item to the **consumer.properties** file in the *{Client installation directory}*\ **/Kafka/kafka/config** directory.

   -  If the "nearby consumption in a rack" is enabled on the server, add the information about the rack where the client is located, for example, **client.rack = /default0/rack1**.
   -  If the "nearby consumption in an AZ" is enabled on the server, add the information about the rack where the client is located, for example, **client.rack = /AZ1/rack1**.

Ranger Unified Authentication
-----------------------------

Feature description: In versions earlier than Kafka 2.4.0, Kafka supports only the SimpleAclAuthorizer authentication plugin provided by the community. In Kafka 2.4.0 and later versions, MRS Kafka supports both the Ranger authentication plugin and the authentication plugin provided by the community. Ranger authentication is used by default. Based on the Ranger authentication plugin, fine-grained Kafka ACL management can be performed.

.. note::

   If the Ranger authentication plugin is used on the server and **allow.everyone.if.no.acl.found** is set to **true**, all actions are allowed when a non-secure port is used for access. You are advised to disable **allow.everyone.if.no.acl.found** for security clusters that use the Ranger authentication plugin.
