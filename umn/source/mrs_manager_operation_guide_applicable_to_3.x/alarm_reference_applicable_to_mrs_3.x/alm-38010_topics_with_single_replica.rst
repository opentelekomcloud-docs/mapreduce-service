:original_name: ALM-38010.html

.. _ALM-38010:

ALM-38010 Topics with Single Replica
====================================

Description
-----------

The system checks the number of replicas of each topic every 60 seconds on the node where the Kafka Controller resides. This alarm is generated when there is one replica for a topic.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38010    Warning        No
======== ============== =====================

Parameters
----------

+-------------+----------------------------------------------------------------+
| Name        | Meaning                                                        |
+=============+================================================================+
| Source      | Specifies the cluster for which the alarm is generated.        |
+-------------+----------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.        |
+-------------+----------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.           |
+-------------+----------------------------------------------------------------+
| TopicName   | Specifies the list of topics for which the alarm is generated. |
+-------------+----------------------------------------------------------------+

Impact on the System
--------------------

There is the single point of failure (SPOF) risk for topics with only one replica. When the node where the replica resides becomes abnormal, the partition does not have a leader, and services on the topic are affected.

Possible Causes
---------------

-  The number of replicas for the topic is incorrectly configured.

Procedure
---------

**Check the number of replicas for the topic.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, click |image1| of this alarm, and view the **TopicName** list in **Location**.

#. Check whether replicas need to be added for the topic for which the alarm is generated.

   -  If yes, go to :ref:`3 <alm-38010__li135931325311>`.
   -  If no, go to :ref:`5 <alm-38010__li477744715546>`.

#. .. _alm-38010__li135931325311:

   On the MRS client, re-plan topic replicas and describe the partition distribution of the topic in the **add-replicas-reassignment.json** file in the following format: {"partitions":[{"topic": "*topic name*","partition": 1,"replicas": [1,2] }],"version":1}. Then, run the following command to add replicas:

   **kafka-reassign-partitions.sh** **--zookeeper** *{zk_host}:{port}*\ **/kafka** **--reassignment-json-file** *{manual assignment json file path}* **--execute**

   For example:

   **/opt/client/Kafka/kafka/bin/kafka-reassign-partitions.sh --zookeeper 192.168.0.90:2181,192.168.0.91:2181,192.168.0.92:2181/kafka --reassignment-json-file add-replicas-reassignment.json --execute**

#. Run the following command to check the task execution progress:

   **kafka-reassign-partitions.sh** **--zookeeper** *{zk_host}:{port}*\ **/kafka** **--reassignment-json-file** *{manual assignment json file path}* **--verify**

   For example:

   **/opt/client/Kafka/kafka/bin/kafka-reassign-partitions.sh --zookeeper 192.168.0.90:2181,192.168.0.91:2181,192.168.0.92:2181/kafka --reassignment-json-file add-replicas-reassignment.json --verify**

#. .. _alm-38010__li477744715546:

   After completing the handling operations or confirming that the alarm has no impact, manually clear the alarm on MRS Manager.

#. After a period of time, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`7 <alm-38010__li266761095919>`.

**Collect fault information.**

7.  .. _alm-38010__li266761095919:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

8.  In the **Service** area, select **Kafka** in the required cluster.

9.  Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

If the alarm has no impact, manually clear the alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448170.png
.. |image2| image:: /_static/images/en-us_image_0000001582927549.png
