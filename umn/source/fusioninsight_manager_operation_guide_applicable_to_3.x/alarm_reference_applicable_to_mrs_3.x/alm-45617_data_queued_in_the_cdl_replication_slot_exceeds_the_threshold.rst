:original_name: ALM-45617.html

.. _ALM-45617:

ALM-45617 Data Queued in the CDL Replication Slot Exceeds the Threshold
=======================================================================

Description
-----------

If a large number of write-ahead logs (WALs) are stacked in the PostgreSQL database, the PostgreSQL disk space may be used up. The system checks whether the amount of data queued in the replication slot configured for a CDL job exceeds the threshold every 5 minutes. This alarm is generated when the amount of data queued in the replication slot exceeds the threshold. This alarm is cleared when the number of data queued in the replication slot falls below the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45617    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+---------------------------------------------------------------------------+
| Name        | Meaning                                                                   |
+=============+===========================================================================+
| Source      | Specifies the cluster for which the alarm is generated.                   |
+-------------+---------------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.                   |
+-------------+---------------------------------------------------------------------------+
| JobName     | Specifies the job for which the alarm is generated.                       |
+-------------+---------------------------------------------------------------------------+
| DBName      | Specifies the database for which the alarm is generated.                  |
+-------------+---------------------------------------------------------------------------+
| SlotName    | Specifies the database replication slot for which the alarm is generated. |
+-------------+---------------------------------------------------------------------------+
| Lag         | Specifies the data queued in the slot.                                    |
+-------------+---------------------------------------------------------------------------+

Impact on the System
--------------------

WALs are continuously accumulated in the source PostgreSQL database, causing the disk space of the source database to be used up.

Possible Causes
---------------

The CDL job is abnormal, and data processing stops; the source database is updated quickly, and CDL data processing is slow.

Procedure
---------

#. Log in to FusionInsight Manager as a user who has the CDL job creation or administrator permission.

#. .. _alm-45617__li118681057135018:

   Choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**, click |image1| in the row where **Alarm ID** is **45617**, and view the name of the job for which this alarm is generated in **Location**.

#. Check whether **ALM-45616 CDL Job Execution Exception** is displayed in the alarm list.

   -  If yes, handle the alarm by performing operations provided for **ALM-45616 CDL Job Execution Exception**.
   -  If no, go to :ref:`4 <alm-45617__li28682575508>`.

#. .. _alm-45617__li28682575508:

   Choose **Cluster** > **Services** > **CDL**. Click the link next to **CDLService UI** to go to the CDL web UI and check whether the job is displayed in the job list based on its name obtained in :ref:`2 <alm-45617__li118681057135018>`.

   -  If yes, check whether the job is abnormal.

      -  If it is abnormal, go to :ref:`5 <alm-45617__li15868185712504>`.
      -  If it is not, data processing is slow. Contact O&M personnel.

   -  If no, go to :ref:`7 <alm-45617__li1486755735016>`.

#. .. _alm-45617__li15868185712504:

   Click **Abnormal** or **Failed** in the row where the job is located and rectify the fault based on the error information displayed on the page.

#. After rectifying the fault, run the job again and check whether the job can be executed successfully.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-45617__li1486755735016>`.

**Collect the fault information.**

7.  .. _alm-45617__li1486755735016:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Select **CDL** in the required cluster for **Service**.

9.  Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is cleared when the amount of data queued in the replication slot is less than the threshold. You do not need to manually clear the alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927521.png
.. |image2| image:: /_static/images/en-us_image_0000001582807573.png
