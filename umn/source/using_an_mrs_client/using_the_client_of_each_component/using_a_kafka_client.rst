:original_name: mrs_01_24191.html

.. _mrs_01_24191:

Using a Kafka Client
====================

Scenario
--------

You can create, query, and delete topics on a cluster client.

Prerequisites
-------------

The client has been installed. For example, the client is installed in the **/opt/hadoopclient** directory. The client directory in the following operations is only an example. Change it to the actual installation directory.

Using the Kafka Client (Versions Earlier Than MRS 3.x)
------------------------------------------------------

#. Access the ZooKeeper instance page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services** > **ZooKeeper** > **Instance**.
   -  For MRS 1.9.2 or later to versions earlier than 3.x, click the cluster name on the MRS console and choose **Components** > **ZooKeeper** > **Instances**.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

#. View the IP addresses of the ZooKeeper role instance.

   Record any IP address of the ZooKeeper instance.

#. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, **/opt/hadoopclient/Kafka/kafka/bin**.

   **cd /opt/hadoopclient/Kafka/kafka/bin**

#. Run the following command to configure environment variables:

   **source /opt/hadoopclient/bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. If Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** *Kafka user*

#. .. _mrs_01_24191__en-us_topic_0264266588_li1147589014556:

   Create a topic.

   **sh kafka-topics.sh --create --topic** *Topic name* **--partitions** *Number of partitions occupied by the topic* **--replication-factor** *Number of replicas of the topic* **--zookeeper** *IP address of the node where the ZooKeeper instance resides\ *\ **:**\ *\ clientPort*\ **/kafka**

   Example: **sh kafka-topics.sh --create --topic** **TopicTest** **--partitions** **3** **--replication-factor** **3** **--zookeeper** **10.10.10.100:2181/kafka**

#. Run the following command to view the topic information in the cluster:

   **sh kafka-topics.sh --list --zookeeper** *IP address of the node where the ZooKeeper instance resides\ *\ **:**\ *\ clientPort*\ **/kafka**

   Example: **sh kafka-topics.sh --list --zookeeper** **10.10.10.100:2181/kafka**

#. Delete the topic created in :ref:`7 <mrs_01_24191__en-us_topic_0264266588_li1147589014556>`.

   **sh kafka-topics.sh --delete --topic** *Topic name* **--zookeeper** *IP address of the node where the ZooKeeper instance resides*:*clientPort*\ **/kafka**

   Example: **sh kafka-topics.sh --delete --topic** **TopicTest** **--zookeeper** **10.10.10.100:2181/kafka**

   Type **y** and press **Enter**.

Using the Kafka Client (MRS 3.x or Later)
-----------------------------------------

#. Access the ZooKeeper instance page.

   Log in to MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Instance**.

#. View the IP addresses of the ZooKeeper role instance.

   Record any IP address of the ZooKeeper instance.

#. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, **/opt/hadoopclient/Kafka/kafka/bin**.

   **cd /opt/hadoopclient/Kafka/kafka/bin**

#. Run the following command to configure environment variables:

   **source /opt/hadoopclient/bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. If Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** *Kafka user*

#. Log in to MRS Manager, choose **Cluster** > **Name of the desired cluster** > **Services** > **ZooKeeper**, and click the **Configurations** tab and then **All Configurations**. On the displayed page, search for the **clientPort** parameter and record its value.

#. .. _mrs_01_24191__en-us_topic_0264266588_li4808125415465:

   Create a topic.

   **sh kafka-topics.sh --create --topic** *Topic name* **--partitions** *Number of partitions occupied by the topic* **--replication-factor** *Number of replicas of the topic* **--zookeeper** *IP address of the node where the ZooKeeper instance resides\ *\ **:**\ *\ clientPort*\ **/kafka**

   Example: **sh kafka-topics.sh --create --topic** **TopicTest** **--partitions** **3** **--replication-factor** **3** **--zookeeper** **10.10.10.100:2181/kafka**

#. Run the following command to view the topic information in the cluster:

   **sh kafka-topics.sh --list --zookeeper** *IP address of the node where the ZooKeeper instance resides\ *\ **:**\ *\ clientPort*\ **/kafka**

   Example: **sh kafka-topics.sh --list --zookeeper** **10.10.10.100:2181/kafka**

#. Delete the topic created in :ref:`8 <mrs_01_24191__en-us_topic_0264266588_li4808125415465>`.

   **sh kafka-topics.sh --delete --topic** *Topic name* **--zookeeper** *IP address of the node where the ZooKeeper instance resides*:*clientPort*\ **/kafka**

   Example: **sh kafka-topics.sh --delete --topic** **TopicTest** **--zookeeper** **10.10.10.100:2181/kafka**
