:original_name: alm_14012.html

.. _alm_14012:

ALM-14012 HDFS JournalNode Data Is Not Synchronized
===================================================

Description
-----------

On the active NameNode, the system checks data synchronization on all JournalNodes in the cluster every 5 minutes. This alarm is generated when data on a JournalNode is not synchronized with that on other JournalNodes.

This alarm is cleared in 5 minutes after data on JournalNodes is synchronized.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14012    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+------------------------------------------------------------------------------------------------+
| Parameter   | Description                                                                                    |
+=============+================================================================================================+
| ServiceName | Specifies the service for which the alarm is generated.                                        |
+-------------+------------------------------------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                                           |
+-------------+------------------------------------------------------------------------------------------------+
| IP          | Specifies the service IP address of the JournalNode instance for which the alarm is generated. |
+-------------+------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

When a JournalNode is working incorrectly, data on the node is not synchronized with that on other JournalNodes. If data on more than half of JournalNodes is not synchronized, the NameNode cannot work correctly, making the HDFS service unavailable.

Possible Causes
---------------

-  The JournalNode instance has not been started or has been stopped.
-  The JournalNode instance is working incorrectly.
-  The network of the JournalNode is unreachable.

Procedure
---------

#. Check whether the JournalNode instance has been started.

   a. On the MRS cluster details page, click **Alarms**. In the alarm list, click the alarm.

   b. In the **Alarm Details** area, check **Location** and obtain the IP address of the JournalNode for which the alarm is generated.

   c. Choose **Components** > **HDFS** > **Instances**. In the instance list, click the JournalNode for which the alarm is generated and check whether **Operating Status** of the node is **Started**.

      -  If yes, go to :ref:`2.a <alm_14012__en-us_topic_0191813911_alm14012_mmccppss_s6>`.
      -  If no, go to :ref:`1.d <alm_14012__en-us_topic_0191813911_alm14012_mmccppss_s4>`.

   d. .. _alm_14012__en-us_topic_0191813911_alm14012_mmccppss_s4:

      Select the JournalNode instance and choose **More** > **Start Instance** to start it.

   e. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_14012__en-us_topic_0191813911_li572522141314>`.

#. Check whether the JournalNode instance is working correctly.

   a. .. _alm_14012__en-us_topic_0191813911_alm14012_mmccppss_s6:

      Check whether **Health Status** of the JournalNode instance is **Good**.

      -  If yes, go to :ref:`3.a <alm_14012__en-us_topic_0191813911_alm14012_mmccppss_s10>`.
      -  If no, go to :ref:`2.b <alm_14012__en-us_topic_0191813911_s7>`.

   b. .. _alm_14012__en-us_topic_0191813911_s7:

      Select the JournalNode instance and choose **More** > **Restart Instance** to restart it.

   c. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_14012__en-us_topic_0191813911_li572522141314>`.

#. Check whether the network of the JournalNode is reachable.

   a. .. _alm_14012__en-us_topic_0191813911_alm14012_mmccppss_s10:

      On the MRS cluster details page, choose **Components** > **HDFS** > **Instances** to check the service IP address of the active NameNode.

   b. Log in to the active NameNode.

   c. Run the **ping** command to check whether a timeout occurs or the network between the active NameNode and the JournalNode is unreachable.

      **ping** *service IP address of the JournalNode*

      -  If yes, go to :ref:`3.d <alm_14012__en-us_topic_0191813911_alm14012_mmccppss_s13>`.
      -  If no, go to :ref:`4 <alm_14012__en-us_topic_0191813911_li572522141314>`.

   d. .. _alm_14012__en-us_topic_0191813911_alm14012_mmccppss_s13:

      Contact O&M personnel to rectify the network fault. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_14012__en-us_topic_0191813911_li572522141314>`.

#. .. _alm_14012__en-us_topic_0191813911_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
