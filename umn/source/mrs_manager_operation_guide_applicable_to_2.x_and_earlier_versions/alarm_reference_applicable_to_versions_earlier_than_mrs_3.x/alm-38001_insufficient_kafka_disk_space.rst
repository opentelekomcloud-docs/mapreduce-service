:original_name: alm_38001.html

.. _alm_38001:

ALM-38001 Insufficient Kafka Disk Space
=======================================

Description
-----------

The system checks the Kafka disk usage every 60 seconds and compares it with the threshold. This alarm is generated if the disk usage exceeds the threshold.

To modify the threshold, users can choose **System** > **Threshold Configuration** on MRS Manager.

This alarm is cleared if the Kafka disk usage is lower than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
38001    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| PartitionName     | Specifies the disk partition where the alarm is generated.                          |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger Condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Kafka fails to write data to the disks.

Possible Causes
---------------

-  The Kafka disk configurations (such as disk count and disk size) are insufficient for the data volume.
-  The data retention period is long and historical data occupies large space.
-  Services are improperly planned. As a result, data is unevenly distributed and some disks are full.

Procedure
---------

#. Go to the MRS cluster details page and choose **Alarms**.

#. .. _alm_38001__en-us_topic_0191813921_li13769123214531:

   In the alarm list, click the alarm and view the **HostName** and **PartitionName** of the alarm in **Location** of **Alarm Details**.

#. On the **Hosts** page, click the host name obtained in :ref:`2 <alm_38001__en-us_topic_0191813921_li13769123214531>`.

#. Check whether the **Disk** area contains the **PartitionName** of the alarm.

   -  If yes, go to :ref:`5 <alm_38001__en-us_topic_0191813921_li15769133210538>`.
   -  If no, manually clear the alarm and no further action is required.

#. .. _alm_38001__en-us_topic_0191813921_li15769133210538:

   In the **Disk** area, check whether the usage of the alarmed partition has reached 100%.

   -  If yes, go to :ref:`6 <alm_38001__en-us_topic_0191813921_li16769832165314>`.
   -  If no, go to :ref:`8 <alm_38001__en-us_topic_0191813921_li1476912324536>`.

#. .. _alm_38001__en-us_topic_0191813921_li16769832165314:

   In **Instance**, choose **Broker > Instance Configuration**. On the **Instance Configuration** page that is displayed, set **Type** to **All** and query the data directory parameter **log.dirs**.

#. Choose **Components > Kafka > Instances**. On the **Kafka Instance** page that is displayed, stop the Broker instance corresponding to :ref:`2 <alm_38001__en-us_topic_0191813921_li13769123214531>`. Then log in to the alarmed node and manually delete the data directory in :ref:`6 <alm_38001__en-us_topic_0191813921_li16769832165314>`. After all subsequent operations are complete, start the Broker instance.

#. .. _alm_38001__en-us_topic_0191813921_li1476912324536:

   Choose **Components > Kafka > Service Configuration**. The **Kafka Configuration** page is displayed.

#. Check whether **disk.adapter.enable** is **true**.

   -  If yes, go to :ref:`11 <alm_38001__en-us_topic_0191813921_li19769532105319>`.
   -  If no, change the value to **true** and go to :ref:`10 <alm_38001__en-us_topic_0191813921_li37691432185316>`.

#. .. _alm_38001__en-us_topic_0191813921_li37691432185316:

   Check whether the **adapter.topic.min.retention.hours** parameter, indicating the minimum data retention period, is properly configured.

   -  If yes, go to :ref:`12 <alm_38001__en-us_topic_0191813921_li076953295311>`.
   -  If no, set it to a proper value and go to :ref:`12 <alm_38001__en-us_topic_0191813921_li076953295311>`.

   .. note::

      If the retention period cannot be adjusted for certain topics, the topics can be added to **disk.adapter.topic.blacklist**.

#. .. _alm_38001__en-us_topic_0191813921_li19769532105319:

   Wait 10 minutes and check whether the disk usage is reduced.

   -  If yes, wait until the alarm is cleared.
   -  If no, go to :ref:`12 <alm_38001__en-us_topic_0191813921_li076953295311>`.

#. .. _alm_38001__en-us_topic_0191813921_li076953295311:

   Go to the **Kafka Topic Monitor** page and query the data retention period configured for Kafka. Determine whether the retention period needs to be shortened based on service requirements and data volume.

   -  If yes, go to :ref:`13 <alm_38001__en-us_topic_0191813921_li10769173213539>`.
   -  If no, go to :ref:`14 <alm_38001__en-us_topic_0191813921_li1176913210535>`.

#. .. _alm_38001__en-us_topic_0191813921_li10769173213539:

   Find the topics with great data volumes based on the disk partition obtained in :ref:`2 <alm_38001__en-us_topic_0191813921_li13769123214531>`. Log in to the Kafka client and manually shorten the data retention period for these topics using the following command:

   **kafka-topics.sh --zookeeper** *ZooKeeper address:24002/kafka* **--alter --topic** *Topic name* **--config retention.ms=**\ *Retention period*

#. .. _alm_38001__en-us_topic_0191813921_li1176913210535:

   Check whether partitions are properly configured for topics. For example, if the number of partitions for a topic with a large data volume is smaller than the number of disks, data may be unevenly distributed to the disks and the usage of some disks will reach the upper limit.

   .. note::

      To identify topics with great data volumes, log in to the relevant nodes that are obtained in :ref:`2 <alm_38001__en-us_topic_0191813921_li13769123214531>`, go to the data directory (the directory before **log.dirs** in :ref:`6 <alm_38001__en-us_topic_0191813921_li16769832165314>` is modified), and check the disk space occupied by the partitions of the topics.

   -  If the partitions are improperly configured, go to :ref:`15 <alm_38001__en-us_topic_0191813921_li137701132145312>`.
   -  If the partitions are properly configured, go to :ref:`16 <alm_38001__en-us_topic_0191813921_li9770103214530>`.

#. .. _alm_38001__en-us_topic_0191813921_li137701132145312:

   On the Kafka client, add partitions to the topics.

   **kafka-topics.sh --zookeeper** *ZooKeeper address:24002/kafka* **--alter --topic** *Topic name* **--partitions=**\ *Number of new partitions*

   .. note::

      It is advised to set the number of new partitions to a multiple of the number of Kafka disks.

      This operation may not quickly clear the alarm. Data will be gradually balanced among the disks.

#. .. _alm_38001__en-us_topic_0191813921_li9770103214530:

   Check whether the cluster capacity needs to be expanded.

   -  If yes, add nodes to the cluster and go to :ref:`17 <alm_38001__en-us_topic_0191813921_li4770432185318>`.
   -  If no, go to :ref:`17 <alm_38001__en-us_topic_0191813921_li4770432185318>`.

#. .. _alm_38001__en-us_topic_0191813921_li4770432185318:

   Wait a moment and then check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`18 <alm_38001__en-us_topic_0191813921_li572522141314>`.

#. .. _alm_38001__en-us_topic_0191813921_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
