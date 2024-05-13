:original_name: ALM-16001.html

.. _ALM-16001:

ALM-16001 Hive Warehouse Space Usage Exceeds the Threshold
==========================================================

Description
-----------

This alarm is generated when the Hive warehouse space usage exceeds the specified threshold (85% by default). The system checks the Hive data warehouse space usage every 30s. The indicator **Percentage of HDFS Space Used by Hive to the Available Space** can be viewed on the Hive service monitoring page.

To change the threshold, choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **Hive > Percentage of HDFS Space Used by Hive to the Available Space**.

When the **Trigger Count** is 1, this alarm is cleared when the Hive warehouse space usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the Hive warehouse space usage is less than or equal to 90% of the threshold.

.. note::

   The administrator can reduce the warehouse space usage by expanding the warehouse capacity or releasing the used space.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
16001    Minor          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

The system fails to write data, which causes data loss.

Possible Causes
---------------

-  The upper limit of the HDFS capacity available for Hive is too small.
-  The HDFS space is insufficient.
-  Some data nodes break down.

Procedure
---------

**Expand the system configuration.**

#. Analyze the cluster HDFS capacity usage and increase the upper limit of the HDFS capacity available for Hive.

   Log in to MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations > All Configurations**, find **hive.metastore.warehouse.size.percent**, and increase its value so that larger HDFS capacity will be available for Hive. Assume that the value of the configuration item is A, the total HDFS storage space is B, the threshold is C, and the HDFS space used by Hive is D. The adjustment policy is A x B x C > D. The total HDFS storage space can be viewed on the HDFS NameNode page. The HDFS space used by Hive can be viewed on the Hive monitoring page.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-16001__li1104893615539>`.

**Expand the system.**

3. .. _alm-16001__li1104893615539:

   Expand the system.

4. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-16001__li56638164155624>`.

**Check whether the data node is normal.**

5. .. _alm-16001__li56638164155624:

   On the MRS Manager portal, click **O&M > Alarm > Alarms**.

6. Check whether "ALM-12006 Node Fault", "ALM-12007 Process Fault", or "ALM-14002 DataNode Disk Usage Exceeds the Threshold" exist.

   -  If yes, go to :ref:`7 <alm-16001__li46923068155624>`.
   -  If no, go to :ref:`9 <alm-16001__li3112518015571>`.

7. .. _alm-16001__li46923068155624:

   Clear the alarm by following the steps provided in "ALM-12006 Node Fault", "ALM-12007 Process Fault", and "ALM-14002 DataNode Disk Usage Exceeds the Threshold".

8. Check whether the alarm is cleared.

-  If yes, no further action is required.
-  If no, go to :ref:`9 <alm-16001__li3112518015571>`.

**Collect fault information.**

9.  .. _alm-16001__li3112518015571:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

10. Select **Hive** in the required cluster from the **Service**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927578.png
