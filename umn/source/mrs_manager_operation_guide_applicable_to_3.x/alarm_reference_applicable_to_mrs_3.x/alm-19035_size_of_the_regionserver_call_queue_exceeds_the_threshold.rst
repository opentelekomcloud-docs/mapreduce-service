:original_name: ALM-19035.html

.. _ALM-19035:

ALM-19035 Size of the RegionServer Call Queue Exceeds the Threshold
===================================================================

Alarm Description
-----------------

The system checks the size of the RegionServer call queue for each HBase service every 30 seconds. This alarm is generated when the call queue of a RegionServer instance is bigger than the threshold for 10 consecutive times.

This alarm is cleared when the call queue of a RegionServer instance is no bigger than the threshold.

This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

+-----------------------+-----------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                          | Auto Cleared          |
+=======================+=========================================+=======================+
| 19035                 | -  Critical (default threshold: 800 MB) | Yes                   |
|                       | -  Major (default threshold: 600 MB)    |                       |
+-----------------------+-----------------------------------------+-----------------------+

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

Request queues are stacked, and the RegionServer memory GC pressure increases. As a result, the response time of read requests increases. For latency-sensitive services, a large number of service read requests may time out.

Possible Causes
---------------

-  The RegionServer heap memory configuration is improper.
-  A slow disk fault occurred.
-  The RegionServer configuration is improper.
-  Regions of RegionServers are not evenly distributed and hotspotting occurred.
-  The latency of WAL Sync operations is high.

Handling Procedure
------------------

#. .. _alm-19035__en-us_topic_0000001786275390_li187081734191516:

   Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19035**, and view the service instance and host name in **Location**.

**Check the heap memory configuration.**

2. In the alarm list on MRS Manager, check whether the "Heap Memory Usage of the HBase Process Exceeds the Threshold" alarm is generated for the service instance in :ref:`1 <alm-19035__en-us_topic_0000001786275390_li187081734191516>`.

   -  If yes, go to :ref:`3 <alm-19035__en-us_topic_0000001786275390_li167081134161511>`.
   -  If no, go to :ref:`5 <alm-19035__en-us_topic_0000001786275390_li522015310223>`.

3. .. _alm-19035__en-us_topic_0000001786275390_li167081134161511:

   Rectify the fault by following the handling procedure of "ALM-19008 Heap Memory Usage of the HBase Process Exceeds the Threshold".

4. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19035__en-us_topic_0000001786275390_li522015310223>`.

5. .. _alm-19035__en-us_topic_0000001786275390_li522015310223:

   On MRS Manager, choose **Cluster** > **Services** > **HBase** > **Chart**, select **GC** from the chart category, and check whether the GC times and GC monitoring period are normal.

   -  If yes, go to :ref:`6 <alm-19035__en-us_topic_0000001786275390_li397815491814>`.
   -  If no, go to :ref:`9 <alm-19035__en-us_topic_0000001786275390_li13480621153420>`.

6. .. _alm-19035__en-us_topic_0000001786275390_li397815491814:

   Click **Configurations**, search for **GC_OPTS**, and increase the value of **Xmx** of the RegionServer within the allowed memory range. Set the value to a number less than or equal to 31 GB. Click **Save**.

7. Click **Dashboard** and click **More** > **Restart Service** to restart the HBase service.

   .. important::

      During HBase service restart, the service is unavailable. For example, data cannot be read or written, table operations cannot be performed, and the HBase web UI is inaccessible.

8. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-19035__en-us_topic_0000001786275390_li13480621153420>`.

**Check for slow disk fault.**

9. .. _alm-19035__en-us_topic_0000001786275390_li13480621153420:

   Check whether alarm **Slow Disk Fault** or **Disk Unavailable** are generated for the same node in :ref:`1 <alm-19035__en-us_topic_0000001786275390_li187081734191516>`.

   -  If yes, go to :ref:`10 <alm-19035__en-us_topic_0000001786275390_li1679510131369>`.
   -  If no, go to :ref:`12 <alm-19035__en-us_topic_0000001786275390_li1435343019397>`.

10. .. _alm-19035__en-us_topic_0000001786275390_li1679510131369:

    Rectify the fault by following the handling procedure of "ALM-12033 Slow Disk Fault" or "ALM-12063 Disk Unavailable".

11. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-19035__en-us_topic_0000001786275390_li1435343019397>`.

**Check the RegionServer configuration.**

12. .. _alm-19035__en-us_topic_0000001786275390_li1435343019397:

    On MRS Manager, choose **Cluster** > **Service** > **HBase**, click **Configurations** > **All Configurations**, and check whether the values of **hbase.wal.hsync** and **hbase.hfile.hsync** are **true**.

    -  If yes, go to :ref:`13 <alm-19035__en-us_topic_0000001786275390_li12678144164214>`.
    -  If no, go to :ref:`15 <alm-19035__en-us_topic_0000001786275390_li2708203154412>`.

13. .. _alm-19035__en-us_topic_0000001786275390_li12678144164214:

    Set both **hbase.wal.hsync** and **hbase.hfile.hsync** to **false** and click **Save**. Click **Dashboard** and click **More** > **Restart Service** to restart the HBase service.

14. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-19035__en-us_topic_0000001786275390_li2708203154412>`.

**Check whether RegionServer regions are evenly distributed.**

15. .. _alm-19035__en-us_topic_0000001786275390_li2708203154412:

    On MRS Manager, choose **Cluster** > **Services** > **HBase**. Click **HMaster(Active)** on the right of **HMaster Web UI** to go to the web UI of the HBase instance. View the **Base Stats** tab in the **Region Servers** area. Check whether the number of regions in the **Num.Regions** column is even.

    -  If yes, go to :ref:`20 <alm-19035__en-us_topic_0000001786275390_li1962212914618>`.
    -  If no, go to :ref:`16 <alm-19035__en-us_topic_0000001786275390_li87091331184413>`.

    |image1|

16. .. _alm-19035__en-us_topic_0000001786275390_li87091331184413:

    Log in to the faulty RegionServer node as user **omm**.

17. Run the following commands to go to the client installation directory and set the environment variable:

    **cd** *Client installation directory*

    **source bigdata_env**

    **kinit** **supergroup** *user group or a user with the Global Admin permission* (If Kerberos authentication is disabled for the cluster, skip this operation.)

18. Run the following commands to enable load balancing and check whether the function is successfully enabled:

    **hbase shell**

    **balance_switch true**

    **balancer_enabled**

    If the command output is **true**, load balancing is enabled.

    Run the **balancer** command to manually trigger the load balancing function.

    .. note::

       You are advised to enable and manually trigger the load balancing function during off-peak hours.

19. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm-19035__en-us_topic_0000001786275390_li1962212914618>`.

**Check the WAL sync latency.**

20. .. _alm-19035__en-us_topic_0000001786275390_li1962212914618:

    On MRS Manager, choose **Cluster** > **Services** > **HBase** > **Chart**. In the **Chart Category** area, select **Operations**. Check whether the value of "**P99.9th Percentile of WAL Sync Operation Delay-All Instances**" exceeds 500 ms.

    -  If yes, go to :ref:`21 <alm-19035__en-us_topic_0000001786275390_li101391353194720>`.
    -  If no, go to :ref:`22 <alm-19035__en-us_topic_0000001786275390_li959275915215>`.

21. .. _alm-19035__en-us_topic_0000001786275390_li101391353194720:

    Click **Instances**, select the RegionServer instance for which the alarm is generated, and choose **More** > **Restart Instance**. You also need to perform :ref:`22 <alm-19035__en-us_topic_0000001786275390_li959275915215>` and provide the logs to O&M personnel for fault locating.

    .. important::

       During RegionServer restart, client requests will be retried for multiple times. Read and write operations are affected for a short period of time.

**Collect fault information.**

22. .. _alm-19035__en-us_topic_0000001786275390_li959275915215:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

23. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

24. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

25. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002415833501.png
