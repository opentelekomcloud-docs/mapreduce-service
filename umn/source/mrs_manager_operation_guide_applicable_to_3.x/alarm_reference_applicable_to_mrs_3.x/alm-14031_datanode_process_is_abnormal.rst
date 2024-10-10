:original_name: ALM-14031.html

.. _ALM-14031:

ALM-14031 DataNode Process Is Abnormal
======================================

Alarm Description
-----------------

The DataNode process checks the process status every 20 seconds. This alarm is generated when the process status is abnormal and does not recover for a long time.

This alarm is cleared when the process status recovers.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
14031    Major          Yes
======== ============== ============

Alarm Parameters
----------------

=========== =======================================================
Parameter   Description
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

If the process status is abnormal, the process cannot provide services properly. As a result, the entire service may become abnormal.

Possible Causes
---------------

The host responds slowly to I/O (disk I/O and network I/O) requests and some processes are in the D state and Z state. The process may also be suspended and enter the T state.

Handling Procedure
------------------

**Check whether the process is in the D, Z, or T state.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms**. Wait for about 10 minutes and check whether the alarm is automatically cleared.

   -  If the alarm is not in the list, no further action is required.
   -  If the alarm is in the list, view the alarm details and record the IP address of the host where the alarm is generated. Run the command in :ref:`2 <alm-14031__li162831544134616>`.

#. .. _alm-14031__li162831544134616:

   Log in to the host where the alarm is generated as the **root** user and run the **su - omm** command to switch to the **omm** user.

#. Run the following command to check the process state:

   **ps ww -eo stat,cmd\| grep -w org.apache.hadoop.hdfs.server.datanode.DataNode \| grep -v grep \| awk '{print$1}'**

#. Check whether the command output contains any abnormal state (D, Z, or T).

   -  If the output contains any abnormal state, go to :ref:`5 <alm-14031__li39471558560>`.
   -  If the output does not contain abnormal states, go to :ref:`7 <alm-14031__li14805191513412>`.

#. .. _alm-14031__li39471558560:

   Switch to user **root** and run the **reboot** command to restart the host for which the alarm is generated. (Restarting a host is risky. Ensure that the service process is normal after the restart.)

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If the alarm is cleared, no further action is required.
   -  If the alarm fails to be cleared, go to :ref:`7 <alm-14031__li14805191513412>`.

**Collect fault information.**

7.  .. _alm-14031__li14805191513412:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
