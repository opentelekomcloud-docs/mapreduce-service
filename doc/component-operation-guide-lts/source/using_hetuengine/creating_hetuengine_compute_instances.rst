:original_name: mrs_01_1731.html

.. _mrs_01_1731:

Creating HetuEngine Compute Instances
=====================================

Scenario
--------

This section describes how to create a HetuEngine compute instance. If you want to stop the cluster where compute instances are successfully created, you need to manually stop the compute instances first. If you want to use the compute instances after the cluster is restarted, you need to manually start them.

Prerequisites
-------------

-  You have created a user for accessing the HetuEngine web UI. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.
-  You have created a tenant in the cluster to be operated. For details about how to create a tenant. Ensure that the tenant has sufficient memory and CPUs when modifying the HetuEngine compute instance configuration.

   .. note::

      You must use a leaf tenant when creating a HetuEngine compute instance. Yarn tasks can be submitted only to the queues of the leaf tenant.

Procedure
---------

#. Log in to FusionInsight Manager as a user who can access the HetuEngine web UI and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.
#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
#. Click **Create Configuration** above the instance list. In the **Configure Instance** dialog box, set parameters.

   a. Set parameters in the **Basic Configuration** area. For details about the parameters, see :ref:`Table 1 <mrs_01_1731__en-us_topic_0000001173631202_table18558203113529>`.

      .. _mrs_01_1731__en-us_topic_0000001173631202_table18558203113529:

      .. table:: **Table 1** Basic configuration

         +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------+
         | Parameter                              | Description                                                                                                                                                                                                                                                                                                                                                                                                    | Example Value                                              |
         +========================================+================================================================================================================================================================================================================================================================================================================================================================================================================+============================================================+
         | Resource Queue                         | Resource queue of the instance. Only one compute instance can be created in a resource queue.                                                                                                                                                                                                                                                                                                                  | Select a queue from the **Resource Queue** drop-down list. |
         +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------+
         | Instance Deployment Timeout Period (s) | Timeout interval for starting a compute instance by Yarn service deployment. The system starts timing when the compute instance is started. If the compute instance is still in the **Creating** or **Starting** state after the time specified by this parameter expires, the compute instance status is displayed as **Error** and the compute instance that is being created or started on Yarn is stopped. | 300                                                        |
         |                                        |                                                                                                                                                                                                                                                                                                                                                                                                                |                                                            |
         |                                        |                                                                                                                                                                                                                                                                                                                                                                                                                | The value ranges from 1 to 2147483647.                     |
         +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------+

   b. Set parameters in the **Coordinator Container Resource Configuration** area. For details about the parameters, see :ref:`Table 2 <mrs_01_1731__en-us_topic_0000001173631202_table6559143115525>`.

      .. _mrs_01_1731__en-us_topic_0000001173631202_table6559143115525:

      .. table:: **Table 2** Parameters for configuring Coordinator container resources

         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
         | Parameter             | Description                                                                                                                                                                                                                                                                                           | Example Value                          |
         +=======================+=======================================================================================================================================================================================================================================================================================================+========================================+
         | Container Memory (MB) | Memory size (MB) allocated by Yarn to a single container of the compute instance Coordinator                                                                                                                                                                                                          | Default value: 5120                    |
         |                       |                                                                                                                                                                                                                                                                                                       |                                        |
         |                       |                                                                                                                                                                                                                                                                                                       | The value ranges from 1 to 2147483647. |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
         | vcore                 | Number of vCPUs (vCores) allocated by Yarn to a single container of the compute instance Coordinator                                                                                                                                                                                                  | Default value: 1                       |
         |                       |                                                                                                                                                                                                                                                                                                       |                                        |
         |                       |                                                                                                                                                                                                                                                                                                       | The value ranges from 1 to 2147483647. |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
         | Quantity              | Number of containers allocated by Yarn to the compute instance Coordinator                                                                                                                                                                                                                            | Default value: 2                       |
         |                       |                                                                                                                                                                                                                                                                                                       |                                        |
         |                       |                                                                                                                                                                                                                                                                                                       | The value ranges from 1 to 3.          |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
         | JVM                   | Log in to FusionInsight Manager and choose **Cluster** > **Services** > **HetuEngine** > **Configurations**. On the **All Configurations** tab page, search for **extraJavaOptions**. The value of this parameter in the **coordinator.jvm.config** parameter file is the value of the JVM parameter. | ``-``                                  |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+

   c. Set parameters in the **Worker Container Resource Configuration** area. For details about the parameters, see :ref:`Table 3 <mrs_01_1731__en-us_topic_0000001173631202_table25611531175211>`.

      .. _mrs_01_1731__en-us_topic_0000001173631202_table25611531175211:

      .. table:: **Table 3** Parameters for configuring Worker container resources

         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
         | Parameter             | Description                                                                                                                                                                                                                                                                                      | Example Value                          |
         +=======================+==================================================================================================================================================================================================================================================================================================+========================================+
         | Container Memory (MB) | Memory size (MB) allocated by Yarn to a single container of the compute instance Worker                                                                                                                                                                                                          | Default value: 10240                   |
         |                       |                                                                                                                                                                                                                                                                                                  |                                        |
         |                       |                                                                                                                                                                                                                                                                                                  | The value ranges from 1 to 2147483647. |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
         | vcore                 | Number of vCPUs (vCores) allocated by Yarn to a single container of the compute instance Worker                                                                                                                                                                                                  | Default value: 1                       |
         |                       |                                                                                                                                                                                                                                                                                                  |                                        |
         |                       |                                                                                                                                                                                                                                                                                                  | The value ranges from 1 to 2147483647. |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
         | Quantity              | Number of containers allocated by Yarn to the compute instance Worker                                                                                                                                                                                                                            | Default value: 2                       |
         |                       |                                                                                                                                                                                                                                                                                                  |                                        |
         |                       |                                                                                                                                                                                                                                                                                                  | The value ranges from 1 to 256.        |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
         | JVM                   | Log in to FusionInsight Manager and choose **Cluster** > **Services** > **HetuEngine** > **Configurations**. On the **All Configurations** tab page, search for **extraJavaOptions**. The value of this parameter in the **worker.jvm.config** parameter file is the value of the JVM parameter. | ``-``                                  |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+

   d. Set parameters in the **Advanced Configuration** area. For details about the parameters, see :ref:`Table 4 <mrs_01_1731__en-us_topic_0000001173631202_table15562731135211>`.

      .. _mrs_01_1731__en-us_topic_0000001173631202_table15562731135211:

      .. table:: **Table 4** Advanced configuration parameters

         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Parameter             | Description                                                                                                                                                                                                                                                                                      | Example Value |
         +=======================+==================================================================================================================================================================================================================================================================================================+===============+
         | Ratio of Query Memory | Ratio of the node query memory to the JVM memory. The default value is **0**. When this parameter is set to **0**, the calculation function is disabled.                                                                                                                                         | 0             |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Scaling               | If auto scaling is enabled, you can increase or decrease the number of Workers without restarting the instance. However, the instance performance may deteriorate. For details about the parameters for enabling dynamic scaling, see :ref:`Adjusting the Number of Worker Nodes <mrs_01_2320>`. | OFF           |
         +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

   e. .. _mrs_01_1731__en-us_topic_0000001173631202_li135621231135216:

      Configure **Custom Configuration** parameters. Choose **Advanced Configuration** > **Custom Configuration** and add custom parameters to the specified parameter file. Select the specified parameter file from the **Parameter File** drop-down list.

      -  You can click **Add** to add custom configuration parameters.

      -  You can click **Delete** to delete custom configuration parameters.

      -  **resource-groups.json** takes effect only in the customized configuration of the Coordinator node. For details about the parameters for configuring resource groups, see :ref:`Table 5 <mrs_01_1731__en-us_topic_0000001173631202_table439014781612>`.

         .. _mrs_01_1731__en-us_topic_0000001173631202_table439014781612:

         .. table:: **Table 5** Resource pool group parameters

            +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
            | Parameter             | Description                                                                                                                            | Example Value                    |
            +=======================+========================================================================================================================================+==================================+
            | resourcegroups        | Resource management group configuration of the cluster. Select **resource-groups.json** from the drop-down list of the parameter file. | .. code-block::                  |
            |                       |                                                                                                                                        |                                  |
            |                       |                                                                                                                                        |    {                             |
            |                       |                                                                                                                                        |    "rootGroups": [{              |
            |                       |                                                                                                                                        |    "name": "global",             |
            |                       |                                                                                                                                        |    "softMemoryLimit": "100%",    |
            |                       |                                                                                                                                        |    "hardConcurrencyLimit": 1000, |
            |                       |                                                                                                                                        |    "maxQueued": 10000            |
            |                       |                                                                                                                                        |    }],                           |
            |                       |                                                                                                                                        |    "selectors": [{               |
            |                       |                                                                                                                                        |    "group": "global"             |
            |                       |                                                                                                                                        |    }]                            |
            |                       |                                                                                                                                        |    }                             |
            +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+

      .. note::

         For the **coordinator.config.properties**, **worker.config.properties**, **log.properties**, and **resource-groups.json** parameter files, if a user-defined parameter name already exists in the specified parameter file, the original parameter values in the parameter file are replaced with the customized parameter value. If the name of the custom parameter does not exist in the specified parameter file, the custom parameter is added to the specified parameter file.

   f. Determine whether to start the instance immediately after the configuration is complete.

      -  Select **Start Now** to start the instance immediately after the configuration is complete.
      -  Deselect **Start Now** and manually start the instance after the configuration is complete.

#. Click **OK** and wait until the instance configuration is complete.
