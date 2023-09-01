:original_name: admin_guide_000074.html

.. _admin_guide_000074:

Log Online Search
=================

Scenario
--------

FusionInsight Manager allows you to search for logs online and view the log content of components to locate faults.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **O&M** > **Log** > **Online Search**.

#. Configure the parameters listed in :ref:`Table 1 <admin_guide_000074__table14922145885914>` to search for the logs you need. You can select a default log search duration (including **0.5h**, **1h**, **2h**, **6h**, **12h**, **1d**, **1w**, and **1m**), or click |image1| to customize **Start Data** and **End Data**.

   .. _admin_guide_000074__table14922145885914:

   .. table:: **Table 1** Log search parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================================================================================================================+
      | Search Content                    | Keywords or regular expression to be searched for                                                                                                                                                                                                                                           |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Service                           | Service or module for which you want to query logs                                                                                                                                                                                                                                          |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | File                              | Log files to be searched for when only one role is selected                                                                                                                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Lowest Log Level                  | Lowest level of logs to be queried. After you select a level, the logs of this level and higher levels are displayed.                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                             |
      |                                   | The levels in ascending order are as follows:                                                                                                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                                             |
      |                                   | TRACE < DEBUG < INFO < WARN < ERROR < FATAL                                                                                                                                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Host Scope                        | -  You can click |image2| to select hosts.                                                                                                                                                                                                                                                  |
      |                                   | -  Enter the host name of the node for which you want to query logs or the IP address of the management plane.                                                                                                                                                                              |
      |                                   | -  Use commas (,) to separate IP addresses, for example, **192.168.10.10**,\ **192.168.10.11**.                                                                                                                                                                                             |
      |                                   | -  Use hyphens (-) to indicate an IP address segment if the IP addresses are consecutive, for example, **192.168.10.[10-20]**.                                                                                                                                                              |
      |                                   | -  Use hyphens (-) to indicate an IP address segment if the IP addresses are consecutive, and use commas (,) to separate IP address segments, for example, **192.168.10.[10-20,30-40]**.                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                             |
      |                                   |    .. note::                                                                                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                             |
      |                                   |       -  If this parameter is not specified, all hosts are selected by default.                                                                                                                                                                                                             |
      |                                   |       -  A maximum of 10 expressions can be entered at a time.                                                                                                                                                                                                                              |
      |                                   |       -  A maximum of 2,000 hosts can be matched for all entered expressions at a time.                                                                                                                                                                                                     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Advanced Configurations           | -  **Max Quantity**: maximum number of logs that can be displayed at a time. If the number of queried logs exceeds the value of this parameter, the earliest logs will be ignored. If this parameter is not set, the maximum number of logs that can be displayed at a time is not limited. |
      |                                   | -  **Timeout Duration**: log query timeout duration. This parameter is used to limit the maximum log query time on each node. When the query times out, the query is stopped and the logs that have been searched for are still displayed.                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Search**. :ref:`Table 2 <admin_guide_000074__table92081419119>` describes the fields in search results.

   .. _admin_guide_000074__table92081419119:

   .. table:: **Table 2** Parameters in search results

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                |
      +===================================+============================================================================================================================================================================================================================================================================================================+
      | Time                              | Time when a line of log is generated                                                                                                                                                                                                                                                                       |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source Cluster                    | Cluster for which the log is generated                                                                                                                                                                                                                                                                     |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Host Name                         | Host name of the node where the log file recording the line of log is located                                                                                                                                                                                                                              |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Location                          | Path of the log file recording the line of log                                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                            |
      |                                   | Click the location information to go to the online log browsing page. By default, 100 lines of logs before and 100 lines after the line of log are displayed. You can click **Load More** on the top or bottom of the page to view more logs. Click **Download** to download the log file to the local PC. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Line No.                          | Line number of a line of log in the log file                                                                                                                                                                                                                                                               |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Level                             | Level of the line of log                                                                                                                                                                                                                                                                                   |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Log                               | Log content                                                                                                                                                                                                                                                                                                |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      You can click **Stop** to forcibly stop the search. You can view the search results in the list.

#. Click **Filter** to filter the logs to display on the page. :ref:`Table 3 <admin_guide_000074__table5795173012197>` lists the fields that you can use to filter logs. After you configure these parameters, click **Filter** to search for logs meeting the search criteria. You can click **Reset** to clear the information that you have filled in.

   .. _admin_guide_000074__table5795173012197:

   .. table:: **Table 3** Parameters for filtering logs

      ============== ==========================================
      Parameter      Description
      ============== ==========================================
      Keywords       Keywords of the losg to be searched for
      Host Name      Name of the host to be searched for
      Location       Path of the log file to be searched for
      Started        Start time for logs to be searched for
      Completed      End time for logs to be searched for
      Source Cluster Cluster for which logs need to be searched
      ============== ==========================================

.. |image1| image:: /_static/images/en-us_image_0000001442413841.png
.. |image2| image:: /_static/images/en-us_image_0000001442773597.png
