:original_name: ALM-45432.html

.. _ALM-45432:

ALM-45432 ClickHouse User Synchronization Process Fails
=======================================================

Description
-----------

The system checks the status of the ClickHouse user role synchronization process every 5 minutes. This alarm is generated when the system detects that the ClickHouse user role synchronization process is faulty or the user role synchronization fails.

This alarm is automatically cleared when the ClickHouse user role synchronization process or function becomes normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45432    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Some ClickHouseServer instances are unavailable.

Possible Causes
---------------

-  The ClickHouse user role synchronization process is not started properly or exits abnormally.
-  The ClickHouse user role synchronization process fails to synchronize user role information because the LdapServer service is faulty.

Procedure
---------

**Check whether the ClickHouse user role synchronization process is normal.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, search for **ALM-45432 ClickHouse User Synchronization Process Fails**.

#. Check the host name and additional information in the alarm details.

   -  If the additional information is "Process clickhouse-ugsync is not exit.", go to :ref:`3 <alm-45432__li172317474333>`.
   -  If the additional information is "Process clickhouse-ugsync sync user failed.", go to :ref:`6 <alm-45432__li622471521412>`.

#. .. _alm-45432__li172317474333:

   Log in to the faulty host as user **omm** and run the following command to check whether the ClickHouse user role synchronization process is normal:

   **ps -ef \| grep 'clickhouse-ugsync'**

   Abnormal result of the synchronization process:

   .. code-block:: console

      [omm@server-2110081635-0001 ~]$ ps -ef | grep 'clickhouse-ugsync'
      omm      20104 13146  0 15:57 pts/7    00:00:00 grep --color=auto clickhouse-ugsync

   -  If yes, the alarm is automatically cleared. If the alarm is cleared, no further action is required. If the alarm persists, go to :ref:`8 <alm-45432__li1272184713332>`.
   -  If no, go to :ref:`4 <alm-45432__li177241147103317>`.

#. .. _alm-45432__li177241147103317:

   Log in to the faulty host as user **omm** and run the following command to check whether the crontab daemon task is correctly configured:

   **crontab -l**

   Normal setting of the crontab daemon task:

   .. code-block::

      */5 * * * * bash /xxxxx/clickhouse_ugsync_check.sh >/dev/null 2>&1

   -  If yes, check whether the alarm is cleared 5 minutes later. If the alarm is cleared, no further action is required. If the alarm persists, go to :ref:`8 <alm-45432__li1272184713332>`.
   -  If no, go to :ref:`5 <alm-45432__li672411477337>`.

#. .. _alm-45432__li672411477337:

   Log in to FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse**. On the page that is displayed, click the **Instance** tab. On this tab page, find the abnormal ClickHouseServer instance based on the fault information, and restart it. Wait for 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45432__li622471521412>`.

**Check whether the LdapServer service is normal.**

6. .. _alm-45432__li622471521412:

   Log in to FusionInsight Manager, choose **Cluster** > **Services**, and check whether **Running Status** of LdapServer is **Normal**.

   -  If yes, go to :ref:`8 <alm-45432__li1272184713332>`.
   -  If no, go to :ref:`7 <alm-45432__li18742173311518>`.

7. .. _alm-45432__li18742173311518:

   Handle the LdapServer service unavailable alarm according to ALM-25000 LdapServer Service Unavailable.

   After **Running Status** of LdapServer becomes **Normal**, check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45432__li1272184713332>`.

**Collect fault information.**

8.  .. _alm-45432__li1272184713332:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

9.  Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **ClickHouseServer** for the target cluster.

10. Expand the **Hosts** list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607798.png
