:original_name: ALM-17010.html

.. _ALM-17010:

ALM-17010 Abnormal Connection Between Oozie and HDFS
====================================================

Alarm Description
-----------------

Oozie depends on HDFS. After a task is submitted, the system checks HDFS connectivity. This alarm is generated when the service fails the check for 3 consecutive times.

This alarm is cleared when the connection between Oozie and HDFS becomes normal.

This alarm applies to MRS 3.3.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
17010    Minor          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------------+---------------------------------------------------------+
| Parameter         | Description                                             |
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

Running scheduling tasks are blocked and new scheduling tasks cannot be submitted.

Possible Causes
---------------

The HDFS service restarts, there is a fault, or the network connectivity is abnormal.

Handling Procedure
------------------

**Check the HDFS service status.**

#. In the service list on MRS Manager, check whether **Running Status** of HDFS is **Normal**.

   -  If yes, go to :ref:`5 <alm-17010__li21011035113113>`.
   -  If no, go to :ref:`2 <alm-17010__li41021352312>`.

#. .. _alm-17010__li41021352312:

   In the alarm list, check whether the "ALM-14000 HDFS Service Unavailable" alarm is generated.

   -  If yes, go to :ref:`3 <alm-17010__li16102123513112>`.
   -  If no, go to :ref:`5 <alm-17010__li21011035113113>`.

#. .. _alm-17010__li16102123513112:

   Rectify the fault by performing the operations provided for :ref:`ALM-14000 HDFS Service Unavailable <alm-14000>`.

#. Wait for several minutes and check whether the alarm **Abnormal Connection Between Oozie and HDFS** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-17010__li21011035113113>`.

**Check the connectivity between Oozie and HDFS.**

5. .. _alm-17010__li21011035113113:

   Log in to MRS Manager, choose **O&M** > **Log** > **Online Search**, select the Oozie service, and search for the keyword **[Oozie Alarm Enhancement][HDFS]** in the log. View the cause in the log, and rectify the fault. In the alarm list, check whether the alarm **Abnormal Connection Between Oozie and HDFS** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-17010__li181920381319>`.

**Collect fault information.**

6. .. _alm-17010__li181920381319:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Select **Oozie** for **Service** and click **OK**.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002416013105.png
