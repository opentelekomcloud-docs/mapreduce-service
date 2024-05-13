:original_name: ALM-38009.html

.. _ALM-38009:

(Applicable to Versions Later Than MRS 3.1.0)ALM-38009 Busy Broker Disk I/Os (Applicable to Versions Later Than MRS 3.1.0)
==========================================================================================================================

.. note::

   This section applies to versions later than MRS 3.1.0.

Description
-----------

The system checks the I/O status of each Kafka disk every 60 seconds. This alarm is generated when the disk I/O of a Kafka data directory on a broker exceeds the threshold (80% by default).

Its **Trigger Count** is **3**. This alarm is cleared when the disk I/O is lower than the threshold (80% by default).

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
38009    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------+
| Name              | Meaning                                                                 |
+===================+=========================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                 |
+-------------------+-------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                 |
+-------------------+-------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                    |
+-------------------+-------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                    |
+-------------------+-------------------------------------------------------------------------+
| DataDirectoryName | Specifies the name of the Kafka data directory with frequent disk I/Os. |
+-------------------+-------------------------------------------------------------------------+

Impact on the System
--------------------

The disk partition has frequent I/Os. Data may fail to be written to the Kafka topic for which the alarm is generated.

Possible Causes
---------------

-  There are many replicas configured for the topic.
-  The parameter for batch writing producer's messages is inappropriately configured. The service traffic of this topic is too heavy, and the current partition configuration is inappropriate.

Procedure
---------

**Check the number of topic replicas.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. Locate the row that contains this alarm, click |image1|, and view the host name in **Location**.

#. On MRS Manager, choose **Cluster**, click the name of the desired cluster, choose **Services** > **Kafka** > **KafkaTopic Monitor**, search for the topic for which the alarm is generated, and check the number of replicas.

#. .. _alm-38009__li8398191175118:

   Reduce the replication factors of the topic (for example, reduce to **3**) if the number of replicas is greater than 3.

   Run the following command on the MRS client to replan the replicas of Kafka topics:

   **kafka-reassign-partitions.sh** **--zookeeper** *{zk_host}:{port}*\ **/kafka** **--reassignment-json-file** *{manual assignment json file path}* **--execute**

   For example:

   **/opt/client/Kafka/kafka/bin/kafka-reassign-partitions.sh** **--zookeeper 10.149.0.90:2181,10.149.0.91:2181,10.149.0.92:2181/kafka** **--reassignment-json-file expand-cluster-reassignment.json** **--execute**

   .. note::

      In the **expand-cluster-reassignment.json** file, describe the brokers to which the partitions of the topic are migrated in the following format: {"partitions":[{"topic": "*topicName*","partition": 1,"replicas": [1,2,3] }],"version":1}

#. Observe for a period of time and check whether the alarm is cleared. If the alarm persists, go to :ref:`5 <alm-38009__li15319131241119>`.

**Check the partition planning of the topic.**

5. .. _alm-38009__li15319131241119:

   On the **KafkaTopic Monitor** page, view **Topic Input Traffic** in the **Topic Traffic** area of each topic, obtain the topic with the largest value, and check the partitions of this topic as well as information about the host of these partitions.

6. .. _alm-38009__li7320112121118:

   Log in to the host queried in :ref:`5 <alm-38009__li15319131241119>` and run the **iostat -d -x** command to check the **%util** value of each disk.

   |image2|

   -  If the **%util** value of each disk exceeds the threshold (**80%** by default), expand the Kafka disk capacity. After the capacity expansion, replan the topic partitions by referring to :ref:`3 <alm-38009__li8398191175118>`.

   -  If the **%util** values of the disks vary greatly, check the disk partition configuration of Kafka. For example, check the value of **log.dirs** in the **${BIGDATA_HOME}/FusionInsight_HD\_8.1.0.1/1_14_Broker/etc/server.properties** file.

      Run the following command to view the **Filesystem** information:

      **df -h** *log.dirs value*

      The command output is as follows.

      |image3|

   -  If the partition where Filesystem is located matches the partition with a high **%util** value, plan Kafka partitions on idle disks, configure **log.dirs** as an idle disk directory, and replan topic partitions by referring to :ref:`3 <alm-38009__li8398191175118>`. Ensure that the partitions of the topic are evenly distributed to each disk.

7. Observe for a period of time and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, repeat :ref:`5 <alm-38009__li15319131241119>` to :ref:`6 <alm-38009__li7320112121118>` three times. Then, go to :ref:`8 <alm-38009__li1032011218115>`.

8. .. _alm-38009__li1032011218115:

   Observe for a period of time and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-38009__li1473912318017>`.

**Collect fault information.**

9.  .. _alm-38009__li1473912318017:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **Kafka** for the target cluster.

11. Click |image4| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927450.png
.. |image2| image:: /_static/images/en-us_image_0000001532607778.png
.. |image3| image:: /_static/images/en-us_image_0000001583087429.png
.. |image4| image:: /_static/images/en-us_image_0000001582807721.png
