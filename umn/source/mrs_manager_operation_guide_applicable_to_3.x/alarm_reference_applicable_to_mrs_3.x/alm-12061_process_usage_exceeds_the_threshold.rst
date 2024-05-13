:original_name: ALM-12061.html

.. _ALM-12061:

ALM-12061 Process Usage Exceeds the Threshold
=============================================

Description
-----------

The system checks the usage of the omm process every 30 seconds. Users can run the **ps -o nlwp, pid, args, -u omm \| awk '{sum+=$1} END {print "", sum}'** command to obtain the number of concurrent processes of user **omm**. Run the **ulimit -u**\ command to obtain the maximum number of processes that can be simultaneously opened by user **omm**. Divide the number of concurrent processes by the maximum number to obtain the process usage of user **omm**. The process usage has a default threshold. This alarm is generated when the process usage exceeds the threshold.

If **Trigger Count** is **3** and the process usage is less than or equal to the threshold, this alarm is cleared. If **Trigger Count** is greater than **1**\ and the process usage is less than or equal to 90% of the threshold, this alarm is cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12061    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------+
| Name              | Meaning                                                           |
+===================+===================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.           |
+-------------------+-------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                 |
+-------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

-  Switch to user **omm** fails.
-  New omm process cannot be created.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The maximum number of processes (including threads) that can be concurrently opened by user **omm** is inappropriate.
-  An excessive number of threads are opened at the same time.

Procedure
---------

**Check whether the alarm threshold or alarm hit number is properly configured.**

#. On the MRS Manager, change the alarm threshold and **Trigger Count** based on the actual CPU usage.

   Specifically, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Host**> **Process** > **omm Process Usage** to change Trigger Count.

   .. note::

      The alarm is generated when the process usage exceeds the threshold for the times specified by **Trigger Count**.

   Set the alarm threshold based on the actual process usage. To check the process usage, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Host**> **Process** > **omm Process Usage**, as shown in :ref:`Figure 1 <alm-12061__fig437414238216>`.

   .. _alm-12061__fig437414238216:

   .. figure:: /_static/images/en-us_image_0000001583127621.png
      :alt: **Figure 1** Setting an alarm threshold

      **Figure 1** Setting an alarm threshold

#. 2 minutes later, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`3 <alm-12061__li936717234216>`.

**Check whether the maximum number of processes (including threads) opened by user omm is appropriate.**

3. .. _alm-12061__li936717234216:

   In the alarm list on MRS Manager, locate the row that contains the alarm, and view the IP address of the host for which the alarm is generated.

4. Log in to the host where the alarm is generated as user **root**.

5. Run the **su - omm** command to switch to user **omm**.

6. Run the **ulimit -u** command to obtain the maximum number of threads that can be concurrently opened by user **omm** and check whether the number is greater than or equal to 60000.

   -  If it is, go to :ref:`8 <alm-12061__li293443912213>`.
   -  If it is not, go to :ref:`7 <alm-12061__li8367152314217>`.

7. .. _alm-12061__li8367152314217:

   Run the **ulimit -u 60000** command to change the maximum number to 60000. Two minutes later, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`12 <alm-12061__li1668345092117>`.

**Check whether an excessive number of processes are opened at the same time.**

8.  .. _alm-12061__li293443912213:

    In the alarm list on MRS Manager, locate the row that contains the alarm, and view the IP address of the host for which the alarm is generated.

9.  Log in to the host where the alarm is generated as user **root**.

10. Run the **ps -o nlwp, pid, lwp, args, -u omm|sort -n** command to check the numbers of threads used by the system. The result is sorted based on the thread number. Analyze the top 5 thread numbers and check whether the threads are incorrectly used. If they are, contact maintenance personnel to rectify the fault. If they are not, run the **ulimit -u** command to change the maximum number to be greater than 60000.

11. Five minutes later, check whether the alarm is cleared.

    -  If it is, no further action is required.
    -  If it is not, go to :ref:`12 <alm-12061__li1668345092117>`.

**Collect fault information.**

12. .. _alm-12061__li1668345092117:

    On the MRS Manager home page of the active clusters, choose **O&M** > **Log** > **Download**.

13. Select **OmmServer** and **NodeAgent** from the **Service** and click **OK**.

14. Click |image1| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 10 minutes before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

15. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927646.png
