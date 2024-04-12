:original_name: mrs_01_24544.html

.. _mrs_01_24544:

Configuring Caching of Materialized Views
=========================================

After a materialized view is created for an SQL statement, the SQL statement is rewritten to be queried through the materialized view when the SQL statement is executed. If the rewrite cache function is enabled for materialized views, the rewritten SQL statements will be saved to the cache (a maximum of 10,000 records can be saved by default) after the SQL statement is executed for multiple times. When the SQL statement is executed within the cache validity period (24 hours by default), the system obtains the rewritten SQL statement from the cache instead of rewriting the SQL statement.

You can add user-defined parameters **rewrite.cache.timeout** and **rewrite.cache.limit** to a compute instance to set the cache validity period and the maximum number of rewritten SQL statements that can be saved.

-  When a new materialized view is created or an existing materialized view is deleted, the cache becomes invalid.
-  If the materialized view associated with a rewritten SQL query in the cache becomes invalid or is in the **Refreshing** status, the rewritten SQL query will not be used.
-  When the cache is used, the executed SQL query cannot be changed. Otherwise, it will be treated as a new SQL query.
-  A maximum of 500 materialized views can be rewritten for SQL queries. That is, if the materialized views used during SQL rewriting are included in the 500 materialized views, the views will be rewritten. Otherwise, the views will be executed as common SQL statements. You can refer to :ref:`System level <mrs_01_24544__en-us_topic_0000001470000412_li2891647173015>` to add user-defined parameter **hetu.select.top.materialized.view** to compute instances to change the number of materialized views that can be used.

Enabling Rewrite Cache for Materialized Views
---------------------------------------------

-  Session level:

   Run the **set session rewrite_cache_enabled=true** command on the HetuEngine client by referring to :ref:`Using the HetuEngine Client <mrs_01_1737>`.

-  .. _mrs_01_24544__en-us_topic_0000001470000412_li2891647173015:

   Enabling the materialized view rewriting capability at the system level:

   #. Log in to FusionInsight Manager as a user who can access the HetuEngine web UI.
   #. Choose **Cluster** > **Services** > **HetuEngine** to go its service page.
   #. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
   #. Check whether the status of the instance to be operated is **STOPPED**. If not, change the status to **STOPPED**.
   #. Locate the row that contains the target instance, click **Configure** in the **Operation** column, and add the following customized parameters:

      +-----------------------+-----------------+-------------------------------+--------------------------------------------------------------------------------------+
      | Parameter             | Value           | Parameter File                | Description                                                                          |
      +=======================+=================+===============================+======================================================================================+
      | rewrite.cache.enabled | true            | coordinator.config.properties | Enable the rewrite cache function for materialized views.                            |
      +-----------------------+-----------------+-------------------------------+--------------------------------------------------------------------------------------+
      | rewrite.cache.timeout | 86400000        | coordinator.config.properties | -  Change the validity period of the rewrite cache.                                  |
      |                       |                 |                               | -  If this parameter is left blank, **86400000** is used by default. The unit is ms. |
      +-----------------------+-----------------+-------------------------------+--------------------------------------------------------------------------------------+
      | rewrite.cache.limit   | 10000           | coordinator.config.properties | -  Modify the upper limit of the rewrite cache.                                      |
      |                       |                 |                               | -  If this parameter is left blank, **10000** is used by default.                    |
      +-----------------------+-----------------+-------------------------------+--------------------------------------------------------------------------------------+

   #. After the parameters are added, select **Start Now** and click **OK**.
