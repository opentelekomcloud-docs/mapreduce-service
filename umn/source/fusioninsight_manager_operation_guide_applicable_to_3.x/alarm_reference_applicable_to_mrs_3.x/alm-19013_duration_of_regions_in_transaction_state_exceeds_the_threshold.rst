:original_name: ALM-19013.html

.. _ALM-19013:

ALM-19013 Duration of Regions in transaction State Exceeds the Threshold
========================================================================

Description
-----------

The system checks the number of regions in transaction state on HBase every 300 seconds. This alarm is generated when the system detects that the duration of regions in transaction state exceeds the threshold for two consecutive times. This alarm is cleared when all timeout regions are restored.

.. note::

   If the multi-instance function is enabled in the cluster and multiple HBase service instances are installed, you need to determine the HBase service instance where the alarm is generated based on the value of **ServiceName** in **Location**. For example, if the HBase1 service is unavailable, **ServiceName=HBase1** is displayed in **Location**, and the operation object in the procedure needs to be changed from HBase to HBase1.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
19013    Major          Yes
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

Some data in the table gets lost or becomes unavailable.

Possible Causes
---------------

-  Compaction is permanently blocked.
-  The HDFS files are abnormal.

Procedure
---------

**Locate the alarm cause.**

#. On the FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, select this alarm, and view the **HostName** and **RoleName** in **Location**.

#. Choose **Cluster** > *Name of the desired cluster* > **Services > HBase**, Click the drop-down menu in the chartarea and choose **Customize >** **Service** >

   **Region in transaction count** to view **Region in transaction count over threshold**. Check whether the monitoring item detects a value in three consecutive detection periods. (The default threshold is 60 seconds.)

   -  If yes, go to :ref:`3 <alm-19013__li0444398318>`.
   -  If no, go to :ref:`7 <alm-19013__li11456104183119>`.

#. .. _alm-19013__li0444398318:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **HMaster (Active)** > **Tables** to check whether the regions of only one table transaction status time out.

   -  If yes, go to :ref:`4 <alm-19013__li1318724573113>`.
   -  If no, go to :ref:`7 <alm-19013__li11456104183119>`.

#. .. _alm-19013__li1318724573113:

   Run the **hbase hbck** command on the client and check whether the error message "No table descriptor file under hdfs://hacluster/hbase/data/default/table" is displayed.

   -  If yes, go to :ref:`5 <alm-19013__li417435203115>`.
   -  If no, go to :ref:`7 <alm-19013__li11456104183119>`.

#. .. _alm-19013__li417435203115:

   Log in to the client as user **root**. Run the following command:

   **cd** *client installation directory*

   **source bigdata_env**

   If the cluster is in security mode, run the **kinit hbase** command

   Log in to the HMaster WebUI, choose **Procedure & Locks** in the navigation tree, and check whether any process ID is in the **Waiting** state in **Procedures**. If yes, run the following command to release the procedure lock:

   **hbase hbck -j** *client installation directory*\ **/HBase/hbase/tools/hbase-hbck2-*.jar bypass -o** *pid*

   Check whether the state is in the **Bypass** state. If the procedure on the UI is always in **RUNNABLE(Bypass)** state, perform an active/standby switchover. Run the **assigns** command to bring the region online again.

   **hbase hbck -j** *client installation directory*\ **/HBase/hbase/tools/hbase-hbck2-*.jar assigns -o** *regionName*

#. Repeat :ref:`4 <alm-19013__li1318724573113>`. Run the **hbase hbck** command on the client and check whether the error message "No table descriptor file under hdfs://hacluster/hbase/data/default/table" is displayed.

   -  If yes, go to :ref:`7 <alm-19013__li11456104183119>`.
   -  If no, no further action is required.

**Collect fault information.**

7.  .. _alm-19013__li11456104183119:

    On the FusionInsight Manager page of the active and standby clusters, choose **O&M** > **Log** > **Download**.

8.  In the **Service** area, select faulty HBase services in the required cluster.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417429.png
