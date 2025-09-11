:original_name: ALM-45477.html

.. _ALM-45477:

ALM-45477 Failed to Restore Data After a Disk of Kudu Is Replaced
=================================================================

Alarm Description
-----------------

This alarm is generated when Kudu fails to restore data by invoking the script in SetupTool after a disk is replaced.

This alarm is cleared when the data is successfully restored.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45477    Critical       Yes
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

Kudu fails to restore data, and historical data is unavailable.

Possible Causes
---------------

Kudu fails to restore the UUID or the data from the remote end.

Handling Procedure
------------------

**Collect fault information.**

#. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.
#. Expand the **Service** drop-down list, and select **Kudu** for the target cluster.
#. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

   .. note::

      Collect NodeAgent logs and check whether data is successfully restored after the disk replacement.

      The logs are saved in the following directory:

      /var/log/Bigdata/nodeagent/scriptlog/disk_manager_notify.log


      .. figure:: /_static/images/en-us_image_0000002415262005.png
         :alt: **Figure 1** Collecting NodeAgent logs

         **Figure 1** Collecting NodeAgent logs

#. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
