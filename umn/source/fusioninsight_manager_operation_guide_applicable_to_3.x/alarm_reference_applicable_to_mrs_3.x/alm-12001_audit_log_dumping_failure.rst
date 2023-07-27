:original_name: ALM-12001.html

.. _ALM-12001:

ALM-12001 Audit Log Dumping Failure
===================================

Description
-----------

Cluster audit logs need to be dumped on a third-party server due to the local historical data backup policy. The system starts to check the dump server at 3 a.m. every day. If the dump server meets the configuration conditions, audit logs can be successfully dumped. This alarm is generated when the audit log dump fails if the disk space of the dump directory on the third-party server is insufficient or a user changes the username, password, or dump directory of the dump server.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12001    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

System can store a maximum of only 50 dump files locally. If the fault persists on the dump server, the local audit logs may be lost.

Possible Causes
---------------

-  The network connection is abnormal.
-  The username, password, or dump directory of the dump server does not meet the configuration conditions.
-  The disk space of the dump directory is insufficient.

Procedure
---------

**Check whether the network connection is normal.**

#. On the FusionInsight Manager home page, choose **Audit > Configurations**.

#. Check whether the SFTP IP on the dump configuration page is valid.

   Log in to the node where Manager is located as user **root** and run the **ping** command to check whether the network connection between the SFTP server and the cluster is normal.

   -  If yes, go to :ref:`5 <alm-12001__li33093593154533>`.
   -  If no, go to :ref:`3 <alm-12001__li64797305153659>`.

#. .. _alm-12001__li64797305153659:

   Repair the network connection, reset the SFTP password, and click **OK**.

#. Wait for 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-12001__li33093593154533>`.

**Check whether the username, password, or dump directory are correct.**

5. .. _alm-12001__li33093593154533:

   On the dump configuration page, check whether the username, password, and dump directory of the third-party server are correct.

   -  If yes, go to :ref:`8 <alm-12001__li56273719154547>`.
   -  If no, go to :ref:`6 <alm-12001__li63335387154533>`.

6. .. _alm-12001__li63335387154533:

   Change the username, password, or dump directory, reset the SFTP password and click **OK**.

7. Wait for 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-12001__li56273719154547>`.

**Check whether the disk space of the dump directory is sufficient.**

8.  .. _alm-12001__li56273719154547:

    Log in to the third-party server as user **root** and run the **df** command to check whether the disk space of the dump directory of the third-party server exceeds 100 MB.

    -  If yes, go to :ref:`11 <alm-12001__li37575023154554>`.
    -  If no, go to :ref:`9 <alm-12001__li61877356154547>`.

9.  .. _alm-12001__li61877356154547:

    Expand disk space capacity for the third-party server, Reset the SFTP password and click **OK**

10. Wait for 2 minutes, view real-time alarms and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-12001__li37575023154554>`.

**Reset the dump rule.**

11. .. _alm-12001__li37575023154554:

    On the FusionInsight Manager home page, choose **Audit > Configurations**.

12. Reset dump rules, set the parameters properly, and click **OK**.

13. Wait for 2 minutes, view real-time alarms and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-12001__li5991045915463>`.

**Collect fault information.**

14. .. _alm-12001__li5991045915463:

    On the FusionInsight Manager, choose **O&M** > **Log > Download**.

15. Select **OmmServer** from the **Service** and click **OK**.

16. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

17. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807597.png
