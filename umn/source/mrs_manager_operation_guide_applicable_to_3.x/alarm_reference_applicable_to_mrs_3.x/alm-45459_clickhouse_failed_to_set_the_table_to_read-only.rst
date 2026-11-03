:original_name: ALM-45459.html

.. _ALM-45459:

ALM-45459 ClickHouse Failed to Set the Table to Read-Only
=========================================================

.. note::

   This section applies only to MRS 3.6.0-LTS.1 or later.

Alarm Description
-----------------

This alarm is generated when the read-only function of the standby cluster is enabled in the DR cluster but the ClickHouse DR table fails to be set to read-only.

This alarm is cleared when the DR table is successfully set to read-only.

Alarm Attributes
----------------

======== ============== ============== ============ ============
Alarm ID Alarm Severity Alarm Type     Service Type Auto Cleared
======== ============== ============== ============ ============
45459    Major          Error handling ClickHouse   Yes
======== ============== ============== ============ ============

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

If the table of the standby ClickHouse cluster fails to be set to read-only, writing data to the DR table in the DR cluster will cause DR data damage.

Possible Causes
---------------

-  The target table does not exist on the ClickHouseServer node.
-  The ClickHouseServer has reached its maximum concurrency limit.

Handling Procedure
------------------

**Check whether the target table exists on the ClickHouseServer node.**

#. .. _alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li15319205119354:

   Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address of the hostname in **Location**.

#. .. _alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li1334310002415:

   Log in to the node queried in :ref:`1 <alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li15319205119354>` as the **root** user and run the following commands to check the table that fails to be set to read-only:

   **su - omm**

   **cd ${BIGDATA_TMP}/disaster/ClickHouse/readOnly**

   **more failedTables.txt**

   .. note::

      In the preceding command, **ClickHouse** indicates the internal service name. In the multi-service scenario, it may be **ClickHouse-1,ClickHouse-2,...**

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm was reported* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm was reported* **--user** *Username* **--password --port** 9440

#. Run the following statement to check whether the table in :ref:`2 <alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li1334310002415>` exists:

   .. code-block::

      select database||'.'||name from system.tables where database = 'Database name' and name = 'Table name';

   -  If yes, go to :ref:`5 <alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li195348914449>`.
   -  If no, go to :ref:`7 <alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li6769733151816>`.

#. .. _alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li195348914449:

   Log in to the node queried in :ref:`1 <alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li15319205119354>` as the **root** user and run the following command to check whether the maximum concurrency limit is reached:

   .. code-block::

      grep -i "too many" /var/log/Bigdata/clickhouse/clickhouseServer/clickhouse-server.log | tail -n 3;

   -  If yes, go to :ref:`6 <alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li5558551128>`.
   -  If no, go to :ref:`7 <alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li6769733151816>`.

#. .. _alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li5558551128:

   Log in to MRS Manager of the active cluster, choose **Active/Standby Cluster DR** > **Details** > **Notifying the DR status**, enter the user password, and click **OK**. Wait for three minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li6769733151816>`.

**Collect fault information.**

7.  .. _alm-45459__en-us_topic_0000002605470735_en-us_topic_0000002554596599_li6769733151816:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list and select **ClickHouse** for the target cluster.

9.  Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Send the collected fault logs to O&M personnel for help.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
