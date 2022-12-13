:original_name: mrs_01_0247.html

.. _mrs_01_0247:

Configuring Customized Service Parameters
=========================================

Each component of MRS supports all open-source parameters. You can modify some parameters for key application scenarios on MRS Manager. Some component clients may not include all parameters with open-source features. For component parameters that cannot be directly modified on Manager, users can add new parameters for components by using the configuration customization function on Manager. Newly added parameters are saved in component configuration files and take effect after restart.

Impact on the System
--------------------

-  After the service attributes are configured, the service needs to be restarted and cannot be accessed.
-  You need to download and update the client configuration files after configuring HBase, HDFS, Hive, Spark, Yarn, and MapReduce service properties.

Prerequisites
-------------

You have understood the meanings of parameters to be added, configuration files that have taken effect, and the impact on components.

Procedure
---------

#. On MRS Manager, click **Services**.

#. Select the target service from the service list.

#. Click **Service Configuration**.

#. Set **Type** to **All**.

#. In the navigation tree, select **Customization**. The customized parameters of the current component are displayed on Manager.

   The configuration files that save the newly added customized parameters are displayed in the **Parameter File** column. Different configuration files may have same open source parameters. After the parameters in different files are set to different values, whether the configuration takes effect depends on the loading sequence of the configuration files by components. You can customize parameters for services and roles as required. Adding customized parameters for a single role instance is not supported.

#. Based on the configuration files and parameter functions, locate the row where a specified parameter resides, enter the parameter name supported by the component in the **Name** column and enter the parameter value in the **Value** column.

   -  You can click |image1| or |image2| to add or delete a user-defined parameter. You can delete a customized parameter only after you click |image3| for the first time.
   -  If you want to cancel the modification of a parameter value, click |image4| to restore it.

#. Click **Save Configuration** and select **Restart the affected services or instances**. Click **OK** to restart the services.

   After **Operation successful.** is displayed, click **Finish**. The service is started successfully.

.. _mrs_01_0247__en-us_topic_0035251703_section32890065192053:

Task Example
------------

**Configuring Customized Hive Parameters**

Hive depends on HDFS. By default, Hive accesses the HDFS client. The configuration parameters to take effect are controlled by HDFS in a unified manner. For example, the HDFS parameter **ipc.client.rpc.timeout** affects the RPC timeout period for all clients to connect to the HDFS server. If you need to modify the timeout period for Hive to connect to HDFS, you can use the configuration customization function. After this parameter is added to the **core-site.xml** file of Hive, this parameter can be identified by the Hive service and its configuration overwrites the parameter configuration in HDFS.

#. On MRS Manager, choose **Services** > **Hive** > **Service Configuration**.

#. Set **Type** to **All**.

#. In the navigation tree on the left, select **Customization** for the Hive service. The system displays the customized service parameters supported by Hive.

#. In **core-site.xml**, locate the row that contains the **core.site.customized.configs** parameter, enter **ipc.client.rpc.timeout** in the **Name** column, and enter a new value in the **Value** column, for example, **150000**. The unit is millisecond.

#. Click **Save Configuration** and select **Restart the affected services or instances**. Click **OK** to restart the service.

   After **Operation successful.** is displayed, click **Finish**. The service is started successfully.

.. |image1| image:: /_static/images/en-us_image_0000001349057937.jpg
.. |image2| image:: /_static/images/en-us_image_0000001295898276.jpg
.. |image3| image:: /_static/images/en-us_image_0000001349057937.jpg
.. |image4| image:: /_static/images/en-us_image_0000001295738324.jpg
