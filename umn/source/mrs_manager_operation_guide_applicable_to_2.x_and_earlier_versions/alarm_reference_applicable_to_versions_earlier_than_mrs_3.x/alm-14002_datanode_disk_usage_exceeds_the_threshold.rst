:original_name: alm_14002.html

.. _alm_14002:

ALM-14002 DataNode Disk Usage Exceeds the Threshold
===================================================

Description
-----------

The system checks the DataNode disk usage every 30 seconds and compares the actual disk usage with the threshold. The **Percentage of DataNode Capacity** indicator has a default threshold. This alarm is generated when the value of the **Percentage of DataNode Capacity** indicator exceeds the threshold.

This alarm is cleared when the value of the **Percentage of DataNode Capacity** indicator is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14002    Major          Yes
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
| Trigger condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Insufficient disk space will impact read/write to HDFS.

Possible Causes
---------------

-  The disk space configured for the HDFS cluster is insufficient.
-  Data skew occurs among DataNodes.

Procedure
---------

#. Check the cluster disk capacity.

   a. Go to the MRS cluster details page. On the **Alarms** page, check whether the ALM-14001 HDFS Disk Usage Exceeds the Threshold alarm exists.

      -  If yes, go to :ref:`1.b <alm_14002__en-us_topic_0191813920_yt2>`.
      -  If no, go to :ref:`2.a <alm_14002__en-us_topic_0191813920_li64268160>`.

   b. .. _alm_14002__en-us_topic_0191813920_yt2:

      Handle the alarm by following the instructions in ALM-14001 HDFS Disk Usage Exceeds the Threshold and check whether the alarm is cleared.

      -  If yes, go to :ref:`1.c <alm_14002__en-us_topic_0191813920_yt3>`.
      -  If no, go to :ref:`3 <alm_14002__en-us_topic_0191813920_li572522141314>`.

   c. .. _alm_14002__en-us_topic_0191813920_yt3:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_14002__en-us_topic_0191813920_li64268160>`.

#. Check the balance status of DataNodes.

   a. .. _alm_14002__en-us_topic_0191813920_li64268160:

      Use the client on the cluster node, run the **hdfs dfsadmin -report** command to view the value of **DFS Used%** on the DataNode for which the alarm is generated, and compare the value with those on other DataNodes. Check whether the difference between the values is larger than 10.

      -  If yes, go to :ref:`2.b <alm_14002__en-us_topic_0191813920_step17>`.
      -  If no, go to :ref:`3 <alm_14002__en-us_topic_0191813920_li572522141314>`.

   b. .. _alm_14002__en-us_topic_0191813920_step17:

      If data skew occurs, use the client on the cluster node and run the **hdfs balancer -threshold 10** command.

   c. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_14002__en-us_topic_0191813920_li572522141314>`.

#. .. _alm_14002__en-us_topic_0191813920_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
