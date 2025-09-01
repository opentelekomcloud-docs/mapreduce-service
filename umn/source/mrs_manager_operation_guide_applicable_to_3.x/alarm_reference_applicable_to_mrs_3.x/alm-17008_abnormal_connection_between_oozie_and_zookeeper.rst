:original_name: ALM-17008.html

.. _ALM-17008:

ALM-17008 Abnormal Connection Between Oozie and ZooKeeper
=========================================================

Alarm Description
-----------------

In HA mode, Oozie depends on ZooKeeper. This alarm is generated when the connection between Oozie and ZooKeeper is abnormal for three consecutive times.

This alarm is cleared when the connection between Oozie and ZooKeeper becomes normal.

This alarm applies to MRS 3.3.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
17008    Minor          Yes
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

Running scheduling tasks are blocked and new scheduling tasks cannot be submitted. In HA mode, the Oozie service will restart if this alarm is reported.

Possible Causes
---------------

-  The ZooKeeper service is abnormal.
-  Oozie fails to connect to ZooKeeper.

Handling Procedure
------------------

**Check the ZooKeeper service status.**

#. In the service list on MRS Manager, check whether **Running Status** of ZooKeeper is **Normal**.

   -  If yes, go to :ref:`5 <alm-17008__li571051132910>`.
   -  If no, go to :ref:`2 <alm-17008__li107100116298>`.

#. .. _alm-17008__li107100116298:

   In the alarm list, check whether **ALM-13000 ZooKeeper Service Unavailable** is reported.

   -  If yes, go to :ref:`3 <alm-17008__li197112115297>`.
   -  If no, go to :ref:`5 <alm-17008__li571051132910>`.

#. .. _alm-17008__li197112115297:

   Rectify the fault by performing the operations provided for :ref:`ALM-13000 ZooKeeper Service Unavailable <alm-13000>`.

#. Wait for several minutes and check whether the alarm **Abnormal Connection Between Oozie and ZooKeeper** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-17008__li571051132910>`.

**Check the connectivity between Oozie and ZooKeeper.**

5. .. _alm-17008__li571051132910:

   Log in to MRS Manager, choose **O&M** > **Log** > **Online Search**, select the Oozie service, and search for the keyword **[Oozie Alarm Enhancement][ZooKeeper]** in the log. View the cause in the log, and rectify the fault. In the alarm list, check whether the alarm **Abnormal Connection Between Oozie and ZooKeeper** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-17008__li113211349123620>`.

**Collect fault information.**

6. .. _alm-17008__li113211349123620:

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

.. |image1| image:: /_static/images/en-us_image_0000002415853277.png
