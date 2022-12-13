:original_name: mrs_01_0250.html

.. _mrs_01_0250:

Configuring Role Instance Parameters
====================================

Scenario
--------

You can view and modify default role instance configurations on MRS Manager based on site requirements. The configurations can be imported and exported.

Impact on the System
--------------------

You need to download and update the client configuration files after configuring HBase, HDFS, Hive, Spark, Yarn, and MapReduce service properties.

Procedure
---------

-  Modifying role instance configurations

   #. Click **Services**.

   #. Select the target service from the service list.

   #. Click the **Instances** tab.

   #. Click the target role instance from the role instance list.

   #. Click **Instance Configuration**.

   #. Set **Type** to **All**. The navigation tree of all configuration parameters of the role instance is displayed.

   #. In the navigation tree, select a specified parameter and change its value. You can also enter the parameter name in the **Search** box to search for the parameter and view the result.

      If you want to cancel the modification of a parameter value, click |image1| to restore it.

   #. Click **Save Configuration**, select **Restart the role instance**, and click **OK** to restart the role instance.

      After **Operation successful.** is displayed, click **Finish**. The role instance is started successfully.

-  Exporting Configuration Parameters of a Role Instance

   #. Click **Services**.
   #. Select a service.
   #. Select a role instance or click the **Instances** tab.
   #. Select a role instance on a specified host.
   #. Click **Instance Configuration**.
   #. Click **Export Instance Configuration** to export the configuration data of a specified role instance, and choose a path for saving the configuration file.

-  Import configuration data of a role instance.

   #. Click **Services**.

   #. Select a service.

   #. Select a role instance or click the **Instances** tab.

   #. Select a role instance on a specified host.

   #. Click **Instance Configuration**.

   #. Click **Import Instance Configuration** to import the configuration data of the specified role instance.

   #. Click **Save Configuration** and select **Restart the role instance**. Click **OK**.

      After **Operation successful.** is displayed, click **Finish**. The role instance is started successfully.

.. |image1| image:: /_static/images/en-us_image_0000001295738324.jpg
