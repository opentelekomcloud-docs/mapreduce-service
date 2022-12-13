:original_name: ALM-27006.html

.. _ALM-27006:

ALM-27006 Disk Space Usage of the Data Directory Exceeds the Threshold
======================================================================

Description
-----------

The system checks the disk space usage of the data directory on the active DBServer node every 30 seconds and compares the disk usage with the threshold. The alarm is generated when the disk space usage exceeds the threshold for five consecutive times (the default value). The number of consecutive times is configurable. The disk space usage threshold of the data directory is set to 80% by default, which is configurable as well.

The value of **hit number** is configurable. When the value is set to **1** and the disk space usage is lower than or equal to the threshold, the alarm is cleared. When the value is greater than 1 and the disk space usage is lower than 90% of the threshold, the alarm is cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
27006    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                     |
+===================+=============================================================================================================================+
| ClusterName       | Specifies the cluster for which the alarm is generated.                                                                     |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                     |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                        |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                        |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| PartitionName     | Specifies the disk partition where the alarm is generated.                                                                  |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the actual indicator value exceeds this threshold, the alarm is generated. |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

-  Service processes become unavailable.
-  When the disk space usage of the data directory exceeds 90%, the database reports the "Database Enters the Read-Only Mode" alarm and enters the read-only mode, which may cause service data loss.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The data volume of the database is too large or the disk configuration cannot meet service requirements, causing excessive disk usage.

Procedure
---------

**Check whether the threshold is set properly.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **DBService** > **Database** > **Disk Space Usage of the Data Directory** to check whether the alarm threshold is proper (the default value 80% is a proper value).

   -  If yes, go to :ref:`3 <alm-27006__li165316427014>`.
   -  If no, go to :ref:`2 <alm-27006__li165311142601>`.

#. .. _alm-27006__li165311142601:

   Change the alarm threshold based on the actual service situation.

#. .. _alm-27006__li165316427014:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **DBService**. On the **Dashboard** page, view the **Disk Space Usage of the Data Directory** chart and check whether the disk space usage of the data directory is lower than the threshold.

   -  If yes, go to :ref:`4 <alm-27006__li1553118426012>`.
   -  If no, go to :ref:`5 <alm-27006__li1453211421204>`.

#. .. _alm-27006__li1553118426012:

   Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-27006__li1453211421204>`.

   **Check whether large files are incorrectly written into the disk.**

#. .. _alm-27006__li1453211421204:

   Log in to the active DBService node as user **omm**.

#. Run the following commands to view the files whose size exceeds 500 MB in the data directory and check whether there are large files incorrectly written into the directory:

   **source $DBSERVER_HOME/.dbservice_profile**

   **find "$DBSERVICE_DATA_DIR"/../ -type f -size +500M**

   -  If yes, go to :ref:`7 <alm-27006__li1453214421204>`.
   -  If no, go to :ref:`8 <alm-27006__li1853216425019>`.

#. .. _alm-27006__li1453214421204:

   Handle the large files based on the actual scenario and check whether the alarm is cleared 2 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-27006__li1853216425019>`.

   **Collect fault information.**

#. .. _alm-27006__li1853216425019:

   On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

#. Expand the **Service** drop-down list, and select **DBService** for the target cluster.

#. Specify the host for collecting logs by setting the **Host** parameter which is optional. By default, all hosts are selected.

#. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

#. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269623978.png
