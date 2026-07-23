:original_name: ALM-14042.html

.. _ALM-14042:

ALM-14042 Average RPC Processing Time of the Router Exceeds the Threshold
=========================================================================

Alarm Description
-----------------

The system checks the average RPC processing time of Router every 30 seconds and compares the actual average RPC processing time with the threshold. This alarm is generated when the average RPC processing time of Router exceeds the threshold for multiple consecutive times (10 times by default).

To change the threshold, choose **O&M** > **Alarm** > **Thresholds**, click the name of the desired cluster, and choose **HDFS**.

If **Trigger Count** is **1** and the average RPC processing time of Router is less than or equal to the threshold, this alarm is cleared. If **Trigger Count** is greater than **1** and the average RPC processing time of Router is less than or equal to 90% of the threshold, this alarm is cleared.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

+-----------------------+--------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                       | Auto Cleared          |
+=======================+======================================+=======================+
| 14042                 | Critical (default threshold: 300 ms) | Yes                   |
|                       |                                      |                       |
|                       | Major (default threshold: 1000 ms)   |                       |
+-----------------------+--------------------------------------+-----------------------+

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
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

Router cannot process the RPC requests from HDFS clients, upper-layer services that depend on HDFS, and DataNodes in a timely manner. Specifically, the services that access HDFS run slowly or the HDFS service is unavailable.

Possible Causes
---------------

-  The alarm threshold is improperly set.
-  The CPU performance of Router nodes is insufficient, and therefore Router nodes cannot process messages in a timely manner.
-  The memory configured for Router is too small, and frame freezing occurs on the JVM due to frequent full garbage collection.
-  Router parameters are configured improperly. As a result, Router cannot make full use of the device performance.

Handling Procedure
------------------

**Check whether the alarm threshold is too small.**

#. .. _alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li828989815529:

   Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the **Location** field of the alarm details, view the host name of the Router instance for which this alarm is generated.

2. Check the status of the services that depend on HDFS. Check whether the services run slowly or the task execution times out.

   -  If yes, go to :ref:`6 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li2190062915649>`.
   -  If no, go to :ref:`3 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li12794575145018>`.

3. .. _alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li12794575145018:

   On MRS Manager, choose **Cluster** > **Services** > **HDFS** > **Instances**, click the Router role obtained in :ref:`1 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li828989815529>`, and choose **Chart** > **RPC**. View the **Average Time of Router RPC Processing** chart and obtain the peak value within one day before and after the alarm is generated.

4. Choose **O&M** > **Alarm** > **Thresholds**, locate the desired cluster, choose **HDFS**, and click **Average Time of Router RPC Processing**. Click **Modify** in the **Operation** column of the **default** rule, and change the threshold to 150% of the peak value displayed within one day before and after the alarm is generated. Click **OK** to save the new threshold.

5. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li2190062915649>`.

**Check whether the CPU performance of the Router node is sufficient.**

6. .. _alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li2190062915649:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether alarm **ALM-12016 CPU Usage Exceeds the Threshold** is generated and whether the host name is the same as that obtained in :ref:`1 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li828989815529>`.

   -  If yes, go to :ref:`7 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li4691210415930>`.
   -  If no, go to :ref:`9 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li1696839151443>`.

7. .. _alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li4691210415930:

   Rectify the fault by following the handling procedure of **ALM-12016 CPU Usage Exceeds the Threshold**.

8. Wait 10 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li1696839151443>`.

**Check whether the memory of the Router node is too small.**

9.  .. _alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li1696839151443:

    On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether alarm **ALM-14038 Router Heap Memory Usage Exceeds the Threshold** is generated and whether the host name is the same as that obtained in :ref:`1 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li828989815529>`.

    -  If yes, go to :ref:`10 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li51365499151443>`.
    -  If no, go to :ref:`12 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li1573154019525>`.

10. .. _alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li51365499151443:

    Rectify the fault by following the handling procedure of **ALM-14038 Router Heap Memory Usage Exceeds the Threshold**.

11. Wait 10 minutes and check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li1573154019525>`.

**Check whether the Router parameters are properly configured.**

12. .. _alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li1573154019525:

    On MRS Manager, choose **Cluster** > **Services** > **HDFS** > **Configurations**.

    -  Search for **dfs.federation.router.connection.pool-size** and check its value. If the value is less than **64**, set it to **64**. If the value is greater than **64** but less than **128**, set it to **128**.
    -  Search for **dfs.federation.router.handler.count** and check its value. If the value is less than **128**, set it to **128**.

13. Click **Save**, and then click **OK**

14. On the **Instances** page of HDFS, select the Router role for which the alarm is generated, click **More**, select **Restart Instance**, and verify the password to restart the instance.

15. Wait 1 hour and check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li162921216241>`.

**Collect fault information.**

16. .. _alm-14042__en-us_topic_0000002166069868_en-us_topic_0000002199625333_li162921216241:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

17. Expand the **Service** drop-down list, select the HDFS services for the target cluster, and click **OK**.

18. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

19. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
