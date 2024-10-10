:original_name: ALM-29016.html

.. _ALM-29016:

ALM-29016 Impalad Instance in the Sub-healthy State
===================================================

Alarm Description
-----------------

In MRS 3.1.5, the system checks every 60 seconds whether the Hive Server2 HTTP port (28000) of Impalad responds to cURL requests. This alarm is generated when the returned result has been incorrect for 20 seconds in two consecutive times. This alarm is cleared when the system correctly responds within 20 seconds.

In other MRS versions, the system checks every 60 seconds whether Impalad can execute **select 1**. This alarm is generated when the returned result has been incorrect for 20 seconds in two consecutive times. This alarm is cleared when the SQL statement is correctly executed within 20 seconds.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
29016    Minor          Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+----------------------------------------------------------+
| Type                 | Parameter   | Description                                              |
+======================+=============+==========================================================+
| Location Information | Source      | Specifies the cluster for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

Impalad cannot execute SQL statements or SQL statement execution times out, which affects data read and write.

Possible Causes
---------------

The Impalad service maintains too many queries.

Handling Procedure
------------------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Impala** > **Impalad Web UI**. On the displayed page, click any node to go to the web UI.

#. On the web UI, click **/backends** to view the Impala instance list. Locate the instance for which the alarm is generated and click **Web UI**. After the web UI of the subhealthy node is displayed, click **/queries** to check the task execution status and check whether any task is executed slowly.

   -  If yes, go to :ref:`3 <alm-29016__li918651451111>`.
   -  If no, go to :ref:`4 <alm-29016__li668151171315>`.

#. .. _alm-29016__li918651451111:

   After the task is complete, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-29016__li668151171315>`.

#. .. _alm-29016__li668151171315:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Impala** > **Instances**, select the Impala instance for which the alarm is generated, click **More**, and select **Restart Instance**. Then, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-29016__li1698242954313>`.

      .. note::

         The service will become unavailable when all instances are restarted. If a single instance is restarted, the tasks that are being executed on that instance will fail and the service will become available.

**Collect fault information.**

5. .. _alm-29016__li1698242954313:

   On FusionInsight Manager of the active or standby cluster, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **Impala** for the target cluster.

7. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000002007530509.png
