:original_name: ALM-14001.html

.. _ALM-14001:

ALM-14001 HDFS Disk Usage Exceeds the Threshold
===============================================

Description
-----------

The system checks the HDFS disk usage every 30 seconds and compares the actual HDFS disk usage with the threshold. The HDFS disk usage indicator has a default threshold, this alarm is generated when the value of the disk usage of a Hadoop distributed file system (HDFS) indicator exceeds the threshold.

To change the threshold, choose **O&M** > **Alarm >** **Thresholds** > *Name of the desired cluster* **>** **HDFS**.

When the **Trigger Count** is 1, this alarm is cleared when the value of the disk usage of HDFS cluster indicator is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the value of the disk usage of HDFS cluster indicator is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14001    Major          Yes
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
| NameServiceName   | Specifies the NameService for which the alarm is generated.                                                                  |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Writing Hadoop distributed file system (HDFS) data is affected.

Possible Causes
---------------

The disk space configured for the HDFS cluster is insufficient.

Procedure
---------

**Check the disk capacity and delete unnecessary files.**

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS**.

#. Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **Disk**, and select **Percentage of HDFS Capacity** to check whether the HDFS disk usage exceeds the threshold (80% by default).

   -  If yes, go to :ref:`3 <alm-14001__li25340212162555>`.
   -  If no, go to :ref:`11 <alm-14001__li18825614162555>`.

#. .. _alm-14001__li25340212162555:

   In the **Basic Information** area, click the **NameNode(Active)** of the failure NameService and the HDFS WebUI page is displayed.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

#. On the HDFS web user interface (WebUI), click **Datanodes** tab. In the **Block pool used** column, view the disk usage of all DataNodes to check whether the disk usage of any DataNode exceeds the threshold.

   -  If yes, go to :ref:`6 <alm-14001__li13663615162555>`.
   -  If no, go to :ref:`11 <alm-14001__li18825614162555>`.

#. Log in to the MRS client node as user **root**.

#. .. _alm-14001__li13663615162555:

   Run **cd /opt/client** to switch to the client installation directory, and run **source bigdata_env**. If the cluster uses the security mode, perform security authentication. Run **kinit hdfs** and enter the password as prompted. Please obtain the password from the administrator.

#. Run the **hdfs dfs -rm -r** *file or directory* command to delete unnecessary files.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14001__li35348823162555>`.

**Expand the system.**

9.  .. _alm-14001__li35348823162555:

    Expand the disk capacity.

10. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-14001__li18825614162555>`.

**Collect fault information.**

11. .. _alm-14001__li18825614162555:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

12. Select the following nodes in the required cluster from the **Service**:

    -  ZooKeeper
    -  HDFS

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383958.png
