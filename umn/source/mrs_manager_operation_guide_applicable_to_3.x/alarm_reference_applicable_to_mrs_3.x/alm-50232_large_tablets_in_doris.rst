:original_name: ALM-50232.html

.. _ALM-50232:

ALM-50232 Large Tablets in Doris
================================

Alarm Description
-----------------

The alarm module checks whether a tablet greater than 3 GB (specified by the **alarm_tablet_max_size** parameter) exists in the Doris cluster every 5 minutes. This alarm is generated when such a tablet exists in the Doris cluster.

This alarm is cleared when no such a tablet exists in the Doris cluster.

This alarm applies only to MRS 3.5.0.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50232    Warning        Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------+--------------------------------------------------------------------+
| Type                   | Parameter   | Description                                                        |
+========================+=============+====================================================================+
| Location Information   | Source      | Specifies the cluster or system for which the alarm was generated. |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | ServiceName | Specifies the service for which the alarm was generated.           |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | RoleName    | Specifies the role for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | HostName    | Specifies the host for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
| Additional Information | db          | Specifies the database where a large tablet exists.                |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | table       | Specifies the table name of the large tablet.                      |
+------------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

If a tablet is large, the Doris query speed or compaction speed may slow down.

Possible Causes
---------------

The data written to the Doris table is greater than the estimated value or the partition settings are improper. As a result, the sizes of tablets in different partitions differ greatly.

Handling Procedure
------------------

**Check whether the imported data is too large or the table field partitions are improperly set.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, select the alarm whose ID is **50232**, and view the **db** and **table** values in **Additional Information**. If there are too many large tablets and the additional information cannot completely display related information, search for "Large tablets have" in the **${BIGDATA_LOG_HOME}/nodeagent/monitorlog/pluginmonitor.log** file on the Master FE node. View the information about all large tablets.

#. Log in to the node where MySQL is installed and connect to the Doris database.

   If Kerberos authentication (security mode) has been enabled for the cluster, run the following commands to connect to the Doris database:

   **export LIBMYSQL_ENABLE_CLEARTEXT_PLUGIN=1**

   **mysql -u**\ *Database login username* **-p**\ *Database login password* **-P**\ *Connection port for FE queries* **-h**\ *IP address of the Doris FE instance*

   .. note::

      -  To obtain the query connection port of the Doris FE instance, you can log in to MRS Manager, choose **Cluster** > **Services** > **Doris** > **Configurations**, and query the value of **query_port** of the Doris service.
      -  You can log in to MRS Manager and choose **Cluster** > **Services** > **Doris** > **Instances** to view the service IP address of any Doris FE instance.

#. Run the following command to view details about the abnormal tablet:

   **show tablets from** *dbName*\ **.**\ *tableName*\ **;**

   Check whether the ratio of the tablet sizes in the command output is less than 10%.

   -  If yes, go to :ref:`4 <alm-50232__en-us_topic_0000001963918056_li992494822910>`.
   -  If no, go to :ref:`5 <alm-50232__en-us_topic_0000001963918056_li132322306332>`.

#. .. _alm-50232__en-us_topic_0000001963918056_li992494822910:

   The imported data is greater than the estimated data. As a result, the sizes of tablets in different partitions differ greatly. Run the following command to view the table creation statement:

   **show create table** *dbName.tableName*\ **;**

   Re-estimate the amount of data to be written to the table. Based on the data volume, increase the size of **BUCKETS** to ensure that the tablet size in each partition ranges from 100 MB to 3 GB. Re-create the *tableNameBak* table and go to :ref:`6 <alm-50232__en-us_topic_0000001963918056_li127921227235>`.

#. .. _alm-50232__en-us_topic_0000001963918056_li132322306332:

   Tablet sizes in different partitions vary greatly due to improper settings of table partition fields. Run the following command to view the table creation statement:

   **show create table** *dbName.tableName*\ **;**

   Reset the partition field in the table creation statement. The partition field can be used to distinguish data in the table more evenly. Create the *tableNameBak* table and go to :ref:`6 <alm-50232__en-us_topic_0000001963918056_li127921227235>`.

#. .. _alm-50232__en-us_topic_0000001963918056_li127921227235:

   Run the following command to write the data in the *tableName* table reported in the alarm to the *tableNameBak* table:

   **insert into** *tableNameBak* **select \* from** *tableName*\ **;**

#. .. _alm-50232__en-us_topic_0000001963918056_li11793192214231:

   After data is successfully written, run the following commands to check whether the number of data records in the *tableName* table is the same as that in the *tableNameBak* table:

   **select count(*) from** *dbName.tableName*\ **;**

   **select count(*) from** *dbName.tableNameBak*\ **;**

   -  If yes, go to :ref:`9 <alm-50232__en-us_topic_0000001963918056_li05779337517>`.
   -  If no, go to :ref:`8 <alm-50232__en-us_topic_0000001963918056_li979342216231>`.

#. .. _alm-50232__en-us_topic_0000001963918056_li979342216231:

   Run the following command to delete the *tableNameBak* table:

   **drop table** *dbName.tableNameBak*\ **;**

   After the table is deleted, increase the value of **BUCKETS** or reset the table fields to create a table, perform :ref:`6 <alm-50232__en-us_topic_0000001963918056_li127921227235>` to :ref:`7 <alm-50232__en-us_topic_0000001963918056_li11793192214231>` to import data, and compare the data. If the data records are still inconsistent, go to :ref:`11 <alm-50232__en-us_topic_0000001963918056_li15316430237>`.

#. .. _alm-50232__en-us_topic_0000001963918056_li05779337517:

   Run the following command to delete the *tableName* table:

   **drop table** *dbName.tableName*\ **;**

   Run the following command to change the table name:

   **alter table** *dbName.tableNameBak* **rename** *dbName.tableName*\ **;**

10. After the data in the two tables is consistent, wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-50232__en-us_topic_0000001963918056_li15316430237>`.

**Collect fault information.**

11. .. _alm-50232__en-us_topic_0000001963918056_li15316430237:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

12. Expand the **Service** drop-down list, and select **Doris** for the target cluster.

13. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.
