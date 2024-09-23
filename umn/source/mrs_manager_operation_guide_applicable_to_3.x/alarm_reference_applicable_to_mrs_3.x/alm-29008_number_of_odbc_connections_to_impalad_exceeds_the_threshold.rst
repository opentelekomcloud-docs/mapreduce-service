:original_name: ALM-29008.html

.. _ALM-29008:

ALM-29008 Number of ODBC Connections to Impalad Exceeds the Threshold
=====================================================================

Alarm Description
-----------------

The system checks the number of client connections to the Impalad node every 30 seconds. This alarm is generated when the number of client connections exceeds the customized threshold (60 by default).

This alarm is automatically cleared when the number of client connections is less than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
29008    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the threshold for triggering the alarm.        |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

New client connections may be blocked or even fail.

Possible Causes
---------------

The number of client connections maintained by the Impalad service is too large or the threshold is too small.

Handling Procedure
------------------

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds** > **Impala** > **Connections** > **Number of ODBC Connections to Impalad Process (Impalad)** to check the threshold.

#. Check the number of ODBC applications connected to Impalad and stop idle applications. Check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-29008__li1507754134111>` to change the number of concurrent connections supported by Impalad.

#. .. _alm-29008__li1507754134111:

   On FusionInsight Manager, choose **Cluster** > **Impala** > **Configurations** > **All Configurations** > **Impalad** > **Customization**. Add the custom parameter **--fe_service_threads**. The default value of this parameter is **64**. Change the value as required and click **Save**.

#. After the query tasks on all clients are complete, click the **Instances** tab. Select all Impalad instances, and restart them.

   .. note::

      The service will become unavailable when all instances are restarted. If a single instance is restarted, the tasks that are being executed on that instance will fail and the service will become available.

#. After the restart is complete, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If yes, go to :ref:`6 <alm-29008__li17918612154249>`.

**Collect fault information.**

6. .. _alm-29008__li17918612154249:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Impala** for the target cluster.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
