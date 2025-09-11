:original_name: ALM-50231.html

.. _ALM-50231:

ALM-50231 Abnormal Tablets Exist in Doris
=========================================

Alarm Description
-----------------

The alarm module checks for abnormal tablets in the Doris cluster every 5 minutes. This alarm is generated when an abnormal tablet is detected.

This alarm is cleared when no abnormal tablet exists in the Doris cluster.

This alarm applies only to MRS 3.5.0.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50231    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+--------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                        |
+======================+=============+====================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm was generated. |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated.           |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

Tablet exceptions may cause data query or write failures.

Possible Causes
---------------

The Doris data write frequency is too high, causing abnormal compaction operations or tablet migration failures.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, wait two minutes, and check whether the alarm is automatically cleared (the alarm logic includes the automatic clearance function).

   -  If yes, no further action is required.
   -  If no, go to :ref:`2 <alm-50231__en-us_topic_0000002000518905_li8386112192615>`.

**Check the abnormal tablet and rectify the fault.**

2. .. _alm-50231__en-us_topic_0000002000518905_li8386112192615:

   Select the alarm and check the value of **tabletId** in **Additional Information**. If there are a large number of abnormal tablets and the additional information cannot completely display related information, search for "Abnormal tablets have" in the **${BIGDATA_LOG_HOME}/nodeagent/monitorlog/pluginmonitor.log** file on the Master FE node. View the information about all abnormal tablets.

3. Log in to the node where MySQL is installed and connect to the Doris database.

   If Kerberos authentication (security mode) has been enabled for the cluster, run the following commands to connect to the Doris database:

   **export LIBMYSQL_ENABLE_CLEARTEXT_PLUGIN=1**

   **mysql -u**\ *Database login username* **-p**\ *Database login password* **-P**\ *Connection port for FE queries* **-h**\ *IP address of the Doris FE instance*

   .. note::

      -  To obtain the query connection port of the Doris FE instance, you can log in to MRS Manager, choose **Cluster** > **Services** > **Doris** > **Configurations**, and query the value of **query_port** of the Doris service.
      -  You can log in to MRS Manager and choose **Cluster** > **Services** > **Doris** > **Instances** to view the service IP address of any Doris FE instance.

4. .. _alm-50231__en-us_topic_0000002000518905_li15387221152613:

   Run the following command to view details about the abnormal tablet:

   **show tablet** *tabletId*\ **;**

   Record the **DbName** and **TableName** values of the abnormal tablet. Copy and run the command in the **DetailCmd** column in the command output as follows:

   **show proc** *xxx*\ **;**

   In the command output, check whether the value of **LstFailedTime** is **NULL** and whether the value of **VersionCount** is greater than the specified threshold (**200** by default).

   -  If yes, go to :ref:`5 <alm-50231__en-us_topic_0000002000518905_li1388162111261>`.
   -  If no, go to :ref:`8 <alm-50231__en-us_topic_0000002000518905_li2919122165013>`.

5. .. _alm-50231__en-us_topic_0000002000518905_li1388162111261:

   Run the following command to view the tablet repair and scheduling tasks that are being executed in the system:

   **show proc "/cluster_balance";**

   Check whether the values of **pending_tablets** and **running_tablets** in the command output decrease significantly based on the actual running environment.

   -  If yes, go to :ref:`6 <alm-50231__en-us_topic_0000002000518905_li1538872116263>`.
   -  If no, go to :ref:`8 <alm-50231__en-us_topic_0000002000518905_li2919122165013>`.

6. .. _alm-50231__en-us_topic_0000002000518905_li1538872116263:

   Restore the abnormal table first. In the command, replace *tableName* with the table name recorded in :ref:`4 <alm-50231__en-us_topic_0000002000518905_li15387221152613>`.

   **admin repair table** *tableName*\ **;**

7. After the abnormal table is restored, wait 2 minutes and check whether the alarm is automatically cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-50231__en-us_topic_0000002000518905_li2919122165013>`.

**Collect fault information.**

8.  .. _alm-50231__en-us_topic_0000002000518905_li2919122165013:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **Doris** for the target cluster.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
