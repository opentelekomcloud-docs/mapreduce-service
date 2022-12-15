:original_name: mrs_01_1037.html

.. _mrs_01_1037:

Configuring Kafka HA and High Reliability Parameters
====================================================

Scenario
--------

For the Kafka message transmission assurance mechanism, different parameters are available for meeting different performance and reliability requirements. This section describes how to configure Kafka high availability (HA) and high reliability parameters.

This section applies to MRS 3.x or later.

Impact on the System
--------------------

-  Impact of HA and high performance configurations:

   .. important::

      After HA and high performance are configured, the data reliability decreases. Specifically, data may be lost of disks or nodes are faulty.

-  Impact of high reliability configurations:

   -  Deteriorated performance

      If **ack** is set to **-1**, data written is considered as successful only when data is written to multiple replicas. As a result, the delay of a single message increases and the client processing capability decreases. The impact is subject to the actual test data.

   -  Reduced availability

      A replica that is not in the ISR list cannot be elected as a leader. If the leader goes offline and other replicas are not in the ISR list, the partition remains unavailable until the leader node recovers. When the node where a replica of a partition is located is faulty, the minimum number of successful replicas cannot be met. As a result, service writing fails.

-  If parameters are at the service level, Kafka needs to be restarted. You are advised to modify the service-level configuration in the change window.

Parameter Description
---------------------

-  If services require high availability and high performance,

   set the parameters listed in :ref:`Table 1 <mrs_01_1037__table97904317438>` on the server. For details about the parameter configuration entry, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

   .. _mrs_01_1037__table97904317438:

   .. table:: **Table 1** Server HA and high performance parameters

      +--------------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                      | Default Value         | Description                                                                                                                                                                      |
      +================================+=======================+==================================================================================================================================================================================+
      | unclean.leader.election.enable | true                  | Specifies whether a replica that is not in the ISR can be selected as the leader. If this parameter is set to **true**, data may be lost.                                        |
      +--------------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | auto.leader.rebalance.enable   | true                  | Specifies whether the leader automated balancing function is used.                                                                                                               |
      |                                |                       |                                                                                                                                                                                  |
      |                                |                       | If this parameter is set to **true**, the controller periodically balances the leader of each partition on all nodes and assigns the leader to a replica with a higher priority. |
      +--------------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | min.insync.replicas            | 1                     | Specifies the minimum number of replicas to which data is written when **acks** is set to **-1** for the Producer.                                                               |
      +--------------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   Set the parameters listed in :ref:`Table 2 <mrs_01_1037__table337919499593>` in the client configuration file **producer.properties**. The path for storing **producer.properties** is /**opt/client/Kafka/kafka/config/producer.properties**, where **/opt/client** indicates the installation directory of the Kafka client.

   .. _mrs_01_1037__table337919499593:

   .. table:: **Table 2** Client HA and high performance parameters

      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Default Value         | Description                                                                                                                                                                                                                                                                                                                                                     |
      +=======================+=======================+=================================================================================================================================================================================================================================================================================================================================================================+
      | acks                  | 1                     | The leader needs to check whether the message has been received and determine whether the required operation has been processed. This parameter affects message reliability and performance.                                                                                                                                                                    |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       | -  If this parameter is set to **0**, the producer does not wait for any response from the server, and the message is considered successful.                                                                                                                                                                                                                    |
      |                       |                       | -  If this parameter is set to **1**, when the leader of the replica verifies that data has been written into the cluster, the leader returns a response without waiting for data to be written to all replicas. In this case, if the leader is abnormal when the leader makes the confirmation but replica synchronization is not complete, data will be lost. |
      |                       |                       | -  If this parameter is set to **-1**, the message is considered to be successfully received only when all synchronized replicas are confirmed. If the **min.insync.replicas** parameter is also configured, data can be written into multiple replicas. In this case, records will not be lost as long as one replica remains active.                          |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  To ensure high data reliability for services,

   set the parameters listed in :ref:`Table 3 <mrs_01_1037__table1779493174311>` on the server. For details about the parameter configuration entry, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

   .. _mrs_01_1037__table1779493174311:

   .. table:: **Table 3** Server HA parameters

      +--------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------+
      | Parameter                      | Recommended Value     | Description                                                                                                        |
      +================================+=======================+====================================================================================================================+
      | unclean.leader.election.enable | false                 | A replica that is not in the ISR list cannot be elected as a leader.                                               |
      +--------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------+
      | min.insync.replicas            | 2                     | Specifies the minimum number of replicas to which data is written when **acks** is set to **-1** for the Producer. |
      |                                |                       |                                                                                                                    |
      |                                |                       | Ensure that the value of **min.insync.replicas** is equal to or less than that of **replication.factor**.          |
      +--------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------+

   Set the parameters listed in :ref:`Table 4 <mrs_01_1037__table22137713255>` in the client configuration file **producer.properties**. The path for storing **producer.properties** is **/opt/client/Kafka/kafka/config/producer.properties**, where **/opt/client** indicates the installation directory of the Kafka client.

   .. _mrs_01_1037__table22137713255:

   .. table:: **Table 4** Server HA parameters

      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Recommended Value     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
      +=======================+=======================+==============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | acks                  | -1                    | The leader needs to check whether the message has been received and determine whether the required operation has been processed.                                                                                                                                                                                                                                                                                                                                                                             |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
      |                       |                       | If this parameter is set to **-1**, the message is considered to be successfully received only when all replicas in the ISR list have confirmed to receive the message. This parameter is used along with **min.insync.replicas** to ensure that multiple copies are successfully written. As long as one copy is active, the record will not be lost. If this parameter is set to **-1**, the production performance deteriorates. Therefore, you need to set this parameter based on the actual situation. |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Configuration Suggestions
-------------------------

Configure parameters based on requirements on reliability and performance in the following service scenarios:

-  For valued data, you are advised to configure RAID1 or RAID5 for Kafka data directory disks to improve data reliability when a single disk is faulty.

-  For parameters that can be modified at the topic level, the service level configurations are used by default.

   These parameters can be separately configured based on topic reliability requirements. For example, log in to the Kafka client as user **root**, and run the following command to configure the reliability parameter with topic named test in the client installation directory:

   **cd Kafka/kafka/bin**

   **kafka-topics.sh --zookeeper 192.168.1.205:2181/kafka --alter --topic test --config unclean.leader.election.enable=false --config min.insync.replicas=2**

   **192.168.1.205** indicates the ZooKeeper service IP address.

-  If parameters are at the service level, Kafka needs to be restarted. You are advised to modify the service-level configuration in the change window.
