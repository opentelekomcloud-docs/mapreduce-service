:original_name: mrs_01_0246.html

.. _mrs_01_0246:

Configuring Service Parameters
==============================

On MRS Manager, you can view and modify the default service configurations based on site requirements and export or import the configurations.

Impact on the System
--------------------

-  You need to download and update the client configuration files after configuring HBase, HDFS, Hive, Spark, Yarn, and MapReduce service properties.
-  The parameters of DBService cannot be modified when only one DBService role instance exists in the cluster.

Procedure
---------

-  Modify a service.

   #. Click **Services**.

   #. Select the target service from the service list.

   #. Click **Service Configuration**.

   #. Set **Type** to **All**. All configuration parameters of the service are displayed in the navigation tree. The root nodes from top down in the navigation tree represent the service names and role names.

   #. In the navigation tree, select a specified parameter and change its value. You can also enter the parameter name in the **Search** box to search for the parameter and view the result.

      If you want to cancel the modification of a parameter value, click |image1| to restore it.

      .. note::

         You can also use host groups to change role instance configurations in batches. Select a role name from the **Role** drop-down list and choose **< Select Host >** in the **Host** drop-down list. Enter a name in the **Host Group Name** text box, select the hosts to be modified from the **Host** list, add them to the **Selected hosts** area, and click **OK**. The added host group can be selected from **Host** and is only valid on the current page. The page cannot be saved after being refreshed.

   #. Click **Save Configuration** and select **Restart the affected services or instances**. Click **OK** to restart the services.

      After **Operation successful.** is displayed, click **Finish**. The service is started successfully.

      .. note::

         To update the queue configuration of the Yarn service without restarting service, choose **More** > **Refresh Queue** to update the queue for the configuration to take effect.

-  Export service configuration parameters.

   #. Click **Services**.
   #. Select a service.
   #. Click **Service Configuration**.
   #. Click **Export Service Configuration**. Select a path for saving the configuration files.

-  Import service configuration parameters.

   #. Click **Services**.

   #. Select a service.

   #. Click **Service Configuration**.

   #. Click **Import Service Configuration**.

   #. Select the target configuration file.

   #. Click **Save Configuration** and select **Restart the affected services or instances**. Click **OK**.

      After **Operation successful.** is displayed, click **Finish**. The service is started successfully.

.. |image1| image:: /_static/images/en-us_image_0000001295738324.jpg
