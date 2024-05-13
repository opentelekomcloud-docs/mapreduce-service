:original_name: ALM-19012.html

.. _ALM-19012:

ALM-19012 HBase System Table Directory or File Lost
===================================================

Description
-----------

The system checks whether HBase directories and files exist on the HDFS every 120 seconds. This alarm is generated when the system detects that the files or directories do not exist. This alarm is cleared when the files or directories are restored.

The HBase directories and files are as follows:

-  Directory of the namespace **hbase** on the HDFS
-  **hbase.version** file
-  Directory of the table **hbase:meta** on the HDFS, .tableinfo file, and .regioninfo file
-  Directory of the table **hbase:namespace** on the HDFS, .tableinfo file, and .regioninfo file
-  Directory of the table **hbase:hindex** on the HDFS, .tableinfo file, and .regioninfo file
-  Directory of the **hbase:acl** table on the HDFS, .tableinfo, and .regioninfo file (This table does not exist in the common mode cluster by default.)

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
19012    Critical       Yes
======== ============== =====================

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The HBase service fails to restart or start.

Possible Causes
---------------

Files or directories on the HDFS are missing.

Procedure
---------

**Locate the alarm cause.**

#. On the MRS Manager, choose **O&M** > **Alarm** > **Alarms**. Click this alarm and check whether **Alarm Cause** indicates unknown errors.

   -  If yes, go to :ref:`4 <alm-19012__li11456104183119>`.
   -  If no, go to :ref:`2 <alm-19012__li5458941113112>`

#. .. _alm-19012__li5458941113112:

   On the MRS Manager home page, choose **O&M** > **Backup and Restoration** > **Backup Management**. Check whether there are success records of the backup task named **default** or other HBase metadata backup tasks that have been successfully executed.

   -  If yes, go to :ref:`3 <alm-19012__li164581941183116>`.
   -  If no, go to :ref:`4 <alm-19012__li11456104183119>`.

#. .. _alm-19012__li164581941183116:

   Use the latest backup metadata to restore the metadata of the HBase service.

**Collect fault information.**

4. .. _alm-19012__li11456104183119:

   On the MRS Manager page of the active and standby clusters, choose **O&M** > **Log** > **Download**.

5. In the **Service** area, select faulty HBase services in the required cluster.

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927334.png
