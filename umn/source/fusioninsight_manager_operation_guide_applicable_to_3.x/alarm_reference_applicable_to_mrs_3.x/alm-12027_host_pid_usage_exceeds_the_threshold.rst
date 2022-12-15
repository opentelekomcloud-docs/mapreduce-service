:original_name: ALM-12027.html

.. _ALM-12027:

ALM-12027 Host PID Usage Exceeds the Threshold
==============================================

Description
-----------

The system checks the PID usage every 30 seconds and compares the actual PID usage with the default PID usage threshold. This alarm is generated when the system detects that the PID usage exceeds the threshold.

When the **Trigger Count** is 1, this alarm is cleared when the PID usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the PID usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12027    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated.                                                            |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

No PID is available for new processes and service processes are unavailable.

Possible Causes
---------------

Too many processes are running on the node. You need to increase the value of **pid_max**.

Procedure
---------

**Increase the value of pid_max.**

#. In the alarm list on FusionInsight Manager, click |image1| in the row where the alarm is located to view the alarm host address in the alarm details.

#. Log in to the host where the alarm is generated as user **root**.

#. Run the **cat /proc/sys/kernel/pid_max**\ command to check the value of **pid_max**.

#. If the PID usage exceeds the threshold, run the command **echo** *new value* **> /proc/sys/kernel/pid_max** to enlarge the value of **pid_max**.

   Example: **echo 65536 > /proc/sys/kernel/pid_max**

   .. note::

      The maximum value of **pid_max** is as follows:

      -  On 32-bit systems: 32768
      -  On 64-bit systems: 4194304 (2^22)

#. Wait for 5 minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12027__li377225729750>`.

**Collect fault information.**

6. .. _alm-12027__li377225729750:

   On the FusionInsight Manager home page of the active cluster, choose **O&M** > **Log > Download**.

7. Select all services from the **Service** and click **OK**.

8. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383832.png
.. |image2| image:: /_static/images/en-us_image_0269383834.png
