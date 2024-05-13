:original_name: ALM-14021.html

.. _ALM-14021:

ALM-14021 NameNode Average RPC Processing Time Exceeds the Threshold
====================================================================

Description
-----------

The system checks the average RPC processing time of NameNode every 30 seconds, and compares the actual average RPC processing time with the threshold (default value: 100 ms). This alarm is generated when the system detects that the average RPC processing time exceeds the threshold for several consecutive times (10 times by default).

You can choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **HDFS** to change the threshold.

When the **Trigger Count** is 1, this alarm is cleared when the average RPC processing time of NameNode is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the average RPC processing time of NameNode is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14021    Major          Yes
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

Procedure
---------

**Obtain alarm information.**

#. On the MRS Manager portal, choose **O&M > Alarm > Alarms**. In the alarm list, click the alarm.
#. Check the alarm. Obtain the host name of the NameNode node involved in this alarm from the **HostName** information of **Location**. Then obtain the name of the NameService node involved in this alarm from the **NameServiceName** information of **Location**.

**Check whether the threshold is too small.**

3. Check the status of the services that depend on HDFS. Check whether the services run slowly or task execution times out.

   -  If yes, go to :ref:`8 <alm-14021__li48203297172449>`.
   -  If no, go to :ref:`4 <alm-14021__li29484482172449>`.

4. .. _alm-14021__li29484482172449:

   On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS**. Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **RPC**, and select **Average Time of Active NameNode RPC Processing** and click **OK**.

5. On the **Average Time of Active NameNode RPC Processing** monitoring page, obtain the value of the NameService node involved in this alarm.

6. On the MRS Manager portal, choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* **>** **HDFS**. Locate **Average Time of Active NameNode RPC Processing** and click the **Modify** in the **Operation** column of the default rule. The **Modify Rule** page is displayed. Change **Threshold** to 150% of the peak value within one day before and after the alarm is generated. Click **OK** to save the new threshold.

7. Wait for 5 minutes and then check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14021__li48203297172449>`.

**Check whether the CPU performance of the NameNode node is sufficient.**

8.  .. _alm-14021__li48203297172449:

    On the MRS Manager portal, click **O&M > Alarm >Alarms** and check whether **ALM-12016 CPU Usage Exceeds the Threshold** is generated for the NameNode node.

    -  If yes, go to :ref:`9 <alm-14021__li23155373172449>`.
    -  If no, go to :ref:`11 <alm-14021__li29576569172449>`.

9.  .. _alm-14021__li23155373172449:

    Handle **ALM-12016 CPU Usage Exceeds the Threshold** by taking recommended actions.

10. Wait for 10 minutes and check whether alarm 14021 is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-14021__li29576569172449>`.

**Check whether the memory of the NameNode node is too small.**

11. .. _alm-14021__li29576569172449:

    On the MRS Manager portal, click **O&M > Alarm >Alarms** and check whether **ALM-14007 HDFS NameNode Heap Memory Usage Exceeds the Threshold** is generated for the NameNode node.

    -  If yes, go to :ref:`12 <alm-14021__li26363673172449>`.
    -  If no, go to :ref:`14 <alm-14021__li41096175172449>`.

12. .. _alm-14021__li26363673172449:

    Handle **ALM-14007 HDFS NameNode Heap Memory Usage Exceeds the Threshold** by taking recommended actions.

13. Wait for 10 minutes and check whether alarm 14021 is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-14021__li41096175172449>`.

**Check whether NameNode parameters are configured properly.**

14. .. _alm-14021__li41096175172449:

    On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Configurations** > **All** **Configurations**. Search for parameter **dfs.namenode.handler.count** and view its value. If the value is less than or equal to 128, change it to **128**. If the value is greater than 128 but less than 192, change it to **192**.

15. Search for parameter **ipc.server.read.threadpool.size** and view its value. If the value is less than 5, change it to **5**.

16. Click **Save** and click **OK**.

17. On the **Instance** page of HDFS, select the standby NameNode of NameService involved in this alarm and choose **More** > **Restart Instance**. Enter the password and click **OK**. Wait until the standby NameNode is started up.

18. On the **Instance** page of HDFS, select the active NameNode of NameService involved in this alarm and choose **More** > **Restart Instance**. Enter the password and click **OK**. Wait until the active NameNode is started up.

19. Wait for 1 hour and then check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm-14021__li59520454172449>`.

**Collect fault information.**

20. .. _alm-14021__li59520454172449:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

21. Select the following node in the required cluster from the **Service**.

    -  HDFS

22. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

23. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807617.png
