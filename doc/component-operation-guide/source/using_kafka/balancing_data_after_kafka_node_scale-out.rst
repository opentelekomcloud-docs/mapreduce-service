:original_name: mrs_01_24299.html

.. _mrs_01_24299:

Balancing Data After Kafka Node Scale-Out
=========================================

Scenario
--------

This section describes how to use the Kafka balancing tool on the client to balance the load of the Kafka cluster after Kafka nodes are scaled out.

This section applies to versions earlier than MRS 3.\ *x*. For MRS 3.\ *x* or later, see :ref:`Kafka Balancing Tool Instructions <mrs_01_1040>`.

Prerequisites
-------------

-  The system administrator has understood service requirements and prepared a Kafka administrator (belonging to the **kafkaadmin** group and not required for the normal mode).

-  The Kafka client has been installed, for example, in the **/opt/kafkaclient** directory.

-  Two topics named **test_2** and **test_3** has been created by referring to :ref:`7 <mrs_01_0376__lef5a65dfacd94aca8c9991c442b4a360>`. The **move-kafka-topic.json** file has been created in the **/opt/kafkaclient/Kafka/kafka** directory. The topic format is as follows:

   .. code-block::

      {
      "topics":
      [{"topic":"test_2"},{"topic":"test_3"}],
      "version":1
      }

Procedure
---------

#. Log in to the node where the Kafka client is installed as the client installation user.

#. Run the following command to switch to the client installation directory:

   **cd /opt/kafkaclient**

#. Run the following command to set environment variables:

   **source bigdata_env**

#. Run the following command to perform user authentication (skip this step if the cluster is in normal mode):

   **kinit** *Component service user*

#. Run the following command to go to the **bin** directory of the Kafka client:

   **cd Kafka/kafka/bin**

#. .. _mrs_01_24299__li1423719131942:

   Run the following command to generate an execution plan:

   **./kafka-reassign-partitions.sh --zookeeper** *172.16.0.119:*\ **2181/kafka --topics-to-move-json-file ../move-kafka-topic.json --broker-list "**\ *1,2,3*\ **" --generate**

   .. note::

      -  **172.16.0.119**: service IP address of the ZooKeeper instance
      -  **--broker-list "1,2,3"**: list of broker instances. **1,2,3** indicates all broker IDs after a scale-out.

   |image1|

#. Run the **vim ../reassignment.json** command to create the **reassignment.json** file and save it to the **/opt/kafkaclient/Kafka/kafka** directory.

   Copy the content under **Proposed partition reassignment configuration** generated in :ref:`6 <mrs_01_24299__li1423719131942>` to the **reassignment.json** file, as shown in the follows:

   .. code-block::

      {"version":1,"partitions":[{"topic":"test","partition":4,"replicas":[1,2],"log_dirs":["any","any"]},{"topic":"test","partition":1,"replicas":[1,3],"log_dirs":["any","any"]},{"topic":"test","partition":3,"replicas":[3,1],"log_dirs":["any","any"]},{"topic":"test","partition":0,"replicas":[3,2],"log_dirs":["any","any"]},{"topic":"test","partition":2,"replicas":[2,1],"log_dirs":["any","any"]}]}

#. Run the following command to redistribute partitions:

   **./kafka-reassign-partitions.sh --zookeeper** *172.16.0.119:*\ **2181/kafka --reassignment-json-file ../reassignment.json --execute --throttle** *50000000*

   .. note::

      **--throttle 50000000**: The maximum bandwidth is 50 MB/s. You can change the bandwidth based on the data volume and the customer's requirements on the balancing time. If the data volume is 5 TB, the bandwidth is 50 MB/s and the data balancing takes about 8 hours.

   |image2|

#. Run the following command to check the data migration status:

   **./kafka-reassign-partitions.sh --zookeeper** *172.16.0.119:*\ **2181/kafka --reassignment-json-file ../reassignment.json --verify**

   |image3|

.. |image1| image:: /_static/images/en-us_image_0000001349289889.png
.. |image2| image:: /_static/images/en-us_image_0000001349170305.png
.. |image3| image:: /_static/images/en-us_image_0000001438962057.png
