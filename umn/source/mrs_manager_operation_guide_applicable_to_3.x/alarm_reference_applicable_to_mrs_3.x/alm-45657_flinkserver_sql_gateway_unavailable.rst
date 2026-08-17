:original_name: ALM-45657.html

.. _ALM-45657:

ALM-45657 FlinkServer SQL Gateway Unavailable
=============================================

This section applies to MRS 3.6.0-LTS.1 or later.

Alarm Description
-----------------

The alarm module checks the FlinkServer SQL Gateway status every 60 seconds. This alarm is generated when the SQL Gateway cannot be connected. This alarm is cleared when the SQL Gateway recovers.

Alarm Attributes
----------------

======== ============== =========== ============ ============
Alarm ID Alarm Severity Alarm Type  Service Type Auto Cleared
======== ============== =========== ============ ============
45657    Major          Environment Flink        Yes
======== ============== =========== ============ ============

Alarm Parameters
----------------

+----------------------+-------------+----------------------------------------------------------+
| Type                 | Parameter   | Description                                              |
+======================+=============+==========================================================+
| Location Information | Source      | Specifies the cluster for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

When the FlinkServer SQL Gateway is unavailable, the syntax verification, lineage analysis, and catalog management functions on the FlinkServer page are also unavailable.

Possible Causes
---------------

The SQL Gateway port binding failed, and the SQL Gateway becomes unavailable.

Handling Procedure
------------------

**View alarm information.**

#. Log in to MRS Manager as a user with FlinkServer administrator permissions.
#. Choose **O&M** > **Alarm** > **Alarms** > **ALM-45657 FlinkServer SQL Gateway Unavailable**, and view the host name in the **Location** field. Click the hyperlink next to **HostName**, and check and record the IP address corresponding to the host name.

**Check whether the SQL Gateway port failed to bind.**

3. Log in to the host for which the alarm is reported as user **omm**.

4. Run the following command to check whether the port is occupied by another process:

   .. code-block::

      netstat -anp | grep 28947

   -  If yes, replan the port range of the process and go to :ref:`5 <alm-45657__en-us_topic_0000002544664979_en-us_topic_0000002512229592_li1423917141284>`.
   -  If no, go to :ref:`6 <alm-45657__en-us_topic_0000002544664979_en-us_topic_0000002512229592_li4749473185459>`.

5. .. _alm-45657__en-us_topic_0000002544664979_en-us_topic_0000002512229592_li1423917141284:

   Wait for 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45657__en-us_topic_0000002544664979_en-us_topic_0000002512229592_li4749473185459>`.

**Collect fault information.**

6. .. _alm-45657__en-us_topic_0000002544664979_en-us_topic_0000002512229592_li4749473185459:

   On MRS Manager, choose **O&M** > **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Flink** for the target cluster.

8. Click |image1| in the upper right corner, and select a time span starting 30 minutes before and ending 30 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002685889343.png
