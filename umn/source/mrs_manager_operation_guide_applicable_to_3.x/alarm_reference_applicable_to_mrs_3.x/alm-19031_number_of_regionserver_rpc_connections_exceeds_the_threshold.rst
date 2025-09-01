:original_name: ALM-19031.html

.. _ALM-19031:

ALM-19031 Number of RegionServer RPC Connections Exceeds the Threshold
======================================================================

Alarm Description
-----------------

The system checks the number of RegionServer RPC connections in each HBase service every 30 seconds. This alarm is generated when the number of RPC connections of a RegionServer instance exceeds the threshold for 10 consecutive times.

This alarm is cleared when the number of RPC connections of a RegionServer instance is less than or equal to the threshold.

This alarm is generated only for MRS 3.3.1 or later.

Alarm Attributes
----------------

+-----------------------+---------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                        | Auto Cleared          |
+=======================+=======================================+=======================+
| 19031                 | -  Critical (default threshold: 2000) | Yes                   |
|                       | -  Major (default threshold: 1000)    |                       |
+-----------------------+---------------------------------------+-----------------------+

Alarm Parameters
----------------

+------------------------+-------------+----------------------------------------------------------+
| Type                   | Parameter   | Description                                              |
+========================+=============+==========================================================+
| Location Information   | Source      | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------+----------------------------------------------------------+
|                        | ServiceName | Specifies the service for which the alarm was generated. |
+------------------------+-------------+----------------------------------------------------------+
|                        | RoleName    | Specifies the role for which the alarm was generated.    |
+------------------------+-------------+----------------------------------------------------------+
|                        | HostName    | Specifies the host for which the alarm was generated.    |
+------------------------+-------------+----------------------------------------------------------+
| Additional Information | Threshold   | Specifies the threshold for generating the alarm.        |
+------------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

There are a large amount of concurrent access requests on the RegionServer node, which imposes great pressure and causes slow response. For latency-sensitive services, a large number of service read and write requests may time out.

Possible Causes
---------------

Too many concurrent requests are sent from applications to access HBase.

Handling Procedure
------------------

#. Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19031**, and view the service instance and host name in **Location**.

**Check the number of concurrent requests accessing HBase.**

2. Log in to the node where the HBase client is installed and check whether **hbase.client.ipc.pool.size** in the *Client installation directory*\ **/HBase/hbase/conf/hbase-site.xml** file is set to a value greater than **5**.

   -  If yes, go to :ref:`3 <alm-19031__en-us_topic_0000001774710640_li923414287410>`.
   -  If no, go to :ref:`5 <alm-19031__en-us_topic_0000001774710640_li1891341510112>`.

3. .. _alm-19031__en-us_topic_0000001774710640_li923414287410:

   Decrease the value of **hbase.client.ipc.pool.size** and save the change.

4. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19031__en-us_topic_0000001774710640_li1891341510112>`.

5. .. _alm-19031__en-us_topic_0000001774710640_li1891341510112:

   Check whether the number of concurrent requests accessing the HBase service is too large.

   -  If yes, go to :ref:`6 <alm-19031__en-us_topic_0000001774710640_li7961131445410>`.
   -  If no, go to :ref:`8 <alm-19031__en-us_topic_0000001774710640_li959275915215>`.

   .. note::

      The number of concurrent HBase API calls by all applications must be less than or equal to the following value:

      Number of RegionServer instances x Maximum number of handlers of a single RegionServer

      To obtain the number of RegionServer instances, log in to Manager and choose **Cluster** > **Services** > **HBase** > **Instances**. To obtain the maximum number of handlers of a single RegionServer, click **Configurations** and search for the **hbase.regionserver.handler.count** parameter.

6. .. _alm-19031__en-us_topic_0000001774710640_li7961131445410:

   Contact the upper-layer service support personnel to decrease the concurrent requests based on actual service requirements.

7. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-19031__en-us_topic_0000001774710640_li959275915215>`.

**Collect fault information.**

8.  .. _alm-19031__en-us_topic_0000001774710640_li959275915215:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **HBase** for the target cluster.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
