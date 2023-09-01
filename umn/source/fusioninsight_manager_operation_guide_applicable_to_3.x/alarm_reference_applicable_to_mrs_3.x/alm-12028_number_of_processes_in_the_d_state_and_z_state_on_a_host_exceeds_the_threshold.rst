:original_name: ALM-12028.html

.. _ALM-12028:

ALM-12028 Number of Processes in the D State and Z State on a Host Exceeds the Threshold
========================================================================================

Description
-----------

The system checks the number of processes in the D stateand Z state of user **omm** on the host every 30 seconds and compares the actual number with the threshold. The number of processes in the D state and Z state on the host has a default threshold range. This alarm is generated when the number of processes exceeds the threshold.

This alarm is cleared when the **Trigger Count** is **1** and the total number of processes in the D state and Z state of user **omm** on the host does not exceed the threshold. This alarm is cleared when the **Trigger Count** is greater than **1** and the total number of processes in the D state and Z state of user **omm** on the host is less than or equal to 90% of the threshold.

.. note::

   The function of checking the number of processes in the Z state on the host applies to MRS 3.2.0 or later.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12028    Major          Yes
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

Excessive system resources are used and service processes respond slowly.

Possible Causes
---------------

The host responds slowly to I/O (disk I/O and network I/O) requests and some processes are in the D state and Z state.

Procedure
---------

**Check the processes in the D state** **and Z state.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and click |image1| to view the IP address of the host for which the alarm is generated.

#. Log in to the host for which the alarm is generated as user **root**. () Then run the **su - omm** command to switch to user **omm**.

#. Run the following command as user **omm** to view the PID of the process that is in the D state and Z state:

   **ps -elf \| grep -v "\\[thread_checkio\\]" \| awk 'NR!=1 {print $2, $3, $4}' \| grep omm \| awk -F' ' '{print $1, $3}' \| grep -E "Z|D" \| awk '{print $2}'**

#. Check whether the command output is empty.

   -  If yes, the service process is running properly. Then go to :ref:`6 <alm-12028__li2701143291049>`.
   -  If no, go to :ref:`5 <alm-12028__li573000391049>`.

#. .. _alm-12028__li573000391049:

   Switch to user **root** and run the **reboot** command to restart the host for which the alarm is generated. (Restarting a host is risky. Ensure that the service process is normal after the restart.)

#. .. _alm-12028__li2701143291049:

   Check whether the alarm is cleared 5 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12028__li4177630091049>`.

**Collect the fault information.**

7.  .. _alm-12028__li4177630091049:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Select **OMS** for **Service** and click **OK**.

9.  Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448262.png
.. |image2| image:: /_static/images/en-us_image_0000001583087581.png
