:original_name: ALM-14044.html

.. _ALM-14044:

ALM-14044 XceiverCount Value Exceeds the Threshold
==================================================

Alarm Description
-----------------

The system checks the **XceiverCount** value of each DataNode every 30 seconds. This alarm is generated when a DataNode's **XceiverCount** value exceeds 95% of the **dfs.datanode.max.transfer.threads** value. This parameter defines the maximum number of threads allowed for data transmission between DataNodes, with a default value of 8192. This alarm is cleared when the XceiverCount value on the DataNode falls to or below the configured threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
14044    Minor          Yes
======== ============== ============

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

The write speed in HDFS decreases, affecting the overall HDFS performance.

Possible Causes
---------------

-  The DataNode's **XceiverCount** value is not properly configured.
-  There is an excessive number of write requests in HDFS.

Handling Procedure
------------------

**Check whether the DataNode's XceiverCount value is properly configured.**

#. Log in to MRS Manager and choose **Cluster** > **Services** > **HDFS**. Click **Configurations** and then **All Configurations**. Search for the **dfs.datanode.max.transfer.threads** parameter.

#. Check whether the value is much smaller than the default value.

   -  If yes, go to :ref:`3 <alm-14044__en-us_topic_0000002519999855_en-us_topic_0000002476684101_li14470193752910>`.
   -  If no, go to :ref:`6 <alm-14044__en-us_topic_0000002519999855_en-us_topic_0000002476684101_li4795431151710>`.

#. .. _alm-14044__en-us_topic_0000002519999855_en-us_topic_0000002476684101_li14470193752910:

   Reset the parameter value to its default setting and click **Save**.

#. Click **Instances**, select all DataNode instances, and choose **More** > **Restart Instance** to restart all DataNode instances.

#. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-14044__en-us_topic_0000002519999855_en-us_topic_0000002476684101_li4795431151710>`.

**Expand the DataNode capacity.**

6. .. _alm-14044__en-us_topic_0000002519999855_en-us_topic_0000002476684101_li4795431151710:

   Expand the DataNode capacity.

7. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14044__en-us_topic_0000002519999855_en-us_topic_0000002476684101_li34608589013>`.

**Collect fault information.**

8.  .. _alm-14044__en-us_topic_0000002519999855_en-us_topic_0000002476684101_li34608589013:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, select the HDFS services for the target cluster, and click **OK**.

10. Click the edit icon in the upper right corner and select a time span starting 10 minutes before and ending 10 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
