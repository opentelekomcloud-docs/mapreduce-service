:original_name: ALM-18022.html

.. _ALM-18022:

ALM-18022 Insufficient Yarn Queue Resources
===========================================

Description
-----------

The alarm module checks Yarn queue resources every 60 seconds. This alarm is generated when available resources or ApplicationMaster (AM) resources of a queue are insufficient.

This alarm is cleared when available resources are sufficient.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18022    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Parameter Name    | Description                                                                                                                  |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| QueueName         | Specifies the queue for which the alarm is generated.                                                                        |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| QueueMetric       | Specifies the metric of the queue for which the alarm is generated.                                                          |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

-  An application being executed takes longer time.
-  An application fails to be executed for a long time after being submitted.

Possible Causes
---------------

-  NodeManager node resources are insufficient.
-  The configured maximum resource capacity of the queue is excessively small.
-  The configured maximum AM resource percentage is excessively small.

Procedure
---------

**View alarm details.**

#. On the FusionInsight Manager, choose **O&M** > **Alarm > Alarms**.
#. View location information of this alarm and check whether **QueueName** is **root** and **QueueMetric** is **Memory** or **QueueName** is **root** and **QueueMetric** is **vCores**.

   -  If yes, go to :ref:`3 <alm-18022__li1118842213014>`.
   -  If no, go to :ref:`4 <alm-18022__li550716317319>`.

3. .. _alm-18022__li1118842213014:

   The memory or CPU of the Yarn cluster is insufficient. In this case, log in to the node where NodeManager resides and run the **free -g** and **cat /proc/cpuinfo** commands to query the available memory and available CPU of the node, respectively. On FusionInsight Manager, increase the values of **yarn.nodemanager.resource.memory-mb** and **yarn.nodemanager.resource.cpu-vcores** for the Yarn NodeManager based on the query results. Then, restart the NodeManager instance. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-18022__li550716317319>`.

4. .. _alm-18022__li550716317319:

   View location information of this alarm and check whether **QueueName** is **<Tenant Queue>** and **QueueMetric** is **Memory**, or **QueueName** is **<Tenant Queue>** and **QueueMetric** is **vCores** in **Location**, check whether **available Memory =** or **available vCores =** are included in **Additional Information**.

   -  If yes, go to :ref:`5 <alm-18022__li11123116735>`.
   -  If no, go to :ref:`7 <alm-18022__li1189109935>`.

5. .. _alm-18022__li11123116735:

   The memory or CPU of the tenant queue is insufficient. In this case, choose **Tenant Resources** > **Dynamic Resource Plan > Resource Distribution Policy** and increase the value of **Maximum Capacity**. Then, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-18022__li109354114148>`.

6. .. _alm-18022__li109354114148:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **Configurations** > **All Configurations**. Enter the keyword "threshold" and click **ResourceManager**. Adjust the threshold values of the following parameters:

   If **Additional Information** contains **available Memory =**, change the value of **yarn.queue.memory.alarm.threshold** to a value smaller than that of **available Memory =** in **Additional Information**.

   If **Additional Information** contains **available vCores =**, change the value of **yarn.queue.vcore.alarm.threshold** to a value smaller than that of **available vCores =** in **Additional Information**.

   Wait for five minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-18022__li1973131339>`.

7. .. _alm-18022__li1189109935:

   If **available AmMemory =** or **available AmvCores =** is included in **Additional Information**, ApplicationMaster memory or CPU of the tenant queue is insufficient. In this case, choose **Tenant Resources** > **Dynamic Resource Plan** > **Queue Configuration** and increase the value of **Maximum Am Resource Percent**. Then, check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-18022__li1382974791617>`.

8. .. _alm-18022__li1382974791617:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **Configurations** > **All Configurations**. Enter the keyword "threshold" and click **ResourceManager**. Adjust the threshold values of the following parameters:

   If **Additional Information** contains **available AmMemory =**, change the value of **yarn.queue.memory.alarm.threshold** to a value smaller than that of **available AmMemory =** in **Additional Information**.

   If **Additional Information** contains **available AmvCores =**, change the value of **yarn.queue.vcore.alarm.threshold** to a value smaller than that of **available AmvCores =** in **Additional Information**.

   Wait for five minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-18022__li1973131339>`.

**Collect fault information.**

9.  .. _alm-18022__li1973131339:

    Log in to FusionInsight Manager of the active cluster, and choose **O&M** > **Log** > **Download**.

10. Select **Yarn** in the required cluster from the **Service**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Reference
---------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927482.png
