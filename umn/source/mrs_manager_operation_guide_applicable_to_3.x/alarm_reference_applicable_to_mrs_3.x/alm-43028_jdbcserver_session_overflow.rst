:original_name: ALM-43028.html

.. _ALM-43028:

ALM-43028 JDBCServer Session Overflow
=====================================

.. note::

   This section applies only to MRS 3.3.1-LTS or later.

Alarm Description
-----------------

This alarm is generated when the JDBCServer process forwards requests and triffic control is triggered due to insufficient session resources. In this case, too many requests are sent to the JDBCServer process, exceeding the processing capability of the JDBCServer process.

Alarm Attributes
----------------

+-----------------------+--------------------------------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                                               | Auto Cleared          |
+=======================+==============================================================+=======================+
| 43028                 | Minor (default threshold: 9 for three consecutive times)     | No                    |
|                       |                                                              |                       |
|                       | Critical (default threshold: 12 for three consecutive times) |                       |
+-----------------------+--------------------------------------------------------------+-----------------------+

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

Requests that cannot be processed are responded with a failure message.

Possible Causes
---------------

The JDBCServer process on the node is overloaded.

Handling Procedure
------------------

**Check the source of the requests for connecting to the JDBCServer service.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms** and select the alarm whose ID is **43028**. Check the role name and the IP address of the host where the alarm is generated in **Location**.
#. On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark** > **Instances**, click the JDBCServer for which this alarm is generated, and click **jdbcserver-audit** in the **Log** column on the left.
#. Click the download button in the lower left corner to download the logs to the local PC.
#. Search for **UserIP** in the logs, collect statistics on the IP addresses of the clients that submit a large number of requests, and limit the traffic of these clients to reserve resources for other clients.

**Collect fault information.**

5. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.
6. Expand the **Service** drop-down list, and select **Spark** for the target cluster.
7. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.
8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm needs to be cleared manually.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002381622762.png
