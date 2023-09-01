:original_name: ALM-12018.html

.. _ALM-12018:

ALM-12018 Memory Usage Exceeds the Threshold
============================================

Description
-----------

The system checks the memory usage of the system every 30 seconds and compares the actual memory usage with the threshold. The memory usage has a default threshold, this alarm is generated when the value of the memory usage exceeds the threshold.

When the **Trigger Count** is 1, this alarm is cleared when the host memory usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the host memory usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12018    Major          Yes
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

Service processes respond slowly or become unavailable.

Possible Causes
---------------

-  Memory configuration cannot meet service requirements. The memory usage reaches the upper limit.
-  The SUSE 12.X OS has an earlier **free** command. The calculated memory usage cannot reflect the real-world memory usage.

Procedure
---------

**Perform the following operations if SUSE 12.X is used.**

#. Log in to any node in the cluster as user **root**, and run the **cat /etc/*-release** command to check whether the OS is SUSE 12.X as user **root**.

   -  If yes, go to :ref:`2 <alm-12018__li348492949252>`.
   -  If no, go to :ref:`4 <alm-12018__li5861159252>`.

#. .. _alm-12018__li348492949252:

   Run the **cat /proc/meminfo \| grep Mem** command to check the real-world memory usage of the OS.

   .. code-block::

      MemTotal: 263576192 kB
      MemFree: 198283116 kB
      MemAvailable: 227641452 kB

#. Calculate the real-world memory usage: Memory usage = 1 - (Memory available/Memory total)

   -  If the memory usage is lower than 90%, manually disable transferring from monitoring indicators to alarms.
   -  If the memory usage is higher than 90%, go to :ref:`4 <alm-12018__li5861159252>`.

**Expand the system.**

4. .. _alm-12018__li5861159252:

   In the alarm list on FusionInsight Manager, click |image1| in the row where the alarm is located to view the alarm host address in the alarm details.

5. Log in to the host where the alarm is generated as user **root**.

6. If the memory usage exceeds the threshold, perform memory capacity expansion.

7. Run the command **free -m \| grep Mem\\: \| awk '{printf("%s,", $3 \* 100 / $2)}'** to check the system memory usage.

8. Wait for 5 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-12018__li372014939252>`.

**Collect fault information.**

9.  .. _alm-12018__li372014939252:

    On the FusionInsight Manager in the active cluster, choose **O&M** > **Log > Download**.

10. Select **OmmServer** from the **Servic**\ e and click **OK**.

11. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927669.png
.. |image2| image:: /_static/images/en-us_image_0000001583127413.png
