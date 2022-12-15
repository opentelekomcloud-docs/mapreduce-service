:original_name: ALM-12085.html

.. _ALM-12085:

ALM-12085 Service Audit Log Dump Failure
========================================

Description
-----------

The system dumps service audit logs at 03:00 every day and stores them on the OMS node. This alarm is generated when the dump fails. This alarm is cleared when the next dump succeeds.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12085    Minor          Yes
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

The service audit logs may be lost.

Possible Causes
---------------

-  The service audit logs are oversized.
-  The OMS backup storage space is insufficient.
-  The storage space of a host where the service is located is insufficient.

Procedure
---------

**Check whether the service audit logs are oversized.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and view the IP address of the host and additional information for which the alarm is generated.

#. Log in to the host where the alarm is generated as user **root**.

#. Run the **vi ${BIGDATA_LOG_HOME}/controller/scriptlog/getLogs.log** command to check whether the keyword "LOG SIZE is more than 5000MB" can be searched.

   -  If it can, go to :ref:`4 <alm-12085__li1525114552513>`.
   -  If it cannot, go to :ref:`5 <alm-12085__li17248145525118>`.

#. .. _alm-12085__li1525114552513:

   Check whether the oversized service audit logs are caused by exceptions.

**The OMS backup storage space is insufficient.**

5.  .. _alm-12085__li17248145525118:

    Run the **vi ${BIGDATA_LOG_HOME}/controller/scriptlog/getLogs.log** command to check whether the keyword "Collect log failed, too many logs on" can be searched.

    -  If it can, obtain the host IP address following the keyword "Collect log failed, too many logs on", and go to :ref:`6 <alm-12085__li1324811555511>`.
    -  If it cannot, go to :ref:`11 <alm-12085__li274114665213>`.

6.  .. _alm-12085__li1324811555511:

    Log in to the host with the IP address obtained in :ref:`5 <alm-12085__li17248145525118>` as user **root**.

7.  Run the **vi {BIGDATA_LOG_HOME}/nodeagent/scriptlog/collectLog.log** command to check whether the keyword "log size exceeds" can be searched.

    -  If it can, go to :ref:`9 <alm-12085__li1411119282589>`.
    -  If it cannot, go to :ref:`8 <alm-12085__li1532033151617>`.

8.  .. _alm-12085__li1532033151617:

    Check whether the alarm additional information contains the keyword "no enough space".

    -  If yes, go to :ref:`9 <alm-12085__li1411119282589>`.
    -  If no, go to\ :ref:`11 <alm-12085__li274114665213>`.

9.  .. _alm-12085__li1411119282589:

    Perform the following operations to expand the disk capacity or reduce the maximum number of audit log backups:

    -  Expand the capacity of the OMS node\ *.*

    -  Run the following command to edit the file and decrease the value of **MAX_NUM_BK_AUDITLOG**.

       **vi ${CONTROLLER_HOME}/etc/om/componentsauditlog.properties**

10. In the next execution period, 03:00, check whether the alarm is cleared.

    -  If it is, no further action is required.
    -  If it is not, go to :ref:`11 <alm-12085__li274114665213>`.

**Check whether the space of the host where the service is located is insufficient.**

11. .. _alm-12085__li274114665213:

    Run the **vi ${BIGDATA_LOG_HOME}/controller/scriptlog/getLogs.log** command to check whether the keyword "Collect log failed, no enough space on *hostIp*" can be searched.

    -  If it can, obtain the IP address of the abnormal host and go to :ref:`12 <alm-12085__li137411362525>`.
    -  If it cannot, go to :ref:`15 <alm-12085__li1181415165216>`.

12. .. _alm-12085__li137411362525:

    Log in to the host with the IP address obtained as user **root**, and run the **df "$BIGDATA_HOME/tmp" -lP \| tail -1 \| awk '{print ($4/1024)}'** command to obtain the remaining space of the host log directory. Check whether the value is less than 1000 MB.

    -  If it is, go to :ref:`13 <alm-12085__li274186155216>`.
    -  If it is not, go to :ref:`15 <alm-12085__li1181415165216>`.

13. .. _alm-12085__li274186155216:

    Expand the capacity of the node

14. In the next execution period, 03:00, check whether the alarm is cleared.

    -  If it is, no further action is required.
    -  If it is not, go to :ref:`15 <alm-12085__li1181415165216>`.

**Collect fault information.**

15. .. _alm-12085__li1181415165216:

    On FusionInsight Manager, choose **O&M**> **Log** > **Download**.

16. Select **Controller** for **Service** and click **OK**.

17. Click |image1| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 10 minutes before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

18. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383932.png
