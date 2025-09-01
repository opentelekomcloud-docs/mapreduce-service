:original_name: ALM-19033.html

.. _ALM-19033:

ALM-19033 Number of Tasks in the RegionServer RPC Read Queue Exceeds the Threshold
==================================================================================

Alarm Description
-----------------

The system checks the number of tasks waiting in the RPC read queue for the RegionServer instances of the HBase service every 30 seconds. This alarm is generated when the number of waiting tasks exceeds the threshold for 10 consecutive times.

This alarm is cleared when the number of waiting tasks is less than or equal to the threshold.

This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

+-----------------------+---------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                        | Auto Cleared          |
+=======================+=======================================+=======================+
| 19033                 | -  Critical (default threshold: 2000) | Yes                   |
|                       | -  Major (default threshold: 1600)    |                       |
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

Request queues are stacked, and the response time of read requests increases. For latency-sensitive services, a large number of service read requests may time out.

Possible Causes
---------------

-  The RegionServer heap memory configuration is improper.
-  The RegionServer configuration is improper.
-  Regions of RegionServers are unevenly distributed, and read hotspotting occurred.
-  A slow disk fault occurred.

Handling Procedure
------------------

#. .. _alm-19033__en-us_topic_0000001774870312_li183271731133218:

   Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19033**, and view the service instance and host name in **Location**.

**Check the heap memory configuration.**

2. In the alarm list on MRS Manager, check whether the "Heap Memory Usage of the HBase Process Exceeds the Threshold" alarm is generated for the service instance in :ref:`1 <alm-19033__en-us_topic_0000001774870312_li183271731133218>`.

   -  If yes, go to :ref:`3 <alm-19033__en-us_topic_0000001774870312_li33270319322>`.
   -  If no, go to :ref:`5 <alm-19033__en-us_topic_0000001774870312_li1358155631914>`.

3. .. _alm-19033__en-us_topic_0000001774870312_li33270319322:

   Rectify the fault by following the handling procedure of "ALM-19008 Heap Memory Usage of the HBase Process Exceeds the Threshold".

4. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19033__en-us_topic_0000001774870312_li1358155631914>`.

5. .. _alm-19033__en-us_topic_0000001774870312_li1358155631914:

   On MRS Manager, choose **Cluster** > **Services** > **HBase** > **Chart**, select **GC** from the chart category, and check whether the GC times and GC monitoring period are normal.

   -  If yes, go to :ref:`6 <alm-19033__en-us_topic_0000001774870312_li397815491814>`.
   -  If no, go to :ref:`9 <alm-19033__en-us_topic_0000001774870312_li1313719555514>`.

6. .. _alm-19033__en-us_topic_0000001774870312_li397815491814:

   Click **Configurations**, search for **GC_OPTS**, and increase the value of **Xmx** of the RegionServer within the allowed memory range. Set the value to a number less than or equal to 31 GB. Click **Save**.

   .. note::

      On MRS Manager, choose **Cluster** > **Services** > **HBase** > **Instances** and obtain the hostnames of all nodes where RegionServer resides. Go back to the MRS Manager homepage and choose **Hosts**. In the host list, view the **Memory(GB)** values of all nodes where RegionServer resides and check the remaining memory of each host. Increase the value of **Xmx** based on the minimum remaining memory, and ensure that the used memory of each node does not exceed 80% after the adjustment.

7. Click **Dashboard** and click **More** > **Restart Service** to restart the HBase service.

   .. important::

      During HBase service restart, the service is unavailable. For example, data cannot be read or written, table operations cannot be performed, and the HBase web UI is inaccessible.

8. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-19033__en-us_topic_0000001774870312_li1313719555514>`.

**Check the RegionServer configuration.**

9.  .. _alm-19033__en-us_topic_0000001774870312_li1313719555514:

    On MRS Manager, choose **Cluster** > **Services** > **HBase**, click **Configurations** > **All Configurations**, and check whether **hbase.bucketcache.size** is properly set. A larger value indicates a larger read cache and higher read performance. Increase the value based on the remaining memory of the node and click **Save**. Click **Dashboard** and click **More** > **Restart Service** to restart the HBase service.

10. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-19033__en-us_topic_0000001774870312_li8133731529>`.

11. .. _alm-19033__en-us_topic_0000001774870312_li8133731529:

    On the HBase dashboard, click the hyperlink on the right of **HMaster Web UI**. In the **User Tables** tab in the **Tables** area, click the name of the table hit by a large number of user read requests. In the **Table Schema** area of the **Table** tab, check whether the value of **BLOCKCACHE** is false.

    -  If yes, go to :ref:`12 <alm-19033__en-us_topic_0000001774870312_li1510015190167>`.
    -  If no, go to :ref:`14 <alm-19033__en-us_topic_0000001774870312_li533616116386>`.

    |image1|

12. .. _alm-19033__en-us_topic_0000001774870312_li1510015190167:

    Log in to the node where the HBase client is installed as user **omm**. Run the following commands to change the value of **BLOCKCACHE** of the :ref:`11 <alm-19033__en-us_topic_0000001774870312_li8133731529>` table column family to **true**:

    **cd** *Client installation directory*

    **source bigdata_env**

    **kinit** *the* **supergroup** *user group or a user with the Global Admin permission* (If Kerberos authentication is disabled for the cluster, skip this operation.)

    **hbase shell**

    **alter'**\ *Table name*\ **', {NAME =>'**\ *Column family name*\ **', BLOCKCACHE => true}**

    Run the following command to check whether the value of **BLOCKCACHE** of the column family is changed to **true**:

    **describe**'*Table name*'

13. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-19033__en-us_topic_0000001774870312_li533616116386>`.

**Check whether regions of RegionServers are evenly distributed.**

14. .. _alm-19033__en-us_topic_0000001774870312_li533616116386:

    On MRS Manager, choose **Cluster** > **Services** > **HBase** and click **HMaster(Active)**. On the HBase web UI, check whether regions are evenly distributed in the **Num.Regions** column in the **Base Stats** tab in the **Region Servers** area.

    -  If yes, go to :ref:`20 <alm-19033__en-us_topic_0000001774870312_li107672317591>`.
    -  If no, go to :ref:`15 <alm-19033__en-us_topic_0000001774870312_li1295083819381>`.

    |image2|

15. .. _alm-19033__en-us_topic_0000001774870312_li1295083819381:

    Log in to the faulty RegionServer node as user **omm**.

16. Run the following commands to go to the client installation directory and set the environment variable:

    **cd** *Client installation directory*

    **source bigdata_env**

    **kinit** *the* **supergroup** *user group or a user with the Global Admin permission* (If Kerberos authentication is disabled for the cluster, skip this operation.)

17. Run the following commands to check whether the load balancing function is enabled:

    **hbase shell**

    **balancer_enabled**

    If the command output is **true**, load balancing is enabled.

    -  If yes, go to :ref:`20 <alm-19033__en-us_topic_0000001774870312_li107672317591>`.
    -  If no, go to :ref:`18 <alm-19033__en-us_topic_0000001774870312_li61341947114413>`.

18. .. _alm-19033__en-us_topic_0000001774870312_li61341947114413:

    Run the following commands to enable load balancing and check whether the function is successfully enabled:

    **balance_switch true**

    **balancer_enabled**

    Run the **balancer** command to manually trigger the load balancing function.

    .. note::

       You are advised to enable and trigger load balancing during off-peak hours.

19. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm-19033__en-us_topic_0000001774870312_li107672317591>`.

**Check for slow disk fault.**

20. .. _alm-19033__en-us_topic_0000001774870312_li107672317591:

    Check whether alarm "Slow Disk Fault" or "Disk Unavailable" are generated on the node in :ref:`1 <alm-19033__en-us_topic_0000001774870312_li183271731133218>`.

    -  If yes, go to :ref:`21 <alm-19033__en-us_topic_0000001774870312_li189661023135911>`.
    -  If no, go to :ref:`23 <alm-19033__en-us_topic_0000001774870312_li18299145910288>`.

21. .. _alm-19033__en-us_topic_0000001774870312_li189661023135911:

    Rectify the fault by following the handling procedure of "ALM-12033 Slow Disk Fault" or "ALM-12063 Disk Unavailable".

22. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`23 <alm-19033__en-us_topic_0000001774870312_li18299145910288>`.

**Collect fault information.**

23. .. _alm-19033__en-us_topic_0000001774870312_li18299145910288:

    On MRS Manager, choose **Cluster** > **Services** > **HBase** > **Chart**, select **IO** from the **Chart Category** area, and view the values of **Maximum Pread Latency-All Instances** and **Maximum Read Latency-All Instances**. Normal values do not exceed 100 ms.

24. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

25. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

26. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

27. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002382434022.png
.. |image2| image:: /_static/images/en-us_image_0000002382274158.png
