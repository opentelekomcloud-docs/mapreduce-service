:original_name: ALM-50215.html

.. _ALM-50215:

ALM-50215 Longest Duration of RPC Requests Received by Each FE Thrift Method Exceeds the Threshold
==================================================================================================

Alarm Description
-----------------

The system checks the longest duration of RPC requests received by each FE Thrift method every 30 seconds. This alarm is generated when the longest duration exceeds the threshold (5000 ms by default).

This alarm is cleared when the longest duration of RPC requests received by each FE Thrift method is less than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50215    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------------+-------------------------------------------------------------------+
| Parameter         | Description                                                       |
+===================+===================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.           |
+-------------------+-------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                 |
+-------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

A longer RPC duration indicates a higher performance load and slower network request processing, which may cause service congestion.

Possible Causes
---------------

-  The network has a latency.
-  There are too many concurrent large SQL tasks.

Handling Procedure
------------------

#. Log in to the host where the faulty node is deployed as user **root** and run **ping** *IP addresses of all Doris nodes* to check whether the peer host can be pinged.

   -  If yes, go to :ref:`3 <alm-50215__li1581425812514>`.
   -  If no, go to :ref:`2 <alm-50215__li828020013183>`.

#. .. _alm-50215__li828020013183:

   Contact the network administrator to restore the network.

#. .. _alm-50215__li1581425812514:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Doris**. Click the **Chart** tab, select **Connection** from **Chart Category** in the left pane, and view the **FE MySQL Port Connections** chart. If the number of connections is large, click **Instances**, select the FE instance, and click the **Chart** tab. Select **CPU and Memory** from **Chart Category** and view the **CPU Usage of FE** chart. If the CPU usage is high, check the **Time** field in FE audit **log /var/log/Bigdata/audit/doris/fe/fe.audit.log** to collect statistics on the average task duration. If the value is also high, the alarm is caused by large concurrent tasks.

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds**, click the name of the desired cluster, and choose **Doris** > **Performance** > **Longest duration of RPC requests received by each method of the FE thrift interface (FE)**.

#. Click the edit button next to **Trigger Count**, change the number based on site requirements, and click **OK**.

#. Click **Modify** in the **Operation** column, change the alarm threshold based on site requirements, and click **OK**.

#. Wait 10 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-50215__li727840151813>`.

**Collect fault information.**

8.  .. _alm-50215__li727840151813:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **Doris** for the target cluster.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
