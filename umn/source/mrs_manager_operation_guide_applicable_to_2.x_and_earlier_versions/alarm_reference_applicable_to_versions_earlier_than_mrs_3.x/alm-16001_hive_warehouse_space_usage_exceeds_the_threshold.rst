:original_name: alm_16001.html

.. _alm_16001:

ALM-16001 Hive Warehouse Space Usage Exceeds the Threshold
==========================================================

Description
-----------

The system checks the Hive warehouse space usage every 30 seconds. The indicator **Percentage of HDFS Space Used by Hive to the Available Space** can be viewed on the Hive service monitoring page. This alarm is generated when the Hive warehouse space usage exceeds the specified threshold (85% by default).

This alarm is cleared when the Hive warehouse space usage is less than or equal to the threshold. You can reduce the warehouse space usage by expanding the warehouse capacity or releasing the used space.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16001    Major          Yes
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

The system fails to write data, which causes data loss.

Possible Causes
---------------

-  The upper limit of the HDFS capacity available for Hive is too small.
-  The system disk space is insufficient.
-  Some data nodes break down.

Procedure
---------

#. Expand the system configuration.

   a. Analyze the cluster HDFS capacity usage and increase the upper limit of the HDFS capacity available for Hive.

      Go to the MRS cluster details page, choose **Components** > **Hive** > **Service Configuration**, set **Type** to **All**, search for **hive.metastore.warehouse.size.percent**, and increase the value of this parameter. Suppose that the value of the configuration item is A, total HDFS storage space is B, the threshold is C, and HDFS space used by Hive is D. Adjust the value of the configuration item according to A x B x C > D. The total HDFS storage space can be viewed on the HDFS monitoring page, and HDFS space used by Hive can be viewed on the Hive monitoring page.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Components** > **Hive** > **Service Configuration**.

   b. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_16001__en-us_topic_0191813901_s332>`.

#. Expand the system.

   a. .. _alm_16001__en-us_topic_0191813901_s332:

      Add nodes.

   b. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3.a <alm_16001__en-us_topic_0191813901_li51692872>`.

#. Check whether the data node is normal.

   a. .. _alm_16001__en-us_topic_0191813901_li51692872:

      Go to the cluster details page and choose **Alarms**.

   b. Check whether ALM-12006 Node Fault, ALM-12007 Process Fault, or ALM-14002 DataNode Disk Usage Exceeds the Threshold exists.

      -  If yes, go to :ref:`3.c <alm_16001__en-us_topic_0191813901_aalm-16001_mmccppss_step5>`.
      -  If no, go to :ref:`4 <alm_16001__en-us_topic_0191813901_li572522141314>`.

   c. .. _alm_16001__en-us_topic_0191813901_aalm-16001_mmccppss_step5:

      Clear the alarm by following the steps provided in ALM-12006 Node Fault, ALM-12007 Process Fault, or ALM-14002 DataNode Disk Usage Exceeds the Threshold.

   d. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_16001__en-us_topic_0191813901_li572522141314>`.

#. .. _alm_16001__en-us_topic_0191813901_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
