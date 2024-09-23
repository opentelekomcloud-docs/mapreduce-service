:original_name: ALM-19025.html

.. _ALM-19025:

ALM-19025 Damaged StoreFile in HBase
====================================

Alarm Description
-----------------

The system checks the **hdfs://hacluster/hbase/autocorrupt** and **hdfs://hacluster/hbase/MasterData/autocorrupt** directories on HDFS of each HBase service every 120 seconds. This alarm is generated when there are files in the directories.

This alarm is cleared when the **hdfs://hacluster/hbase/autocorrupt** and **hdfs://hacluster/hbase/MasterData/autocorrupt** directories do not exist or are empty.

This alarm applies only to MRS 3.3.0 or later.

.. note::

   **hdfs://hacluster** indicates the name of the file system used by HBase, and **/hbase** indicates the root directory of HBase in the file system. You can log in to FusionInsight Manager, choose **Cluster** > **Services** > **HBase** and click **Configuration**. Search for **fs.defaultFS** and **hbase.data.rootdir**.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
19025    Major          Yes
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

There are damaged StoreFile files in HBase, which may cause data loss.

Possible Causes
---------------

The StoreFile files are damaged.

Handling Procedure
------------------

#. Log in to FusionInsight Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19025**, and view the service in **Location**.

#. Log in to the node where the HDFS and HBase clients are installed as the client installation user and run the following commands:

   **cd** *Client installation directory*

   **source bigdata_env**

   **kinit** *Component service user* (If Kerberos authentication is disabled for the cluster (the cluster is in normal mode), skip this step.)

#. Check the damaged StoreFile file.

   -  Run the following command to check whether the **/hbase/autocorrupt** directory of HDFS is empty. If it is not, go to :ref:`4 <alm-19025__li202731117105511>`.

      **hdfs dfs -ls -R** **hdfs://hacluster/hbase/autocorrupt**

   -  Run the following command to check whether the **/hbase/MasterData/autocorrupt** directory of HDFS is empty. If it is not, go to :ref:`9 <alm-19025__li13270141719556>`.

      **hdfs dfs -ls -R** **hdfs://hacluster/hbase/MasterData/autocorrupt**

#. .. _alm-19025__li202731117105511:

   Run the following command to restore the StoreFile files in the **hdfs://hacluster/hbase/autocorrupt** directory:

   **hdfs debug recoverLease -path hdfs://hacluster/hbase/autocorrupt/**\ *Name space*\ **/**\ Table\ **/**\ Region\ **/**\ Column family\ **/**\ *StoreFile files*

#. Check whether the damaged StoreFile files are restored. If the following information is displayed, the restoration is successful:

   .. code-block::

      recoverLease SUCCEEDED on hdfs://hacluster/hbase/autocorrupt/default/h1/865665fe32db62dadada68b644359809/cf1/95f210f931ad44c99e4028470be7d292

   If yes, go to :ref:`6 <alm-19025__li1427441715510>`.

   If no, go to :ref:`9 <alm-19025__li13270141719556>`.

#. .. _alm-19025__li1427441715510:

   Run the following command to move the files back to the **hdfs://hacluster/hbase/data** directory:

   **hdfs dfs -mv hdfs://hacluster/hbase/autocorrupt/**\ *Name space*\ **/**\ Table\ **/**\ Region\ **/**\ Column family\ **/**\ *StoreFile files*\ **hdfs://hacluster/hbase/data/**\ *Name space*\ **/**\ Table\ **/**\ Region\ **/**\ Column family\ **/**\ *StoreFile files*

#. Run the following command on HBase Shell to bring the region online again:

   **hbase shell**

   **unassign'**\ *Region*\ **'**

   **assign'**\ *Region*\ **'**

#. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-19025__li13270141719556>`.

**Collect fault information.**

9.  .. _alm-19025__li13270141719556:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

11. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
