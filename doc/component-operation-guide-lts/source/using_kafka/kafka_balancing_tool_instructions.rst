:original_name: mrs_01_1040.html

.. _mrs_01_1040:

Kafka Balancing Tool Instructions
=================================

Scenario
--------

This section describes how to use the Kafka balancing tool on a client to balance the load of the Kafka cluster based on service requirements in scenarios such as node decommissioning, node recommissioning, and load balancing.

Prerequisites
-------------

-  The system administrator has understood service requirements and prepared a Kafka administrator (belonging to the **kafkaadmin** group. It is not required for the normal mode.).
-  The Kafka client has been installed.

Procedure
---------

#. Log in as a client installation user to the node on which the Kafka client is installed.

#. Switch to the Kafka client installation directory, for example, **/opt/kafkaclient**.

#. Run the following command to configure environment variables:

   **source bigdata_en**\ v

#. Run the following command to authenticate the user (skip this step in normal mode):

   **kinit** *Component service user*

#. Run the following command to switch to the Kafka client installation directory:

   **cd Kafka/kafka**

#. Run the **kafka-balancer.sh** command to balance user cluster. The commonly used commands are:

   -  Run the **--run** command to perform cluster balancing:

      **./bin/kafka-balancer.sh --run --zookeeper** *<ZooKeeper* *service IP address of any ZooKeeper node:zkPort\ *\ **/kafka**\ *>* **--bootstrap-server** *<Kafka* *cluster IP: port>* **--throttle 10000000 --consumer-config config/consumer.properties --show-details**

      This command consists of generation and execution of the balancing solution. **--show-details** is optional, indicating whether to print the solution details. **--throttle** indicates the bandwidth limit during the execution of the balancing solution. The unit is bytes per second (bytes/sec).

   -  Run the **--run** command to decommission a node:

      **./bin/kafka-balancer.sh --run --zookeeper** *<Service IP address of any ZooKeeper node:zkPort\ *\ **/kafka**\ *>* **--bootstrap-server** *<Kafka cluster IP address: port>* **--throttle 10000000 --consumer-config config/consumer.properties --remove-brokers** *<BrokerId list>* **--force**

      In the command, **--remove-brokers** indicates the list of broker IDs to be deleted. Multiple broker IDs are separated by commas (,). **--force** is optional, indicating that the disk usage alarm is ignored and the migration solution is forcibly generated.r.

   -  Run the following command to view the execution status:

      **./bin/kafka-balancer.sh --status --zookeeper** *<Service IP address of any ZooKeeper node:zkPort\ *\ **/kafka**\ *>*

   -  Run the following command to generate a balancing solution:

      **./bin/kafka-balancer.sh --generate --zookeeper** *<Service IP address of any ZooKeeper node:zkPort\ *\ **/kafka**\ *>* **--bootstrap-server** *<Kafka* *cluster IP address:port>* **--consumer-config config/consumer.properties**

      This command is used to generate a migration solution based on the current cluster status and print the solution to the console.

   -  Clearing the intermediate status

      **./bin/kafka-balancer.sh --clean --zookeeper** *<Service IP address of any ZooKeeper node:zkPort\ *\ **/kafka**\ *>*

      This command is used to clear the intermediate status information on the ZooKeeper when the migration is not complete.

      .. important::

         The port number of the Kafka cluster's IP address is 21007 in security mode and 9092 in normal mode.

Troubleshooting
---------------

During partition migration using the Kafka balancing tool, if the execution progress of the balancing tool is blocked due to a Broker fault in the cluster, you need to manually rectify the fault. The scenarios are as follows:

-  The Broker is faulty because the disk usage reaches 100%.

   #. Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**, stop the Broker instance in the **Restoring** state, and record the management IP address of the node where the instance resides and the corresponding **broker.id**. You can click the role name to view the value, on the **Instance Configurations** page, select **All Configurations** and search for the **broker.id** parameter.

   #. Log in to the recorded management IP address as user **root**, and run the **df -lh** command to view the mounted directory whose disk usage is 100%, for example, **${BIGDATA_DATA_HOME}/kafka/data1**.

   #. Go to the directory, run the **du -sh \*** command to view the size of each file in the directory, Check whether files other than files in the **kafka-logs** directory exist, and determine whether these files can be deleted or migrated.

      -  If yes, delete or migrate the related data and go to :ref:`8 <mrs_01_1040__en-us_topic_0000001219029157_li286010416517>`.
      -  If no, go to :ref:`4 <mrs_01_1040__en-us_topic_0000001219029157_li207716388315>`.

   #. .. _mrs_01_1040__en-us_topic_0000001219029157_li207716388315:

      Go to the **kafka-logs** directory, run the **du -sh \*** command, select a partition folder to be moved. The naming rule is **Topic name-Partition ID**. Record the topic and partition.

   #. .. _mrs_01_1040__en-us_topic_0000001219029157_l847204e787034666b0ffc45eaaaf2cd4:

      Modify the **recovery-point-offset-checkpoint** and **replication-offset-checkpoint** files in the **kafka-logs** directory in the same way.

      a. Decrease the number in the second line in the file. (To remove multiple directories, the number deducted is equal to the number of files to be removed.
      b. Delete the line of the to-be-removed partition. (The line structure is "*Topic name Partition ID Offset*". Save the data before deletion. Subsequently, the content must be added to the file of the same name in the destination directory.)

   #. Modify the **recovery-point-offset-checkpoint** and **replication-offset-checkpoint** files in the destination data directory (for example, **${BIGDATA_DATA_HOME}/kafka/data2/kafka-logs**) in the same way.

      -  Increase the number in the second line in the file. (To move multiple directories, the number added is equal to the number of files to be moved.
      -  Add the to-be moved partition to the end of the file. (The line structure is "*Topic name Partition ID Offset*". You can copy the line data saved in :ref:`5 <mrs_01_1040__en-us_topic_0000001219029157_l847204e787034666b0ffc45eaaaf2cd4>`.)

   #. Move the partition to the destination directory. After the partition is moved, run the **chown omm:wheel -R** *Partition directory* command to modify the directory owner group for the partition.

   #. .. _mrs_01_1040__en-us_topic_0000001219029157_li286010416517:

      Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance** to start the stopped Broker instance.

   #. Wait for 5 to 10 minutes and check whether the health status of the Broker instance is **Good**.

      -  If yes, resolve the disk capacity insufficiency problem according to the handling method of "ALM-38001 Insufficient Kafka Disk Capacity" after the alarm is cleared.
      -  If no, contact O&M support.

   After the faulty Broker is recovered, the blocked balancing task continues. You can run the **--status** command to view the task execution progress.

-  The Broker fault occurs because of other causes, the fault scenario is clear, and the fault can be rectified within a short period of time.

   #. Restore the faulty Broker according to the root cause.
   #. After the faulty Broker is recovered, the blocked balancing task continues. You can run the **--status** command to view the task execution progress.

-  The Broker fault occurs because of other causes, the fault scenario is complex, and the fault cannot be rectified within a short period of time.

   #. Run the **kinit** *Kafka* *administrator account* command (skip this step in normal mode).
   #. Run the **zkCli.sh -server** **<**\ *ZooKeeper cluster service IP address*:*zkPort*\ **/kafka>** command to log in to ZooKeeper Shell.
   #. Run the **addauth krbgroup** command (skip this step in normal mode).
   #. Delete the **/admin/reassign_partitions** and **/controller** directories.
   #. Perform the preceding steps to forcibly stop the migration. After the cluster recovers, run the **kafka-reassign-partitions.sh** command to delete redundant copies generated during the intermediate process.
