:original_name: ALM-14029.html

.. _ALM-14029:

ALM-14029 Number of Blocks in a Replica Exceeds the Threshold
=============================================================

Description
-----------

The system checks the number of blocks in a single replica every four hours and compares the number with the threshold. There is a threshold for the number of blocks in a single replica. This alarm is generated when the actual number of blocks in a single replica exceeds the threshold.

This alarm is cleared when the number of blocks to be supplemented is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14029    Minor          Yes
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
| NameServiceName   | Specifies the NameService for which the alarm is generated. |
+-------------------+-------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.           |
+-------------------+-------------------------------------------------------------+

Impact on the System
--------------------

Replica data is prone to be lost when a node is faulty. Too many files of a single replica affect the security of the HDFS file system.

Possible Causes
---------------

-  The DataNode is faulty.
-  The disk is faulty.
-  Files are written to a single replica.

Procedure
---------

#. On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, check whether alarm **ALM-14003 Number of Lost HDFS Blocks Exceeds the Threshold** is generated.

   -  If yes, go to :ref:`2 <alm-14029__li23401293163156>`.
   -  If no, go to :ref:`3 <alm-14029__li17602112155716>`.

#. .. _alm-14029__li23401293163156:

   Rectify the fault according to the handling procedure of **ALM-14003 Number of Lost HDFS Blocks Exceeds the Threshold**. In the next detection period, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-14029__li17602112155716>`.

#. .. _alm-14029__li17602112155716:

   Check whether files of a single replica have been written into the service.

   -  If yes, go to :ref:`4 <alm-14029__li2696171714538>`.
   -  If no, go to :ref:`7 <alm-14029__li12256203224411>`.

#. .. _alm-14029__li2696171714538:

   Log in to the HDFS client as user **root**. The user password is defined by the user before the installation. Contact the MRS cluster administrator to obtain the password. Run the following commands:

   -  Security mode:

      **cd** *Client installation directory*

      **source bigdata_env**

      **kinit hdfs**

   -  Normal mode:

      **su - omm**

      **cd** *Client installation directory*

      **source bigdata_env**

#. Run the following command on the client node to increase the number of replicas for a single replica file:

   **hdfs dfs -setrep -w** *file replica number* *file name or file path*

#. In the next detection period, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-14029__li12256203224411>`.

**Collect the fault information.**

7.  .. _alm-14029__li12256203224411:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607654.png
