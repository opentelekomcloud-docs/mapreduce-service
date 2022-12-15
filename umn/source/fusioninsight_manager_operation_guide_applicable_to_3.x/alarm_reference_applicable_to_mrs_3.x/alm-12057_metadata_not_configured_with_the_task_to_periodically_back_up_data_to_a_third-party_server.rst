:original_name: ALM-12057.html

.. _ALM-12057:

ALM-12057 Metadata Not Configured with the Task to Periodically Back Up Data to a Third-Party Server
====================================================================================================

Description
-----------

After the system is installed, it checks whether the task for periodically backing up metadata to the third-party server, and then performs the check hourly. If the task for periodically backing up metadata to a third-party server is not configured, a critical alarm is generated.

This alarm is cleared when a user creates such a backup task.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12057    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

If metadata is not backed up to a third-party server, metadata cannot be restored if both the active and standby management nodes of the cluster are faulty and local backup data is lost.

Possible Causes
---------------

Metadata is not configured with the task to periodically back up data to a third-party server.

Procedure
---------

#. On the FusionInsight Manager portal choose **O&M > Alarm > Alarms**.
#. In the alarm list, click |image1| in the row where the alarm is located and identify the data module from which the alarm is generated based on **Additional Information**.
#. Choose **O&M** > **Backup and Restoration > Backup Management** > **Create**.
#. Configure a backup task. The backup data to be configured is consistent with the data in Additional Information of the alarm.
#. After the backup task is created successfully, wait for two minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12057__li1185962516113>`.

**Collect fault information**

6. .. _alm-12057__li1185962516113:

   On FusionInsight Manager, choose **O&M** > **Log > Download**.

7. In the **Service** area, select **Controller** and click **OK**.

8. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383889.png
.. |image2| image:: /_static/images/en-us_image_0269383890.png
