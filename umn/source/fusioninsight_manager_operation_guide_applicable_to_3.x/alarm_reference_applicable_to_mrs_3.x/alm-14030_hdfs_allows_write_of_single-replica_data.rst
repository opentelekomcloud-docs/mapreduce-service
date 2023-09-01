:original_name: ALM-14030.html

.. _ALM-14030:

ALM-14030 HDFS Allows Write of Single-Replica Data
==================================================

Description
-----------

This alarm is generated when **dfs.single.replication.enable** is set to **true**, indicating that HDFS is configured to allow write of single-replica data.

This alarm is cleared when this function is disabled on HDFS.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14030    Warning        Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

If this configuration is enabled on the server and the number of HDFS replicas configured on the client is 1, single-replica data can be written to HDFS. Data of a single replica may be lost. Therefore, the system does not allow write of single-replica data by default. If a service requires single-replica data write to a directory, modify the HDFS configuration item **dfs.single.replication.exclude.pattern**.

Possible Causes
---------------

The HDFS configuration item **dfs.single.replication.enable** is set to **true**.

Procedure
---------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **HDFS**. On the page that is displayed, click the **Configurations** tab then the **All Configurations** sub-tab.
#. Search for **dfs.single.replication.enable** in the search box, change the value of the configuration item to **false**, and click **Save**.
#. Wait for about 10 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14030__li5733165943316>`.

**Collect fault information.**

4. .. _alm-14030__li5733165943316:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807773.png
