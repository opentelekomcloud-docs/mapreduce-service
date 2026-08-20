:original_name: ALM-16055.html

.. _ALM-16055:

ALM-16055 Hive Failed to Access the Data Warehouse Directory
============================================================

Alarm Description
-----------------

The Hive service checks whether the Hive data warehouse directory can be accessed properly at startup and periodically every 60 seconds after startup. If the directory cannot be accessed, this alarm is reported.

When the Hive service can access the Hive data warehouse directory at startup and every 60 seconds after startup, this alarm is cleared.

This section applies only to MRS 3.6.0-LTS or later.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
16055    Critical       Quality of service Hive         Yes
======== ============== ================== ============ ============

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
|                      | HostName    | Specifies the host for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

The system cannot provide data loading, query, and extraction functions.

Possible Causes
---------------

-  The HDFS service is abnormal.
-  OBS is abnormal.

Handling Procedure
------------------

#. Log in to MRS Manager, and choose **O&M** > **Alarm** > **Alarms**.
#. Click the alarm name to expand the details and check **Alarm Cause** to obtain the cause of the alarm.

   -  If **HDFS abnormal** is displayed, go to :ref:`3 <alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li1790735272819>`.
   -  If **Failed to access OBS. Check whether the OBS connection is normal.** is displayed, go to :ref:`6 <alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li1470212916466>`.

3. .. _alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li1790735272819:

   In the alarm list, check whether there is an **HDFS Service Unavailable** alarm.

   -  If yes, go to :ref:`4 <alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li28666548161349>`.
   -  If no, go to :ref:`6 <alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li1470212916466>`.

4. .. _alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li28666548161349:

   Rectify the fault by performing the operations provided for **ALM-14000 HDFS Service Unavailable**.

5. In the alarm list, check whether the HDFS Service Unavailable and Hive Failed to Access the Data Warehouse Directory alarms are cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li1470212916466>`.

6. .. _alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li1470212916466:

   Contact O&M personnel of OBS to rectify the OBS fault.

7. Check whether the alarm is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li38650106161349>`.

**Collect fault information.**

8.  .. _alm-16055__en-us_topic_0000002409812577_en-us_topic_0000002404986161_li38650106161349:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, select **HDFS** and **Hive** for the target cluster, and click **OK**.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.
