:original_name: ALM-19026.html

.. _ALM-19026:

ALM-19026 Damaged WAL Files in HBase
====================================

Alarm Description
-----------------

The system checks the **hdfs://hacluster/hbase/corrupt** directory on the HDFS of each HBase service every 120 seconds. This alarm is generated when there are WAL files in the **/hbase/corrupt** directory.

This alarm is cleared when the **/hbase/corrupt** directory does not exist or does not contain WAL files.

This alarm applies only to MRS 3.3.0 or later.

.. note::

   **hdfs://hacluster** indicates the name of the file system used by HBase, and **/hbase** indicates the root directory of HBase in the file system. You can log in to FusionInsight Manager, choose **Cluster** > **Services** > **HBase** and click **Configuration**. Search for **fs.defaultFS** and **hbase.data.rootdir**.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
19026    Major          Yes
======== ============== ============

Alarm Parameters
----------------

=========== =======================================================
Parameter   Description
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

There are damaged WAL files in HBase, which may cause data loss.

Possible Causes
---------------

The WAL files are damaged.

Handling Procedure
------------------

#. Log in to FusionInsight Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19026**, and view the service in **Location**.

#. Log in to the node where the HDFS clients are installed as the client installation user and run the following commands:

   **cd** *Client installation directory*

   **source bigdata_env**

   **kinit** *Component service user* (If Kerberos authentication is disabled for the cluster (the cluster is in normal mode), skip this step.)

#. Run the following command to check the damaged WAL files and go to :ref:`4 <alm-19026__li135201823182014>`:

   **hdfs dfs -ls** **hdfs://hacluster/hbase/corrupt/*%2C\***

**Collect fault information.**

4. .. _alm-19026__li135201823182014:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

6. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
