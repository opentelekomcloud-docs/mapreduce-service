:original_name: ALM-14022.html

.. _ALM-14022:

ALM-14022 NameNode Average RPC Queuing Time Exceeds the Threshold
=================================================================

Description
-----------

The system checks the average RPC queuing time of NameNode every 30 seconds, and compares the actual average RPC queuing time with the threshold (default value: 200 ms). This alarm is generated when the system detects that the average RPC queuing time exceeds the threshold for several consecutive times (10 times by default).

You can choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **HDFS** to change the threshold.

When the **Trigger Count** is 1, this alarm is cleared when the average RPC queuing time of NameNode is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the average RPC queuing time of NameNode is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14022    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| NameServiceName   | Specifies the NameService service for which the alarm is generated.                                                          |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

NameNode cannot process the RPC requests from HDFS clients, upper-layer services that depend on HDFS, and DataNode in a timely manner. Specifically, the services that access HDFS run slowly or the HDFS service is unavailable.

Possible Causes
---------------

-  The CPU performance of NameNode nodes is insufficient and therefore NameNode nodes cannot process messages in a timely manner.
-  The configured NameNode memory is too small and frame freezing occurs on the JVM due to frequent full garbage collection.
-  NameNode parameters are not configured properly, so NameNode cannot make full use of system performance.
-  The volume of services that access HDFS is too large and therefore NameNode is overloaded.

Procedure
---------

**Obtain alarm information.**

#. On the MRS Manager portal, choose **O&M > Alarm > Alarms**. In the alarm list, click the alarm.
#. Check the alarm. Obtain the alarm generation time from **Generated**. Obtain the host name of the NameNode node involved in this alarm from the **HostName** information of **Location**. Then obtain the name of the NameService node involved in this alarm from the **NameServiceName** information of **Location**.

**Check whether the threshold is too small.**

3.  Check the status of the services that depend on HDFS. Check whether the services run slowly or task execution times out.

    -  If yes, go to :ref:`8 <alm-14022__li6328681517318>`.
    -  If no, go to :ref:`4 <alm-14022__li4999873217318>`.

4.  .. _alm-14022__li4999873217318:

    On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS**. Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **RPC**, and select **Average Time of Active NameNode RPC Queuing** and click **OK**.

5.  On the **Average Time of Active NameNode RPC Queuing** monitoring page, obtain the value of the NameService node involved in this alarm.

6.  On the MRS Manager portal, choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* **>** **HDFS**. Locate **Average Time of Active NameNode RPC Queuing** and click the **Modify** in the **Operation** column of the default rule. The **Modify Rule** page is displayed. Change **Threshold** to 150% of the monitored value. Click **OK** to save the new threshold.

7.  Wait for 1 minute and then check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`8 <alm-14022__li6328681517318>`.

    **Check whether the CPU performance of the NameNode node is sufficient.**

8.  .. _alm-14022__li6328681517318:

    On the MRS Manager portal, click **O&M > Alarm > Alarms** and check whether **ALM-12016 HDFS NameNode Memory Usage Exceeds the Threshold** is generated.

    -  If yes, go to :ref:`9 <alm-14022__li922016517318>`.
    -  If no, go to :ref:`11 <alm-14022__li3577444117318>`.

9.  .. _alm-14022__li922016517318:

    Handle **ALM-12016 CPU Usage Exceeds the Threshold** by taking recommended actions.

10. Wait for 10 minutes and check whether alarm 14022 is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-14022__li3577444117318>`.

**Check whether the memory of the NameNode node is too small.**

11. .. _alm-14022__li3577444117318:

    On the MRS Manager portal, click **O&M > Alarm > Alarms** and check whether **ALM-14007 HDFS NameNode Memory Usage Exceeds the Threshold** is generated.

    -  If yes, go to :ref:`12 <alm-14022__li5900064917318>`.
    -  If no, go to :ref:`14 <alm-14022__li2539715217318>`.

12. .. _alm-14022__li5900064917318:

    Handle **ALM-14007 CPU Usage Exceeds the Threshold** by taking recommended actions.

13. Wait for 10 minutes and check whether alarm 14022 is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-14022__li2539715217318>`.

**Check whether NameNode parameters are configured properly.**

14. .. _alm-14022__li2539715217318:

    On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Configurations** > **All** **Configurations**. Search for parameter **dfs.namenode.handler.count** and view its value. If the value is less than or equal to 128, change it to **128**. If the value is greater than 128 but less than 192, change it to **192**.

15. Search for parameter **ipc.server.read.threadpool.size** and view its value. If the value is less than 5, change it to **5**.

16. Click **Save**, and click **OK**.

17. On the **Instance** page of HDFS, select the standby NameNode of NameService involved in this alarm and choose **More** > **Restart Instance**. Enter the password and click **OK**. Wait until the standby NameNode is started up.

18. On the **Instance** page of HDFS, select the active NameNode of NameService involved in this alarm and choose **More** > **Restart Instance**. Enter the password and click **OK**. Wait until the active NameNode is started up.

19. Wait for 1 hour and then check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm-14022__li2529838417318>`.

**Check whether the HDFS workload changes and reduce the workload properly.**

20. .. _alm-14022__li2529838417318:

    On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS**. Click the drop-down menu in the upper right corner of **Chart**, click **Customize**, select **Average Time of Active NameNode RPC Queuing** and click **OK**.

21. Click |image1|. The **Details** page is displayed.

22. Set the monitoring data display period, from 5 days before the alarm generation time to the alarm generation time. Click **OK**.

23. On the **Average RPC Queuing Time** monitoring page, check whether the point in time when the queuing time increases abruptly exists.

    -  If yes, go to :ref:`24 <alm-14022__li6583884617318>`.
    -  If no, go to :ref:`27 <alm-14022__li4075154117318>`.

24. .. _alm-14022__li6583884617318:

    Confirm and check the point in time. Check whether a new task frequently accesses HDFS and whether the access frequency can be reduced.

25. If a Balancer task starts at the point in time, stop the task or specify a node for the task to reduce the HDFS workload.

26. Wait for 1 hour and then check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`27 <alm-14022__li4075154117318>`.

**Collect fault information.**

27. .. _alm-14022__li4075154117318:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

28. Select **HDFS** in the required cluster from the **Service**.

29. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

30. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807777.png
.. |image2| image:: /_static/images/en-us_image_0000001532767570.png
