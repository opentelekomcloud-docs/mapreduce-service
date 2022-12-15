:original_name: ALM-14025.html

.. _ALM-14025:

ALM-14025 Tenant File Object Usage Exceeds the Threshold
========================================================

Description
-----------

The system checks the file object usage (used file objects of each directory/number of file objects allocated to each directory) of each directory associated with a tenant every hour and compares the file object usage of each directory with the threshold set for the directory. This alarm is generated when the file object usage exceeds the threshold.

This alarm is cleared when the file object usage is less than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14025    Minor          Yes
======== ============== =====================

Parameters
----------

+-------------------+-----------------------------------------------------------+
| Name              | Meaning                                                   |
+===================+===========================================================+
| Source            | Specifies the cluster for which the alarm is generated.   |
+-------------------+-----------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.   |
+-------------------+-----------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.      |
+-------------------+-----------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.      |
+-------------------+-----------------------------------------------------------+
| TenantName        | Specifies the tenant for which the alarm is generated.    |
+-------------------+-----------------------------------------------------------+
| DirectoryName     | Specifies the directory for which the alarm is generated. |
+-------------------+-----------------------------------------------------------+
| Trigger condition | Specifies the threshold for triggering the alarm.         |
+-------------------+-----------------------------------------------------------+

Impact on the System
--------------------

This alarm is generated if the usage of file objects in a tenant directory exceeds the custom threshold. File writing to the directory is not affected. If the number of used file objects exceeds the maximum number of file objects allocated to the directory, the HDFS fails to write data to the directory.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The maximum number of file objects allocated to the tenant directory is inappropriate.

Procedure
---------

**Check whether the alarm threshold is appropriate.**

#. View the alarm location information to obtain the tenant name and tenant directory for which the alarm is generated.

#. On the FusionInsight Manager portal, choose the **Tenant Resources** page, select the tenant for which the alarm is generated, and click **Resources**. Check whether the file object threshold configured for the tenant directory for which the alarm is generated is proper. (The default value 90% is a proper value. You can set it based on the site requirements.)

   -  If yes, go to :ref:`5 <alm-14025__li125757435197>`.
   -  If no, go to :ref:`3 <alm-14025__li195771843121910>`.

#. .. _alm-14025__li195771843121910:

   On the **Resources** page, click **Modify** to modify or delete the file object threshold of the tenant directory for which the alarm is generated.

#. About one minute later, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-14025__li125757435197>`.

**Check whether the maximum number of file objects allocated to the tenant is appropriate.**

5. .. _alm-14025__li125757435197:

   On the FusionInsight Manager portal, choose the **Tenant** **Resources** page, select the tenant for which the alarm is generated, and click **Resources**. Check whether the maximum number of file objects configured for the tenant directory for which the alarm is generated is proper based on the actual service status of the tenant directory.

   -  If yes, go to :ref:`8 <alm-14025__li10103154142014>`.
   -  If no, go to :ref:`6 <alm-14025__li2022812133204>`.

6. .. _alm-14025__li2022812133204:

   On the **Resources** page, click **Modify** to modify or delete the maximum number of file objects configured for the tenant directory.

7. About one minute later, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14025__li10103154142014>`.

**Collect fault information.**

8.  .. _alm-14025__li10103154142014:

    On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

9.  Select **HDFS** in the required cluster and **NodeAgent** under **Manager** from the **Service**.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 20 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417370.png
