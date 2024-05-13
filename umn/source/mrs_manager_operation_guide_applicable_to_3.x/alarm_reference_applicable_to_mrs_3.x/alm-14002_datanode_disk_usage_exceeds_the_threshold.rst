:original_name: ALM-14002.html

.. _ALM-14002:

ALM-14002 DataNode Disk Usage Exceeds the Threshold
===================================================

Description
-----------

The system checks the DataNode disk usage every 30 seconds and compares the actual disk usage with the threshold. A default threshold range is provided for the DataNode disk usage. This alarm is generated when the DataNode disk usage exceeds the threshold.

To change the threshold, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **HDFS**.

If **Trigger Count** is **1**, this alarm is cleared when the DataNode disk usage is less than or equal to the threshold. If **Trigger Count** is greater than **1**, this alarm is cleared when the DataNode disk usage is less than or equal to 80% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14002    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Meaning                                                 |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

Insufficient disk space will impact data write to HDFS.

Possible Causes
---------------

-  The disk space configured for the HDFS cluster is insufficient.
-  Data skew occurs among DataNodes.

Procedure
---------

**Check whether the cluster disk capacity is full.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether the **ALM-14001 HDFS Disk Usage Exceeds the Threshold** alarm exists.

   -  If yes, go to :ref:`2 <alm-14002__li48847933162749>`.
   -  If no, go to :ref:`4 <alm-14002__li49504103162749>`.

#. .. _alm-14002__li48847933162749:

   Handle the alarm by following the instructions in **ALM-14001 HDFS Disk Usage Exceeds the Threshold** and check whether the alarm is cleared.

   -  If yes, go to :ref:`3 <alm-14002__li5500455162749>`.
   -  If no, go to :ref:`11 <alm-14002__li17443443162749>`.

#. .. _alm-14002__li5500455162749:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14002__li49504103162749>`.

**Check the balance status of DataNodes.**

4.  .. _alm-14002__li49504103162749:

    On MRS Manager, choose **Hosts**. Check whether the number of DataNodes on each rack is almost the same. If the difference is large, adjust the racks to which DataNodes belong to ensure that the number of DataNodes on each rack is almost the same. Restart the HDFS service for the settings to take effect.

5.  Choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS**.

6.  In the **Basic Information** area, click **NameNode(Active)**. The HDFS web UI is displayed.

    .. note::

       By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

7.  In the **Summary** area of the HDFS web UI, check whether the value of **Max** is 10% greater than that of **Median** in **DataNodes usages**.

    -  If yes, go to :ref:`8 <alm-14002__li25048823162749>`.
    -  If no, go to :ref:`11 <alm-14002__li17443443162749>`.

8.  .. _alm-14002__li25048823162749:

    Balance skewed data in the cluster. Log in to the MRS client as user **root**. If the cluster is in normal mode, run the **su - omm** command to switch to user **omm**. Run the **cd** command to go to the client installation directory and run the **source bigdata_env** command. If the cluster uses the security mode, perform security authentication. Run **kinit hdfs** and enter the password as prompted. Obtain the password from the MRS cluster administrator.

9.  Run the following command to balance data distribution:

    **hdfs balancer -threshold 10**

10. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-14002__li17443443162749>`.

**Collect the fault information.**

11. .. _alm-14002__li17443443162749:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

12. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927350.png
