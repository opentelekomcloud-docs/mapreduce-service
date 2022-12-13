:original_name: mrs_01_0232.html

.. _mrs_01_0232:

Managing Services and Monitoring Hosts
======================================

You can manage the following status and indicators of all services (including role instances) and hosts on the MRS Manager:

-  Status information: includes operation, health, configuration, and role instance status.
-  Metric information: includes key monitoring metrics for services.
-  Metric export: allows you to export monitoring reports.

.. note::

   Set an automatic refresh interval or click |image1| for an immediate refresh.

   The following refresh interval options are supported:

   -  Refresh every 30 seconds
   -  Refresh every 60 seconds
   -  Stop refreshing

.. _mrs_01_0232__en-us_topic_0035209600_section37246995143046:

Managing Service Monitoring
---------------------------

#. On MRS Manager, click **Services**.

   The service list includes **Service**, **Operating Status**, **Health Status**, **Configuration Status**, **Roles**, and **Operation** are displayed in the component list.

   -  :ref:`Table 1 <mrs_01_0232__en-us_topic_0035209600_table4224219143943>` describes the service operating status.

      .. _mrs_01_0232__en-us_topic_0035209600_table4224219143943:

      .. table:: **Table 1** Service operating status

         +-----------------+------------------------------------------------------------------------+
         | Status          | Description                                                            |
         +=================+========================================================================+
         | Started         | The service is started.                                                |
         +-----------------+------------------------------------------------------------------------+
         | Stopped         | The service is stopped.                                                |
         +-----------------+------------------------------------------------------------------------+
         | Failed to start | Failed to start the role instance.                                     |
         +-----------------+------------------------------------------------------------------------+
         | Failed to stop  | Failed to stop the role instance.                                      |
         +-----------------+------------------------------------------------------------------------+
         | Unknown         | Indicates initial service status after the background system restarts. |
         +-----------------+------------------------------------------------------------------------+

   -  :ref:`Table 2 <mrs_01_0232__en-us_topic_0035209600_table43931038143943>` describes the service health status.

      .. _mrs_01_0232__en-us_topic_0035209600_table43931038143943:

      .. table:: **Table 2** Service health status

         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Status            | Description                                                                                                                                                        |
         +===================+====================================================================================================================================================================+
         | Good              | Indicates that all role instances in the service are running properly.                                                                                             |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Bad               | Indicates that the running status of at least one role instance is **Faulty** or the status of the service on which the current service depends is abnormal.       |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Unknown           | Indicates that all role instances in the service are in the **Unknown** state.                                                                                     |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Concerning        | Indicates that the background system is restarting the service.                                                                                                    |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Partially Healthy | Indicates that the status of the service on which the service depends is abnormal, and APIs related to the abnormal service cannot be invoked by external systems. |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   -  :ref:`Table 3 <mrs_01_0232__en-us_topic_0035209600_table16122213143943>` describes the service health status.

      .. _mrs_01_0232__en-us_topic_0035209600_table16122213143943:

      .. table:: **Table 3** Service configuration status

         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Status       | Description                                                                                                                                                  |
         +==============+==============================================================================================================================================================+
         | Synchronized | The latest configuration takes effect.                                                                                                                       |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Expired      | The latest configuration does not take effect after the parameter modification. Related services need to be restarted.                                       |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Failed       | The communication is incorrect or data cannot be read or written during the parameter configuration. Use **Synchronize Configuration** to rectify the fault. |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Configuring  | Parameters are being configured.                                                                                                                             |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Unknown      | Current configuration status cannot be obtained.                                                                                                             |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+

   By default, the **Service** column is sorted in ascending order. You can click the icon next to **Service**, **Operating Status**, **Health Status**, or **Configuration Status** to change the sorting mode.

#. Click a specified service in the list to view its status and metric information.

#. Customize monitoring metrics and export customized monitoring information.

   a. In the **Charts** area, click **Customize** to customize service monitoring metrics.
   b. In **Period** area, select a time of period and click **View** to view the monitoring data within the time period.
   c. Click **Export** to export the displayed metrics.

   **For MRS 1.7.2 or earlier:**

   a. In the **Real time** area, click **Customize** to customize service monitoring metrics.
   b. Click **History** to go to the historical monitoring query page.
   c. Select a time of period and click **View** to view the monitoring data within the time period.
   d. Click **Export** to export the displayed metrics.

.. _mrs_01_0232__en-us_topic_0035209600_section65508505145118:

Managing Role Instances
-----------------------

#. On MRS Manager, click **Services** and click the target service name in the service list.

#. Click **Instance** to view the role status.

   The role instance list contains the **Role**, **Host Name**, **OM IP Address**, **Business IP Address**, **Rack**, **Operation Status**, **Health Status,** and **Configuration Status** of an instance.

   -  :ref:`Table 4 <mrs_01_0232__en-us_topic_0035209600_table37414462155145>` shows the configuration status of a role instance.

      .. _mrs_01_0232__en-us_topic_0035209600_table37414462155145:

      .. table:: **Table 4** Role instance status

         +-----------------+------------------------------------------------------------------------------+
         | Status          | Description                                                                  |
         +=================+==============================================================================+
         | Started         | The role instance has been started.                                          |
         +-----------------+------------------------------------------------------------------------------+
         | Stopped         | The role instance has been stopped.                                          |
         +-----------------+------------------------------------------------------------------------------+
         | Failed to start | Failed to start the role instance.                                           |
         +-----------------+------------------------------------------------------------------------------+
         | Failed to stop  | Failed to stop the role instance.                                            |
         +-----------------+------------------------------------------------------------------------------+
         | Decommissioning | The role instance is being decommissioned.                                   |
         +-----------------+------------------------------------------------------------------------------+
         | Decommissioned  | The role instance has been decommissioned.                                   |
         +-----------------+------------------------------------------------------------------------------+
         | Recommissioning | The role instance is being recommissioned.                                   |
         +-----------------+------------------------------------------------------------------------------+
         | Unknown         | Indicates initial role instance status after the background system restarts. |
         +-----------------+------------------------------------------------------------------------------+

   -  :ref:`Table 5 <mrs_01_0232__en-us_topic_0035209600_table61889899144412>` shows the health status of a role instance.

      .. _mrs_01_0232__en-us_topic_0035209600_table61889899144412:

      .. table:: **Table 5** Role instance health status

         +------------+------------------------------------------------------------------------------------------------+
         | Status     | Description                                                                                    |
         +============+================================================================================================+
         | Good       | The role instance is running properly.                                                         |
         +------------+------------------------------------------------------------------------------------------------+
         | Bad        | The role instance is abnormal. For example, the port cannot be accessed if PID does not exist. |
         +------------+------------------------------------------------------------------------------------------------+
         | Unknown    | The host where a role instance resides does not connect to the background system.              |
         +------------+------------------------------------------------------------------------------------------------+
         | Concerning | The background system is restarting a role instance.                                           |
         +------------+------------------------------------------------------------------------------------------------+

   -  :ref:`Table 6 <mrs_01_0232__en-us_topic_0035209600_table20951019144412>` shows the configuration status of a role instance.

      .. _mrs_01_0232__en-us_topic_0035209600_table20951019144412:

      .. table:: **Table 6** Role instance configuration status

         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Status       | Description                                                                                                                                                  |
         +==============+==============================================================================================================================================================+
         | Synchronized | The latest configuration takes effect.                                                                                                                       |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Expired      | The latest configuration does not take effect after the parameter modification. Related services need to be restarted.                                       |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Failed       | The communication is incorrect or data cannot be read or written during the parameter configuration. Use **Synchronize Configuration** to rectify the fault. |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Configuring  | Parameters are being configured.                                                                                                                             |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Unknown      | Current configuration status cannot be obtained.                                                                                                             |
         +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+

   By default, the **Role** column is sorted in ascending order. You can click the sorting icon next to **Role**, **Host Name**, **OM IP Address**, **Business IP Address**, **Rack**, **Operating Status**, **Health Status**, or **Configuration Status** to change the sorting mode.

   You can filter out all instances of the same role in the **Role** column.

   You can set search criteria in the role search area by clicking **Advanced Search**, and click **Search** to view specified role information. Click **Reset** to clear the search criteria. Fuzzy search is supported.

#. Click the target role instance to view its status and metric information.

#. Customize monitoring metrics and export customized monitoring information.

   a. In the **Charts** area, click **Customize** to customize service monitoring metrics.
   b. In **Period** area, select a time of period and click **View** to view the monitoring data within the time period.
   c. Click **Export** to export the displayed metrics.

   **For MRS 1.7.2 or earlier:**

   a. In the **Real time** area, click **Customize** to customize service monitoring metrics.
   b. Click **History** to go to the historical monitoring query page.
   c. Select a time of period and click **View** to view the monitoring data within the time period.
   d. Click **Export** to export the displayed metrics.

.. _mrs_01_0232__en-us_topic_0035209600_section47168733145426:

Managing Hosts
--------------

#. On MRS Manager, click **Hosts** to view the status of all hosts.

   The host list contains the host name, management IP address, service IP address, rack, network speed, operating status, health status, disk usage, memory usage, and CPU usage.

   -  :ref:`Table 7 <mrs_01_0232__en-us_topic_0035209600_table63059102152614>` shows the host operating status.

      .. _mrs_01_0232__en-us_topic_0035209600_table63059102152614:

      .. table:: **Table 7** Host operating status

         +----------+-----------------------------------------------------------------------+
         | Status   | Description                                                           |
         +==========+=======================================================================+
         | Normal   | The host and service roles on the host are running properly.          |
         +----------+-----------------------------------------------------------------------+
         | Isolated | The host is isolated, and the service roles on the host stop running. |
         +----------+-----------------------------------------------------------------------+

   -  :ref:`Table 8 <mrs_01_0232__en-us_topic_0035209600_table48654081152619>` describes the host health status.

      .. _mrs_01_0232__en-us_topic_0035209600_table48654081152619:

      .. table:: **Table 8** Host health status

         +---------+---------------------------------------------------------------------------------------+
         | Status  | Description                                                                           |
         +=========+=======================================================================================+
         | Good    | The host can properly send heartbeats.                                                |
         +---------+---------------------------------------------------------------------------------------+
         | Bad     | The host fails to send heartbeats due to timeout.                                     |
         +---------+---------------------------------------------------------------------------------------+
         | Unknown | The host initial status is unknown during the operation of adding or deleting a host. |
         +---------+---------------------------------------------------------------------------------------+

   By default, the **Host Name** column is sorted by host name in ascending order. You can click the sorting icon next to **Host Name**, **OM IP Address**, **Business IP Address**, **Rack**, **Network Speed**, **Operating Status**, **Health Status**, **Disk Usage**, **Memory Usage**, or **CPU Usage** to change the sorting mode.

   You can set search criteria in the role search area by clicking **Advanced Search**, and click **Search** to view specified role information. Click **Reset** to clear the search criteria. Fuzzy search is supported.

#. Click the target host in the host list to view its status and metric information.

#. Customize monitoring metrics and export customized monitoring information.

   a. In the **Charts** area, click **Customize** to customize service monitoring metrics.
   b. In **Period** area, select a time of period and click **View** to view the monitoring data within the time period.
   c. Click **Export** to export the displayed metrics.

   **For MRS 1.7.2 or earlier:**

   a. In the **Real time** area, click **Customize** to customize service monitoring metrics.
   b. Click **History** to go to the historical monitoring query page.
   c. Select a time of period and click **View** to view the monitoring data within the time period.
   d. Click **Export** to export the displayed metrics.

.. |image1| image:: /_static/images/en-us_image_0000001348737925.png
