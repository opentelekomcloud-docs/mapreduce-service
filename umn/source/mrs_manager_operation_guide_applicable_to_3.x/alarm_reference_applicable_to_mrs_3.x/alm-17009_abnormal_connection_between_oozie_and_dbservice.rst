:original_name: ALM-17009.html

.. _ALM-17009:

ALM-17009 Abnormal Connection Between Oozie and DBService
=========================================================

Alarm Description
-----------------

Oozie depends on DBService. After a task is submitted, the system checks DBService connectivity. This alarm is generated when the service fails the check for 10 consecutive times.

This alarm is cleared when the connection between Oozie and DBService becomes normal.

This alarm applies to MRS 3.3.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
17009    Minor          Yes
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

-  The DBService service is abnormal.
-  Oozie fails to connect to DBService.

Handling Procedure
------------------

**Check the DBService status.**

#. In the service list on MRS Manager, check whether **Running Status** of DBService is **Normal**.

   -  If yes, go to :ref:`5 <alm-17009__li1877010345257>`.
   -  If no, go to :ref:`2 <alm-17009__li1691284919247>`.

#. .. _alm-17009__li1691284919247:

   In the alarm list, check whether **ALM-27001 DBService Service Unavailable** is reported.

   -  If yes, go to :ref:`3 <alm-17009__li139121449162411>`.
   -  If no, go to :ref:`5 <alm-17009__li1877010345257>`.

#. .. _alm-17009__li139121449162411:

   Rectify the fault by performing the operations provided for :ref:`ALM-27001 DBService Service Unavailable <alm-27001>`.

#. Wait for several minutes and check whether the alarm **Abnormal Connection Between Oozie and DBService** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-17009__li1877010345257>`.

**Check the connectivity between Oozie and DBService.**

5. .. _alm-17009__li1877010345257:

   Log in to MRS Manager, choose **O&M** > **Log** > **Online Search**, select the Oozie service, and search for the keyword **[Oozie Alarm Enhancement][DB Service]** in the log. View the cause in the log, and rectify the fault. In the alarm list, check whether the alarm **Abnormal Connection Between Oozie and DBService** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-17009__li16610154216258>`.

**Collect fault information.**

6. .. _alm-17009__li16610154216258:

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

.. |image1| image:: /_static/images/en-us_image_0000002382453800.png
