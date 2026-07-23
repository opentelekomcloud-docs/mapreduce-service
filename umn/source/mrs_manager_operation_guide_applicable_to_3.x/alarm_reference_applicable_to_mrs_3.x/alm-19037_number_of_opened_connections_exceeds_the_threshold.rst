:original_name: ALM-19037.html

.. _ALM-19037:

ALM-19037 Number of Opened Connections Exceeds the Threshold
============================================================

Alarm Description
-----------------

The system checks the PhoenixQueryServer instance connection usage of each HBase service every 30 seconds. This alarm is generated when the connection usage of a PhoenixQueryServer instance exceeds the threshold for five consecutive times by default. This alarm is cleared when the connection usage of PhoenixQueryServer is less than or equal to the threshold.

Alarm Attributes
----------------

+-------------+------------------------------------+--------------------+--------------+--------------+
| Alarm ID    | Alarm Severity                     | Alarm Type         | Service Type | Auto Cleared |
+=============+====================================+====================+==============+==============+
| 19037       | Critical (default threshold: 100%) | Quality of service | HBase        | Yes          |
|             |                                    |                    |              |              |
|             | Major (default threshold: 90%)     |                    |              |              |
+-------------+------------------------------------+--------------------+--------------+--------------+

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

PhoenixQueryServer may not be able to provide services externally. As a result, PhoenixQueryServer's ability to process client requests diminishes, leading to increased read/write latency and potential request failures.

Possible Causes
---------------

-  The maximum number of PhoenixQueryServer connections is configured with an insufficient value.
-  Requests sent to the PhoenixQueryServer may encounter hotspot issues.

Handling Procedure
------------------

#. Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19037**, and view the service instance and host name in **Location**.

**View the PhoenixQueryServer connection configuration.**

2. Choose **Cluster** > **Services** > **HBase** and click the **Configurations** tab. In the upper right corner of the page, search for **avatica.connectioncache.maxcapacity** and check whether its value for the PhoenixQueryServer role is too small. The default value is **200**.

   -  If yes, go to :ref:`3 <alm-19037__en-us_topic_0000002585580915_en-us_topic_0000002414099166_li195843102017>`.
   -  If no, go to :ref:`5 <alm-19037__en-us_topic_0000002585580915_en-us_topic_0000002414099166_li5581133206>`.

3. .. _alm-19037__en-us_topic_0000002585580915_en-us_topic_0000002414099166_li195843102017:

   Increase the value of this parameter based on service requirements and click **Save**. Click the **Instances** tab, select the affected PhoenixQueryServer instances, and choose **More** > **Instance Rolling Restart**. In the displayed dialog box, enter the username and password, and click **OK**. Wait until the rolling restart is complete for the configuration to take effect.

4. After the configuration takes effect, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19037__en-us_topic_0000002585580915_en-us_topic_0000002414099166_li5581133206>`.

**Check whether requests sent to the PhoenixQueryServer have hotspot issues.**

5. .. _alm-19037__en-us_topic_0000002585580915_en-us_topic_0000002414099166_li5581133206:

   On MRS Manager, choose **Cluster** > **Services** > **HBase**. Click the **Chart** tab and select **Connections** for **Chart Category**. Check the top 3 PhoenixQueryServer instances with the most opened connections on the **Number of Connections Opened-All Instances** chart. If a usage hotspot is observed, where the number of connections on the top 1 PhoenixQueryServer instance significantly exceeds those on the top 2 and top 3 instances, redistribute service access to balance the load across other PhoenixQueryServer instances.

6. After the services are adjusted, wait a period of time, log in to MRS Manager, and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-19037__en-us_topic_0000002585580915_en-us_topic_0000002414099166_li66014362013>`.

**Collect fault information.**

7.  .. _alm-19037__en-us_topic_0000002585580915_en-us_topic_0000002414099166_li66014362013:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **HBase** for the target cluster.

9.  Click the edit icon in the upper right corner, and select a time span starting 10 minutes before and ending 10 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
