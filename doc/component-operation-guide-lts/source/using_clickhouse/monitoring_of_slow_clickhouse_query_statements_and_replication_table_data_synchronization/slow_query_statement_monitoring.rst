:original_name: mrs_01_24230.html

.. _mrs_01_24230:

Slow Query Statement Monitoring
===============================

Scenario
--------

The SQL statement query in ClickHouse is slow because the conditions such as partitions, where conditions, and indexes of SQL statements are set improperly. As a result, the overall performance of the database is affected. To solve this problem, MRS provides the function of monitoring slow ClickHouse query statements.

Ongoing Slow Queries
--------------------

You can query information about slow SQL statements that are being executed but do not return any result.

-  **Procedure**

   Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. On the displayed page, click the **Query Management** tab and then the **Ongoing Slow Queries** tab.

-  **Parameters**

   .. _mrs_01_24230__en-us_topic_0000001173470902_table1578619528431:

   .. table:: **Table 1** Slow query parameters

      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter              | Description                                                                                                                                                                                                     |
      +========================+=================================================================================================================================================================================================================+
      | Server Node IP Address | IP address of the ClickHouseServer instance. To view the IP address, log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. On the displayed page, click the **Instance** tab. |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Query ID               | Unique ID generated internally.                                                                                                                                                                                 |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Query                  | Slow query SQL statement.                                                                                                                                                                                       |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Start Time             | Time when the execution of a slow query SQL statement starts.                                                                                                                                                   |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | End Time               | Time when the execution of a slow query SQL statement ends.                                                                                                                                                     |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Duration (s)           | Total execution time of a slow query SQL statement, in seconds.                                                                                                                                                 |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | User                   | ClickHouse user who executes a slow query SQL statement.                                                                                                                                                        |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Client IP Address      | IP address of the client that submits a slow query SQL statement.                                                                                                                                               |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Memory Used (MB)       | Memory used by a slow query SQL statement, in MB.                                                                                                                                                               |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Operation              | You can click **Terminate** to terminate the slow query using a slow query SQL statement.                                                                                                                       |
      +------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **Filter conditions**

   Select the query condition as required and filter the query results.

   |image1|

   .. _mrs_01_24230__en-us_topic_0000001173470902_table12626134121116:

   .. table:: **Table 2** Filter conditions

      +-----------------------------------+--------------------------------------------------------------------------------------------------------+
      | Condition                         | Description                                                                                            |
      +===================================+========================================================================================================+
      | Slow query duration exceeding     | Filters the slow queries based on the duration.                                                        |
      |                                   |                                                                                                        |
      |                                   | The value can be **3 (s)**, **9 (s)**, **15 (s)**, or **25 (s)**.                                      |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------+
      | By Query ID                       | Filters the slow queries based on the query ID.                                                        |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------+
      | By User                           | Filters the slow queries based on the ClickHouse user.                                                 |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------+
      | By Client IP Address              | Filters the slow queries based on the IP address of the client that submits slow query SQL statements. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------+

Completed Queries
-----------------

You can query information about slow SQL statements that have been executed and returned results.

Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. On the displayed page, click the **Query Management** tab and then the **Completed Queries** tab.

For details about slow query parameters and filter conditions, see :ref:`Table 1 <mrs_01_24230__en-us_topic_0000001173470902_table1578619528431>` and :ref:`Table 2 <mrs_01_24230__en-us_topic_0000001173470902_table12626134121116>`, respectively.

.. |image1| image:: /_static/images/en-us_image_0000001441092221.png
