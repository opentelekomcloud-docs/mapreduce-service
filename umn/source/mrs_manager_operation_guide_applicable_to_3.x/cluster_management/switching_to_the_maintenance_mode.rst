:original_name: admin_guide_000189.html

.. _admin_guide_000189:

Switching to the Maintenance Mode
=================================

Scenario
--------

MRS Manager allows you to set clusters, services, hosts, or OMSs to the maintenance mode. Objects in maintenance mode do not report alarms. This prevents the system from generating a large number of unnecessary alarms during maintenance changes, such as upgrade, because these alarms may influence O&M personnel's judgment on the cluster status.

-  Cluster maintenance mode

   If a cluster is not brought online or has been brought offline due to O&M operations (for example, non-rolling upgrade), you can set the entire cluster to the maintenance mode.

-  Service maintenance mode

   When performing maintenance operations on a specific service (for example, performing service-affecting commissioning operations like batch restart of service instances, directly powering on or off nodes of the service, or repairing the service), you can set only this service to the maintenance mode.

-  Host maintenance mode

   When performing maintenance operations on a host (such as powering on or off, isolating, or reinstalling the host, upgrading its OS, or replacing the host), you can set only this host to the maintenance mode.

-  OMS maintenance mode

   When restarting, replacing, or repairing an OMS node, you can set the OMS node to the maintenance mode.

Impact on the System
--------------------

After the maintenance mode is set, alarms caused by non-maintenance operations are suppressed and cannot be reported. Alarms can be reported only when faults persist after the system exits the maintenance mode. Therefore, exercise caution when setting the maintenance mode.

Procedure
---------

#. Log in to MRS Manager.

#. Set the maintenance mode.

   Determine the object to set the maintenance mode based on the service scenario. For details, see :ref:`Table 1 <admin_guide_000189__table8578183123419>`.

   .. _admin_guide_000189__table8578183123419:

   .. table:: **Table 1** Setting to the maintenance mode

      +----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scenario                                           | Operation                                                                                                                                                                                                                    |
      +====================================================+==============================================================================================================================================================================================================================+
      | Configure a cluster to enter the maintenance mode. | a. On MRS Manager, click |image1| next to the target cluster name and select **Enter Maintenance Mode**.                                                                                                                     |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    | b. In the displayed dialog box, click **OK**.                                                                                                                                                                                |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    |    After the cluster enters the maintenance state, the status of the cluster becomes |image2|. After maintenance is complete, click **Exit Maintenance Mode**. The cluster then exits the maintenance mode.                  |
      +----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configure a service to enter the maintenance mode. | a. On MRS Manager, choose **Cluster**, click the name of the desired cluster, choose **Services**, and click the service name.                                                                                               |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    | b. On the service details page, click **More** and select **Enter Maintenance Mode**.                                                                                                                                        |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    | c. In the displayed dialog box, click **OK**.                                                                                                                                                                                |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    |    After a service enters the maintenance mode, the status of the service becomes |image3| in the service list. After maintenance is complete, click **Exit Maintenance Mode**. The service then exits the maintenance mode. |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    |    .. note::                                                                                                                                                                                                                 |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    |       When configuring a service to enter the maintenance mode, you are advised to set the upper-layer services that depend on this service to the maintenance mode as well.                                                 |
      +----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configure a host to the maintenance mode.          | a. On MRS Manager, choose **Hosts**.                                                                                                                                                                                         |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    | b. On the **Hosts** page, select the target host, click **More**, and select **Enter Maintenance Mode**.                                                                                                                     |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    | c. In the displayed dialog box, click **OK**.                                                                                                                                                                                |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    |    After the host enters the maintenance mode, the status of the host becomes |image4| in the host list. After maintenance is complete, click **Exit Maintenance Mode**. The host then exits the maintenance mode.           |
      +----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configure the OMS to enter the maintenance mode.   | a. On MRS Manager, choose **System** > **OMS** > **Enter Maintenance Mode**.                                                                                                                                                 |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    | b. In the displayed dialog box, click **OK**.                                                                                                                                                                                |
      |                                                    |                                                                                                                                                                                                                              |
      |                                                    |    After the OMS enters the maintenance state, the OMS status becomes |image5|. After maintenance is complete, click **Exit Maintenance Mode**. The OMS then exits the maintenance mode.                                     |
      +----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Check the cluster maintenance view.

   On MRS Manager, click |image6| next to the cluster name and select **Maintenance Mode View**. In the displayed window, you can view the services and hosts in maintenance mode in the cluster.

   After maintenance is complete, you can select services and hosts in batches in the maintenance mode view and click **Exit Maintenance Mode** to make them exit the maintenance mode.

.. |image1| image:: /_static/images/en-us_image_0000001392254954.png
.. |image2| image:: /_static/images/en-us_image_0000001392734042.png
.. |image3| image:: /_static/images/en-us_image_0000001442413957.png
.. |image4| image:: /_static/images/en-us_image_0000001442773713.png
.. |image5| image:: /_static/images/en-us_image_0000001392734038.png
.. |image6| image:: /_static/images/en-us_image_0000001442773709.png
