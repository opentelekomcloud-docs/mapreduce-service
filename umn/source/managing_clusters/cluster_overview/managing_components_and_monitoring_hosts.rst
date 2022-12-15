:original_name: mrs_01_0517.html

.. _mrs_01_0517:

Managing Components and Monitoring Hosts
========================================

You can manage the following status and metrics of all components (including role instances) and hosts on the MRS console:

-  Status information: includes operation, health, configuration, and role instance status.
-  Indicator information: includes key monitoring indicators for each component.
-  Export monitoring metrics. (This function is not supported in MRS 3.x or later.)

.. note::

   -  For MRS 1.7.2 or later and MRS 2.x, see :ref:`Managing Services and Monitoring Hosts <mrs_01_0232>`.

   -  For MRS 3.x or later, see :ref:`Procedure <mrs_01_0517__section18139102419196>`.
   -  You can set the interval for automatically refreshing the page or click |image1| to refresh the page immediately.
   -  Component management supports the following parameter values:

      -  Refresh every 30 seconds
      -  Refresh every 60 seconds
      -  Stop refreshing

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

.. _mrs_01_0517__section18139102419196:

Procedure
---------

**Managing Components**

.. note::

   For details about how to perform operations on MRS Manager, see :ref:`Managing Service Monitoring <mrs_01_0232__en-us_topic_0035209600_section37246995143046>`.

#. On the MRS cluster details page, click **Components**.

   On the **Components** tab page, **Service**, **Operating Status**, **Health Status**, **Configuration Status**, **Role**, and **Operation** are displayed in the component list.

   -  :ref:`Table 1 <mrs_01_0517__table4726131425215>` describes the service operating status.

      .. _mrs_01_0517__table4726131425215:

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
         | Failed to stop  | Failed to stop the service.                                            |
         +-----------------+------------------------------------------------------------------------+
         | Unknown         | Indicates initial service status after the background system restarts. |
         +-----------------+------------------------------------------------------------------------+

   -  :ref:`Table 2 <mrs_01_0517__table1972816146524>` describes the service health status.

      .. _mrs_01_0517__table1972816146524:

      .. table:: **Table 2** Service health status

         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Status            | Description                                                                                                                                                        |
         +===================+====================================================================================================================================================================+
         | Good              | Indicates that all role instances in the service are running properly.                                                                                             |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Faulty            | Indicates that the running status of at least one role instance is **Faulty** or the status of the service on which the current service depends is abnormal.       |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Unknown           | Indicates that all role instances in the service are in the **Unknown** state.                                                                                     |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Restoring         | Indicates that the background system is restarting the service.                                                                                                    |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Partially Healthy | Indicates that the status of the service on which the service depends is abnormal, and APIs related to the abnormal service cannot be invoked by external systems. |
         +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   -  :ref:`Table 3 <mrs_01_0517__table1172913145524>` describes the service health status.

      .. _mrs_01_0517__table1172913145524:

      .. table:: **Table 3** Service configuration status

         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Status                | Description                                                                                                                                                  |
         +=======================+==============================================================================================================================================================+
         | Synchronized          | The latest configuration takes effect.                                                                                                                       |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Configuration expired | The latest configuration does not take effect after the parameter modification. Related services need to be restarted.                                       |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Configuration failed  | The communication is incorrect or data cannot be read or written during the parameter configuration. Use **Synchronize Configuration** to rectify the fault. |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Configuring           | Parameters are being configured.                                                                                                                             |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Unknown               | Indicates that configuration status cannot be obtained.                                                                                                      |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+

   By default, the **Service** column is sorted in ascending order. You can click the icon next to **Service**, **Operating Status**, **Health Status**, or **Configuration Status** to change the sorting mode.

2. Click a specified service in the list to view its status and metric information.
3. Customize and view monitoring graphs.

   a. In the **Charts** area, click **Customize** to customize service monitoring metrics.
   b. In **Period** area, select a time of period and click **View** to view the monitoring data within the time period.

**Managing Role Instances**

.. note::

   For versions earlier than MRS 3.x, see :ref:`Managing Role Instances <mrs_01_0232__en-us_topic_0035209600_section65508505145118>`.

#. On the MRS cluster details page, click **Components**. In the component list, click the specified service name.

#. Click **Instances** to view the role status.

   The role instance list contains the Role, Host Name, Management IP Address, Service IP Address, Rack, Running Status, and Configuration Status of each instance.

   -  :ref:`Table 4 <mrs_01_0517__table1573318141522>` shows the running status of a role instance.

      .. _mrs_01_0517__table1573318141522:

      .. table:: **Table 4** Role instance running status

         +---------------------+----------------------------------------------------------------------------------------------------------+
         | Status              | Description                                                                                              |
         +=====================+==========================================================================================================+
         | **Good**            | Indicates that the instance is running properly.                                                         |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Bad**             | Indicates that the instance cannot run properly.                                                         |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Decommissioned**  | Indicates that the instance is out of service.                                                           |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Not started**     | Indicates that the instance is stopped.                                                                  |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Unknown**         | Indicates that the initial status of the instance cannot be detected.                                    |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Starting**        | Indicates that the instance is being started.                                                            |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Stopping**        | Indicates that the instance is being stopped.                                                            |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Restoring**       | Indicates that an exception may occur in the instance and the instance is being automatically rectified. |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Decommissioning** | Indicates that the instance is being decommissioned.                                                     |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Recommissioning** | Indicates that the instance is being recommissioned.                                                     |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Failed to start** | Indicates that the service fails to be started.                                                          |
         +---------------------+----------------------------------------------------------------------------------------------------------+
         | **Failed to stop**  | Indicates that the service fails to be stopped.                                                          |
         +---------------------+----------------------------------------------------------------------------------------------------------+

   -  :ref:`Table 5 <mrs_01_0517__table07347145524>` shows the configuration status of a role instance.

      .. _mrs_01_0517__table07347145524:

      .. table:: **Table 5** Role instance configuration status

         +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Status                    | Description                                                                                                                                                  |
         +===========================+==============================================================================================================================================================+
         | **Synchronized**          | The latest configuration takes effect.                                                                                                                       |
         +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **Configuration expired** | The latest configuration does not take effect after the parameter modification. Related services need to be restarted.                                       |
         +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **Configuration failed**  | The communication is incorrect or data cannot be read or written during the parameter configuration. Use **Synchronize Configuration** to rectify the fault. |
         +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **Configuring**           | Parameters are being configured.                                                                                                                             |
         +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **Unknown**               | Current configuration status cannot be obtained.                                                                                                             |
         +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+

   By default, the **Role** column is sorted in ascending order. You can click the sorting icon next to **Role**, **Host Name**, **OM IP Address**, **Business IP Address**, **Rack**, **Running Status**, or **Configuration Status** to change the sorting mode.

   You can filter out all instances of the same role in the **Role** column.

   You can set search criteria in the role search area by clicking **Advanced Search**, and click **Search** to view specified role information. You can click **Reset** to reset the search criteria. Fuzzy search is supported.

#. Click the target role instance to view its status and metric information.

#. Customize and view monitoring graphs.

   a. In the **Charts** area, click **Customize** to customize service monitoring metrics.
   b. In **Period** area, select a time of period and click **View** to view the monitoring data within the time period.

**Managing Hosts**

.. note::

   For versions earlier than MRS 3.x, see :ref:`Managing Hosts <mrs_01_0232__en-us_topic_0035209600_section47168733145426>`.

#. On the MRS cluster details page, click the **Nodes** tab and expand a node group to view the host status.

   The host list contains the **Node Name**, **IP Address**, **Rack**, **Operating** **Status**, **Health Status**, **CPU Usage**, **Memory Usage**, **Disk Usage**, **Network Speed**, Specification Name, **Specifications** and **AZ**.

   -  :ref:`Table 6 <mrs_01_0517__table107411314105212>` shows the host operating status.

      .. _mrs_01_0517__table107411314105212:

      .. table:: **Table 6** Host operating status

         +----------+-----------------------------------------------------------------------+
         | Status   | Description                                                           |
         +==========+=======================================================================+
         | Normal   | The host and service roles on the host are running properly.          |
         +----------+-----------------------------------------------------------------------+
         | Isolated | The host is isolated, and the service roles on the host stop running. |
         +----------+-----------------------------------------------------------------------+

   -  :ref:`Table 7 <mrs_01_0517__table1774281415526>` describes the host health status.

      .. _mrs_01_0517__table1774281415526:

      .. table:: **Table 7** Host health status

         +---------+---------------------------------------------------------------------------------------+
         | Status  | Description                                                                           |
         +=========+=======================================================================================+
         | Good    | The host can properly send heartbeats.                                                |
         +---------+---------------------------------------------------------------------------------------+
         | Bad     | The host fails to send heartbeats due to timeout.                                     |
         +---------+---------------------------------------------------------------------------------------+
         | Unknown | The host initial status is unknown during the operation of adding or deleting a host. |
         +---------+---------------------------------------------------------------------------------------+

   The nodes are sorted in ascending order by default. You can click **Node Name**, **IP Address**, **Rack**, **Operating** **Status**, **Health Status**, **CPU Usage**, **Memory Usage**, **Disk Usage**, **Network Speed**, **Specification Name**, or **Specifications** to change the sorting mode.

#. Click the target node in the list to view its status and metric information.

.. |image1| image:: /_static/images/en-us_image_0000001348737925.png
