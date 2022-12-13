:original_name: alm_14010.html

.. _alm_14010:

ALM-14010 NameService Service Is Abnormal
=========================================

Description
-----------

The system checks the NameService service status every 180 seconds. This alarm is generated when the NameService service is unavailable.

This alarm is cleared when the NameService service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14010    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+---------------------------------------------------------------------+
| Parameter   | Description                                                         |
+=============+=====================================================================+
| ServiceName | Specifies the service for which the alarm is generated.             |
+-------------+---------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+
| NSName      | Specifies the NameService service for which the alarm is generated. |
+-------------+---------------------------------------------------------------------+

Impact on the System
--------------------

HDFS fails to provide services for upper-layer components based on the NameService service, such as HBase and MapReduce. As a result, users cannot read or write files.

Possible Causes
---------------

-  The JournalNode is faulty.
-  The DataNode is faulty.
-  The disk capacity is insufficient.
-  The NameNode enters safe mode.

Procedure
---------

#. Check the status of the JournalNode instance.

   a. On the MRS Manager home page, click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services**.

   b. Click **HDFS**.

   c. Click **Instance**.

   d. Check whether the **Health Status** of the JournalNode is **Good**.

      -  If yes, go to :ref:`2.a <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step11>`.
      -  If no, go to :ref:`1.e <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step12>`.

   e. .. _alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step12:

      Select the faulty JournalNode, and choose **More** > **Restart Instance**. Check whether the JournalNode successfully restarts.

      -  If yes, go to :ref:`1.f <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step10>`.
      -  If no, go to :ref:`5 <alm_14010__en-us_topic_0191813899_li572522141314>`.

   f. .. _alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step10:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step11>`.

#. Check the status of the DataNode instance.

   a. .. _alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step11:

      On the MRS cluster details page, click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services**.

   b. Click **HDFS**.

   c. In **Operation and Health Summary**, check whether the **Health Status** of all DataNodes is **Good**.

      -  If yes, go to :ref:`3.a <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step24>`.
      -  If no, go to :ref:`2.d <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step14>`.

   d. .. _alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step14:

      Click **Instances**. On the DataNode management page, select the faulty DataNode, and choose **More** > **Restart Instance**. Check whether the DataNode successfully restarts.

      -  If yes, go to :ref:`2.e <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step15>`.
      -  If no, go to :ref:`3.a <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step24>`.

   e. .. _alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step15:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4.a <alm_14010__en-us_topic_0191813899_step28>`.

#. Check the disk status.

   a. .. _alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step24:

      On the MRS cluster details page, click the **Nodes** tab and expand a node group.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Hosts**.

   b. In the **Disk Usage** column, check whether disk space is insufficient.

      -  If yes, go to :ref:`3.c <alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step26>`.
      -  If no, go to :ref:`4.a <alm_14010__en-us_topic_0191813899_step28>`.

   c. .. _alm_14010__en-us_topic_0191813899_alm14010_mmccppss_step26:

      Expand the disk capacity.

   d. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4.a <alm_14010__en-us_topic_0191813899_step28>`.

#. Check whether NameNode is in the safe mode.

   a. .. _alm_14010__en-us_topic_0191813899_step28:

      Use the client on the cluster node, and run the **hdfs dfsadmin -safemode get** command to check whether **Safe mode is ON** is displayed.

      Information behind **Safe mode is ON** is alarm information and is displayed based actual conditions.

      -  If yes, go to :ref:`4.b <alm_14010__en-us_topic_0191813899_li66373591>`.
      -  If no, go to :ref:`5 <alm_14010__en-us_topic_0191813899_li572522141314>`.

   b. .. _alm_14010__en-us_topic_0191813899_li66373591:

      Use the client on the cluster node and run the **hdfs dfsadmin -safemode leave** command.

   c. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`5 <alm_14010__en-us_topic_0191813899_li572522141314>`.

#. .. _alm_14010__en-us_topic_0191813899_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
