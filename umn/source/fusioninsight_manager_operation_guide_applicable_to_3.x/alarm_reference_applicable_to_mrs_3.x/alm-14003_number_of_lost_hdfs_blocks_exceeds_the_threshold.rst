:original_name: ALM-14003.html

.. _ALM-14003:

ALM-14003 Number of Lost HDFS Blocks Exceeds the Threshold
==========================================================

Description
-----------

The system checks the lost blocks every 30 seconds and compares the actual lost blocks with the threshold. The lost blocks indicator has a default threshold. This alarm is generated when the number of lost HDFS blocks exceeds the threshold.

To change the threshold, choose **O&M** > **Alarm >** **Thresholds** > *Name of the desired cluster* **>** **HDFS**.

If **Trigger Count** is **1**, this alarm is cleared when the value of lost HDFS blocks is less than or equal to the threshold. If **Trigger Count** is greater than **1**, this alarm is cleared when the value of lost HDFS blocks is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14003    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------+
| Name              | Meaning                                                     |
+===================+=============================================================+
| Source            | Specifies the cluster for which the alarm is generated.     |
+-------------------+-------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.     |
+-------------------+-------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.        |
+-------------------+-------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.        |
+-------------------+-------------------------------------------------------------+
| NameServiceName   | Specifies the NameService for which the alarm is generated. |
+-------------------+-------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.           |
+-------------------+-------------------------------------------------------------+

Impact on the System
--------------------

Data stored in HDFS is lost. HDFS may enter the safe mode and cannot provide write services. Lost block data cannot be restored.

Possible Causes
---------------

-  The DataNode instance is abnormal.
-  Data is deleted.

Procedure
---------

**Check the DataNode instance.**

#. On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Instance**.

#. Check whether the **Running** **Status** of all DataNode instance is **Normal**.

   -  If yes, go to :ref:`11 <alm-14003__li19356361163156>`.
   -  If no, go to :ref:`3 <alm-14003__li6471267163156>`.

#. .. _alm-14003__li6471267163156:

   Restart the DataNode instance and check whether the DataNode instance restarts successfully.

   -  If yes, go to :ref:`4 <alm-14003__li177391556152310>`.
   -  If no, go to :ref:`5 <alm-14003__li58241411163156>`.

#. .. _alm-14003__li177391556152310:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-14003__li58241411163156>`.

**Delete the damaged file.**

5.  .. _alm-14003__li58241411163156:

    On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **NameNode(Active)**. On the WebUI page of the HDFS, view the information about lost blocks.

    .. note::

       -  If a block is lost, a line in red is displayed on the WebUI.
       -  By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

6.  The user checks whether the file containing the lost data block is useful.

    .. note::

       Files generated in directories **/mr-history**, **/tmp/hadoop-yarn**, and **/tmp/logs** during MapReduce task execution are unnecessary.

    -  If yes, go to :ref:`7 <alm-14003__li7098948163156>`.
    -  If no, go to :ref:`8 <alm-14003__li2696171714538>`.

7.  .. _alm-14003__li7098948163156:

    The user checks whether the file containing the lost data block is backed up.

    -  If yes, go to :ref:`8 <alm-14003__li2696171714538>`.
    -  If no, go to :ref:`11 <alm-14003__li19356361163156>`.

8.  .. _alm-14003__li2696171714538:

    Log in to the HDFS client as user **root**. The user password is defined by the user before the installation. Contact the MRS cluster administrator to obtain the password. Run the following commands:

    -  Security mode:

       **cd** *Client installation directory*

       **source bigdata_env**

       **kinit hdfs**

    -  Normal mode:

       **su - omm**

       **cd** *Client installation directory*

       **source bigdata_env**

9.  On the node client, run **hdfs fsck / -delete** to delete the lost file. If the file where the lost block is located is a useful file, you need to write the file again to restore the data.

    .. note::

       Deleting a file or folder is a high-risk operation. Ensure that the file or folder is no longer required before performing this operation.

10. Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-14003__li19356361163156>`.

**Collect the fault information.**

11. .. _alm-14003__li19356361163156:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

12. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383960.png
