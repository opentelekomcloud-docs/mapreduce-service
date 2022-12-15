:original_name: mrs_01_0376.html

.. _mrs_01_0376:

Managing Kafka Topics
=====================

Scenario
--------

You can manage Kafka topics on a cluster client based on service requirements. Management permission is required for clusters with Kerberos authentication enabled.

Prerequisites
-------------

You have installed the Kafka client.

Procedure
---------

#. Access the ZooKeeper instance page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services** > **ZooKeeper** > **Instance**.
   -  For MRS 1.9.2 or later to versions earlier than 3.x, click the cluster name on the MRS console and choose **Components** > **ZooKeeper** > **Instances**.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

#. View the IP addresses of the ZooKeeper role instance.

   Record any IP address of the ZooKeeper instance.

#. Prepare the client based on service requirements. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, /**opt/client/Kafka/kafka/bin**.

   **cd /opt/client/Kafka/kafka/bin**

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Run the following command to perform user authentication (skip this step in normal mode):

   **kinit** *Component service user*

#. .. _mrs_01_0376__lef5a65dfacd94aca8c9991c442b4a360:

   For versions earlier than MRS 3.x, run the following commands to manage Kafka topics:

   -  Creating a topic

      **sh kafka-topics.sh --create --topic** *Topic name* **--partitions** *Number of partitions occupied by the topic* **--replication-factor** *Number of replicas of the topic* **--zookeeper** *IP address of the node where the ZooKeeper instance resides\ *\ **:**\ *\ clientPort*\ **/kafka**

   -  Deleting a topic

      **sh kafka-topics.sh --delete --topic** *Topic name* **--zookeeper** *IP address of the node where the ZooKeeper instance resides*:*clientPort*\ **/kafka**

   .. note::

      -  The number of topic partitions or topic backup replicas cannot exceed the number of Kafka instances.

      -  By default, the value of **clientPort** of ZooKeeper is **2181**.

         For MRS 1.6.2 or earlier, the value of ZooKeeper's **clientPort** defaults to **24002**.

      -  There are three ZooKeeper instances. Use the IP address of any one.

      -  For details about managing messages in Kafka topics, see :ref:`Managing Messages in Kafka Topics <mrs_01_0379>`.

#. MRS 3.\ *x* and later versions: Use **kafka-topics.sh** to manage Kafka topics.

   -  Creating a topic:

      By default, partitions of a topic are distributed based on the number of partitions on the node and disk. To distribute partitions based on the disk capacity, set **log.partition.strategy** to **capacity** for the Kafka service.

      When a topic is created in Kafka, partitions and copies can be generated based on the combination of rack awareness and cross-AZ feature. The **--zookeeper** and **--bootstrap-server** modes are supported.

      -  Disable the rack policy and cross-AZ feature (default policy).

         Copies of topics created based on this policy are randomly allocated to any node in the cluster.

         **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic*\ **--zookeeper** *IP address of any ZooKeeper node:clientPort*\ **/kafka**

         **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic* **--bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties**

         If you use **--bootstrap-server** to create a topic, set **rack.aware.enable** and **az.aware.enable** to **false**.

      -  Enable the rack policy and disable the cross-AZ feature.

         The leader of each partition of the topic created based on this policy is randomly allocated on the cluster node. However, different replicas of the same partition are allocated to different racks. Therefore, when this policy is used, ensure that the number of nodes in each rack is the same, otherwise, the load of nodes in the rack with fewer nodes is much higher than the average load of the cluster.

         **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic* **--zookeeper** *IP address of any ZooKeeper node:clientPort*\ **/kafka --enable-rack-aware**

         **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic* **--bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties**

         If you use **--bootstrap-server** to create a topic, set **rack.aware.enable** to **true** and **az.aware.enable** to **false**.

      -  Disable the rack policy and enable the cross-AZ feature.

         The leader of each partition of the topic created based on this policy is randomly allocated on the cluster node. However, different replicas of the same partition are allocated to different AZs. Therefore, when this policy is used, ensure that the number of nodes in each AZ is the same, otherwise, the load of nodes in the AZ with fewer nodes is much higher than the average load of the cluster.

         **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic* **--zookeeper** *IP address of any ZooKeeper node:clientPort*\ **/kafka --enable-az-aware**

         **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic* **--bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties**

         If you use **--bootstrap-server** to create a topic, set **rack.aware.enable** to **false** and **az.aware.enable** to **true**.

      -  Enable the rack policy and cross-AZ feature.

         The leader of each partition of the topic created based on this policy is randomly allocated on the cluster node. However, different replicas of the same partition are allocated to different racks in different AZs. This policy ensures that the number of nodes on each rack in each AZ is the same, otherwise, the load in the cluster is unbalanced.

         **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic* **--replication-factor** *number of replicas of the topic* **--zookeeper** *IP address of any ZooKeeper node:clientPort*\ **/kafka --enable-rack-aware --enable-az-aware**

         **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic* **--bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties**

         If you use **--bootstrap-server** to create a topic, set **rack.aware.enable** and **az.aware.enable** to **true**.

      .. note::

         -  Kafka supports topic creation in either of the following modes:

            -  In **--zookeeper** mode, the client generates a copy allocation scheme. The community supports this mode from the beginning. To reduce the dependency on the ZooKeeper component, the community will delete the support for this mode in later versions. When creating a topic in this mode, you can select a copy allocation policy by combining the **--enable-rack-aware** and **--enable-az-aware** options. Note: The **--enable-az-aware** option can be used only when the cross-AZ feature is enabled on the server, that is, **az.aware.enable** is set to **true**. Otherwise, the execution fails.
            -  In **--bootstrap-server** mode, the server generates a copy allocation solution. In later versions, the community supports only this mode for topic management. When a topic is created in this mode, the **--enable-rack-aware** and **--enable-az-aware** options cannot be used to control the copy allocation policy. The **rack.aware.enable** and **az.aware.enable** parameters can be used together to control the copy allocation policy. Note that the **az.aware.enable** parameter cannot be modified; if the cross-AZ feature is enabled during cluster creation, this parameter is automatically set to **true**; the **rack.aware.enable** parameter can be customized.

   -  List of topics:

      -  **./kafka-topics.sh --list --zookeeper** *service IP address of any ZooKeeper node:clientPort*\ **/kafka**
      -  **./kafka-topics.sh --list --bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties**

   -  Viewing the topic:

      -  **./kafka-topics.sh --describe --zookeeper** *service IP address of any ZooKeeper node:clientPort*\ **/kafka** --**topic** *topic name*
      -  **./kafka-topics.sh --describe --bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties** **--topic** *topic name*

   -  Modifying a topic:

      -  **./kafka-topics.sh --alter --topic** *topic name*\ **--config** *configuration item=configuration value* **--zookeeper** *service IP address of any ZooKeeper node:clientPort*\ **/kafka**

   -  Expanding partitions:

      -  **./kafka-topics.sh --alter --topic** *topic name* **--zookeeper** *service IP address of any ZooKeeper node:clientPort*\ **/kafka --command-config Kafka/kafka/config/client.properties --partitions** *number of partitions after the expansion*
      -  **./kafka-topics.sh --alter --topic** *topic name* **--bootstrap-server** *IP address of the Kafka cluster:21007* **--command-config Kafka/kafka/config/client.properties --partitions** *number of partitions after the expansion*

   -  Deleting a topic

      -  **./kafka-topics.sh --delete --topic** *topic name* **--zookeeper** *Service IP address of any ZooKeeper node:clientPort*\ **/kafka**
      -  **./kafka-topics.sh --delete --topic** *topic name*\ **--bootstrap-server** *IP address of the Kafka cluster:21007* **--command-config ../config/client.properties**
