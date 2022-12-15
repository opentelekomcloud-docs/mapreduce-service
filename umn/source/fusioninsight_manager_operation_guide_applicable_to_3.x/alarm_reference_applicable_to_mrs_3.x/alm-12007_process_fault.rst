:original_name: ALM-12007.html

.. _ALM-12007:

ALM-12007 Process Fault
=======================

Description
-----------

This alarm is generated when the process health check module detects that the process connection status is **Bad** for three consecutive times. The process health check module checks the process status every 5 seconds.

This alarm is cleared when the process can be connected.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12007    Major          Yes
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

The service provided by the process is unavailable.

Possible Causes
---------------

-  The instance process is abnormal.
-  The disk space is insufficient.

.. note::

   If a large number of process fault alarms exist in a time segment, files in the installation directory may be deleted mistakenly or permission on the directory may be modified.

Procedure
---------

**Check whether the instance process is abnormal.**

#. .. _alm-12007__li42005517036:

   In the FusionInsight Manager portal, click **O&M > Alarm > Alarms**, click |image1| in the row where the alarm is located , and click the host name to view the host address for which the alarm is generated

#. On the **Alarms** page, check whether the :ref:`ALM-12006 Node Fault <alm-12006>` is generated.

   -  If yes, go to :ref:`3 <alm-12007__li20006517036>`.
   -  If no, go to :ref:`4 <alm-12007__li195150317036>`.

#. .. _alm-12007__li20006517036:

   Handle the alarm according to :ref:`ALM-12006 Node Fault <alm-12006>`.

#. .. _alm-12007__li195150317036:

   Log in to the host for which the alarm is generated as user **root**. Check whether the installation directory user, user group, and permission of the alarm role are correct. The user, user group, and the permission must be **omm:ficommon 750**.

   For example, the NameNode installation directory is *${BIGDATA_HOME}*\ **/FusionInsight_Current/**\ *1_8_NameNode*\ **/etc**.

   -  If yes, go to :ref:`6 <alm-12007__li3396349817036>`.
   -  If no, go to :ref:`5 <alm-12007__li3247692317036>`.

#. .. _alm-12007__li3247692317036:

   Run the following command to set the permission to **750** and **User:Group** to **omm:ficommon**:

   **chmod 750** *<folder_name>*

   **chown omm:ficommon** *<folder_name>*

#. .. _alm-12007__li3396349817036:

   Wait for 5 minutes. In the alarm list, check whether **ALM-12007 Process Fault** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12007__li2657388817036>`.

**Check whether disk space is sufficient.**

7.  .. _alm-12007__li2657388817036:

    On the FusionInsight Manager, check whether the alarm list contains **ALM-12017 Insufficient Disk Capacity**.

    -  If yes, go to :ref:`8 <alm-12007__li500135217036>`.
    -  If no, go to :ref:`11 <alm-12007__li1622379717036>`.

8.  .. _alm-12007__li500135217036:

    Rectify the fault by following the steps provided in :ref:`ALM-12017 Insufficient Disk Capacity <alm-12017>`.

9.  Wait for 5 minutes. In the alarm list, check whether **ALM-12017 Insufficient Disk Capacity** is cleared.

    -  If yes, go to :ref:`10 <alm-12007__li1723673717036>`.
    -  If no, go to :ref:`11 <alm-12007__li1622379717036>`.

10. .. _alm-12007__li1723673717036:

    Wait for 5 minutes. In the alarm list, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-12007__li1622379717036>`.

**Collect fault information.**

11. .. _alm-12007__li1622379717036:

    On the FusionInsight Manager, choose **O&M** > **Log > Download**.

12. According to the service name obtained in :ref:`1 <alm-12007__li42005517036>`, select the component and **NodeAgent** from the **Service** and click **OK**.

13. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001080201158.png
.. |image2| image:: /_static/images/en-us_image_0269383814.png
