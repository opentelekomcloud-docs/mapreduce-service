:original_name: alm_12028.html

.. _alm_12028:

ALM-12028 Number of Processes in the D State on the Host Exceeds the Threshold
==============================================================================

Description
-----------

The system periodically checks the number of D state processes of user **omm** on the host every 30 seconds and compares the number with the threshold. The number of processes in the D state on the host has a default threshold. This alarm is generated when the number of processes in the D state exceeds the threshold.

This alarm is cleared when the number is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12028    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger Condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Excessive system resources are used and the service process responds slowly.

Possible Causes
---------------

The host responds slowly to I/O (disk I/O and network I/O) requests and a process is in the D state.

**Procedure**
-------------

#. Check the process that is in the D state.

   a. Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the address of the host.

   b. Log in to the node for which the alarm is generated.

   c. Run the following commands to switch the user:

      **sudo su - root**

      **su - omm**

   d. Run the following command as user **omm** to view the PID of the process that is in the D state:

      **ps -elf \| grep -v "\\[thread_checkio\\]" \| awk 'NR!=1 {print $2, $3, $4}' \| grep omm \| awk -F' ' '{print $1, $3}' \| grep D \| awk '{print $2}'**

   e. Check whether the command output is empty.

      -  If yes, the service process is running properly. Then go to :ref:`1.g <alm_12028__en-us_topic_0191813960_li49836187112011>`.
      -  If no, go to :ref:`1.f <alm_12028__en-us_topic_0191813960_li3581599211204>`.

   f. .. _alm_12028__en-us_topic_0191813960_li3581599211204:

      Switch to user **root** and run the **reboot** command to restart the alarm host.

      Restarting the host brings certain risks. Ensure that the service process runs properly after the restart.

   g. .. _alm_12028__en-us_topic_0191813960_li49836187112011:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12028__en-us_topic_0191813960_li572522141314>`.

#. .. _alm_12028__en-us_topic_0191813960_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

**Reference**
-------------

None
