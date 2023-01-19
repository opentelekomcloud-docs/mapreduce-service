:original_name: mrs_01_1038.html

.. _mrs_01_1038:

Changing the Broker Storage Directory
=====================================

Scenario
--------

When a broker storage directory is added, the system administrator needs to change the broker storage directory on FusionInsight Manager, to ensure that the Kafka can work properly. The new topic partition will be generated in the directory that has fewest partitions. Changing the ZooKeeper storage directory includes the following scenarios:

.. note::

   Because Kafka does not detect disk capacity, ensure that the disk quantity and capacity configured for each Broker instance are the same.

-  Change the storage directory of the Broker role. In this way, the storage directories of all Broker instances are changed.
-  Change the storage directory of a single Broker instance. In this way, only the storage directory of this Broker instance is changed, and the storage directories of other Broker instances remain the same.

Impact on the System
--------------------

-  Changing the Broker role storage directory requires the restart of services. The services cannot be accessed during the restart.
-  The storage directory of a single Broker instance can be changed only after the instance is restarted. The instance cannot provide services during the restart.
-  The directory for storing service parameter configurations must also be updated.

Prerequisites
-------------

-  New disks have been prepared and installed on each data node, and the disks are formatted.
-  The Kafka client has been installed.
-  When you change the storage directory of a single Broker instance, the number of active Broker instances must be greater than the number of backups specified during topic creation.

Procedure
---------

**Changing the storage directory of the Kafka role**

#. Log in as user **root** to each node on which the Kafka service is installed, and perform the following operations:

   a. Create a target directory.

      For example, to create the target directory **${BIGDATA_DATA_HOME}/kafka/data2**, run the following command:

      **mkdir ${BIGDATA_DATA_HOME}/kafka/data2**

   b. Mount the directory to the new disk. For example, mount **${BIGDATA_DATA_HOME}/kafka/data2** to the new disk.

   c. Modify permissions on the new directory.

      For example, to modify permissions on the **${BIGDATA_DATA_HOME}/kafka/data2** directory, run the following commands:

      **chmod 700 ${BIGDATA_DATA_HOME}/kafka/data2 -R** and **chown omm:wheel ${BIGDATA_DATA_HOME}/kafka/data2 -R**

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Kafka** > **Configurations**.

#. Add a new directory to the end of the default value of **log.dirs**.

   Enter **log.dirs** in the search box and add the new directory to the end of the default value of the **log.dirs** configuration item. Use commas (,) to separate multiple directories. For example:

   **${BIGDATA_DATA_HOME}/kafka/data1/kafka-logs,${BIGDATA_DATA_HOME}/kafka/data2/kafka-logs**

#. Click **Save**, and then click **OK**. When **Operation succeeded** is displayed, click **Finish**.

#. Choose **Cluster** > **Services** > **Kafka**. In the upper right corner, choose **More** > **Restart Service** to restart the Kafka service.

**Changing the storage directory of a single Kafka instance**

6.  Log in to the Broker node as user **root** and perform the following operations:

    a. Create a target directory.

       For example, to create the target directory **${BIGDATA_DATA_HOME}/kafka/data2**, run the following command:

       **mkdir ${BIGDATA_DATA_HOME}/kafka/data2**

    b. Mount the directory to the new disk. For example, mount **${BIGDATA_DATA_HOME}/kafka/data2** to the new disk.

    c. Modify permissions on the new directory.

       For example, to modify permissions on the **${BIGDATA_DATA_HOME}/kafka/data2** directory, run the following commands:

       **chmod 700 ${BIGDATA_DATA_HOME}/kafka/data2 -R** and **chown omm:wheel ${BIGDATA_DATA_HOME}/kafka/data2 -R**

7.  Log in to FusionInsight Managerand choose **Cluster** > **Services** > **Kafka** > **Instance**.

8.  Click the specified broker instance and switch to **Instance Configurations**.

    Enter **log.dirs** in the search box and add the new directory to the end of the default value of the **log.dirs** configuration item. Use commas (,) to separate multiple directories, for example, **${BIGDATA_DATA_HOME}/kafka/data1/kafka-logs,${BIGDATA_DATA_HOME}/kafka/data2/kafka-logs**.

9.  Click **Save**, and then click **OK**. A message is displayed, indicating that the operation is successful. Click **Finish**.

10. On the Broker instance page, choose **More** > **Restart Instance** to restart the Broker instance.
