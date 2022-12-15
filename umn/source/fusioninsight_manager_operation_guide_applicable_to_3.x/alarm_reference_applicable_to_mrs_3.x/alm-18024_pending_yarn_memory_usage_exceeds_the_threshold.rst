:original_name: ALM-18024.html

.. _ALM-18024:

ALM-18024 Pending Yarn Memory Usage Exceeds the Threshold
=========================================================

Description
-----------

The alarm module checks the pending memory of Yarn every 60 seconds. The alarm is generated when the pending memory exceeds the threshold. Pending memory indicates the total memory that is not allocated to submitted Yarn applications.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18024    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+------------------------------------------------------------------+
| Name        | Meaning                                                          |
+=============+==================================================================+
| Source      | Specifies the cluster for which the alarm is generated.          |
+-------------+------------------------------------------------------------------+
| QueueName   | Identifies the queue for which the alarm is generated.           |
+-------------+------------------------------------------------------------------+
| QueueMetric | Identifies the queue indicator for which the alarm is generated. |
+-------------+------------------------------------------------------------------+

Impact on the System
--------------------

-  It takes long time to end an application.
-  A new application cannot run after submission.

Possible Causes
---------------

-  NodeManager node resources are insufficient.
-  The maximum resource capacity of the queue and the maximum AM resource percentage are too small.
-  The monitoring threshold is too small.

Procedure
---------

**Check NodeManager resources.**

#. On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **ResourceManager (Active)** to access the ResourceManager web UI.

#. Click **Scheduler** and check whether the root queue resources are used up in **Application Queues**.

   -  If yes, go to :ref:`3 <alm-18024__li1894618168247>`.
   -  If no, go to :ref:`4 <alm-18024__li156321342274>`.

#. .. _alm-18024__li1894618168247:

   Expand the capacity of the NodeManager instance of the Yarn service. After the capacity expansion, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-18024__li15314143611285>`.

**Check the maximum queue resource capacity and the maximum AM resource percentage.**

4. .. _alm-18024__li156321342274:

   Check whether the resources of the queue corresponding to the pending task are used up.

   -  If yes, go to :ref:`5 <alm-18024__li1663218419278>`.
   -  If no, go to :ref:`6 <alm-18024__li15314143611285>`.

5. .. _alm-18024__li1663218419278:

   On FusionInsight Manager, choose **Tenant Resources** > **Dynamic Resource Plan** and add resources as required. Check whether the alarms are cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-18024__li15314143611285>`.

**Adjust the monitoring thresholds.**

6. .. _alm-18024__li15314143611285:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Yarn** > **CPU and Memory** > **Pending Memory**, and increase the threshold as required.

7. Check whether the alarm is cleared 5 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-18024__li76841314475>`.

**Collect the fault information.**

8.  .. _alm-18024__li76841314475:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **Yarn** for the target cluster.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0263895617.png
