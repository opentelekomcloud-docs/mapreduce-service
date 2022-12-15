:original_name: alm_12027.html

.. _alm_12027:

ALM-12027 Host PID Usage Exceeds the Threshold
==============================================

Description
-----------

The system checks the PID usage every 30 seconds and compares the actual PID usage with the default threshold. This alarm is generated when the PID usage exceeds the threshold.

This alarm is cleared when the host PID usage is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12027    Major          Yes
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

No PID is available for new processes and service processes are unavailable.

Possible Causes
---------------

Too many processes are running on the node. You need to increase the value of **pid_max**. The system is abnormal.

Procedure
---------

#. Increase the value of **pid_max**.

   a. On the MRS cluster details page, click the alarm from the real-time alarm list. In the **Alarm Details** area, obtain the IP address of the host for which the alarm is generated.

   b. Log in to the node for which the alarm is generated.

   c. Run the **cat /proc/sys/kernel/pid_max** command to check the value of **pid_max**.

   d. If the PID usage exceeds the threshold, run the following command to double the value of **pid_max**:

      **echo** *New pid_max value* **> /proc/sys/kernel/pid_max**

      Example:

      **echo 65536 > /proc/sys/kernel/pid_max**

      .. note::

         The maximum value of **pid_max** is as follows:

         -  32-bit OS: **32768**
         -  64-bit OS: **4194304** (22nd power of 2)

   e. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12027__en-us_topic_0191813904_li6558431911107>`.

#. .. _alm_12027__en-us_topic_0191813904_li6558431911107:

   Check whether the system environment is abnormal.

   a. Contact the O&M personnel to check whether the operating system is abnormal.

      -  If yes, rectify the operating system fault and go to :ref:`2.b <alm_12027__en-us_topic_0191813904_li48344862111230>`.
      -  If no, go to :ref:`3 <alm_12027__en-us_topic_0191813904_li572522141314>`.

   b. .. _alm_12027__en-us_topic_0191813904_li48344862111230:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_12027__en-us_topic_0191813904_li572522141314>`.

#. .. _alm_12027__en-us_topic_0191813904_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

**Reference**
-------------

None
